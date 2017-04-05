# Architecture styles

We use the term *architecture style* to mean a family of architectures that share certain characteristics. *N-tier* and *microservices* are examples of architecture styles. Architecture styles are not design patterns, but they are analogous. A design pattern is an abstraction that identifies a set of common elements found in concrete implementations, to solve a particular class of problems. Similarly, an architecture style identifies the common elements in a class of architectures, abstracting away details such as technology choice or platform.

## Architecture styles as constraints

An architecture style places *constraints* on the design of a system, including what elements can appear, and the allowed relationships between elements (see Fielding, *Architectural Styles and the Design of Network-based Software Architectures*). Constraints guide the "shape" of an architectur by restricting the universe of choices. When an architecture conforms to the constraints of a particular style, certain desirable properties emerge. 

For example, in a microservices architecture, the constraints include: 

- A service represents a single responsibility. 
- Every service is independent of the others. 
- Data is private to the service that owns it; services do not share data.

If these constraints are followed, what emerges is a system where services can be deployed independently, faults are isolated, frequent updates are possible, and it's easy to introduce new technologies.

Before choosing an architecture style, make sure that you understand the underlying principles and constraints of that style. Otherwise, you can end up with a design that conforms to the style at a superficial level, but does not achieve the full potential of that style. 

## Challenges and benefits

Constraints also create challenges, so it's important to understand the trade-offs when adopting any of these styles. Do the benefits of the architecture style outweigh the challenges, *for this application domain*. It's also important to be pragmatic. Sometimes it's better to relax a constraint, rather than insist on architectural purity.

The choice of an architecture style does not dictate a particular technology. However, some technologies are more naturally suited for some architectures. For example, containers are a natural fit for microservices.  

## A quick tour of the styles	

This section gives a quick tour of the architecture styles that we've identified, along with some high-level considerations for their use. Later sections go into more detail about each style.

**[N-tier](./n-tier.md)** is a traditional architecture for enterprise applications. Dependencies are managed by dividing the application into *layers* that perform logical functions, such as presentation, business logic, and data access. A layer can only call into layers that sit below it. However, this horizontal layering can be a liability. It can be hard to introduce changes in one part of the application without touching the rest of the application. That makes frequent updates a challenge, and can limit the rate at which new features are added.

![](./images/n-tier-sketch.svg)

N-tier is most often seen in an IaaS context, although it can also include manages services. N-tier is a natural fit for migrating existing applications that already use a layered architecture. 

For a purely PaaS solution, consider a **[Web-Queue-Worker](./web-queue-worker.md)** architecture. In this style, the application has a web front end that handles HTTP requests, and a back-end worker that performs CPU-intensive t[asks or long-running operations. The front end communicates to the worker through an asynchronous message queue. 
 
![](./images/web-queue-worker-sketch.svg)

Web-queue-worker is suitable for relatively simple domains with some resource-intensive tasks. Like N-tier, the architecture is easy to understand. The use of managed services simplifies deployment and operations. But with a complex domains, it can be hard to manage dependencies. The front end and the worker can easily become large, monolithic components, which are hard to maintain and update. As with N-tier, this can reduce the frequency of updates and limit innovation.

If your application has a more complex domain, consider moving to a **[Microservices](./microservices.md)** architecture. A microservices application is composed of many small, independent services. Each service implements a single business capability. Services are loosely coupled, communicating through API contracts.

![](./images/microservices-sketch.svg)

Each service can be built by a small, focused development team. Individual services can be deployed without a lot of coordination between teams, which encourages frequent updates. A microservice architecture is more complex to build and manage than either N-tier or web-queue-worker. It requires a mature development and DevOps culture. But done right, this style can lead to higher release velocity, faster innovation, and a more resilient architecture. 

The **[CQRS](./cqrs.md)** (Command and Query Responsibility Segregation) style separates read and write operations into separate models. This isolates the parts of the system that update data from the parts that read the data. Moreover, reads can be executed against a materialized view that is physically separate from the write database. That lets you scale the read and write workloads independently, and optimize the materialized view for queries.

![](./images/cqrs-sketch.svg)

CQRS makes the most sense when it's applied to a subsystem of a larger architecture. Generally, you shouldn't impose it across the entire application, as that will just create unneeded complexity. Consider it for collaborative domains where many users access the same data.

**[Event-Driven Architecture](./event-driven.md)** uses a publish-subscribe (pub-sub) model, where producers publish events, and consumers subscribe to them. The producers are independent from the consumers, and consumers are independent from each other. 

![](./images/event-driven-sketch.svg)

Consider an event-driven architecture for applications that ingest and process a large volume of data with very low latency, such as IoT solutions. The style is also useful when different subsystems must perform different types of processing on the same event data.

Finally, **[Big Data](./big-data.md)** and **[Big Compute](./big-compute.md)** are specialized architectural styles for workloads that fit certain specific profiles. Big data divides a very large dataset into chunks, performing paralleling processing across the entire set, for analysis and reporting. Big compute, also called high-performance computing (HPC), makes parallel computations across a large number (thousands) of cores. Domains include simulations, modeling, and 3-D rendering.

The following table summarizes how each style manages dependencies, and the types of domain that are best suited for each.

| Architecture style |	Dependency management | Domain type |
|--------------------|------------------------|-------------|
| N-Tier | Horizontal layers | Traditional business domain. Frequency of updates is low. |
| Web-Queue-Worker | Front and backend jobs, decoupled by async messaging. | Relatively simple domain with some resource intensive tasks. |
| Microservices	| Vertical (functional) decoupling. | Complicated domain. Frequent updates. |
| CQRS | Read/write segregation. Schema and scale are optimized separately. | Collaborative domain where lots of users access the same data. |
| Event-driven architecture. | Producer/consumer. Independent view per sub-system. | IoT |
| Big data | Divide a huge dataset into small chunks. Parallel processing on local datasets. | Batch and real-time data analysis. Predictive analysis using ML. |
| Big compute| Data allocation to thousands of cores. | Compute intensive domains such as simulation. |


The next sections go into more detail about each style, including:

- A logical diagram showing the important parts of the architecture.
- Recommendations for when to choose this architecture style.
- Benefits and challenges.
- A diagram showing a recommended deployment, including the relevant Azure services and resources.

