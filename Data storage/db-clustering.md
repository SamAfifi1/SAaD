# Database Clustering Strategy for Tenant Databases

## Context and Problem Statement

The system must provide high availability and consistent performance for tenant data while supporting both transactional complaint workflows and read-heavy operations such as dashboards and reporting.  


The architectural decision concerns how tenant databases should be deployed to meet availability, performance, and recovery objectives.  
Options range from single-instance deployments to clustered configurations with replication and failover, each with different trade-offs in complexity, cost, and operational resilience.

## Decision Drivers

- High availability and fault tolerance for tenant data  
- Read scalability to support reporting and dashboard workloads  
- Recovery objectives, including backup, restore, and failover capabilities  
- Consistency guarantees for transactional complaint operations  
- Operational complexity and infrastructure cost  

## Considered Options

- Single database instance per tenant (no replication)  
- Active–passive clustering with read replicas  
- Multi-primary (active–active) database clustering  

## Decision Outcome

**Chosen option:** Active–passive clustering with read replicas  

Each tenant database is deployed with a primary node responsible for write operations and one or more read replicas. This approach balances availability, consistency, and scalability by enabling automated failover while supporting read-heavy workloads without compromising transactional integrity.

### Consequences

- Good, because automated failover reduces downtime in the event of primary node failure  
- Good, because read replicas can scale independently to support reporting and dashboard queries  
- Good, because transactional consistency is preserved by routing all writes through a single primary  
- Good, because replication and regular backups support defined recovery objectives  
- Bad, because infrastructure costs increase due to additional replicas  
- Bad, because write throughput is still constrained by the primary node  

## Pros and Cons of the Options

### Single database instance per tenant

- Good, because it is simple to deploy and manage  
- Good, because it minimizes infrastructure cost  
- Bad, because it represents a single point of failure  
- Bad, because read-heavy workloads compete with transactional operations  
- Bad, because recovery relies entirely on backups, increasing downtime  

### Active–passive clustering with read replicas

- Good, because it improves availability through failover mechanisms  
- Good, because read replicas offload reporting and dashboard workloads  
- Good, because consistency is easier to reason about than in multi-primary setups  
- Neutral, because operational complexity increases but remains manageable with automation  
- Bad, because additional infrastructure is required for replicas  

### Multi-primary (active–active) clustering

- Good, because it allows write scaling across nodes  
- Good, because failover can be near-instantaneous  
- Bad, because conflict resolution and data consistency become complex  
- Bad, because implementation and operational overhead are significantly higher  
- Bad, because it is unnecessary for the platform’s write patterns  
