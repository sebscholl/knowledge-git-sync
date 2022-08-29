
# Interviewing Customers to Validate Developer User Experience Level

### Sub-prompts
- What made it challenging? 
- What factors did you consider in your talent review? 
- What factors did you consider in the promotion process? 
- Did you incorporate a tool to counter unconscious bias?
- If yes, how? 
- How do you manage perceptions of unfair treatment? 
- What did you learn from this process? 
- Knowing what you know now, would you have done anything differently? (Manager)
- How did you decide to follow-up was necessary? 
- What steps, if any, did you take to validate the assumptions? 
- What was the result? (Manager)


"8base PM assuming customer was junior developer and me doing research and interviews to validate otherwise"

**Situation**
- Early at my time at 8base
	- CEO transferred Product Management responsibility to me
	- To date, he was guiding the team/product vision
- In this role, I managed the UX/UI designer and had the Engineering Team Lead (a Project Manager) as a direct report.
- Through our support channels, we'd gotten customer/developer feedback
	- that RBAC system was too rigid
	- Needed flexibility for Multi-tenant SaaS RBAC 
- This feature improvement was one of the first projects I led
	- After several working sessions with the PM and engineers:
		- Came up with an extremely flexible system
		- Gave developers greater visibility/access into the underlying system
		- Would be straightforward, while effective implementation
			- Writing of JSON objects that reflected data model/filters
- Communicated the idea to the designer
	- The design they came back with was a very, very elaborate form-based approach to constructing the underlying JSON
- I applauded the creativity but said a JSON editor would likely do the trick!
	- They pushed back hard, saying that our users needed a "low-code" interface 
	- Otherwise, users wouldn't understand how to use it
- I took a step back at this point, as these folks had been around much longer than I had
	- Went to CEO and asked for his input
	- He said that he wasn't sure but preferred a "low-code" approach being non-technical himself

**Task**
- At this point, I realized that no one had connected and learned who our users were. 
	- I needed to connect one-on-one with customers and learn who they were.

**Action**
- I asked for a small budget to incentivize users to a 30-minute meeting
	- $50 Amazon gift card for 30 minute discovery interview
	- Structured questions:
		- How'd you hear of us?
		- How technical do you consider yourself?
		- What Technologies are you most comfortable with?
		- What did you first think 8base would do for you?
		- What did you figure out it would do for you?
		- What was your first "AHA!" moment?
		- What 3 features could we get rid of?
		- What 3 features CAN'T we get rid of?
		- What would you be willing to pay more for?
		- Would a JS SDK have helped you get started?
		- Documentation feedback on a scale from 1 to 10
		- Rate Docs 1 to 10
		- If 8base had to disappear, how sad would you be?
		- Rate Sadness 1 to 10 if we were to disappear
- I was able to get 20 meetings scheduled over a 2-week period
	- Added several questions to best inform the road map and other areas of focus
- Completed meetings:
	- Tracked answers in a normalized spreadsheet
	- Posted recordings for team to watch
	- Prepared breakdown analysis of results

**Results**
- I uncovered some very interesting insights and data through this
	- The least interesting of which may have been a JSON editor being beyond approachable and familiar by users who were actually building and getting value from the platform
- On a scale from 1 to 10, how technical do you consider yourself?
	- No matter the interviewee's experience level or discipline, everyone identified themselves as between 7 and 10. That said, _ONE INSIGHT THAT MAY BE EXTRACTED_ is that all engineers/developers are quick and biased towards considering their own technical skills beyond their true competency level. If this is true, marketing and messaging that's written under the premise of a person "being aware of their own limitations and skill-sets" (i.e. "let us handle the hard-stuff" or "a solution for junior/entry level X") will likely be poorly received by the **user audience**; as no one in this initial test group was able/willing to self-identify as anything less-than highly-technical (whether they were 1-year into CSS or 20-years into enterprise software).
- Which of these statements do you identify the most with? AND Which of the following values is most important to you when it comes to your work?
	- Of the 15 interviews, 67% identified themselves by **"I love coding and using frameworks/libraries to solve interesting problems."** while 33% identified themselves by **"I love learning to use platforms/tools that help me work faster".** More interestingly, this is disproportionally weighted to less experienced developers. For those developers who had between **0 and 5 years experience,** 80% identified themselves by **"I love coding and use..."** while 20% identified themselves by **"****I love learning to use...".** This is insight is further enriched by the data that shows **Solution Quality (Code Quality)** being represented as 60% of the **0 and 5 years experience** developers primary concern (10% development speed, 20% Security, 10% Resource Optimization). 
- Meanwhile, for those developers with over 5-years experience, **100% of interviews responded with Development Speed being their primary concern.** Additionally, **60% of developers with over 5-years experience identified themselves by "I love learning to use platforms/tools that help me work faster.**"
- Which low-code/no-code tools/platforms are you most familiar with today? AND Do you use low-code/no-code tools in your professional or personal projects?
	- Interviewee's were somewhat quick to claim that they don't use low-code/no-code. However, it was largely due to a lack of familiarity with _what_ constitutes a no-code or low-code platform. After some further context, the participants ended up dividing evenly into 3 camps; **33% never use, 33% use for personal projects only, 33% use for both personal and professional projects.** That said, the _types_ of tools that they were familiar with and recognized were mainly **Shopify, Wordpress, and Firebase.** Only 1 respondent had knowledge of solutions like Retool or [Bubble.io](http://bubble.io/). 

- When struggling to solve a development challenge, are you most likely to...
	-   73% responded **"****Teach me the required skills to solve it"**
	-   20% responded **"Adopt/purchase a tool that solves it for me"**
	-   7% responded **"Find/hire an expert who can solve it"**
	- 100% of interviewees responded, "Adopt/purchase a tool that solves it for me," had 4+ years of development experience. 81% of interviewees responded, "Teach me the required skills to solve it." had 0 to 4 years of development experience.
- In conclusion
	- Able to very definitively validate and re-calibrate the assumption 
	- Dive deeper into our customers psychology and get really cool insights
