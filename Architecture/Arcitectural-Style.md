# Selection of Hybrid Architectural Style

## Context and Problem Statement

The SAaD platform must support core complaint management workflows while meeting non-functional requirements related to scalability, availability, maintainability, and tenant isolation.  
The system also includes supporting capabilities such as auditing, notifications, reporting, and archival, which have different performance and scalability characteristics from core user-facing operations.

The architectural decision concerns the overall system style: whether to adopt a monolithic architecture, a service-oriented architecture (SOA), a fully distributed microservices architecture, or a hybrid approach. Each option presents trade-offs in complexity, operational overhead, and long-term flexibility.

## Decision Drivers

- Maintainability and clarity of core business logic  
- Scalability for read-heavy and background workloads  
- Fault isolation for non-critical concerns  
- Operational complexity and deployment overhead  
- Alignment with projected system scale and team size  

## Considered Options

- Monolithic architecture  
- Service-Oriented Architecture (SOA)  
- Fully distributed microservices architecture  
- Hybrid architecture with a modular core and supporting microservices  

## Decision Outcome

**Chosen option:** Hybrid architecture with a modular backend and supporting microservices  

The system is designed around a single, modular backend application that encapsulates all core complaint management workflows. This backend serves as the primary coordination point and enforces business rules, tenant isolation, and API contracts.

Supporting concerns are implemented as a small number of independently deployable microservices. Event-driven microservices, such as auditing and notifications, consume domain events published by the backend via an event bus. Scheduled microservices, such as archival and report generation, handle time-based or batch workloads independently of user request flows.

### Consequences

- Good, because core business logic remains cohesive and easier to reason about  
- Good, because supporting services can scale and evolve independently  
- Good, because asynchronous processing improves resilience and responsiveness  
- Good, because architectural complexity is constrained compared to fully distributed approaches  
- Bad, because the core backend remains a single deployment unit  
- Bad, because clear boundaries must be actively enforced to avoid overloading the core  

## Pros and Cons of the Options

### Monolithic architecture

- Good, because it is simple to develop and deploy initially  
- Good, because all logic resides in a single codebase  
- Bad, because scaling and fault isolation are coarse-grained  
- Bad, because non-core workloads can impact core system responsiveness  

### Service-Oriented Architecture (SOA)

- Good, because functionality is decomposed into services with clear contracts  
- Good, because services can be reused across systems  
- Bad, because service orchestration and governance introduce additional complexity  
- Bad, because it typically requires infrastructure (e.g. ESB) that is unnecessary at the platform’s scale  

### Fully distributed microservices architecture

- Good, because services can scale and deploy independently  
- Good, because fault isolation is strong  
- Bad, because operational and cognitive complexity are significantly higher  
- Bad, because distributed data management and consistency become challenging  

### Hybrid architecture with modular core and microservices

- Good, because it balances simplicity with scalability and extensibility  
- Good, because microservices are introduced only where they add clear value  
- Good, because the approach aligns closely with the system’s functional and non-functional requirements  
- Neutral, because some operational overhead is introduced but remains manageable  
