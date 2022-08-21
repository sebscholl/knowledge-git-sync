# RDS Fundamentals (Relational Data Service)

Created: May 8, 2019 2:15 PM
Updated: May 8, 2019 3:02 PM

A managed DB service by AWS that allows for SQL query language. Allows for creating cloud databases easily using:

- Postgres
- Oracle
- MySQL
- MariaDB
- Microsoft SQL Server
- Aurora (AWS Proprietary DB)

Managed DBs allow for:

- OS Patching
- Continuous Backup and Restore to timestamp (Point in Time restore)
- Monitoring dashboards
- Read replicas for improved read performance
- Multi AZ setup for DR (Disaster Recovery)
- Maintenance windows for upgrades
- Scaling capability (vertical and horizontal)
- BUT you can’t SSH into your instances

**RDS Read Replicas**

For applications that need to perform A LOT of read operations from the database, you’re able to create up to 5 RDS read replicas within AZs, across AZs, and across Regions. Whenever a write operation is made to the master DB instance, asynchronous updates are made the the replicas (so reads eventually become consistent ~ short latency). If you want, the replicas can be promoted to be their own DBs.

- Applications must update their connection string to leverage read replicas.
    - 1 DB + 2 Replicas = 3 connection strings for the application.
- ONLY master DB takes read operations

**RDS Multi AZ (Disaster Recovery)**

A more secure setup would be an application that reads an writes to a Master DB (AZ A) that has a SYNCHRONOUS replication with a standby DB (AZ B).

- Only one DNS connection name between application and DB with a failover policy to move to standby DB in the event of failure.
- In the case of AZ loss, network loss, instance storage failure, etc… Standby gets promoted to master in 2nd AZ.
- Application continues to read and write to a single database.
- Not a scaling solution, only a DR solution
- NO MANUAL INTERVENTION

**Backups**

Backups are automatically configured with RDS on a daily interval.

- Daily snapshot of DB
- Transaction logs in real time
- => ability to restore at any point in time
- 7 to 35 day retention policy
    - Backups can be triggered manually and be saved for as long as you want.

**Encryption**

Encryption can happen at rest with AWS KMS AES-256. Addition SSL certificates can be configured to encrypt data to RDS in flight.

- To enforce SSL:
    - PostgreSQL: rds.force_ssl=1 in RDS Console
    - MySQL: run in DB console:
        - GRANT USAGE ON *.* ‘mysqluser’@‘%’ REQUIRE SSL;
- Connect using SSL
    - Similar to ssh on EC2, download .pem from AWS console and provide it when connecting to DB

**Security**

It’s best practice to deploy RDS databases within private subnets so that they are not directly exposed to the web. They are then controlled access using Security Groups (just like EC2).

IAM Policies are used for controlling who can manage an RDS resource. Additionally, tradition username/password is used for logging into RDS DB - though IAM can now be used on MySQL and Aurora.

**Aurora**

Compatible with MySQL and PostgreSQL that is touted to be cloud optimized (5x performance boost).

- Allows for auto incremental storage growth from 10GB to 64TB.
- Allows for 15 replicas and faster replicas
- Auto failover in multi AZs by default with native High Availability (HA)