# What's GraphQL and How Can It Help Teams Developer Faster? VIDEO SCRIPT

Created: June 22, 2020 2:54 PM

Hi! I'm Sebastian, product manager here at 8base. If you find this video helpful, please like it and subscribe to our channel. It really helps us grow!

In this video, we're going to be talking about GraphQL and how it can be the key to helping development teams develop faster.

So first off, what even is GraphQL? 

Well, GraphQL is a "query language" for web APIs - in the name itself, "query language" is what the QL stands for. And that said, GraphQL is entirely unlike anything that developer's have previously used when interfacing with standard web APIs.

We can actually look at this difference right now side by side. 

For most APIs that a developer might fetch data from, for example the ______ API, they typically work by a request being made to a specific endpoint which determines which data comes back. Sometimes the url will accept different parameters that can effect which records come back. However, at the end of the day, with a typical REST API you hit an endpoint and are returned a large chunk of JSON data. 

This has been the status quo for awhile. But what makes GraphQL?

Well instead of just being constrained to whatever data object is predetermined by a REST API endpoint to be returned, GraphQL allows the develop to "ask" for the specific data that they want back. The response they then get from the API is exactly what they asked for, nothing more and nothing less.

On top of that, GraphQL allows for great relational querying that allows developers to make less requests to the API than they would otherwise when using normal REST APIs.

To demonstrate that, let's say that we get back a certain ID in our first query of a related object and we want to fetch more data about it. In the REST world we'd need to do a new API request to a different endpoint than the first one to fetch that data. In the GraphQL world, we're able to update our original query to include the related data. As you can probably guess, this results in only 1 API request being needed.

Now, what's really important to understand about GraphQL is that it's a specification and NOT an implementation. This means that GraphQL isn't a single technology, but instead an set of rules and concepts that any company or developer can build their own implementation of using any coding language or development framework that they choose. Which is awesome, because it allows for a ton of creativity and innovation in any GraphQL implementation project.

So, with all that said, there are really two sides to any GraphQL project which is the server side and the client side - or the back-end and then the front-end. This means that you can just use an existing GraphQL API if you want to without having to learn the server-side. Or if you and your team want to build and maintain a GraphQL server application, you can do so using pretty much any language!

Regardless of what language you're using, what the GraphQL server is doing is defining the API, which gets written our as a series of "type" definitions in which you define the exact shape of your data and resolvers which execute the code to fulfill a request.

Meanwhile, on the client side they're are many tools that make it easier to execute GraphQL requests against a GraphQL API. Under the hood, these all boil down to HTTP Post requests, however the client tools make it easier to pass variables, set headers, and other GraphQL specific validations when writing Queries.

So, at this point we have a pretty good idea of how GraphQL works, however how does it help teams develop faster?

The schema you define when building a GraphQL API should encapsulates a full data model or graph of your project. Once this API is set up, suddenly client-side developers are able to work independently of server-side developers, because all of the data they might require to in the view layer is available through the graph. 

This is different from the REST world, in which if a specific endpoint exposed either too little or even too much data for the client-side developer to use, they would have to wait for a new endpoint to be stood up before moving forward. 

For those developers and teams who are simply looking for a managed GraphQL API that they can just use and customize as needed, rather than build from scratch and have to maintain, full application development can be accelerated even more!

80% of APIs all have the same standard operations, which are CRUD operations. For example, creating, reading, updating, and deleting records. This is where a backend platform, like 8base, is able to shave months off development projects by reverse engineering a GraphQL API based on a given data model. This is how many development teams can start a project and have 80% or more of the backend requirement done, right out of the gate.

If you found this video helpful, please like it and subscribe to our channel. Looking forward to seeing you in future videos!