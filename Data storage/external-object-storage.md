# External Object Storage for Performance Reports

## Context and Problem Statement

The system generates large performance and analytics reports for tenants.  
These reports are static once generated but may be frequently accessed or downloaded.  
We must choose how and where to store these report artifacts efficiently.

## Decision Drivers

* Need to store large static files securely and cost-effectively.  
* Reduce load on tenant databases.  
* Enable efficient distribution and caching for clients.  
* Maintain scalability as report volume grows.

## Considered Options

* Store reports in tenant databases  
* Store reports on internal file storage  
* Use external blob object storage  

## Decision Outcome

Chosen option: **External blob object storage**, because it provides durable, scalable, and low-cost storage for large report files, with native CDN integration.

### Consequences

* Good, because object storage reduces database bloat and improves performance.   
* Good, because versioning and lifecycle rules can automate cleanup.  
* Bad, because external dependencies introduce latency and require network reliability.  

## Pros and Cons of the Options

### External blob object storage

* Good, because it’s highly scalable and cost-efficient.  
* Neutral, because network latency is acceptable for non-real-time access.  
* Bad, because external availability and permissions must be tightly controlled.  

### Internal file storage

* Good, because it keeps all data in-house.  
* Bad, because it lacks scalability and cost efficiency.  
* Bad, because maintenance and redundancy become internal burdens.  
