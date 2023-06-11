#rampex #story_telling #amazon #interviewing 

# Question: What’s the most inventive or innovative thing you’ve done?

### Sub-prompts
- Why hadn't this been explored already? 
- Why did you move forward?
- What were the results or what was the impact?
- How do you know your solution addressed the problem?
- Ask for one or two more examples to see if it's a pattern of innovative thinking. 
- What was the problem it was solving?
- What was innovative about it?
- How did you know you were focusing on the right things? 
- What was the outcome? 
- Would you have done anything differently?
- Did you take that opportunity? 
- Why or why not? 
- What was the outcome? 
- What was the problem and why did it require a novel approach? 
- Was your approach successful? 
- What assumptions did you have to question? 
- How did you evaluate if the change improved the process? 
- Knowing what you know now, would you do anything differently?

Early in my career, I spent one year in sales at a software as a service (SaaS) startup. My onboarding and training consisted of PowerPoint presentations on product and culture for five consecutive days, then moved to immediately calling sales leads. Management knew this training was insufficient for new hires, so they handicapped our sales targets during the first six months by 75%.

It felt unconventional that I was only required to meet 25% of my quota. I soon learned it was a common practice termed "ramp" – the time given to a new sales hire to achieve expected productivity and meet sales targets. However, it being a common practice didn't influence me to view it as a good practice. Ramp causes many negative economic implications for businesses. It also leads to customers engaging with ill-prepared and untrained new hires.

A few years later, I transitioned my career into software development and attended a developer meetup where Samsung made some virtual reality (VR) headsets available. It was my first VR experience and had a profound impact on me. After that experience, I couldn't stop thinking about VR and its potential applications.

I discovered a small niche of the VR community focusing on immersive training applications. The most compelling were several early-stage startups developing technical and procedural training simulations for enterprise employees. For example, one VR startup created a simulation guiding Chipotle employees through an end-of-day inventory checklist.

As a person who loves continuous learning and development, this use case for VR technology immediately captured my imagination. These interests turned to developing simulations that trained soft skills instead of hard ones. I asked myself, "how can I help salespeople train using VR?"

From my onboarding and training experience as a salesperson, I saw an opportunity to better prepare salespeople using simulated sales experiences in VR. I'd begun deep diving into the sales training and enablement space and uncovered detailed research on the efficacy of live sales role-play in reducing ramp time. However, due to varied social and economic factors, I learned that live role-play training rarely occurs with enough frequency to realize its benefits.

This research supported my theory that simulating sales experiences – role-play automation – had the potential to reduce sales ramp. It also brought to my attention that VR could eliminate the economic and social factors deterring companies from investing in role-play training. For example, the cost of hiring live sales consultants or the anxiety of embarrassing oneself in front of a colleague or manager during training.

After formalizing these concepts and research into a company I called RampEX, I presented my vision to dozens of angel investors. I raised $500,000 in seed capital and kicked off development. Our product vision was to enable salespeople to perform sales scenarios in a controlled and life-like VR environment, thereby allowing them to develop experience through practice without jeopardizing actual customer experiences.

A controlled simulation environment also presented the potential to collect discrete training data that would not typically get captured during live training. Such data could enable training quality to be evaluated by correlating training inputs to sales performance rather than just deductively.

While VR was the technology that inspired me down this path, I quickly realized that VR was just one layer of the technical stack needed to enable my solution. The core content of live sales role-play is dialog, which consists of sales scripts, questions, objections, and presentations. Therefore, I couldn't simply put a VR headset on my customers' salespeople and expect them to role-play. I needed to enable digital avatars to converse and realistically impersonate each salesperson's customer.

This led to the realization that I needed to invent a system unlike any I'd seen or experienced. My software would need to enable digital avatars to perform customer conversations realistically. After several iterations of system design and solution architecting, I arrived at three unique components that worked together to allow conversational role-play between a trainee and a digital avatar:

1. **Content Management System (CMS) for Dialogs** - I designed a data model in which dialog structures could be well represented and captured. With an accompanying CMS, sales managers and trainers could easily catalog the call scripts, organize questions and answers, and other conversational training content they'd long stored in disparate documents. RampEX's VR app had access to this data when running a role-play simulation through an application program interface (API).
2. **Semantic Short-text Similarity Algorithm** - I designed and implemented an algorithm that calculates the semantic similarity between text. Trainees needed to use natural speech when navigating sales dialogs. At the time, most natural language processing (NLP) experts relied on the Bag-of-Words model for handling document similarity, essentially an advanced word matching method. My algorithm was novel in that it leveraged a lexical database to calculate the semantic relationships between words, allowing it to interpret similarity in meaning between text instead of detecting keywords.
3. **Client-side Dialog Engine** - This was the engine that queried dialogs from the CMS and leveraged the semantic algorithm to drive life-like sales conversations between trainees and digital avatars. In this engine, I leveraged a real-time speech-2-text API for transcribing a trainee's speech. The transcribed output and relevant dialog layer would run through the semantic algorithm and identify the most likely response from the scenario getting role-played. That response was then synthesized to audio using text-2-speech and recited by a digital avatar.

I coded the database and NLP modules and managed three other engineers and one designer to build the VR app, customer and admin web app, and microservices endpoints for exposing the NLP modules. In 10 months, my team and I successfully took an idea to a software and hardware system that delivered real value to salespeople and businesses.

The first release of RampEX kicked off pilot programs I established with LinkedIn Chicago and Century21's Miami Real Estate franchise. These companies were excited to use cutting-edge technology to prepare their salespeople better. Thanks to our partnership, they were two of the first companies to ever benefit from role-playing automation.

Through surveys completed by pilot participants, salespeople who spent 15-minutes per day during their first month using RampEX reported feeling more confident handling customer interactions than those who did not. Meanwhile, in more controlled test groups with paid participants, the average time it took for a salesperson to recite a script from memory within 90% accuracy of the original text was approximately 45% less when practicing in RampEX.

I consider RampEX the most inventive and innovative thing I have accomplished in my adult life. I am very proud of the technology my team and I developed.
