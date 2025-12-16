# External Archival Provider for Long-Term Data Retention

## Context and Problem Statement

The CMS system must retain historical data for compliance and audit purposes without overloading the primary databases.  
An efficient archival solution is required to store cold or inactive data cost-effectively.

## Decision Drivers

* Reduce cost and load on primary data stores.  
* Meet data retention requirements for regulated industries.  
* Allow retrieval for audits or historical reporting.  
* Ensure durability and security of archived data.

## Considered Options

* Store archival data in primary tenant databases  
* Move archival data to internal cold storage  
* Use an external archival provider  

## Decision Outcome

Chosen option: **External archival provider**, because it offers scalable, secure, and low-cost long-term storage with compliance guarantees.

### Consequences

* Good, because it reduces primary storage costs and database size.  
* Good, because archival systems are optimized for durability and compliance.  
* Bad, because retrieval latency is higher for archived data.  
* Bad, because integration and access management require additional work.  

## Pros and Cons of the Options

### External archival provider

* Good, because of durability and cost efficiency.  
* Good, because it offloads historical data from production systems.  
* Neutral, because retrieval frequency is low.  
* Bad, because accessing archived data adds API or integration overhead.  

### Internal cold storage

* Good, because it gives full control over data.  
* Bad, because it adds operational and maintenance burden.  
* Bad, because it scales poorly with growing tenant data.  
