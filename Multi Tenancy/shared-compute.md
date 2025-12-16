# Shared Compute for Multi-Tenant Processing

## Context and Problem Statement

The CMS system must support multiple tenants efficiently while maintaining data isolation.  
A key decision is how to allocate compute resources across tenants — whether to dedicate compute per tenant or to use a shared compute layer that dynamically balances workloads.  
The goal is to reduce cost and improve scalability without sacrificing fairness or tenant performance.

## Decision Drivers

* Reduce infrastructure and operational costs.  
* Improve scaling efficiency for temporary or uneven load spikes.  
* Maintain performance and fairness across tenants.  
* Allow tariff-based pricing through rate limiting.  

## Considered Options

* Isolated compute per tenant  
* Shared compute across tenants  

## Decision Outcome

Chosen option: **Shared compute across tenants**, because it provides more efficient use of infrastructure and smoother scaling behavior while maintaining tenant fairness through API rate limiting and data isolation.

### Consequences

* Good, because resource pooling reduces idle compute and infrastructure costs.  
* Good, because load spikes from one tenant can be absorbed by the shared pool, leading to fewer performance drops and more predictable uptime.  
* Bad, because noisy-neighbor effects can occur without robust rate limiting or monitoring.  
* Bad, because debugging tenant-specific performance issues may be more complex.  

## Pros and Cons of the Options

### Shared compute across tenants

* Good, because shared resources reduce overall cost.  
* Good, because distributed compute handles variable workloads efficiently — spreading smaller tasks evenly across a shared pool reduces latency spikes and downtime.  
* Neutral, because stateless services make compute sharing safe when data remains isolated.  
* Bad, because resource contention between tenants must be actively managed.  

### Isolated compute per tenant

* Good, because it ensures strict performance and resource isolation.  
* Bad, because infrastructure costs grow linearly with the number of tenants.  
* Bad, because scaling becomes inefficient and wasteful under uneven or temporary load.  

