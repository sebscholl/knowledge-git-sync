# Caching Systems Review

### **What is Caching?**

In computing, a cache is a high-speed data storage layer which stores a subset of data, typically transient in nature, so that future requests for that data are served up faster than is possible by accessing the data’s primary storage location. Caching allows you to efficiently reuse previously retrieved or computed data.

## **How does Caching work?**

The data in a cache is generally stored in fast access hardware such as RAM (Random-access memory) and may also be used in correlation with a software component. A cache's primary purpose is to increase data retrieval performance by reducing the need to access the underlying slower storage layer.

Trading off capacity for speed, a cache typically stores a subset of data transiently, in contrast to databases whose data is usually complete and durable.

- Cached information can include the results of database queries, computationally intensive calculations, API requests/responses and web artifacts such as HTML, JavaScript, and image files.
- Compute-intensive workloads that manipulate data sets, such as recommendation engines and high-performance computing simulations also benefit from an In-Memory data layer acting as a cache.
    - In these applications, very large data sets must be accessed in real-time across clusters of machines that can span hundreds of nodes. Due to the speed of the underlying hardware, manipulating this data in a disk-based store is a significant bottleneck for these applications.
    

**Design Patterns:** 

- In a distributed computing environment, a dedicated caching layer enables systems and applications to run independently from the cache with their own lifecycles without the risk of affecting the cache.
- The cache serves as a central layer that can be accessed from disparate systems with its own lifecycle and architectural topology.
    - This is especially relevant in a system where application nodes can be dynamically scaled in and out.
- If the cache is resident on the same node as the application or systems utilizing it, scaling may affect the integrity of the cache.
    - When local caches are used, they only benefit the local application consuming the data.
    - In a distributed caching environment, the data can span multiple cache servers and be stored in a central location to benefit all the consumers of that data.

**Caching Best Practices:** 

