# Working with Alex on Virtual Vision and Coaching Him as Team Dev

### Sub-prompts
- Were you able to positively impact their performance?
- What started the coaching? 
- What was the outcome?
- How did you deliver feedback? Did their performance improve? (Manager)

**Situation**
- Helping a young startup develop a MedTech app 
	- VR headset to replace the Humphry Machine for optimologists 
	- Early stage Glaucoma detection
- I was helping manage their engineering effort in a part-time capacity 
	- I worked on the algorithm that drove the VR App
- I hired a Front-end developer, Alek, to build the technician interfaces
	- Alek had a great portfolio of Freelance work
	- A good understanding of the frameworks and tools he purported to work with
	- Showed interpersonal skills that could lead to managing other engineers
	- Brought him on board as a remote employee
- I had a really low moment when his first merge request came in
	- Very sloppy syntax
	- No documentation
	- Non-modularized code
	- No commit messages
	- However, everything worked
- Took a step back to think about the best way of handling this
	- I thought about Alek and his career to date
	- Realized that he'd never worked on a "team"
		- Always solo contributor to freelance project
	- Never had been held accountable to a professional standard
- This is even more important when doing "freelance" or "part-time work"
	- On projects with high rotation there's a higher importance on documentation and communicability of design choices and system functionality

**Task**
- I needed to help him grow from an solo contributor to a team contributor.
	- If I didn't, what "works" today will break "tomorrow" with new code changes
	- That simply wasn't acceptable for this customer (elderly)

**Action**
- In our next one on one, I explained to him in a positive way what I noticed
	- Understands the tools and how to use them
	- Needs to improve on how to "code with others"
- He expressed being a bit uncomfortable and embarassed
	- Even admitted "I've never worked with someone who reviewed my code, just tested the interface"
- I found this to be a positive signal and a great starting point for implimenting some best practices
- We first knocked out some low-hanging fruit:
	- Static Syntax Checking (prettier.js)
	- Set-up of CI/CD pipeline for automated tests/checks
	- Established rules for JSDoc comments on important functions/modules
- Found 1-hour early week to do a pair programming + 1-hour late week joint code review 
	- During this time, he'd drive and I'd navigate
	- Top focus was on: 
		- Isolation of logic
		- TTD tests (Mocha)
		- Prioritize interpretability over cleverness
			- Thinking of code as something which evolves with multiple contributors
- We continued working in this fashion for 3-months, at which point I stepped off the project

**Result**
- During this time, I saw exponential improvment in Alek
	- Able to maintain code coverage of 70%
	- Cut code review sessions in half
	- Tie commits to PM system tasks/stories
	- Strong representation of DRY code principle in contribution
- He's still with that company today
	- Brought on as full-time remote hire
	- Leads front-end development and manages one other front-end developer.

___

## References
- [[Amazon Leadership Principles#Insist on the Highest Standards]]
- [[Amazon Leadership Principles#Hire and Develop the Best]]