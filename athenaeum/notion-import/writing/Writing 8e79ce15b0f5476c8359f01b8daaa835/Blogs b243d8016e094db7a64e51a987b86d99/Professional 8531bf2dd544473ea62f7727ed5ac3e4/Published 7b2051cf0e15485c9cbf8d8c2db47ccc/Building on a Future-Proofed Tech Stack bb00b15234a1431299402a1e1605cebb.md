# Building on a Future-Proofed Tech Stack

Chapter 1: About the Author

Chapter 2: The 8base Tech Stack

Chapter 3: Architect for Scale

Chapter 4: The Importance of the Data Model

Chapter 5: Agency Questions

Chapter 6: Conclusion

Chapter 1: About the Author

As a software engineer turned entrepreneur, I've seen it all. Everything type of software imaginable to the wildest of startup successes and failures. In the process of paving my own path, I scaled two venture-backed SaaS companies and raised over $100-million of Silicon Valley venture capital between them.

Those ventures – while successful and still operating – burned through mountains of cash. The products we built were underpinned by complex, single-instance, multi-tenant software systems; requiring highly specialized engineers to maintain them. That's not to mention the many sales and implementation people needed to get our products in the customer's hands!

After the second rodeo, I thought genuinely about my experiences. How could I channel the most valuable lessons learned into one operation? Concluding much thought and deliberation, I founded 8base in mid-2017.

Now, I'm excited to help you, the reader, and many others in the world who are building software applications. My goal is simple; let's streamline building software so that it's:

- Faster
- Better
- Cheaper

In the early Imagineering of what 8base would be, some core ideas percolated up.

First off, it had to be production-ready. This means that whatever users build on 8base can't have a glass ceiling when it comes to scaling.

Secondly, it had to be extremely approachable. Plenty of hard to use and expensive "convenience solutions" exist. 8base must be a straightforward software platform, where complexities get reduced to intuitive interfaces - both for technical and non-technical users.

Lastly, it had to be stable. 8base's architecture can't be flimsy – at all. Our goal for the platform to underpin modern apps is a huge responsibility. Therefore, our architecture couldn't only support our own software, but also our customers'.

8base's Foundational Thinking

Pooling our experience and opinions helped us drive our architectural thinking far beyond that of our competitors. That may make you ask, "So what's our secret sauce?” What do we prioritize in all of our discussions and collaborations?

- API-First: Computing infrastructure, data, and business logic should be abstracted into a backend and provisioned via a single, dynamic GraphQL API.
- Elasticity: Computing infrastructure should be made available as a fully elastic service to a running application.
- Front-End Flexibility: Software is more art than science these days as companies express themselves technologically to their customers. Builders must be able to design and construct user interfaces in any style, across a myriad of device form factors.

If you can't already tell, I'm passionate about modernizing with the changing demands and requirements of building today's applications. Core to that is an understanding that technology is more than just a product – it's the entire user experience. It's something that facilitates storytelling, which is the end-all, be-all today.

That's why my team and I at 8base are now so determined to make our platform flexible and elastic. We don't believe that creativity and planning should be hindered. It should, instead, be augmented with a tool that has been simplified and expanded to accommodate and accelerate application development.

But, enough about me and our company beliefs. It's time to dive into the meat of this e-book.

What is 8base built on? What advice do I have to give? How can you fortify your business as it grows towards the future?

Let's get started.

Chapter 2: Our Tech Stack

"We are changing the world with technology." – Bill Gates

By definition, a tech stack is a combination of programming languages, tools, and frameworks that the developers use to create web and mobile applications. There are two sides to most well-architected and modern apps. They are the client-side and server-side, also known as the frontend and backend.

Needless to stay, a tech stack makes or breaks technological exploration, refinement, and advancement today. That's why having a thoughtful collection of tools and frameworks is so essential. Naturally, we take it pretty seriously ourselves. I'm going to share with you our tech stack and why we've carefully selected each tool that's part of the tech stack.

Amazon Web Services (AWS)

For starters, 8base chose AWS as our computing infrastructure. As the market leader in cloud computing services, there are seemingly infinite ways to use AWS. A few of our own use cases include:

1. AWS Lambda: AWS Lambda lets you run functions without provisioning or managing servers. You pay only for the compute time you consume, and there is no charge when your code is not running. Lambda is what's considered "serverless" or "function-as-a-service," meaning that functions run in response to events while computing resources are automatically managed.

This is a crucial building block of 8base, and why our customers are confident in the scalability of their own projects. Lambda fulfills computing needs like your power company: via a microunit-based, fully elastic, and metered service. Additionally, it minimizes or eliminates the need for DevOps personnel who manage the infrastructure inside of AWS, which means fewer costs for startups.

