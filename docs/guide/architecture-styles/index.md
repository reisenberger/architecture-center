# Architecture styles

We use the term *architecture style* to mean a family of architectures that share certain characteristics. *N-tier architecture* and *microservices architecture* are examples of architecture styles. 

Every architecture style defines certain high-level concepts, such as *tier* in an N-tier architecture, or *microservice* in a microservices architecture. These concepts provide a common vocabulary for describing and reasoning about a particular architecture. 

## Architecture styles as constraints

Along with the high-level concepts, every architecture style implies a set of principles or guidelines. For example, one of the principles of microservices architectures is that every service can be independently deployed. 

These concepts and principles combine to impose a set of *constraints* on an architecture, which guide the design. The hope is that by conforming to these constraints, certain desirable properties will emerge. Therefore it's important to understand not just the constraints (the "shape" of the architecture) but also the motivation behind them. 

Thus, when you look at a particular microservices architecture, you should be able to identity the service boundaries, and also know that the services adhere to the constraints of the microservices architectural style. 

Before choosing a particular style, make sure that you understand the underlying principles and constraints. Otherwise, you can end up with a design that looks superficially as though it conforms to a particular style, but in fact does not achieve the full potential of that style. 

## Technology choices

The choice of an architecture style does not dictate a particular technology. However, certain technologies are more naturally suited for some architectures. For example, container orchestrators are a natural fit for microservices architectures. So the choice of architecture style informs the choice of technologies. 

## Catalog of architecture styles

- [N-tier](./n-tier.md)
- [Web-queue-worker](./web-queue-worker.md)
- [Microservices](./microservices.md)
- [CQRS](./cqrs.md)
- [Event-driven architecture](./event-driven.md)

For each architecture style, we include the following:

- A description of the architecture.
- A logical diagram showing the important parts of the architecture.
- Recommendations for when to choose this architecture style, including benefits and challenges.
- A diagram showing a recommended deployment of this architecture, including the relevant Azure services and resources.

