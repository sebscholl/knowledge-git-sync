# Explaining SQL and NoSQL, to Grandma

Created: August 29, 2021 1:30 PM
Location: Miami, United State of America
Original Publish Date: September 3, 2019
Tags: Research, Tech & Code

![https://cdn-images-1.medium.com/max/2560/1*o2IgqXaoE90j8ZtoXPodjA.png](https://cdn-images-1.medium.com/max/2560/1*o2IgqXaoE90j8ZtoXPodjA.png)

One of the most essential choices a developer must make is about what database technology to use. For many years, the options were limited to different flavors of relational databases that supported Structured Query Language (SQL). These include MS SQL Server, Oracle, MySQL, PostgreSQL, and DB2, to name a few.

Over the last 15 years, many new databases have come to the market as part of the No-SQL movement. These include key-value stores such as Redis and Amazon DynamoDB, wide-column stores such as Cassandra and HBase, document stores such as MongoDB and Couchbase, and graph databases and search engines such as Elasticsearch and Solr.

In this article, we’re focused on gaining a high-level understanding of SQL and NoSQL, without peeling back the features of any of the different vendor offerings.

Also, we’re actually going to try having fun doing it.

### **Explaining SQL to Grandma**

Grandma, imagine that I wasn’t your only grandchild. Instead, Mom and Dad loved each other like rabbits and had 100-kids and then adopted 50 more. Also, it’s probably a good idea to even imagine that protective-child-services was **not** a thing.

Now, you love all of us and would never, ever want to forget any of our names, birthdays, favorite ice cream flavor, clothing sizes, hobbies, spouse’s names, offspring’s names, and other super-duper vital facts. However, let’s face it. You’re 85-years old and good old fashion memory just ain’t gonna cut it.

Fortunately, I — being the smartest of your grandchildren — can help. So I come over to your house, pull out several sheets of lined paper and ask you to bake some cookies before we start.

On one sheet of paper, we make a list called *Grandchildren*. Each *Grandchild* gets written down with some essential information about them, including a unique number that will from now on denote which *Grandchild* they are. Also, for the sake of being organized, we write out named attributes across the top of the list so that we always know what information this list contains.

[Grandchildren](Grandchildren%20ab5a399eead94b51a1ebb003671e1073.csv)

After a while, you get the swing of it and are nearly done with the list! However, you turn to me and say, “We forgot to add room for spouses, hobbies, grandchildren!” But no, we didn’t! That comes next and requires a whole new sheet of lined paper.

So out I pull another sheet of paper, and on this one, we title the list *Spouses.* Again, we add the attributes that we care about across the top of the list and start adding in rows.

[Spouses](Spouses%200dc69b0252e943318dff4d88a712f982.csv)

At this point, I explain to Grandma that if she wants to know who is married to who, she only needs to match up an *id* on the *Grandchildren* list with a *grandchild_id* on the *Spouses* list.

After one-dozen-plus cookies, I need a nap. “Can you take it from here, Grandma?” Off I go for a snooze

I come back to earth a few hours later. You killed it, Grandma! Everything looks great, except for the *Hobbies* list. There are like, 1000 hobbies listed. Most of them being the same ones; what happened?

[Hobbies Bad](Hobbies%20Bad%2022808ea69d1d4f6f9ad3f42e97d0862c.csv)

Sorry that I forgot to tell you! Using one list, we need only to track *Hobbies*. Then on another list, we need to track the *Grandchildren* who do those *Hobbies*! We’re going to call this a “*Join List*.” Seeing that you’re visibly frustrated, I feel bad and jump back into list mode.

[Hobbies](Hobbies%2091f5f4332f2648888ecf4a395a3ca9ef.csv)

Once we have our list of hobbies, we then make our second list and call it *Grandchildren’s Hobbies*.

[Hobbies GC Join](Hobbies%20GC%20Join%2035dc226e1262471cbafb2a86d3d6a9f9.csv)

After all this work, Grandma now has an elephant-grade remembering system for keeping track of her ridiculously large family. Plus — to hold me over longer — she asks the magic question, “Where did you learn to do all this?”

### **Relational Databases**

A ***relational database*** is a set of formally described tables (*lists* in our example) from which ***data*** can be accessed or reassembled in many different ways without having to reorganize the ***database*** tables. There are many different types of relational databases — lined paper, sadly, not being one of them!

A hallmark feature of the most popular relational databases is a query language called SQL (Structured Query Language). Meaning that, if Grandma upgrades her remembering system to a computer, she’d be able to quickly answer questions like, “Who hasn’t visited me in the last year, is married, and doesn’t have any hobbies?”

Among the world’s most popular choices for a SQL Database Management System is MySQL, which is open-source. It is implemented primarily as a Relational Database Management System (RDBMS) for web-based software applications.

Some key features of MySQL include:

- It’s really well known, commonly used, and thoroughly tested.
- There’s a lot of qualified developers experienced in SQL and relational databases.
- Data gets stored in various tables, allowing easy relations using primary and foreign keys (fancy speak for *id*s).
- It’s easy to use and performant, making it ideal for big and small businesses.
- The source code is under the GNU General Public License agreement.

Now, forget **EVERYTHING.**

### **Explaining NoSQL to Grandma**

Grandma, our family, is huge. There are 150 grandkids! Many of which are married, have kids of their own, partake in hobbies, and other stuff. At your age, it’s practically impossible to remember everything about all of us. What you need is a remembering system!

Fortunately, I — **not** wanting you to forget my birthday and favorite ice cream flavor — can help. So I run to the corner store, pick up a composition notebook, and come back to your house.

The first step I do is write “Grandchildren” in big, bold letters across the front of the notebook. Next, I flip to page one and start writing in everything that you should remember about me. After a few minutes, the page looks something like this.

```json
{
	"_id":"dkdigiye82gd87gd99dg87gd",
	"name":"Cody",
	"birthday":"09-12-2006",
	"last_visit":"09-02-2019",
	"clothing_size":"XL",
	"favorite_ice_cream":"Fudge caramel",
	"adopted":false,
	"hobbies":[
	      "video games",
	      "computers",
	      "cooking"
	   ],
	"spouse":null,
	"kids":[
	
	   ],
	"favorite_picture":"file://scrapbook-103/christmas-2010.jpg",
	"misc_notes":"Prefers ice-cream cake on birthday instead of chocolate cake!"
}
```

**Me**: “Looks like we’re done here!”

**Grandma**: “But wait, what about all the other *Grandchildren*?”

**Me**: “Oh, right, them. Just dedicate a single page of the composition book to each of them.”

**Grandma**: “Will I need to write down all of the same information for everyone as I did for you?”

**Me**: “No! Only if you want to! Here, let me show you.”

Snagging the pen right out of Grandma’s hands, you flip to a new page and quickly scribble in a record for your least favorite cousin.

```json
{
	"_id":"dh97dhs9b39397ss001",
	"name":"Tanner",
	"birthday":"09-12-2008",
	"clothing_size":"S",
	"friend_count":0,
	"favorite_picture":null,
	"remember":"Born on same day as Cody but not as important"
}
```

That was easy! Whenever Grandma needs to remember something about one of the grandchildren, she only needs to flip to their page in the Grandchildren notebook. All the information about them will be stored right there on their page, which she can quickly change and update.

After all, is said and done, she asks the magic question, “Where did you learn to do this?”

### **NoSQL Databases**

Many **NoSQL** (“not only” SQL) **databases** exist. In our examples, we exemplified a *Document database.* NoSQL databases model data in ways that exclude the tabular relations provided in relational databases. These databases became popular in the early 2000s amongst companies that required cloud-based database clustering due to their sheer scaling requirements (i.e. Facebook). In such applications, having data consistency was a lot less important than performance and scalability.

In the early days, NoSQL databases often got used for super focused data management tasks. Mainly when it came to web and cloud apps, NoSQL DB’s have been proven to process and distribute significant volumes of data. Engineers building with NoSQL have also liked the flexible data schema (or complete lack thereof), so that fast changes to apps being updated often were possible.

The key features of NoSQL include:

- A highly flexible way of persisting data
- Horizontal scaling to clusters
- Eventual consistency on persistence/propagation
- Documents that are identified using unique keys

### **Head to Head Comparisons**

> MySQL requires a defined and structured schema.NoSQL allows the persistence of any data in the “document.”
> 

> MySQL has a huge community supporting it.NoSQL has a small and rapidly growing community.
> 

> NoSQL features easy scalability.MySQL needs more managed scalability.
> 

> MySQL utilizes SQL, which gets used in a multitude of database types.NoSQL is a design-based database with popular implementations.
> 

> MySQL employs a structured query language (SQL).NoSQL uses no structured query language.
> 

> MySQL has many fantastic reporting tools.NoSQL features few reporting tools that are difficult to standardize.
> 

> MySQL can offer performance problems for big data.NoSQL delivers excellent performance on big data.
> 

**8base’s Thoughts**

At my company, [8base](https://8base.com/), we provision every project’s workspace with an Aurora MySQL relational database that gets hosted on AWS. While NoSQL is a logical choice when your app’s requirement demands big-data grade performance and scalability, we believe that the strict data consistency enforced by an RDBMS is necessary when building SaaS apps (software-as-a-Service) and other business software.

For startups and developers building business applications — ones that need reporting, transactional integrity, and well-defined data models — investing their time into working on a relational database is, in our opinion, the right choice.