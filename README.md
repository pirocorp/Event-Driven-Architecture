# Event Driven Architecture

## Modern Integration Patterns

**Integration** — An integration connects data, applications, and services across our estate. Common integration methods are **files**, **messages** and **APIs**

**Integration Pattern** — An integration pattern is a standardized method for implementing integrations. Common patterns are **point-to-point**, **publish/subscribe**, and **request/response**. Integration patterns make it easier to connect our estate by providing best-practice designs for solving different use cases. Over time, these patterns have evolved, and more "modern" patterns come with additional benefits to "older" patterns.


## Why adopt Modern Integration Patterns

- Well-defined boundaries and ownership of data and applications
- Higher flexibility and quicker time to market for making new changes or releasing new applications
- Reduce the dependency on other teams when building and releasing new features
- Adopt new trends for Data and Analytics
- Readiness to support new transformation initiatives (like Cloud adoption containerization)
- Better interfaces for internal and external communication
- Scalability and Resilience by design
- Support for Real-time data processing, insights, and analytics
- Agility and Flexibility for development teams
- Readiness for Innovation. Enables transformation for future trends and quicker adoption of newer technologies


## Evolution of Modern Integration Patterns

![image](https://github.com/user-attachments/assets/11d40fc6-8fb8-4bd3-8a1b-fcc7e7c3248c)


### Typical Integration Methods

| **Method**       | **Within Domain** | **Between Domains** | **Pros**                      | **Cons**                                                              |
|------------------|-------------------|---------------------|-------------------------------|-----------------------------------------------------------------------|
| File             | Option            | Migrate             | Simple, established           | Limited interface re-use                                              |
| Direct DB Access | Do not use        | Do not use          | Quick time to market          | Very tightly coupled                                                  |
| DB Replication   | Option            | Do not use          | Simple                        | Tightly coupled                                                       |
| ΑΡΙ              | Option            | Strategic           | De-coupled, request/response  | More suitable for 1:1 integrations than 1:M                           |
| Message (MQ)     | Strategic         | Migrate             | Fast, established             | Tightly coupled                                                       |
| Event (Kafka)    | Option            | Strategic           | De-coupled, publish/subscribe | More Suitable for 1:M type of integrations for large scale operations |


## Event-Driven Architecture

### Modes of communication

Modern applications typically communicate with other applications and services either **synchronously** or **asynchronously**. 

Communication is **synchronous** when the **sender waits for the receiver** and vice versa before continuing. **Request/response** patterns are typically synchronous.

**Asynchronous** communication occurs when messages or information are **sent and received at different times**, eliminating the need for an immediate response. **Publish/Subscribe patterns are asynchronous**.


### Events & Event-Driven Architecture

Decoupled systems that trigger/execute in response to events

An event-driven architecture uses **events** to **trigger** and **communicate** between **decoupled** services & applications. An event is a **state change** or an **update**, for example, an item being placed in a shopping cart on an e-commerce website.

Key to **Event-driven architectures** (EDA) are **event producers** and **event consumers**.

The **producers and consumers are decoupled**, which allows them to be scaled, updated, and deployed independently.

```mermaid
---
title: Shared understanding of domain/naming
---
flowchart LR
    id1(Policy Renewed)
    id2(Consumer A)
    id3(Future Consumer)
    id1 --> id2
    id1 --> |new requirements/consumers added rapidly| id3
```


### Benefits of EDA

Key benefits to adopting an **Event-Driven Architecture** are:

- **Loose Coupling & modularity** - This is the crucial benefit of EDA - add or modify components without affecting the existing system
- **Separation of Business Logic** - business logic is kept within the domain
- **Asynchronous Communication** - producer/consumer do not need to wait for each other
- **Adding New Consumers is easy** - no change is required to the producer
- **Fault Tolerance and Resilience** - If one component fails or becomes unresponsive, other elements can continue to function independently
- **Push-Based Communication** - no need to wait for a request. Publish at the time of the event
- **Lower cost** - easier to develop, test, and deploy


### Business events

Each event published outside the domain should be **meaningful to the rest of the business** - we call these "**business events**." Business events are **system-agnostic**. Technical messages shared between systems can also be events, but we don't publish these outside of our domain. Examples of business events:

- **New order placed** — In a fictive example of a web-based store, the application could publish this when someone clicks "buy."
- **Payment received** — This event is published when the system confirms the payment for the order.
- **Order shipped** — the logistics service publishes this when the parcel has been posted.


### Topics

Topic-based communication is one of the critical components in an **event-driven architecture**.

**Topics** are core components of **publish/subscribe** communication. They reduce complexity by replacing all point-to-point connections with a **single connection** to the topic.

**Any number of consumers** can connect to the broker and establish a **topic subscription** for a given topic.

Conceptually, all consumers subscribing to a topic consume data from their virtual queue.


```mermaid
---
title: Topics
---
flowchart TD
    id1(Producer)
    id2(Topic A)
    id3(Topic B)
    id4(Consumer 1)
    id5(Consumer 2)
    id1 --> |publish| id2
    id1 --> |publish| id3
    id2 --> |subscribe| id4
    id2 --> |subscribe| id5
    id3 --> |subscribe| id5
```


### Design Principles

- **Interface first** - we establish the **who**, **how**, and **what** before building. The topic itself becomes the interface between the producer and the consumer.
- **Use business events** - Each event should convey something relevant and well-understood by the business and other domains. Avoid "technical events."
    - A "batch job completion" event is technical (so don't use it) - but it could become a business event, for example, if we make it an "end of business day" notification instead.
    - Business events should be **system agnostic**.
- **Completely de-couple interactions** - the producer should publish generic business events and not target a specific consumer.
    - The producer and consumer **interact via events only** and should not "know" about each other.
    - The producer owns any events and topics it publishes.
    - The **consumer owns any consumer-specific processing**.


### Messages and Patterns













