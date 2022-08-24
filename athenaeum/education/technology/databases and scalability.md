# Databases & Scalability

Not good for dynamic data science (i.e., obscure data requirements).

Ways to Scale relational DB:

- Upsize server
- Create multiple servers (sharding)
- Synchronize multiple servers (read-replicas and eventual consistency)

Attributes of NoSQL:

- Nonrelational (everything stored in a single transaction)
- Schemaless
- Cluster friendly
- Preferably, open-source

NoSQL DBs are more simple to change and easier to use. By being cluster friendly, it means that they are part of a network of servers that can have a transaction published across all of them.

NoSQL DBs are great for storing denormalized data, often in a JSON format.

SQL DBs store all the data in a single instance (with the exception of read-replicas), whereas a NoSQL DB stores the data in multiple nodes that are physically separate from one another. The separations are done based on a partition key or shard key, which allows the cluster to split the physical location of where the data is stored. This allows for it to be distributed across multiple nodes. This enables horizontal scaling by only storing a segment of data in a single node/location at a time. 

This means that where you are looking for data, you need to know which partition key you are looking for the data in. For example, partitionKey = “NYC”. These partitionKeys can be assigned however deemed fit and potentially stored in some way with the user credentials.

**SDK Approach for Partition Identification**

NoSQL deals often with both physical and logical partitions. In identifying which physical partition a user may access, an approach could be requesting a hashmap of ranges representing within which range is a specific partition relevant. A hashout of the user email would identify which node their data should access, which then their email address may further be used for the logical partitioning of data on the node. 

**Gateway Approach for Partition Identification**

This approach is almost identical to the SDK approach though done/resolved at the Gateway level. This may be more appropriate for devices on a network that are not supplying credentials at the device level.

ACID Compliance

- Atomicity - “All or nothing” if a transaction involving multiple data fails, none is saved.
- Consistency - Saved data cannot violate DB integrity. Interrupted modifications roll the DB back to its previous state.
- Isolation - No other transactions can affect the transactions in question. I.e., no “mid-air” collisions
- Durability - Once a transaction is complete, any failure or system restart restores the data to the correct state.

**NoSQL Pitfalls**

- Don’t approach NoSQL like an RDMBS
- You **ALWAYS** need to know at least one property (i.e., partition key) when dealing with NoSQL to have a constant query response
- Your access patterns dictate your partitioning strategy (how you app is being accessed? what data will I always have? Requesting device ID? Customer ID? Request origin location?)
- If a partitionKey is missing, you must scan all nodes until you find the required document.
- Once a partitionKey is set, it CANNOT be changed.
- Choosing a bad key may lead to unbalanced and hot partitioning (a.k.a, “City”)
    - Hot partition is where you’ve selected a bad partitioning key and only a few nodes are being overworked/constantly splitting.
    - You can create heatmaps that allow for the viewing/visualization of this.
- A partitionKey that has good cardinality, resulting in an even distribution across nodes, is what’s required to hypothetically result in unlimited scaling of a NoSQL DB where any node never reaches its limit.

### Sharding Pros and Cons

**Pros:**

- Scalability
- Availability & Fault Tolerance

**Cons:**

- Complexity
    - Partition Mapping
    - Routing Layer
    - Non-uniformity
    - Re-sharding
- Analytical Queries
    - Difficulty for aggregation of information