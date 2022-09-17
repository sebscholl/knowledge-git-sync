# Realizing Slack was Terrible for Customer Support and then Moving to Discourse

- Did you create the metric or was it already available? 
- How did this and other information influence the change? 
- What was the outcome of this change? 
- What was the metric? 
- Why did you create it? 
- How did this and other information influence change? What was the outcome of the change?

**Situation:** 
- At 8base we were experiencing a pretty steady flow of developer support emails 
	- Myself and several developers I managed were responsible for responding to/handling; 
	- There was no system in place for managing these inbound requests. 
- In light of our product-centric responsibilities: 
	- Our email response time wasn’t exactly the best. 
	- One email in particular that a customer sent directly to our CEO about not having received any support on an important bug for over a week is what finally tipped the scales
		- Made us all say “we need to do something about this.”
    
**Task:** 
- The CEO tasked me with implementing a system and policy for handling support questions and ensuring a discrete response time.
    
**Action:** 
- Support tickets often required us to ask many questions to diagnose the problem/solution, 
	- They were very conversational in nature. 
	- Any support request often had 6-messages back and forth. 
- I decided that the best way to handle these conversations was to create a public Slack community 
	- We could have live conversations with developers, as well as other developers with each other. 
- This also felt like a great, low cost and highly actionable way to build better relationships with our developer community.
    
**Result:** 
- Immediately our customers began expecting “real-time” communication and support, 
	- We had no systems in place to support being a US-based company with a global customer base. 
	- None of the incoming messages were organized or prioritized, 
	- Many messages to fall through the cracks as they got lost in the messaging feeds. 
- Lastly, there was significant friction directing customers to sign-up for Slack and then join our channel, when they we’re reaching out via email. 
	- All that said, in retrospect, it was just a terrible solution to the problem. 
    
- I quickly recognized that my solution wasn’t good and its flaws would simply amplify as we scaled. 
	- However, it did surface for me two qualities **that needed** to be in the viable solution. These were:
    
	1. 24-hour accessibility/availability (providing support while we sleep)
	2. Organization/prioritization of support queries (allowing nothing to fall through the cracks)
    
- I dug in on finding the most cost-effective ways of solving this issue 
	- Arrived at building a support forum community on Discourse. 
- Doing so provided a very accessible and public platform for us to handle support conversations, 
	- Users could then benefit from learning from or participating in the clock.
	- It alleviated us from expecting “chat-like” support, which we simply didn’t have the human capital/time resources to provide.  
- Additionally, it allowed us to organize around the tool, and easily gather insights around engagement, response times, and other metrics.
    
- This course correction ended up being a great solution which we still rely heavily on today. 
	- An unintended benefit of which was that all these support conversations are indexed by search engines
	- The community is now one of our primary lead generation assets.

___

### Metric Highlights
- Avg. response time (using time to reply) to support email -> over 36-hours
- Inbound support requests -> ~30 per week
- Discourse solution, brought it down below 24-hours
	- Implimented escalations
	- Used templates and "knowledge"
	- New topics ~30 per week (but content change)