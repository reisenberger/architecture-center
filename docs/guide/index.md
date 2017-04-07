# Azure Application Architecture Guide

The cloud is changing the way applications are built and architected. Instead of monoliths, applications are being decomposed into smaller, decentralized services. Applications scale horizontally, adding new instances as demand requires.

This decomposition brings new challenge. Application state is distributed. The applicatino must handle issues of eventual consistency and parallel, asynchronous operatons. The system as a whole must be resilient when failures occur.

The complexity of distributed systems requires new approaches to operations. Deployments must be predictable, and monitoring and telemetry are critical to give insight into the system.

This guide presents a structured approach for designing applications on Azure that are scalable, resilient, and highly available. It is intended for architects and engineers who are designing solutions for Azure. 

> This is not a how-to guide for individual services in Azure, which are covered in the documentation for those services.

### Comparison of traditional on-premises and modern cloud 

| Traditional on-premises | Modern cloud |
|-------------------------|--------------|
| Monolithic, centralized | Decomposed, de-centralized
| Design for predictable scalability | Design for elastic scale |
| Relational database | Polyglot persistence (mix of storage technologies) |
| Strong consistency | Eventual consistency |
| Serial and synchronized processing | Parallel and asynchronous processing |
| Design to avoid failures. Key metric is mean time between failures (MTBF) | Design for failure. Key metric is mean time to recovery (MTTR) |
| Occasional big updates | Frequent small updates |
| Manual management | Automated self-management |
| Snowflake servers | Immutable infrastructure |

## The software development process

Without getting into debates about agile, waterfall, and other paradigms, at a very high level there are three phases to software architecture design:

1. Analyze the business domain.
2. Design services around the business domain.
3. Implement those services on the platform.

In this guide, we describe a series of steps on the path from analysis and design to implementation. Each step involves decisions about the architecture, starting with the most fundamental: What style of architecture are you building? A microservices archiecture? An N-tier architecture?

As you move from design to implementation, the descisions become more granular and local. Should you place a message queue between two components? Can the application recover from a transient network failure? Using a structured approach helps you to keep the right focus at each stage. You move from the big picture to the particulars, and avoid making premature techical decisions early in the process.

For each step of the process, we point to related guidance on the Azure Architecture Center. This guide serves as a roadmap, while the supporting content goes deeper into each area.
