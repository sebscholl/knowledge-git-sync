# Explaining Data Relationships, to Grandpa

***Note:** This article is #2 of a series. Please enjoy the first article, [Explaining SQL and NoSQL, To Grandma](https://medium.com/swlh/explaining-sql-and-nosql-to-grandma-9d7a69378be8), for context.*

Data modeling is a discipline that even predates databases. Being able to conceptualize data is a competency that’s required to foresee a project’s relationship between information and systems. In many regards, it’s a way of thinking rather than a simple step when building software.

With application development in mind, data modeling largely goes as follows:

1. An app idea probably relies on information (data)
2. That information needs to be broken-down into entities (data models)
3. Every entity will stores its own types of data (fields)
4. Some entities will have associations with others (relationships)

Tools, like an Entity Relationship Diagram (ERD), help visually map the different entities that comprise a full data requirement. That said, they are mostly planning tools – only some generate code. Regardless of a database technology, defining a holistic picture of what data an application requires is paramount. Additionally, it forces a person to think about *why* some data would be needed.

In this article, we’re discussing two fundamentals of data-modeling within the context of a Relational Database Management System (RDMS).

Also – like last time – we’re actually going to try having fun doing it.

## Explaining Normalization to Grandpa

For months now, Grandma’s remembering system for keeping track of her ridiculously large family has been working beautifully. She hasn’t failed to call on a single one of the grandkid’s birthdays! However, while chatting on the phone is nice, she really prefers to send silly cards with hand-written notes.

The problem is that we never added addresses to her remembering system. She would write cards, but doesn’t know where to send them! Grandma, being overly considerate, didn’t want to bother me to solve this seemingly small problem. So she asked Grandpa to help her add in addresses.

He messed up everything.

Once Grandma just knew that something wasn’t right, her and Grandpa called me to talk about the “updates.”

[Grandchildren Addresses]([https://gist.github.com/sebscholl/7d444de3f96c7fdb1e864420f0626381](https://gist.github.com/sebscholl/7d444de3f96c7fdb1e864420f0626381).js)

“Oy vey! That’s not going to work,” I tell Grandpa.

“Of course it will!”, says Grandpa defiantly. “I’ve been remembering things since before you were born you snot nosed rascal.”

Really, Grandpa? My third cousin Bernard has 3-homes and 2-apartments. How are you going to add all those addresses with this approach? Plus, “Next to Jimmy's on 10th” isn’t an address!

We quickly find agreement in that the information needs structure. So I instruct them to pull out a new sheet of lined paper to start a addresses list the same way we did with *hobbies* and *grandchildren* for the first time.

[Addresses]([https://gist.github.com/sebscholl/e838bd7bc021bbf70f35c869cdf3883f](https://gist.github.com/sebscholl/e838bd7bc021bbf70f35c869cdf3883f).js)

Grandma immediately gets back in the swing of things, while Grandpa asks the right question.

“What are we doing?”

## Normalization

Normalization is the process of structuring data tables so that data dependencies and redundancies are effectively mitigated. It’s practiced by organizing columns (attributes) into tables (models) that have relationships. These tables with their relationships help ensure that