- When implementing a [cache layer](https://aws.amazon.com/elasticache/), it’s important to understand the validity of the data being cached.
    - A successful cache results in a high hit rate, which means the data was present when fetched. A cache miss occurs when the data fetched was not present in the cache. Controls such as TTLs (Time to live) can be applied to expire the data accordingly. Another consideration may be whether or not the cache environment needs to be Highly Available, which can be satisfied by [In-Memory engines](https://aws.amazon.com/elasticache/) such as [Redis](https://aws.amazon.com/redis/).
- In some cases, an In-Memory layer can be used as a standalone data storage layer in contrast to caching data from a primary location.
    - In this scenario, it’s important to define an appropriate RTO (Recovery Time Objective--the time it takes to recover from an outage) and RPO (Recovery Point Objective--the last point or transaction captured in the recovery) on the data resident in the [In-Memory engine](https://aws.amazon.com/elasticache/) to determine whether or not this is suitable.
    - Design strategies and characteristics of [different In-Memory engines](https://aws.amazon.com/elasticache/) can be applied to meet most RTO and RPO requirements.
    

## **Benefits of Caching**

### **Improve Application Performance**

Because memory is orders of magnitude faster than disk (magnetic or SSD), reading data from in-memory cache is extremely fast (sub-millisecond). This significantly faster data access improves the overall performance of the application.

### **Reduce Database Cost**

A single cache instance can provide hundreds of thousands of IOPS (Input/output operations per second), potentially replacing a number of database instances, thus driving the total cost down. This is especially significant if the primary database charges per throughput. In those cases the price savings could be dozens of percentage points.

### **Reduce the Load on the Backend**

By redirecting significant parts of the read load from the backend database to the in-memory layer, caching can reduce the load on your database, and protect it from slower performance under load, or even from crashing at times of spikes.

### **Predictable Performance**

A common challenge in modern applications is dealing with times of spikes in application usage. Examples include social apps during the Super Bowl or election day, eCommerce websites during Black Friday, etc. Increased load on the database results in higher latencies to get data, making the overall application performance unpredictable. By utilizing a high throughput in-memory cache this issue can be mitigated.

### **Eliminate Database Hotspots**

In many applications, it is likely that a small subset of data, such as a celebrity profile or popular product, will be accessed more frequently than the rest. This can result in hot spots in your database and may require overprovisioning of database resources based on the throughput requirements for the most frequently used data. Storing common keys in an in-memory cache mitigates the need to overprovision while providing fast and predictable performance for the most commonly accessed data.

### **Increase Read Throughput (IOPS)**

In addition to lower latency, in-memory systems also offer much higher request rates (IOPS) relative to a comparable disk-based database. A single instance used as a distributed side-cache can serve hundreds of thousands of requests per second.

## **Use Cases & Industries**

**Use CasesIndustries**

- **Learn about various caching use cases**
    
    ### **Database Caching**
    
    The performance, both in speed and throughput, that your database provides can be the most impactful factor of your application’s overall performance. And despite the fact that many databases today offer relatively good performance, for a lot use cases your applications may require more. Database caching allows you to dramatically increase throughput and lower the data retrieval latency associated with backend databases, which as a result, improves the overall performance of your applications. The cache acts as an adjacent data access layer to your database that your applications can utilize in order to improve performance. A database cache layer can be applied in front of any type of database, including relational and NoSQL databases. Common techniques used to load data into you’re a cache include lazy loading and write-through methods. For more information, [click here](https://aws.amazon.com/caching/database-caching/).
    
    ### **Content Delivery Network (CDN)**
    
    When your web traffic is geo-dispersed, it’s not always feasible and certainly not cost effective to replicate your entire infrastructure across the globe. A [CDN](https://aws.amazon.com/caching/cdn/) provides you the ability to utilize its global network of edge locations to deliver a cached copy of web content such as videos, webpages, images and so on to your customers. To reduce response time, the [CDN](https://aws.amazon.com/caching/cdn/) utilizes the nearest edge location to the customer or originating request location in order to reduce the response time. Throughput is dramatically increased given that the web assets are delivered from cache. For dynamic data, many [CDNs](https://aws.amazon.com/caching/cdn/) can be configured to retrieve data from the origin servers.
    
    [Amazon CloudFront](https://aws.amazon.com/cloudfront/) is a global CDN service that accelerates delivery of your websites, APIs, video content or other web assets. It integrates with other Amazon Web Services products to give developers and businesses an easy way to accelerate content to end users with no minimum usage commitments. To learn more about CDNs, [click here](https://aws.amazon.com/caching/cdn/).
    
    ### **Domain Name System (DNS) Caching**
    
    Every domain request made on the internet essentially queries [DNS](https://aws.amazon.com/route53/what-is-dns/) cache servers in order to resolve the IP address associated with the domain name. DNS caching can occur on many levels including on the OS, via ISPs and DNS servers.
    
    [Amazon Route 53](https://aws.amazon.com/route53/) is a highly available and scalable cloud [Domain Name System (DNS)](https://aws.amazon.com/route53/what-is-dns/) web service.
    
    ### **Session Management**
    
    HTTP sessions contain the user data exchanged between your site users and your web applications such as login information, shopping cart lists, previously viewed items and so on. Critical to providing great user experiences on your website is managing your HTTP sessions effectively by remembering your user’s preferences and providing rich user context. With modern application architectures, utilizing a centralized session management data store is the ideal solution for a number of reasons including providing, consistent user experiences across all web servers, better session durability when your fleet of web servers is elastic and higher availability when session data is replicated across cache servers.
    
    For more information, [click here](https://aws.amazon.com/caching/session-management/).
    
    ### **Application Programming Interfaces (APIs)**
    
    Today, most web applications are built upon APIs. An API generally is a RESTful web service that can be accessed over HTTP and exposes resources that allow the user to interact with the application. When designing an API, it’s important to consider the expected load on the API, the authorization to it, the effects of version changes on the API consumers and most importantly the API’s ease of use, among other considerations. It’s not always the case that an API needs to instantiate business logic and/or make a backend requests to a database on every request. Sometimes serving a cached result of the API will deliver the most optimal and cost-effective response. This is especially true when you are able to cache the API response to match the rate of change of the underlying data. Say for example, you exposed a product listing API to your users and your product categories only change once per day. Given that the response to a product category request will be identical throughout the day every time a call to your API is made, it would be sufficient to cache your API response for the day. By caching your API response, you eliminate pressure to your infrastructure including your application servers and databases. You also gain from faster response times and deliver a more performant API.
    
    [Amazon API Gateway](https://aws.amazon.com/api-gateway/) is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.
    
    ### **Caching for Hybrid Environments**
    
    In a hybrid cloud environment, you may have applications that live in the cloud and require frequent access to an on-premises database. There are many network topologies that can by employed to create connectivity between your cloud and on-premises environment including VPN and Direct Connect. And while latency from the VPC to your on-premises data center may be low, it may be optimal to cache your on-premises data in your cloud environment to speed up overall data retrieval performance.
    
    ### **Web Caching**
    
    When delivering web content to your viewers, much of the latency involved with retrieving web assets such as images, html documents, video, etc. can be greatly reduced by caching those artifacts and eliminating disk reads and server load. Various web caching techniques can be employed both on the server and on the client side. Server side web caching typically involves utilizing a web proxy which retains web responses from the web servers it sits in front of, effectively reducing their load and latency. Client side web caching can include browser based caching which retains a cached version of the previously visited web content. For more information on Web Caching, [click here](https://aws.amazon.com/caching/web-caching/).
    
    ### **General Cache**
    
    Accessing data from memory is orders of magnitude faster than accessing data from disk or SSD, so leveraging data in cache has a lot of advantages. For many use-cases that do not require transactional data support or disk based durability, using an in-memory key-value store as a standalone database is a great way to build highly performant applications. In addition to speed, application benefits from high throughput at a cost-effective price point. Referenceable data such product groupings, category listings, profile information, and so on are great use cases for a [general cache](https://aws.amazon.com/caching/general-cache/). For more information on general cache, [click here](https://aws.amazon.com/caching/general-cache/).
    
    ### **Integrated Cache**
    
    An integrated cache is an in-memory layer that automatically caches frequently accessed data from the origin database. Most commonly, the underlying database will utilize the cache to serve the response to the inbound database request given the data is resident in the cache. This dramatically increases the performance of the database by lowering the request latency and reducing CPU and memory utilization on the database engine. An important characteristic of an integrated cache is that the data cached is consistent with the data stored on disk by the database engine.
    

## Embedded Cache

This is a cache stored in the application to ease the requirement of accessing the DB for data referenced frequently within the application itself.

- Reference information
- Mapping fields
- Private cache/info

## Client-Server Cache

This is a cache that exists between applications and the database. This is a separate instance from the application that can be connected to by one or more applications. This is often done when the same cache needs to be accessed from multiple applications.

- Shared caches
- Standalone caches

## Distributed Cache

This is when multiple instances of a cache that exists between applications and the database. This allows for low-latency and high-volume transactions, using a cache.

## Cloud Cache or CSP Managed Cache

(AWS ElastiCache) Biggest benefit is that of caching with the management being executed by the CSP.

- Managed cache
- Scalable

## Reverse-Proxy Cache

This is when a cache exists on a proxy, like a Load Balancer, which caches the responses returned by the applications. Thus, a cache can be access and a response returned before every going to the application - when valid. 

- Uncommon
- API Gateway pattern is where it’s most often used.
- Caches the full API response
- No Specific maintenance (no data mapping or transformation or specific server configuration for the cache itself - it borrows from the infrastructure of the Load Balancer)

## Side-car Cache

(AWS EKS - Kubernetes) has a cluster running many pods. In each pod an instance of a cache could be instantiated, serving the the application in the pod. This is exact same as client-server cache, though replicated in pods.

- Low-latency between application and server
- Application behaves like a client-server (App and data isolation)
- Containerized caches

## Reverse-Proxy Side-car Cache

Exact same thing as the reverse-proxy but done within the context of a containerized pod. 

- Caches the full API response
- No Specific maintenance (no data mapping or transformation or specific server configuration for the cache itself - it borrows from the infrastructure of the Load Balancer)
- Low-latency between application and server
- Application behaves like a client-server (App and data isolation)
- Containerized caches