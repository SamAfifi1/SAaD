# Use of an Event Bus and Asynchronous Processing

## Context and Problem Statement

The SAaD platform includes several supporting concerns such as auditing, notifications, reporting, and archival. These concerns are triggered by changes in the complaint lifecycle but do not need to be executed synchronously as part of user-facing request flows.

Implementing these concerns synchronously within the core backend would increase coupling, reduce responsiveness, and risk failures in non-critical services impacting core complaint processing.  
The architectural decision concerns whether these tasks should be handled synchronously within the backend or delegated to asynchronous processing via an event-driven mechanism.

## Decision Drivers

- Responsiveness of user-facing complaint workflows  
- Fault isolation between core functionality and supporting concerns  
- Scalability for non-critical, background workloads  
- Extensibility for future integrations and consumers  
- Simplicity of integration between core and supporting services  

## Considered Options

- Synchronous processing within the backend  
- Direct point-to-point asynchronous calls  
- Event-driven architecture using an event bus  

## Decision Outcome

**Chosen option:** Event-driven architecture using an event bus  

The backend publishes domain events when significant state changes occur in the complaint lifecycle. These events are delivered via an event bus and consumed by supporting microservices, which process them asynchronously. The backend does not depend on the availability or execution of these consumers.

### Consequences

- Good, because core complaint processing remains responsive and isolated from failures in supporting services  
- Good, because new consumers can be added without modifying existing backend logic  
- Good, because asynchronous processing improves scalability for background workloads  
- Good, because event-based integration reduces coupling between services  
- Bad, because eventual consistency must be accepted for non-critical concerns  
- Bad, because debugging and monitoring asynchronous flows are more complex  

## Pros and Cons of the Options

### Synchronous processing within the backend

- Good, because it is simple to implement  
- Bad, because failures in secondary concerns impact core workflows  
- Bad, because response times increase as additional responsibilities are added  

### Point-to-point asynchronous calls

- Good, because it allows background processing  
- Bad, because tight coupling is introduced between producers and consumers  
- Bad, because adding new consumers requires changes to existing integrations  

### Event-driven architecture using an event bus

- Good, because producers and consumers are loosely coupled  
- Good, because the architecture supports extensibility and independent evolution  
- Good, because background workloads scale independently  
- Neutral, because additional infrastructure is required  
