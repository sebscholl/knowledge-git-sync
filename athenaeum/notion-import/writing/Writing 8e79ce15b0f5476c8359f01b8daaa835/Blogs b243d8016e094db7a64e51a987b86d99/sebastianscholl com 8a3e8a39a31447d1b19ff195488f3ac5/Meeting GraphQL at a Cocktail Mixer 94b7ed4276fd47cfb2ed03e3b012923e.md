# Meeting GraphQL at a Cocktail Mixer

Created: August 29, 2021 1:58 PM
Location: Florida, Miami, United State of America
Original Publish Date: October 8, 2019
Tags: Research, Tech & Code

![Photo by [Jakob Dalbjörn](https://unsplash.com/@jakobdalbjorn?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/networking-event?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)](https://cdn-images-1.medium.com/max/2560/1*KRft-aOvMiIx_Y-DzG2yMg.jpeg)

Photo by [Jakob Dalbjörn](https://unsplash.com/@jakobdalbjorn?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/networking-event?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

[GraphQL](https://graphql.org/) and [REST](https://restfulapi.net/) are two specifications used when building APIs for websites to use. REST defines a series of unique identifiers (URLs) that applications use to request and send data. GraphQL defines a query language that allows client applications to specify precisely the data they need from a single endpoint. They are related technologies and used for largely the same things (in fact, they can and often do co-exist), but they are also very different.

Now, that last paragraph was incredibly boring. Let’s explain it like this…

### **🍹 You’re at a cocktail mixer**

You’re attending this mixer to help build your professional network, so naturally, you want to collect some data about the people around you. Close by, there are five other attendees.

Their name-tags read:

- Richy REST
- Friend of Richy REST
- Employer of Richy REST
- Georgia GraphQL

Being the dynamic, social, outgoing animal that you are, you walk right up to Richy REST and say, “Hi, I’m Adam Application, who are you?” Richy REST responds:

```json
{   
  name: "Richy REST",   
  age: 33,   
  married: false,   
  hometown: "Circuits-ville",   
  employed: true   
  // ... 20 other things about Richy REST 
}
```

“Whoa, that was a lot to take in,” you think to yourself. In an attempt to avoid any awkward silence, you remember Richy REST specifying that he was employed and ask, “Where do you work?”

Strangely, Richy REST has no idea where he works. Maybe the Employer of Richy Rest does?

You ask the same question to the Employer of Richy REST, who is delighted to answer your inquiry! He responds like so:

```json
{   
	company: "Mega Corp",   
	employee_count: 11230,   
	head_quarters: "1 Main Avenue, Big City, 10001, PL"   
	year_founded: 2005,   
	revenue: 100000000,   
	// ... 20 other things about Richy REST Employer 
}
```

At this point, you’re exhausted. You don’t even want to meet the Friend of Richy Rest! That might take forever, use up all your energy and, you don’t have the time.

However, Georgia GraphQL has been standing there politely, so you decide to engage her.

“Hi, what’s your name?”

```json
{ 
	name: "Georgia GraphQL" 
}
```

“Where are you from, and how old are you?”

```json
{ 
	hometown: "Pleasant-Ville", 
	age: 28 
}
```

“How many hobbies and friends do you have and what are your friends’ names?”

```json
{   
	hobbies_count: 12,   
	friends_count: 50,   
	friends: [     
		{ name: "Steve" },     
		{ name: "Anjalla" },     
		// ...etc  
	] 
}
```

Georgia GraphQL is incredible, articulate, concise, and to the point. You 100% want to swap business cards and work together on future projects with Georgia.

This anecdote encapsulates the developer’s experience of working with GraphQL over REST. GraphQL allows developers to articulate what they want with a tidy query and, in response, only receive what they specified. Those queries are fully dynamic, so only a single endpoint is required. REST, on the other hand, has predefined responses and often requires applications to utilize multiple endpoints to satisfy a full data requirement.

### **Mixer is over**

To expand further upon essential concepts presented in the cocktail mixer metaphor let’s specifically address two limitations that often surface when using REST.

### **1. Several trips when fetching related resources**

Data-driven mobile and web applications often require related resources and data sets. Thus, retrieving data using a REST API can entail multiple requests to numerous endpoints. For instance, requesting a Post entity and related Author might be completed by two requests to different endpoints:

```
someServer.com/authors/:id 
someServer.com/posts/:id
```

Multiple trips to an API impacts the performance and readiness of an application. It is also a more significant issue for low bandwidth devices (e.g. smart-watches, IoT, older mobile devices, and others).

### **2. Over-fetching and under-fetching**

Over/under-fetching is inevitable with RESTful APIs. Using the example above, the endpoint `domainName.com/posts/:id` fetches data for a specific Post. Every Post is made up of attributes, such as `id`, `body`, `title`, `publishingDate`, `authorId`, and others. In REST, the same data object always gets returned; the response is predefined.

In situations where only a Post title and body are needed, over-fetching happens — as more data gets sent over the network than data that is actually utilized. When an entire Post is required, along with related data about its Author, under-fetching gets experienced — as less data gets sent over the network than is actually utilized. Under-fetching leads to bandwidth overuse from multiple requests to the API.

### **Client-side querying with GraphQL**

GraphQL introduces a genuinely unique approach that provides a tremendous amount of flexibility to client-apps. With GraphQL, a query gets sent to your API and precisely what you need is returned — nothing more and nothing less — in a single request. Query results are returned in the same shape as your query, ensuring that response structures are always predictable. These factors allow apps to run faster and be more stable because *they* are in control of the data they get, and not the server.

> “Results are returned in the same shape as queries.”
> 

```json
/* Query */ 
{   
	myFriends(first: 2) {     
		items {
			name
			age     
		}
	} 
}

/* Response */
{   
	"data": {     
		"items": [      
			{ "name": "Steve", "age": 27 },       
			{ "name": "Kelly", "age": 31 }     
		]   
	} 
}
```

### **Reality Check**

Now, at this point, you probably think GraphQL is as easy as slicing warm butter with a samurai sword. That might be the reality for front-end developers — specifically developers consuming GraphQL APIs. However, when it comes to server-side setup, someone has to make the sausage. Our friend Georgia GraphQL put in some hard work to become the fantastic professional she is!

Building a GraphQL API, server-side, is something that takes time, energy, and expertise. That said, it’s nothing that someone ready for a challenge is unable to handle! There are many different ways to hop in at all levels of abstraction. For example:

- **Un-assisted:** If you really want to get your hands dirty, try building a GraphQL API with the help of packages. For instance, like Rails? Checkout [graphql-ruby](https://graphql-ruby.org/). Love Node.js? Try [express-graphql](https://graphql.org/graphql-js/express-graphql/).
- **Assisted:** If fully maintaining your server/self-hosting is a priority, something like [Graph.cool](https://www.graph.cool/) can help you get going on a GraphQL project.
- **Instant:** Tired of writing CRUD boilerplate and want to get going fast? [8base](https://8base.com/) provides an instant GraphQL API and serverless backend that’s fully extensible.

### **Wrapping up**

REST was a significant leap forward for web services in enabling highly available resource-specific APIs. That said, its design didn’t account for today’s proliferation of connected devices, all with differing data constraints and requirements. This oversight has quickly lead to the spread of GraphQL — open-sourced by Facebook in 2015 — for the tremendous flexibility that it gives front-end developers. Working with GraphQL is a fantastic developer experience, both for individual developers as well as teams.

---