# Why Developers believe "Low Code" means "Can't Code"

It's no secret that developers turn up their noses at platforms and tools branded "low-code." The low-code platforms that have long been around demand that developers learn proprietary tools, adopt sub-optimal infrastructure/architecture, and give up meaningful controls. Simply put, to developers, "low-code" and "can't-code" are synonymous terms.

For developes who dislike low-code, no-code sounds even worse – right? We tend to think of no-code and low-code as tools for building application interfaces. However, they are far too rigid when it comes to building custom-branded client apps with advanced UX/UI design flows. The majority of low-code products have tightly coupled frontends and backends. Nonetheless, prioritizing things like button options over an app's ability to scale.

Let’s forget for a minute that the term low-code even exists. Let's make that even easier and replace "low-code" with "less-code." Don't think of less-code as an industry, but a description of tools and services that allow less code to be written and maintained. What existing platforms and tools come to mind? AWS, Heroku, DigitalOcean, Force.com, Auth0, FileStack, and 100's more – even NPM!

Developers, at the end of the day, love and continuously use platforms, tools, and services that extend superpower functionality to the applications they're developing and responsible for. This is irrespective of whether or not those functionalities are attainable through no-code, low-code, and sometimes whole-lotta-code.

How's this relevant? Traditional low-code players have a bad rap because their products don’t let people create applications they can be proud of. Instead, they ship strict frontend builders with dinky backends to non-developers. These solutions are crutches, not jet-packs. As a result, to developers, low code solutions are total compromise rather than a convenience.

At [8base](https://www.8base.com/), we're rapidly changing the developer experience. The company has taken a new approach to low-code that is rooted in fundamental principles and is developer centric.

## No Boilerplate or "Reinventing the Wheel"

One of the best developer service examples is AWS Simple Storage Service (S3). Most applications, in one way or another, store files and images. However, when developing an app, it's better to find a system that reliably stores images as opposed to building one. App users do not care whether images are handled using X or Y, as long as they are stored. S3 allows you to offload a responsibility that would otherwise distract you from what matters.

This concept goes far beyond what's visible. There are dozens of non-unique systems in every application, which developers spend the majority of their time writing and maintaining. As a result, a significant number of developer hours are spent writing boilerplate code and reinventing systems that already exist.

The 8base GraphQL API was designed to eliminate the need for writing boilerplate API code. In fact, you're data model auto-generates an API that handles all CRUD operations and includes support for pagination, filtering, sorting, and dozens of other features. This eliminates the need for maintaining controllers, serializers, and endpoints that simply interact with a data model.

Along with the API, authentication, single-sign-on, roles and permissions, file uploading, a database, and other systems come ready to use, freeing up developers so they can focus on advancing business logic and user interfaces.

## Commitment to Standards

Only a startup is bold enough to believe that their idea is so big it deserves its own language! While a Domain Specific Language (DSL) might help simplify a concept or syntax, it is a complete turn-off to skilled developers. These pros have spent years refining their skills, and they want tools that work for them - not ones they work for.

Standards, obviously, go beyond simply using popular and open languages. Too often low-code vendors have implemented proprietary technologies at the infrastructure, data, and application level. Choices like these are usually guided by the company's desire to build in vendor lock-in and charge premium consulting fees for customers wanting to leave the vendor’s "ecosystem."

8base, however, is 100% committed to building on standards. This decision started at with our own architecture and is inherited by our customers. Every 8base workspace provisions a unique Aurora MySQL Database instance that is hosted on AWS. The workspace API uses GraphQL, created and open-sourced by Facebook in 2015. Also, custom business logic that's deployed to a project is written in JavaScript and TypeScript.

## API First & Framework Agnostic

Frontend technologies are continually changing across every device. A developer’s choice to build an app using Vue, React, Swift, Kotlin, A-Frame, or Unity, should not be influenced by a cloud backend. However, too many low-code platforms are authoritative in the technologies that can be used client-side; they even control the application itself.

This approach obstructs developers from using the frontend framework of their choice, and it eliminates their ability to evolve over time, thereby pegging their product's ability to innovate on the interface to the low-code platform. With the rare exception of some internal applications, this is always a problem.

8base is an API-first Backend-as-a-Service. This means that we provide everything through a single API endpoint except the frontend. Developers are free to build one or more client applications of any type. The only thing they need is a web connection to securely access their data.

## Build to Scale, Always

The Minimal Viable Product (MVP) mindset has, unfortunately, only justified poorly-architected software. A great MVP can be iterated on. It’s not something that's thrown away once proven. Most of the time, people are going to market with demos. Simply put, an MVP still needs to be a product, not a demo.

When designing 8base, we asked are ourselves a simple question, "How can developers build an MVP that scales into a fully-launched product that never requiries a rewrite?"

Our answer to that question resulted in the adoption of a serverless architecture that is entirely extensible by developers. Leveraging AWS Lambda in the background, a project built on 8base – whether an MVP or Enterprise app – is ready to handle one to 100,000,000 API requests.

You may be wondering how this solves the MVP versus demo issue? The answer lies in the foundation of an application.

Truth be told, there are many fully-launched and successful products that are MVPs. They take a minimalistic approach to feature functionality, providing a "minimally viable solution" to their customers. At any point, they can expand their product offering and know that their technology foundation will meet heightened load requirements.

Core to the 8base platform is its software foundation that developers never need to rewrite. Instead, the 8base community focuses on tweaking their apps, interfaces, and value propositions while knowing that when they get everything right, their application is ready to grow with them.