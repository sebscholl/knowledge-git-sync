# Stories for Amazon Loop Interview 4

## [[Amazon Leadership Principles#Insist on the Highest Standards]]

## [[Amazon Leadership Principles#Bias for Action]]

#### [[Pivoting RampEX from VR to Web]] 
**Describe a time when you brought different perspectives together to solve a problem.**

**Tell me about a time when you made a difficult decision with input from many different sources (customers, stakeholders, partner teams, and so on).**

**Give me an example of when you asked for customer feedback.**

**Give an example of a time you requested additional funding/budget to complete a project**

**Give an example of a time when you challenged your team to come up with a more efficient solution or process.**

#### [[Switching from 14-day Free Trial to Free Tier on 8base]]
**Tell me about a time when you didn't have enough data to make the right decision.**

**Tell me about a strategic decision you made without clear data or (NOT AND) benchmarks.**

**Tell me about a time when you evaluated the customer experience of your product or service.**

#### [[Realizing Slack was Terrible for Customer Support and then Moving to Discourse]]
**We don't always make the right decision all the time. Tell me about a time when you made a bad decision.**

**We don't always make the right judgment all the time. Tell me about a time when you made an error in judgment.**

**Tell me about a time when you discovered that your idea was not the best course of action.**

___

## System Design Interview

#### Potential Systems
- Ticketing System
- Design Photos application with non-functional requirements consideration.
- Design the next twitter
- How you would design a social network like Facebook or Instagram?
- How would you design a system that reads book reviews from other sources and displays them on your online book store?
- How would you build the software behind an amazon pick up location with lockers?
- How do you handle calls between clients and REST API services with increased volumes?
- Design a promotion mechanism which could give 10% cash back on a particular credit card
- Design a short URL system

**Step 1. RECEIVE PROMPT**
- TREAT THE INTERVIEWER AS YOUR TEAMMATE

**Step 2. CLARIFYING QUESTIONS**

*ORDERED LIST*

**FEATURES:**
1. Start with re-capping required features

*SHOULD I MAKE ASSUMPTIONS ABOUT THE TEAM I HAVE ACCESS TO?*
*DO DEVELOPERS NEED ACCESS TO THE SYSTEM?*
*FROM SCRATCH BUILD OR EVOLVING AN EXISTING SYSTEM*

**USERS**
1. Are there different types? (admin, user, etc).
2. When do most users use the system, and how many people do we need to serve? How fast is our userbase growing?
3. Are there higher loads during a particular time of day? Particular time of the year?
4. Do our users log on from different regions?
5. Are they accessing the system from a web interface, mobile app, or both?
6. Who are the customers?
7. Where is this going to be launched? (National/Global)
8. Scale of customers? (how many to anticipate)
9. Discuss customer interfaces (Frontends for Different Per

**Tools and Tech**
11. Wiring that up to backend technologies
	1. Required APIs
		1. If customer is developer, think of develop interface
		2. SDK, CLI, or API (GraphQL or REST)
	2. Components/entities
	3. Monolith or microservices?
12. Database tech

**Step 3. WHITEBOARDING**

Some interviews require free hand drawing on a virtual whiteboard. **A link to InVision, a whiteboarding platform, has been provided below:**  
   
**InVision Whiteboarding Link:** [https://amazon-recruiting.invisionapp.com/freehand/document/vyxrOqWlD](https://amazon-recruiting.invisionapp.com/freehand/document/vyxrOqWlD)  
    
**Please sign in as a Guest on InVision (upper right corner), and then follow the prompts to enter your email address. You do not need to create an account or enter a password.**  
  
- **Delete:** Click ctrl + Z to delete a drawing. Alternatively, hover over the pencil icon to switch to the eraser tool to erase selected drawings. Once you have chosen the eraser tool, click on the drawing you would like to delete.
- **Present Mode:** Once you are ready to begin drawing, press the “play” button (triangle at the top right of the page, next to the pencil) to lead in Present Mode. This will allow the viewer to follow your drawings.

**Step 4. Review**

Be prepared to answer:

1. How will you ensure this system is working at an acceptable level of performance?
2. If a problem occurs, what will be involved in troubleshooting and resolving it quickly?
3. What are possible points of failure, and how can they be made more robust?