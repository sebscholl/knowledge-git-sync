# Putting Myself through a Udacity Course During RampEX

### Sub-prompts
- What did you do about it? 
- What was the outcome? 
- Is there anything you would have done differently?
- How did you identify what you needed to learn to be successful? 
- How did you go about building expertise to meet your goal? 
- Did you meet your goal?
- What resources did you identify to help you develop? 
- What was the impact?

**OPENING ANECDOTE**
- I was a 19-year-old intern having lunch with Hank Greenberg (CEO AIG) and was naive enough to ask him, "what's been the secret to your success?"
	- He responded, "Not knowing how to do anyone's job better than they do it, but knowing how to do it well enough to tell if they're BSing me or not!"
	- Throughout my career, I've tirelessly worked to identify that balance of having enough knowledge to manage a process instead of performing a function.
	- I feel this story is a good representation of that.

**Situation**
- I was 3-month into building my startup, RampEX
- My knowledge of the problem space developed significantly
	- Speaking frequently with sales trainers on how they conduct role-play training
		- One of our customer personas
- It became clear we had a more significant NLP problem than anticipated
	- To provide customers best possible experience, they needed to navigate the training conversations with natural speech
	- Keyword/Bag-of-Words approaches would be too rigid 
		- My originally assumed approach

**Task**
- I needed to devise a solution or hire an expert to solve this problem, which at the time I termed "Non-keyword semantic navigation"
	- Terrible mouthful of words

**Action**
- I thought back to that lunch with Hank
	- Identified that I needed deeper subject matter expertise **even** to manage the process
	- Decided that I wanted to develop the knowledge to solve the problem
		- Maybe it wasn't the wisest choice as a manager
		- But I love language and technology
			- If there is anything I'd go out of my way to learn deeper, NLP is it!
	- I found this field of Computer Science fascinating
		- Enrolled in a 6-month Deep Learning curriculum by Udacity
		- Did this alongside pursuing the startup and solving the problem
- I believed that: 
	- Familiarizing myself with the domain would lead me to identifying the right questions to ask
	- Enable me to address the problem myself
- I'd isolated in a very discrete location of one code base where this algorithim needed to be applied
	- Implimented "good enough" keyword solution
		- Unblocked myself and other engineers from continuing development
	- Meanwhile, completed 10/hrs per weekin the evenings of Deep Learning

**Result**
- In 4-months I was able to complete the course successfully
	- However, during the course I was introduced to several concepts / tools
		- Lemmantization vs. Stemming
		- Princeton Wordnet
		- Semantic Similarity
- I explored the concepts in depth and leveraging them in developing a Semantic Similarity algorithim
	- Was able to develop a performant algorithm that solved for our use case
	- We deployed it as a microservive on AWS
- What was cool about this algorithm was that I recognized meaning over keywords
	- "My car need to be washed" and "The truck needs cleaning"
		- 0 shared words leading to 0 match with BoW/Keyword
		- My algortithm scored them at ~75%
- For customers (people training) this seemed like magic
	- Navigate dialogs and objection comfortably and casually 