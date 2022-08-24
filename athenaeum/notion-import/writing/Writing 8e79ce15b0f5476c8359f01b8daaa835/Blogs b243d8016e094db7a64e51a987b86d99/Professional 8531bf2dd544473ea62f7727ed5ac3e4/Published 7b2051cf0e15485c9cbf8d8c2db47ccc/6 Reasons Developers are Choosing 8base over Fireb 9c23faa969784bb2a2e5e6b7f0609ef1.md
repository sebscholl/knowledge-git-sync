# 6 Reasons Developers are Choosing 8base over Firebase

### Some background

There are a ton of essential pieces that go into building production-ready and scalable apps - for both web and mobile. That said, so many of these pieces are non-unique back-end systems that every app requires. Developers often get caught up "re-inventing the wheel" in this regard and are sidetracked from focusing on the parts that make their projects unique.

Imagine it like this: you're a developer building some epic product that lets users upload images. Do you want to engineer and maintain a full object storage service? No! (hopefully) What you want is a service - like S3 - for storage while you build your app.

Dozens of technology companies have come out with products to fill this exact need; the need for software/systems provided as services. Between AWS, Google Cloud Platform, Azure, Bluemix, and many others, 1000's of critical systems for well-defined requirements are available to developers.

That said, building apps that utilize many services is a puzzle more than a map.

That is why companies like 8base and Firebase are becoming wildly successful. By assembling some very, very important and standard pieces of the *puzzle*, we save developers 100s of development and maintenance hours from going into systems that **every application only needs to work**. And again, we deliver that beautiful little bundle as a service/system for developers to build amazing things using.

### Comparing Apples to Applesauce

8base and Firebase perform many of the same functions. Better said, they primarily *address the same need*, though come at it with two very different approaches. Since the proof is in the pudding, let's dig into the platforms shared capabilities and how each achieves them.

### A Back-end for SaaS Apps

Firebase is a well-known backend-as-a-service. It has a ton of useful features that can all be tuned and tweaked to power the back-end of a SaaS application. That said, they've made a much larger effort to be the cloud back-end for **mobile** apps. As a developer building SaaS, you can configure Firebase services to suit your requirements, but it's always going to be extra work.

With 8base, that's pretty different. 8base designed its platform to best accommodate SaaS apps from day one; with a GraphQL API for any web-client, or mobile, to consume. This naturally makes it ideal for developers looking for a backend-as-a-service on any SaaS project. Why? Because things like authorization, multi-tenancy, user administration, and a relational schema builder are all native to the platform.

### Using SQL vs. NoSQL

NoSQL databases are viral these days. Why? Working with them is speedy and fun. That said, their reputation struggles to support complexity in terms of data structures and relationships. Meaning that, for sophisticated business software, choosing NoSQL is risky business.

Relational databases, on the other hand, handle complexity beautifully and provide a ton of other benefits. While relational databases need some management to scale effectively, they are the #1 choice for SaaS apps, providing a much-needed level of security, reliability, and predictability.

Firebase works with NoSQL and 8base works with a MySQL relational database. Any developer that knows the facts is welcome to pick their poison.

### The API: GraphQL or RESTful?

Today, almost all apps are data-driven. Making sure a developer has access to the data they need when they need it, and as they need it, is super important. For the past decade, REST has been the API standard. While the world has benefited hugely from REST, it has some limitations. Lets name some:

1. REST is rigid, requiring different endpoints for different responses.
2. Teams with back-end and front-end devs need to coordinate any change, increasing the complexity of the development effort
3. Endpoints have a predefined response - often returning more data than needed and consuming precious bandwidth.

GraphQL, on the other hand, comes with some huge advantages when compared to REST.

1. A single endpoint can support any query or mutation (a.k.a. update).
2. Queries get defined on the client-side, meaning no more endpoint updates done by backend developers.
3. Queries **only** return data that the developer wants.

8base focuses on reducing the complexity and management of things that developers need to work. One of those things is a CRUD (Create, Read, Update, Delete) API that securely exposes their data from the cloud. It so happens that, in 2019, [GraphQL is the better and more convenient option](https://www.8base.com/blog/why-is-graphql-incorporated-into-8base-so-prominently) for doing just that. That's why 8base natively built into the platform a GraphQL engine that mirrors a project's data model. So managing data via the API works as seamlessly as possible.

Out of the box, Firebase lets users build REST endpoints. You can set up a GraphQL engine on Firebase, but it takes a lot of time and a lot of know-how.

### Role-Based Security

Meanwhile, as everyone is out there building the sleekest and most straightforward user interface that enchants the pants off users, app security is too often being overlooked. That's why Firebase and 8base have security built directly into their products.

Firebase offers the ability to set up role-based security using custom functions that get stored as *rules*. Every *rule* is then run - or not - against API requests. The developer can define all their custom authentication logic.

8base built role-based security directly into its platform, and expose that to developers through a configurable interface. It makes adding permissions and roles for specific actions on specific tables and fields super straight forward. It also supports role-based scoping of records using custom filters.

Pretty much, if developers follow either platform's documentation around how to set up authorization, they won't have to worry about security. It's just up to them how long they want to take to get there.

### AWS or Google Cloud?

Google owns Firebase. Thus, it's no surprise that the product runs on the Google Cloud Platform (GCP). Google does **not** own 8base. Therefore, it's no surprise that the product runs on Amazon Web Services (AWS), which is the market leader in the cloud industry today by a significant margin

[A lot of people](https://www.parkmycloud.com/blog/aws-vs-azure-vs-google-cloud-market-share/) prefer AWS over GCP. AWS has more availability zones, more mature services, provides virtual hosting to many of the world's most complex IT environments, and offers the most competitive pricing. For developers that prefer AWS, [8base is the way to go](https://www.8base.com/blog/serverless-functions-command-line-interface-and-server-side-builds-in-8base). For developers that prefer GCP, you do you!

### Conclusion

There are millions of developers in the world, each with their nuanced preferences to specific stacks and tools. In the greater software ecosystem, 1000s of tools and services exist to help support developers in building amazing apps. Of all the tools, services, frameworks, platforms, and specifications, only a few stand out.

8base is quickly making a name for itself from a straightforward value prop.

> “8base gives developers a back-end they need when building modern apps, the way that they would have wanted to build it themselves”
> 

By configuring dozens of clutch back-end resources and offering them as a production-ready platform, more thought and creativity can be poured into developing client-side - or extending the 8base back-end only with project-specific business logic. Knowing the whole time that security, scalability, database management, and the like are future proof.

A developer is going to come across both 8base and Firebase when researching backend-as-a-service platforms. Both platforms are going to offer them similar features that are backed by different implementations. That said, the experience that the developer has when using either platform is the real acid test. Based on the feedback 8base has been receiving, developers of all levels say 8base is an absolute joy to build with - especially when compared with alternatives.