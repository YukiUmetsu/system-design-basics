# The System Design Basics

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

## Cashing Layer (Redis)

## Partitions

## Manager - Worker model

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


