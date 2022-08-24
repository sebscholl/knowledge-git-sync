# EBS Fundamentals (Elastic Block Store)

Created: May 7, 2019 8:00 PM
Updated: May 8, 2019 12:22 PM

When an instance is terminated we loose our root drive on the instance. Sometimes this can be the fault of AWS - for example, faulty hardware. In either case, having an ability to safely store our root drive as to protect our instance data BETWEEN instances. Thus, EBS allows you to attach a network drive (not physical drive) to an instance while it is running. It can allow for EBS to be reassigned between instances quickly.

EBS drives are locked to Availability Zones (AZ) - NOT regions (aka. Us-east-1a EBS can’t attached to us-east-1b). To move a volume, you must snapshot it. Multiple volumes may be attached to the same instance.

**VOLUMES ARE TIED TO SPECIFIC INSTANCES**

Params:

- GBs (Size)
- IOPS (I/O operations per second)

**Pricing**

Billed on ALLOCATED CAPACITY, not use. The same volume can have its capacity changed over time.

**Types**

- *Factors: Size, Throughput, IOPS*
- GP2 (SSD-DEFAULT): General purpose SSD volume with solid price/performance balance.
- IOI (SSD): Highest-performance SSD for mission-critical low-latency or high throughput workloads
- ST1 (HDD): Low cost HDD volume for frequently accessed and throughput intensive work
- SC1 (HDD): Lowest cost for not commonly accessed data on low workloads

**Resizing**

Drives can be resized for both Size and IOPS and the to be re-partitioned upon doing so.

**Snapshots**

Backups of EBS storage drives. They only take the volume of data up space-wise (aka. 100GB drive with 5GB of data will only produce 5GB snapshot)

- Backups
- Volume migration
    - resizing
    - changing type
    - Encrypting volumes

**EBS Encryption**

Creating encrypted volumes accomplishes the following.

- Data is encrypted at rest (on write)
- Encrypted “in-flight”, communicating between volume and instance
- All snapshots are automatically encrypted
- All volumes created FROM SNAPSHOTS are encrypted
- ENCRYPTION IS HANDLED BY AWS
- Minimal impact on latency (thus recommended)
- Encryption done using KMS (AES-256)
- Copying an unencrypted volume still allows for encryption

Some EC2 instances come with Instance Store, which are different from EBS Volume Store. This means that the Instance Store is physically attached to the machine. Attributes are:

Pros:

- Better I/O performance

Cons:

- On termination, instance store is lost
- No resizing ability
- Backups must be operated by the user