Since roughly [70% of startups fail](https://medium.com/swlh/why-90-of-startups-fail-and-what-to-do-about-it-b0af17b65059) due to scaling – tech, sales, and marketing – too early. Why? They quickly incur costs they are not prepared or able to pay. With more lean-startups popping up every day, cost reduction is essential for the success of startup platforms in the future.

1. AWS Aurora MySQL & MongoDB Atlas: We use both Aurora MySQL and MongoDB databases because they are fast, redundant, fault-tolerant, managed, and scalable. This is key to not only ensuring the integrity of our data but also data in workspaces. Therefore, every 8base workspace gets a dedicated Aurora MySQL instance that's fully managed.
2. AWS S3 (Simple Storage Service): We use this tool for object storage service. However, we also do the difficult work of exposing S3 to workspaces and front-end applications. The result? It makes it very easy to store documents, pictures, voice files, and more. We chose S3 because it's inexpensive, fast, reliable, and infinite when it comes to storage capacity. What could be more important than that?
3. AWS's API Gateway: Workspaces get a dedicated GraphQL API endpoint that runs on Lambda. However, 8base automatically provisions an API gateway for exposing and securing all endpoints – both for ourselves and customers.

GraphQL API Engine

We went ahead and built a powerful GraphQL API engine as part of our platform. GraphQL is a specification developed by Facebook that got open-sourced in 2015. Using that specification, 8base developed its own GraphQL engine. This allows developers, through a single API endpoint, to dynamic communication between the backend and front-end.

GraphQL lets front-end developers work very quickly without depending upon backend developers for specific resources. 8base's secret sauce in building our engine is that we auto-generate all the operations needed to manage a workspace specific data-models.

In the end, it enables our platform to move faster and our developers to code happier. Everyone using 8base gets that same benefits!

Front-End Technology: React

At the end of the day, 8base support applications built using any front-end technology. However, 8base's client app is built using React: an open-source JavaScript library maintained by Facebook and a sizeable open-source developer community.

That said, if tomorrow 8base decided to build a Vue front-end, or iOS mobile app, or Samsung smartwatch app, we could quickly do so! That is the beauty of being API-first, and why we – and our customers – can use any front-end framework in building their client apps.

Authentication Provider: Auth0

8base uses Auth0 as our authentication provider, as well as the default for customer apps using 8base authentication. Auth0 comes with easy integrations that expose over 30 social and enterprise identity providers. Plus, it includes multi-factor authentication and other powerful features that round out our robust offering.

Final Notes

Besides a few sprinkles here-and-there, these are the core 8base building blocks! Now that you know our tech stack and what to expect when working with 8base, it's time to look at practical tips, tricks, and advice when building your own applications.

Over [19 million](https://thisisglance.com/7-surprising-statistics-about-the-world-of-app-development/) people classify themselves as software developers as 2018. Admittedly, that number is growing. However, you are not alone if you're an entrepreneur or team leader that's unsure about how to proceed or who to trust!

No matter how creative and innovative you might be, your app will only be as good as the tech stack supporting it. Every artist needs paint and a paintbrush to get started on their masterpiece (or strings, hands, etc.). That means every software engineer needs the right tools to bring them to their realized, end technology result, right?

Here are some tips you won't want to forget.

Chapter 3: Architect for Scale

"The best way to predict the future is to create it." – Peter Drucker

The "lean startup" approach is a common strategy for launching a startup. It involves slapping together a software product so that founders can immediately begin pursuing product-market fit.

However, what happens when the product-fit is correct, and everything takes off? Suddenly, the entire product needs to be rewritten! Can you imagine the additional time, frustration, and budgeting costs that get added to the equation? Meanwhile, all of it could be avoided with a more quality-focused approach.

It's always better to invest now in laying a solid foundation for the future of your startup. Approaching everything haphazardly, in the beginning, is going to get you into far more trouble than if you take your time and do things the right way.

Start with a Foundation

It's better to build on a solid foundation with the ability to iterate on a product without ever having to sacrifice the ability to scale. Many startups will fail because their operation is only [planned for the interim](https://www.forentrepreneurs.com/why-startups-fail/), not for the future.

8base, from the get-go, focused on the future. This approach is paying dividends now. We get to improve our product incrementally. Bespoke systems and competitors at our stage are scrambling with technical upgrades and rewrites – which are invisible to their consumers!

So how can you create a solid foundation for your startup?

1. Think Long Term: At the beginning of any project, excitement and potential can cause the more "boring" elements to be ignored. Who wants to worry about building a software foundation when they can go after an MVP prototype that can be shared with users? The excitement can make it easy for us to look past the planning stages that actually set the stage for success far into the future.

Whatever you do, make time now. Slow down and establish a foundation that is going to be conducive to innovation, scalability, and attainable success in the future.

1. Create a Pyramid Model: Always go from the bottom up. Start with a foundation that will support all of the changes, data, requirements, services, and so forth in the future. Again, look at your operation like it's a pyramid and take the time to create a base that will make it possible to scale to any requirement.

Architecting for *scale* is not as complicated as it sounds if you make it the first technical priority. However, it's hugely complex when a prototype app that users are demanding more of being adapted. 8base makes scaling it entirely attainable while avoiding the expensive rewrites that can actually sink a startup before it has a chance to get off of the ground.

Chapter 4: Importance of the Data Model

As we just touched on architecture, we're now going to look at the structure data model of a project. Some of the backends that exist today allow front-end developers, especially mobile developers, to dump data into them without any consideration for the overall structure.

For smaller apps or tinier projects, that can work. I'm not saying something is impossible.

For most apps, it's simply not ok.

Whenever you're choosing an unstructured data approach, you need to make sure it's the right architectural choice – not just the easy one! As we just mentioned in regards to building a foundation, it might be easier to develop now and consider later. However, you'll be better off the more effort you put into the new startup product.

Data is the New Gold

Every [magazine](https://www.itchronicles.com/technology/data-the-new-gold-rush-for-businesses/) in existence agrees that data is the new gold. Forget the shiny stuff you can find in mountains and excavations. Consider the value of data when it comes to any kind of project or undertaking. Data tells you the whole story, like where you've come from, where you can go, what's working, what's not, and what you need to improve.

This makes data one of the most readily available and priceless things you can collect. If you're working on a project that involves a nonsensical data dump (non-structured data), you're going to overlook valuable information and analysis opportunities. You're also going to contribute to an unstable foundation that will signal problems down the line.

Creating a robust data model allows companies to know what data they are collecting and how to analyze it. It is a core and differentiating exercise in designing a well-architected application.

Chapter 5: Agency Questions

Agencies are typically trying to supply the best possible services and products, so they stay in business. They want to provide these services for as long as they can, amassing more clients, hiring more employees, and fortifying their selection, so they stay relevant.

Along the way, their incentives do not always align with those of the founder. There can be miscommunication, or if an agency gets too big, there can be massive disconnects that end up destroying your startup along the way. You don't deserve that kind of side-lining, which is why you should do your due diligence/homework ahead of time.

Here are some critical questions to ask the development agency:

1. Do you approach software development as a design-first or engineering-first exercise? As you can imagine, you want to work with a team that is more preoccupied with an engineering foundation than the design – which is your primary concern.
2. Are application designs wireframes, high-fidelity prototypes, or both? A great agency will provide you with both.
3. What startups have you helped that achieved product-market fit and became financially stable? Don't be afraid to ask for examples, websites, portfolios, etc.!
4. How do you architect applications to ensure I never need to rewrite them? Think back to the previous chapter. You want to work agencies that obsess about creating software foundation, minimizing the complexity and rewrites in the future.
5. Will I be able to hire developers that aren't you? A fair question to ask.
6. Will my software scale when the time comes? You want the answer to be a resounding YES. Scalability should be of the utmost concern.
7. What happens during the project when we are altering our designs based upon new market information? You want a team that is adaptable and receptive to change.
8. What resources will be needed to support our product once it's built and goes live? Do all of your homework now, so you are perfectly prepared for when it's go-time.

Any serious agency will be more than happy to answer these questions/display their work for you to see. If they seem like they would rather sidestep issues or not provide actual tangible work for you to observe, that should give you your answer.

Do your due diligence – no one else is going to do it for you! Don't be afraid to get out there and acquire the information you deserve.

Chapter 6: Conclusion

Building tech products is a never-ending journey for entrepreneurs. Why? Because technology is ever-changing. A piece of technology considered hot today can become outdated the next. The innovation being poured into products is outstanding and sometimes intimidating.

Although it might be fast-paced, aspects of the technology world can be predictable and broken down into a formula that will work for anyone.

The early decisions of:

- Who: Who is architecting the product? Who is designing it? Who is building it?
- What: What underlying technologies are being leveraged?
- How: How are these technologies, and teams involved, work together to reach the end goal?

Make a magnitude of difference between success and failure. Sticking the landing on these three decisions gives an entrepreneur a fighting chance.

Making a mistake in any of these three decisions can mean massive delays, expensive problems, added costs, and perhaps failure. I don't want that for you! With these tips, tricks, questions, and insight, you should be able to control the future of your software engineering.

Thanks for reading! Feel free to add comments or reach out to me with questions at albert@8base.com. Additionally, start your next project off on the right foot at [8base.com](https://www.8base.com/).