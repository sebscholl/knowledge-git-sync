# Phone Screening with Sam D

[**Interviewer: Sam Dwarakanath*](https://www.linkedin.com/in/sam-dwarakanath-3b37b11/)*
**Director and General Manager, AWS**, *Seattle*

### Questions
1) When interfacing with internal teams as the primary customer, how does that relationship get managed?
2) Does TxServices have its roadmap, or is its roadmap tied implicitly to the AWS services it supports?
3) This is a deep domain. What do the onboarding and training look like for Technical PMs and SDEs?
4) You've had an incredible career at Amazon... what inspired you to move from the more external customer/consumer product teams (Fashion, Go, Books, Fresh) to AWS?
5) As a Technical PM, what early actions and focuses would allow me to be the most valuable to the teams I'd be joining?
6) It's very cool that you were on the Amazon RDS Proxy project, as that was an important development to the company I've been with these past few years.
7) I'm interested in recommendation algorithms...when it came to size recommendations, what parameters drove that model? (Amazon Fashion)


### Paxos
- **Paxos** is an algorithm that is used to achieve consensus among a distributed set of computers that communicate via an asynchronous network. 
- One or more clients proposes a value to Paxos and we have consensus when a majority of systems running Paxos agrees on one of the proposed values. 
- Paxos is widely used and is legendary in computer science since it is the first consensus algorithm that has been rigorously proved to be correct.

What's cool about Paxos is it doesn't **require** a leader to be elected to handle all incoming requests.
 
Paxos has three entities:

1.  **Proposers**: Receive requests (values) from clients and try to convince acceptors to accept their proposed values.
2.  **Acceptors**: Accept certain proposed values from proposers and let proposers know if something else was accepted. A response from an acceptor represents a vote for a particular proposal.
3.  **Learners**: Announce the outcome.

### What Paxos does

A client sends a request to any Paxos proposer. The proposer then runs a two-phase protocol with the acceptors. Paxos is a **majority-wins** protocol. A majority avoids split-brain problems and ensures that if you made a proposal and asked over 50% of the systems if somebody else made a proposal and they all reply _no_ then you know for certain that no other system could have asked over 50% of the systems received the same answer. Because of this Paxos requires a majority of its servers to be running for the algorithm to terminate. A majority ensures that there is at least one node in common from one majority to another if servers die and restart. The system requires _2m+1_ servers to tolerate the failure of _m_ servers. As we shall see, Paxos requires a majority of acceptors. We can have one or a smaller number of proposers and learners.

Paxos acceptors cannot forget what they accepted, so they need to keep track of the information they received from proposers by writing it to stable storage. This is storage such as flash memory or disk, whose contents can be retrieved even if the process or system is restarted.

## Our full Paxos protocol now looks like this:

#### Phase 1a: Proposer (PREPARE)

A proposer initiates a **PREPARE** message, picking a unique, ever-incrementing value.

```
ID = cnt++;
send PREPARE(ID)
```

#### Phase 1b: Acceptor (PROMISE)

An acceptor receives a **PREPARE(ID)** message:

```
    if (ID <= max_id)
        do not respond (or respond with a "fail" message)
    else
        max_id = ID     // save highest ID we've seen so far
        if (proposal_accepted == true) // was a proposal already accepted?
            respond: PROMISE(ID, accepted_ID, accepted_VALUE)
        else
            respond: PROMISE(ID)
```

#### Phase 2a: Proposer (PROPOSE)

The proposer now checks to see if it can use its proposal or if it has to use the highest-numbered one it received from among all responses:

```
did I receive PROMISE responses from a majority of acceptors?
if yes
    do any responses contain accepted values (from other proposals)?
    if yes
        val = accepted_VALUE    // value from PROMISE message with the highest accepted ID
    if no
        val = VALUE     // we can use our proposed value
    send PROPOSE(ID, val) to at least a majority of acceptors
```

#### Phase 2b: Acceptor (ACCEPT)

Each acceptor receives a PROPOSE(ID, VALUE) message from a proposer. If the ID is the highest number it has processed then accept the proposal and propagate the value to the proposer and to all the learners.

```
if (ID == max_id) // is the ID the largest I have seen so far?
    proposal_accepted = true     // note that we accepted a proposal
    accepted_ID = ID             // save the accepted proposal number
    accepted_VALUE = VALUE       // save the accepted proposal data
    respond: ACCEPTED(ID, VALUE) to the proposer and all learners
else
    do not respond (or respond with a "fail" message)
```

If a majority of acceptors accept ID, value then consensus is reached. Consensus is on the value, not necessarily the ID.

