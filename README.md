# The System Design Basics

<br>
<br>

## Table of Contents
- [Microservices VS Monolith](#microservices-vs-monolith)
    -  [Microservices](#microservices)
    - [Monolith](#monolith)
- [Vertical VS Horizontal Scaling](#vertical-vs-horizontal-scaling)
    - [Vertical scaling](#vertical-scaling)
    - [Horizontal scaling](#horizontal-scaling)

- [CAP Theorum](#cap-theorum)
- [Database Scaling](#database-scaling)
    - [ACID](#acid)
    - [Cashing Layer](#cashing-layer)
    - [Partitions](#partitions)
    - [Database sharding](#database-sharding)
- [Relational VS Non-Relational Databases](#relational-vs-non-relational-databases)
    - [Relational databases](#relational-databases)
    - [Non-Relationan databases](#non-relationan-databases)
- [OSI Model](#osi-model)
- [Message Queues](#message-queues)
- [GraphQL VS REST API](#graphql-vs-rest-api)
    - [GraphQL](#graphql)
    - [REST API](#rest-api)
- [Backend Security](#backend-security)
- [What is Webhook](#what-is-webhook)
- [OWASP](#owasp)
<br>
<br>

# Microservices VS Monolith

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

# Vertical VS Horizontal Scaling 

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

### Horizontal scaling

**Pros**
- Scaling up/down faster
- Cost effective
- Massively scalable
- Fewer periods of downtime

**Cons**
- Complexity of maintenance and operation
- Legacy monolith needs to be refactored for horizontal scaling

<br><br>

# CAP Theorum

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

# Database Scaling

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

# Relational VS Non-Relational Databases
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

#  OSI Model
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

# Message Queues
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

# GraphQL VS REST API

### GraphQL
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

<br>

### REST API
**Pros**
- Standard, no need to learn new things
- Uses caching automatically
- API can be served from more than one server.
- Can deal with files
- Response can usually be in JSON, XML, YAML formats

**Cons**
- Requires versioning if you remove a field
- There is no way to get limited fields.
- Doesn't offer type safety or auto-generated documentation
- It is hard to get consistency accross all platforms
- If you have to retrieve any data from two endpoints, you need to send two separate requests to API.
- Manipulating nested resources is not possible

<br><br>

# Backend Security

- Check the size of the payload

- Type of the payload
    - NoSQL injection

- Contents
    -  SQL

- Rate limits
    - Prepare for DoS (denial-of-service) attack

- Encryption
    - encrypt secrets

- Expose minimum ports and services

- Disable introspection
    - GraphQL GraphiQL
    - Firebase

<br>

### NoSQL injection example
```
db.collection.find( { $where: function() { 
    return (this.name == $userData) } } 
);

// NoSQL injectiion
db.collection.find( { $where: function() { 
    return (this.name == 'a'; sleep(5000) ) } } );
```
To prevent this
- Check type of inputs
- Sanitize usrer inputs
- Use the most recent version of the db library


<br><br>

# What is Webhook 
A webhook is an HTTP-based callback function that allows lightweight, event-driven communication between 2 APIs.

Benefits:
- Eliminate the need for polling.
- Usually quick to set up.  
- Automate data transfer
- Good for lightweight, specific payloads. 

Examples:
- **MailChimp** uses a webhook to signup users from your website to your newsletter.
- **Paypal** uses it to tell your accounting app when your clients pay you.
- **Shopify** offers webhooks to keep parts of your commerce system up-to-date, so you don’t have to enter new transaction details manually.

**Security**:
- Use HTTPS
- Don't send secrets through webhook
- Add timestamps
    - Replay attacks don’t read or manipulate messages, but they can catch a legitimate, encrypted message and resend it at an good timing for the attacker. 
- Sign messages

    Bad actors can intercept messages sent on the internet and change their contents to benefit themselves. To prevent unwanted changes, we should sign our messages. We can do this using a hash-based message authentication code (HMAC), which consists of a hashing algorithm and a secret code or key that both parties share.

    HMAC hashes (or scrambles) assign a specific hash function to each message. Allowing a webhook consumer to verify a message’s authenticity and integrity by checking the message against the hash.

<br><br>

# OWASP
The OWASP Top 10 is a standard awareness document for developers and web application security. It represents a broad consensus about the most critical security risks to web applications.

- Broken Access Control
    - a scenario in which attackers can access, modify, delete or perform actions outside an application or systems’ intended permissions.

<br>

- Cryptographic Failures
    
    Examples
    
    Scenario #1: An application encrypts credit card numbers in a database using automatic database encryption. However, this data is automatically decrypted when retrieved, allowing a SQL injection flaw to retrieve credit card numbers in clear text.

    Scenario #2: A site doesn't use or enforce TLS for all pages or supports weak encryption. An attacker monitors network traffic (e.g., at an insecure wireless network), downgrades connections from HTTPS to HTTP, intercepts requests, and steals the user's session cookie. The attacker then replays this cookie and hijacks the user's (authenticated) session, accessing or modifying the user's private data. Instead of the above they could alter all transported data, e.g., the recipient of a money transfer.

    Scenario #3: The password database uses unsalted or simple hashes to store everyone's passwords. 

    Prevention:
    - Don't use FTP and SMTP for transfering sensitive data
    - Ensure up-to-date and strong standard algorithms, protocols, and keys are in place
    - Disable caching for response that contain sensitive data

<br>

- Injection
    - SQL, NoSQL, ORM injection

    Prevention:
    - server side input validation
    - escape special charactors

<br>

- Server-Side Request Forgery
    
    SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).

    Scenario #1: Port scan internal servers – If the network architecture is unsegmented, attackers can map out internal networks and determine if ports are open or closed on internal servers from connection results or elapsed time to connect or reject SSRF payload connections.

    Scenario #2: Sensitive data exposure – Attackers can access local files or internal services to gain sensitive information such as file:///etc/passwd and http://localhost:28017/.

    Scenario #3: Access metadata storage of cloud services – Most cloud providers have metadata storage such as http://169.254.169.254/. An attacker can read the metadata to gain sensitive information.

<br>

- Cross-Site Scripting - XSS

    inject client-side scripts into web pages viewed by the users.

- Cross-Site Request Forgery - CSRF
    
    an attack that forces an end user to execute unwanted actions on a web application in which they’re currently authenticated

    Example

    1. The attacker's page will trigger an HTTP request to the vulnerable web site.
    2. If the user is logged in to the vulnerable web site, their browser will automatically include their session cookie in the request (assuming SameSite cookies are not being used).
    3. The vulnerable web site will process the request in the normal way, treat it as having been made by the victim user, and change their email address.


    Prevention
     - CSRF tokens 
     - Multi-Step Transactions
     - User Interaction Based CSRF Defense (one time token, captcha)
     - Use of Custom Request Headers
     - Verifying Origin With Standard Headers