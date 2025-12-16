# Data Separation Strategy for Multi-Tenant Architecture

## Context and Problem Statement

The developed system must support multiple tenants, including clients in heavily regulated industries such as banking and telecommunications.  
A key architectural question is how to separate tenant data to ensure compliance, security, and scalability.  
We must choose between different levels of data isolation — from shared tables with tenant identifiers to fully isolated databases — balancing regulatory needs, operational complexity, and cost.

Additionally, some tenants are subject to **regional data residency regulations** (e.g., GDPR in the EU).  
This requires that data for each tenant can be stored and processed **within the appropriate jurisdiction**, while keeping the architecture extensible for future global clients who may have their own geographic restrictions.

## Decision Drivers

* Regulatory and compliance requirements for tenant isolation and data residency.  
* Security and risk mitigation to prevent cross-tenant data access.  
* Predictable scaling, billing, and cost attribution per tenant.  
* Operational manageability and automation of provisioning and maintenance.  
* Extensibility to support future tenants in different geographic regions or jurisdictions.  

## Considered Options

* Logical separation (tenant ID column in shared tables)  
* Schema-per-tenant separation (shared database, isolated schema)  
* Database-per-tenant separation (dedicated database per tenant)

## Decision Outcome

Chosen option: **Database-per-tenant separation**, because it provides the highest level of data isolation and compliance assurance, supports per-tenant data residency control, and allows clear scaling and cost boundaries for each tenant.

### Consequences

* Good, because regulatory compliance and data privacy are easier to demonstrate and audit.  
* Good, because data for each tenant can be physically located in region-specific infrastructure (e.g., EU clients’ data within the EU to meet GDPR requirements).  
* Good, because the system remains extensible for future global clients with regional residency or compliance needs (e.g., HIPAA, APAC, or local financial data laws).  
* Good, because per-tenant scaling, backup, and restore operations are straightforward.  
* Bad, because infrastructure and maintenance complexity increase with tenant count.  
* Bad, because cross-tenant analytics and global reporting require cross-region aggregation.  

## Pros and Cons of the Options

### Logical separation (tenant ID column in shared tables)

* Good, because it minimizes database count and simplifies schema updates.  
* Good, because it reduces operational overhead for provisioning.  
* Bad, because it increases risk of cross-tenant data exposure due to shared storage.  
* Bad, because compliance with regional residency laws is not easily enforceable.  
* Bad, because per-tenant backup, restore, or migration is cumbersome.  

### Schema-per-tenant separation (shared database, isolated schema)

* Good, because it isolates each tenant’s tables while sharing a single database instance.  
* Good, because it reduces the risk of data leakage compared to logical separation.  
* Neutral, because it partially supports compliance but still shares physical storage.  
* Bad, because enforcing region-specific residency (e.g., EU-only hosting) is not feasible within a shared instance.  
* Bad, because backup and scaling remain coupled across all tenants.  

### Database-per-tenant separation (dedicated database per tenant)

* Good, because it guarantees full isolation and compliance with strict regulations.  
* Good, because per-tenant data can be deployed within the correct geographic region (e.g., EU, US, or APAC) to satisfy local data residency requirements.  
* Good, because automation can handle provisioning, scaling, and backup policies per region.  
* Neutral, because management overhead scales with tenant count but can be mitigated with orchestration tooling.  
* Bad, because cross-region reporting requires an aggregation layer or data lake strategy.  
