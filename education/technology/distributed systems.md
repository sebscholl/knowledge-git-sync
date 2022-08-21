# Distributed Systems Review

## Service Oriented Architecture (SOA)

### **3 Primary Objectives**

1. It aims to structure procedures or software components as services (this IS AWS). This makes them loosely coupled applications.
2. A mechanism for publishing services with clearly defined input/output requirements and functionality, making them easy for developers to leverage in existing Applications.
3. Avoiding security and governance issues. By moving security to single system or application level, you’re able to better control what identities have access to what services, as well as establish clear rights and authorizations between services (a.k.a, finer granularity).

### Benefits of an SOA

- **Reusable.** Services can be reused to make multiple applications. This is facilitated by the fact that SOA services are held in a service repository and linked on demand, making each service a generalized resource available to all -- subject to governance constraints. Reusing services allows organizations to save time and lower costs associated with development.
- **Easily maintained.** Since all services are independent, they can be easily modified and updated without affecting other services. This will also lower an organization's operating costs.
- **Promotes interoperability.** The use of a standardized communication protocol allows platforms to easily transmit data between clients and services regardless of the languages they're built on.
- **High availability.** SOA facilities are available to anyone upon request.
- **Increased reliability.** SOA generates more reliable applications because it is easier to debug small services than large code.
- **Scalable.** SOA allows services to run on different servers, thus increasing [scalability](https://www.techtarget.com/searchdatacenter/definition/scalability). In addition, using a standard communication protocol allows organizations to reduce the level of interaction between clients and services. Lowering the level of interaction allows applications to be scaled without adding extra pressure.

### Disadvantages of an SOA

- **Large Investment.** Implementation of SOA requires a large initial investment.
- **Reporting Complexities.** Service management is complicated since the services exchange millions of messages that are hard to track.
- **Slower Loading/Response Times:** The input parameters of services are validated every time services interact, thus decreasing performance and increasing load and response times.

### Keys to a successful implementation

1. Use of independent services that perform tasks in a standardized way
2. Not needing information about the calling application
3. Not needing the calling application requires knowledge of the tasks the service performs.

### Highlights and Words:

- Loose Coupling
- High Interoperability
- Continued Improvement over Immediate Perfection

**MICROSERVICES ARE THE LATEST VERSION OF SOA’s - small software feature components, accessed through a REST interface.** 

## Distributed Systems

A distributed system is a computing environment in which various components are spread across multiple computers (or other computing devices) on a [network](https://www.splunk.com/en_us/data-insider/network-operations-center.html). These devices split up the work, coordinating their efforts to complete the job more efficiently than if a single device had been responsible for the task.

### Distributed System Benefits

• Distributed systems reduce the risks of having a single point of failure, bolstering reliability and fault tolerance.

### Examples:

- A distributed video rendering application that sends frames to a network of computers to render and then return in realtime.
- Telecommunications networks (including cellular networks and the fabric of the internet)
- Graphical and video-rendering systems
- Scientific computing, such as protein folding and genetic research
- Airline and hotel reservation systems
- Multiuser video conferencing systems
- Cryptocurrency processing systems (e.g. Bitcoin)
- Peer-to-peer file-sharing systems (e.g. BitTorrent)
- Distributed community compute systems (e.g. Folding@Home)
- Multiplayer video games
- Global, distributed retailers and supply chain management (e.g. Amazon)

### **What are key characteristics of a distributed system?**

Distributed systems are commonly defined by the following key characteristics and features:

- **Scalability:** The ability to grow as the size of the workload increases is an essential feature of distributed systems, accomplished by adding additional processing units or nodes to the network as needed.
- **Concurrency:** Distributed system components run simultaneously. They’re also characterized by the lack of a “global clock,” when tasks occur out of sequence and at different rates.
- **Availability/fault tolerance:** If one node fails, the remaining nodes can continue to operate without disrupting the overall computation.
- **Transparency:** An external programmer or end user sees a distributed system as a single computational unit rather than as its underlying parts, allowing users to interact with a single logical device rather than being concerned with the system’s architecture.
- **Heterogeneity:** In most distributed systems, the nodes and components are often asynchronous, with different hardware, middleware, software and operating systems. This allows the distributed systems to be extended with the addition of new components.
- **Replication:** Distributed systems enable shared information and messaging, ensuring consistency between redundant resources, such as software or hardware components, improving fault tolerance, reliability and accessibility.

### **What is distributed tracing?**

[Distributed tracing](https://www.splunk.com/en_us/data-insider/what-is-distributed-tracing.html), sometimes called distributed request tracing, is a method for monitoring applications — typically those built on a [microservices architecture](https://www.splunk.com/en_us/data-insider/what-are-microservices.html) — which are commonly deployed on distributed systems. Distributed tracing is essentially a form of distributed computing in that it’s commonly used to [monitor the operations of applications](https://www.splunk.com/en_us/data-insider/what-is-application-performance-monitoring.html) running on distributed systems.

A tracing system monitors this process step by step, helping a developer to uncover bugs, bottlenecks, latency or other problems with the application. Without distributed tracing, an application built on a microservices architecture and running on a system as large and complex as a globally distributed system environment would be impossible to monitor effectively.

### **What are the benefits of distributed systems?**

Distributed systems offer a number of advantages over monolithic or single, systems, including:

- **Greater flexibility:** It is easier to add computing power as the need for services grows. In most cases today, you can add servers to a distributed system on the fly.
- **Reliability:** A well-designed distributed system can withstand failures in one or more nodes without severely impacting performance. In a monolithic system, the entire application goes down if the server goes down.
- **Enhanced speed:** Heavy traffic can bog down single servers when traffic gets heavy, impacting performance for everyone. The scalability of distributed databases and other distributed systems makes them easier to maintain and also sustain high-performance levels.
- **Geo-distribution:** Distributed content delivery is both intuitive for any internet user, and vital for global organizations.

### **What are some challenges of distributed systems?**

Distributed systems are considerably more complex than monolithic computing environments and raise a number of challenges around design, operations and maintenance. These include:

- **Increased opportunities for failure:** The more systems added to a computing environment, the more opportunity there is for failure. If a system is not carefully designed and a single node crashes, the entire system can go down. While distributed systems are designed to be fault tolerant, that fault tolerance isn’t automatic or foolproof.
- **Synchronization process challenges:** Distributed systems work without a global clock, requiring careful programming to ensure that processes are properly synchronized to avoid transmission delays that result in errors and data corruption. In a complex system — such as a multiplayer video game — synchronization can be challenging, especially on a public network that carries data traffic.
- **Imperfect scalability:** Doubling the number of nodes in a distributed system doesn’t necessarily double performance. Architecting an effective distributed system that maximizes scalability is a complex undertaking that needs to take into account load balancing, bandwidth management and other issues.
- **More complex security:** Managing a large number of nodes in a heterogeneous or globally distributed environment creates numerous security challenges. A single weak link in a file system or larger distributed system network can expose the entire system to attack.
- **Increased complexity:** Distributed systems are more complex to design, manage and understand than traditional computing environments.

### **What are the risks of distributed systems?**

The challenges of distributed systems, as outlined above create a number of correlating risks. These include:

- **Security:** Distributed systems are as vulnerable to attack as any other system, but their distributed nature creates a much larger attack surface that exposes organizations to threats.
- **Risk of network failure:** Distributed systems are beholden to public networks in order to transmit and receive data. If one segment of the internet becomes unavailable or overloaded, distributed system performance may decline.
- **Governance and control issues:** Distributed systems lack the governability of monolithic, single-server-based systems, creating auditing and adherence issues around [global privacy laws such as GDPR](https://www.splunk.com/en_us/data-insider/data-governance-and-gdpr.html). Globally distributed environments can impose barriers to providing certain levels of assurance and impair visibility into where data resides.
- **Cost control:** Unlike centralized systems, the scalability of distributed systems allows administrators to easily add additional capacity as needed, which can also increase costs. Pricing for cloud-based distributed computing systems are based on usage (such as the number of memory resources and CPU power consumed over time). If demand suddenly spikes, organizations can face a massive bill.

### **Monolithic Architecture**

MVC app (or other like architecture) all on a single server or single code-base. Think of one massive Rails or Django App. 

**Drawbacks:**

- Every deployment is a FULL deployment of the system.
- Scaling is adding CPU, RAM, and Disk-size (Vertical scaling)
- Scaling up has diminishing returns (double capacity doesn’t mean double throughput)

### **Microservices Architecture**

All about scaling horizontally. You could technically replicate the monolithic application horizontally. However, it’s instead better to break the service up into a series of apps (micro-services) that each fulfill a specific requirement/capability of the solution being built.

Some immediate benefits of this are:

- Decoupled
- Individually scalable
- Individually deployable
- Each written in a language (or leveraging the technologies) that best suits their needs

In horizontally scaling a microservice, you know that you can replicate it to double its capacity (same specs). This would require a load balancer for distributing the incoming traffic to the appropriate application instance, based on an applied load balancing strategy.

Other benefits include:

- Resilience & High availability - systems that aim to ensure an agreed level of operational performance is met.
    - Load balance across multiple instances of the service is key to achieving high availability, as the load balancer can detect the availability of any instance and route traffic accordingly.
        - This is LOCAL REDUNDANCY
    - Load balancing across multiple instances of a service, replicated across multiple servers in a zone, is the next level.
        - This is ZONE REDUNDANCY
    - Load balancing across multiple instances of a service, replicated across multiple server in a zone, across muliple regions globally is the next level.
        - This is GEO “GEO/ZONE” REDUNDANCY
        - At this level, the downtime is so unlikely it’s almost impractical. The reason you’d go this far is to have lower latency in the regions being served.

### Statelessness

One of the biggest key differences between the monolithic apps and microservices is statelessness. Meaning that there is nothing saved (no state) in memory from one request to another.

REST APIs are a key example of this, as they require no information/state to be kept in memory by the server between requests, even with the JWT being a self contained authentication credential.

### N-Tier Architecture

Refers to applications broken up into a specific number of tiers (i.e., 3-tier serverless). Usually, this is presentation layer, application layer, and data layer.

- Better security (forced granularity)
- Scalability (scale individual tiers as needed)
    - Scaling the DB layer with read-replicas or sharding
    - Scaling the application layer with instances hirozontally
    - Scaling the number of tiers adding a routing layer
    - Scaling the presentation layer with new device types
- More simple maintenance (individual contributors to each tier)
- Easily enhanced (continuous development of individual tiers)