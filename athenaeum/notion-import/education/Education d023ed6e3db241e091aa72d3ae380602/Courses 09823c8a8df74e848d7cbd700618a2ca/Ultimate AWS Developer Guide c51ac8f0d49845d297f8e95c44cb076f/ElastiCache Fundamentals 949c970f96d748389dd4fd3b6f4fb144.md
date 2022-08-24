# ElastiCache Fundamentals

Created: May 8, 2019 3:31 PM
Updated: May 8, 2019 3:49 PM

An AWS managed caching service backed by Redis or Memcache. Essentially, an in-memory datastore to help with reducing read-loads on databases.

- Helps make your application stateless by caching states in a common cache.
- Write Scaling using sharding
- Read Scaling using Read Replicas
- Multi AZ with Failover capability
- AWS takes care of:
    - OS maintenance / patching
    - Optimizations
    - setup
    - configuration
    - monitoring
    - Failure recovery and backups

**Architecture**

ElastiCache ends up sitting between the DB and the Application.

1. Application sends query to ElastiCache
2. If data is available in ElastiCache, it’s returned to app (“Cache Hit")
3. If data is NOT available in ElastiCache, nothing is returned to app (“Cache Miss”)
    1. Application connects to DB and makes query, returning data (“DB read”)
    2. After receiving data, app writes query+data to ElastiCache (“Cache write")

**User Session Store**

When a user is logged in to a instance, the ASG must be able to respect their session across multiple instances/applications.

1. User logs into application using credentials
2. Application writes session data to ElastiCache
3. User hits other application (different instance in ASG, maybe)
4. 2nd Application retrieves user session from ElastiCache

**Redis**

- In-memory key-value store
- Sub ms latency
- Cache can survive reboots by default
- Great to host
    - User sessions
    - Leaderboards (like gaming)
    - Distributed states
    - Relieve pressure on DB (like RDS)
    - Pub / Sub capability for messaging
- All AWS managed benefits:
    - Auto Failover for DR
    - Multi AZ
- Support for Read Replicas

**Memcache**

- In-membory object store
- Does NOT survive reboots
- Use cases:
    - Quick retrieval of objects from memory
    - Cache often accessed objects
- **Redis is preferred**