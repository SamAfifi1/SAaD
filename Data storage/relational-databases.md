# Relational Databases (SQL) for Tenant Data

## Context and Problem Statement

The system manages critical client data that must maintain integrity, consistency, and strong transactional guarantees.  
We must choose an appropriate data storage model for tenant data, balancing scalability, compliance, and reliability.

## Decision Drivers

* Need for ACID transactions and referential integrity.  
* Structured and well-defined data models for analytics and reporting.  
* Compliance requirements (financial, telecom, etc.).  
* Developer familiarity and ecosystem maturity.

## Considered Options

* Relational SQL databases (e.g., PostgreSQL, MySQL)  
* NoSQL databases (e.g., MongoDB, DynamoDB)  

## Decision Outcome

Chosen option: **Relational SQL databases**, because they provide strong data integrity guarantees, are well-suited to transactional workloads, and support compliance and auditability requirements.

### Consequences

* Good, because SQL ensures consistent and reliable data updates across tenants.  
* Good, because relational design supports complex queries and joins required for reporting.  
* Bad, because horizontal scaling is more complex than in NoSQL systems.  
* Bad, because strict schemas may slow schema evolution.

## Pros and Cons of the Options

### Relational SQL databases

* Good, because of ACID guarantees and mature tooling.  
* Good, because it supports strong referential integrity.  
* Neutral, because read scaling can be mitigated with replicas or sharding.  
* Bad, because schema migrations must be planned carefully.  

### NoSQL databases

* Good, because they scale horizontally more easily.  
* Bad, because they provide weaker consistency and transactional semantics.  
* Bad, because compliance, joins, and relational queries are more difficult.  