**Independent failures** and [nondeterminism](https://sampa.cs.washington.edu/new/papers/asplos021-hunt.pdf) cause the most impactful issues in distributed systems.

*Offline distributed systems* are distributed batch processing systems like movie rendering and big data analysis clusters. All the benefits of distributed computing with few downsides (no complex failures or non-determinism)

*Soft real-time distributed systems* must continually product/update results but have workable time windows in which they can do it, like updating search indexes or systems looking for impaired servers.

*Hard real-time distributed systems* are sometimes called request/reply systems. These are what Amazon first focuses on. Everything from front-end web servers to credit card transactions and every AWS API. Unpredictable requests are received, and a response is rapidly expected.

- Hard real-time systems do NOT **share fate** (all crash simultaneously), so engineers need to test for all aspects of network failure. 
- Must consider failure at each step of the request reply life/cycle

```txt
1. POST REQUEST fails: Either NETWORK failed to deliver the message (for example, intermediate router crashed at just the wrong moment), or SERVER rejected it explicitly.

2. DELIVER REQUEST fails: NETWORK successfully delivers MESSAGE to SERVER, but SERVER crashes right after it receives MESSAGE.

3. VALIDATE REQUEST fails: SERVER decides that MESSAGE is invalid. The cause can be almost anything. For example, corrupted packets, incompatible software versions, or bugs on either client or server.

4. UPDATE SERVER STATE fails: SERVER tries to update its state, but it doesn’t work.

5. POST REPLY fails: Regardless of whether it was trying to reply with success or failure, SERVER could fail to post the reply. For example, its network card might fry just at the wrong moment.

6. DELIVER REPLY fails: NETWORK could fail to deliver REPLY to CLIENT as outlined earlier, even though NETWORK was working in an earlier step.

7. VALIDATE REPLY fails: CLIENT decides that REPLY is invalid.

8. UPDATE CLIENT STATE fails: CLIENT could receive message REPLY but fail to update its own state, fail to understand the message (due to being incompatible), or fail for some other reason.

(error, reply) = network.send(remote, actionData)
switch error
  case POST_FAILED:
    // handle case where you know server didn't get it
  case RETRYABLE:
    // handle case where server got it but reported transient failure
  case FATAL:
    // handle case where server got it and definitely doesn't like it
  case UNKNOWN: // i.e., time out
    // handle case where the *only* thing you know is that the server received
    // the message; it may have been trying to report SUCCESS, FATAL, or RETRYABLE
  case SUCCESS:
    if validate(reply)
      // do something with reply object
    else
      // handle case where reply is corrupt/incompatible

```

**The crux of distributed systems:**

"Even if an implementation is itself bug-free...

- the CPU could spontaneously overheat at runtime. 
- The machine’s power supply could fail, also spontaneously.
- The kernel could panic. 
- Memory could fill up, and some objects the program attempts to create can’t be created. 
- The disk on the machine it’s running on could fill up, and the program could fail to update some statistics file and then return an error, even though it probably shouldn’t. 
- A gamma ray could hit the server and flip a bit in RAM. 

**In short, engineering for distributed systems is hard because:**

• Engineers can’t combine error conditions. Instead, they must consider many permutations of failures. Most errors can happen at any time, independently of (and therefore, potentially, in combination with) any other error condition.  
• The result of any network operation can be UNKNOWN, in which case the request may have succeeded, failed, or received but not processed.  
• Distributed problems occur at all logical levels of a distributed system, not just low-level physical machines.  
• Distributed problems get worse at higher levels of the system, due to recursion.  
• Distributed bugs often show up long after they are deployed to a system.  
• Distributed bugs can spread across an entire system.  
• Many of the above problems derive from the laws of physics of networking, which can’t be changed.

But, most of the time, engineers don’t worry about those things. For example, unit tests never cover the “what if the CPU fails” scenario and only rarely cover out-of-memory scenarios."

In typical engineering, these types of failures occur on a single machine; that is, a single _fault domain_.

It is mind-boggling to consider all the permutations of failures that a distributed system can encounter, especially over multiple requests. You must work on the basis of **DISTRUST.**

Testing and Error Handling is the greatest conceptual challenge in distributed systems, requiring engineers to even consider testing unknown unknowns.


**Fun Story of a Distributed Systems Bug Crashing Amazon:**

It also started returning them very quickly, because it’s a lot faster to return nothing than something (at least it was in this case). Meanwhile, the load balancer between the website and the remote catalog service didn’t notice that all the responses were zero-length. But, it _did_ notice that they were blazingly faster than all the other remote catalog servers. So, it sent a huge amount of the traffic from www.amazon.com to the one remote catalog server whose disk was full. Effectively, the entire website went down because one remote server couldn’t display any product information.

this is what ive learned
this is what imm doing
this is what im not doing
tell me if something is wrong
this is what im driving
___
### References
- [Paxos Algorithm](https://people.cs.rutgers.edu/~pxk/417/notes/paxos.html)
- [[databases and scalability]]
- [AWS Distributed System Challenges](https://aws.amazon.com/builders-library/challenges-with-distributed-systems/)

