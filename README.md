# The System Design Basics

<br>
<br>

## Table of Contents
- [Microservices VS Monolith](#Microservices-vs-monolith)
    -  [Microservices](#microservices)
    - [Monolith](#monolith)
- [Vertical VS Horizontal Scaling](#-🔹-Vertical-VS-Horizontal-Scaling)
- [Relational databases](#-relational-databases)

- [GraphQL Pros & Cons](#-🔹-GraphQL-Pros-&-Cons)

<br>
<br>

# 🔹 Microservices VS Monolith

### Microservices
**Pros**
- Each service can scale up down independently
<br>=> no need to test other features before releasing
<br>=> deployment will be easier & faster
- Easier maintenance



**Cons**
- Higher operational overhead: more containers to manage
- Complicated global testing
- Cross-cutting concerns: debugging, logging, metrics are more difficult
- Complexities leading to slower implementation, cost increase for small companies

<br>

### Monolith
**Pros**
- Simple, No over-engineering
- Single code base
- Resource efficient at small scale

**Cons**
- Harder to distribute development work
- All or nothing deployment, or scalability
- Longer release cycles
- Usually requires opting for a single programming language (less flexibility)

<br><br>

# 🔹 Vertical VS Horizontal Scaling 

### Vertical scaling

**Pros**
- Easy implementation
- Less administrative efforts as you manage one system

**Cons**
- Scaling up/down takes longer
- Single point of failure
- Chances of missing transactions during scaling cutover
- Limited scaling
- Expensive

<br>

### Horizontal scaling (with load balancer)

**Pros**
- Scaling up/down faster
- Cost effective
- Massively scalable
- Fewer periods of downtime

**Cons**
- Complexity of maintenance and operation
- Legacy monolith needs to be refactored for horizontal scaling

<br><br>

# 🔹 CAP Theorum

- **Consistency** - Every read receives the most recent write or an error
- **Availability** - Every request receives a response, without guarantee that it contains the most recent version of the information
- **Partition Tolerance** - The system continues to operate despite arbitrary partitioning due to network failures

<br>

### CP - consistency and partition tolerance
Waiting for a response from the partitioned node might result in a timeout error. CP is a good choice if your business needs require atomic reads and writes (transaction).

<br>

### AP - availability and partition tolerance
Responses return the most readily available version of the data available on any node, which might not be the latest. Writes might take some time to propagate when the partition is resolved.

AP is a good choice if the business needs to allow for eventual consistency or when the system needs to continue working despite external errors.

<br><br>

# 🔹 Database Scaling

## ACID

- **Atomicity**
    - all of the commands that make up a transaction are treated as a single unit and either succeed or fail together

<br>

- **Consistency**
    - changes made within a transaction are consistent with database constraints. 
    - If the data gets into an illegal state, the whole transaction fails.

<br>

- **Isolation**
    - ensures that all transactions run in an isolated environment. 
    - enables running transactions concurrently because transactions don’t interfere with each other.

<br>

- **Durability**
    - once the transaction completes and changes are written to the database, they are persisted.


<br><br>

## Cashing Layer
In-memory data caching, key/value NoSQL stores such as Redis and Memcached

<br>

## Partitions
One big table to smaller tables. 
For example, employee table (employee id, first name, last name, employee picture) 

=> employee table (employee id, first name, last name) & employee picture table (employee id, picture)

<br>

## Manager - Worker model

<br>

## Database sharding
 - Sharding key returns subset of data

## Read only, Write only databases
- It allows you to use different databases. For example, write only for apache cassandra, read only for Elasticsearch.

<br><br>

# 🔹 Relational VS Non-Relational Databases
### Relational databases

**Pros**
- Atomicity, Consistency, Isolation, and Durability (ACID) Compliant
- If one change fails, the whole transaction will fail, and the database will remain in the state it was in before
- Normalization
- Widely adopted, more community support

**Cons**
- Scalability, hard to scale horizontally
- Data can't be flexible, allows different inputs
- Making changes to the structure can be complex (less flexible)

<br>

### Non-Relationan databases
**Pros**
- easier to scale horizontally
- capable of handling big data
- high flexibility of data models

**Cons**
- sacrifice a degree of consistency in order to increase availability
- relatively less community support
- lacks standardization => issues during migration

<br><br>

# 🔹 OSI Model
1. Physical Layer
    - Radio, electric, or light is received and converted to digital bits

<br>

2. Data Link Layer
    - Bits => Frames

<br>

3. Network Layer
    - Frames => IP packet

<br>

4. Transport Layer
    - TCP: 
        - Ordered
        - Guaranteed delivery
        - Slower
        - No broadcasting
        - for HTTPS, HTTP, SMTP, POP, FTP
    - UDP: 
        - Unordered
        - Not guarangteed delivery
        - Faster 
        - Support broadcasting
        - For DNS, VoIP, video conference, streaming

<br>

5. Session Layer
    - Maintains connections, control ports & sessions

<br>

6. Presentation Layer
    - Data Encryption, Encoding
    - JSON to byte strings

<br>

7. Application Layer
    - Human-computer interaction layer, where applications can access te network services

<br>
<br>

# 🔹 Message Queues
It act as data buffers. 

Many at the same time => Process one at a time

If the results doesn't impact a user response, think about using message queues. Good for long-running processes and background jobs

<br>

## Benefits
- Decouple monolithic application
- Producers & consumers model scales
- Buffering
    - process data one by one instead of many at the same time
- Resiliency
    - Even if consumer goes down, queues stay the same
- Delivery guarantees
- Order guarantees

## Usecases
- Sending emails
- Delivering notifications
- Image, Video processing (encoding)
- Batch updates for databases
- File scanning, processing


## Different technologies
- Kafka
- RabbitMQ
- Amazon SQS
- GCP pubsub

<br>

# 🔹 GraphQL Pros & Cons

**Pros**
- No over-fetching
- Validation & type checking
- One call instead of multiple endpoint calls
- Work well with multiple microservices
- Autogenerated API documentation
- Removing fields don’t impact existing code => don’t need versioning.
- Too many nested fields cause performance issues

**Cons**
- Single point of failure
- Not caches by default by CDN because all post requests & URL is always the same => cache between data sources and Graphql
- Can’t do File uploading. => It requires a different api for it.
- Learning curve

<br><br>