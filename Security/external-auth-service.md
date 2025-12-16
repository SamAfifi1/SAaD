# Use of an External Authentication and Identity Service

## Context and Problem Statement

The platform must authenticate and authorise multiple types of users, including consumers, support agents, managers, and administrators.  
Authentication is a security-critical concern and must support strong access control, auditability, and future extensibility.

Implementing authentication directly within the CMS would require managing credentials, password policies, token issuance, and security updates, significantly increasing system complexity and risk.  
The architectural decision concerns whether authentication should be implemented internally or delegated to a dedicated external identity provider.

## Decision Drivers

- Security and risk mitigation for credential handling  
- Support for multiple authentication mechanisms (e.g. password-based login, SSO)  
- Compliance with industry best practices and security standards  
- Maintainability and reduced operational overhead  
- Extensibility for future identity federation or third-party integration  

## Considered Options

- Custom authentication implemented within the CMS  
- External authentication and identity service  
- Hybrid approach with partial internal identity management  

## Decision Outcome

**Chosen option:** External authentication and identity service  

Authentication and identity management are delegated to an external provider responsible for credential storage, token issuance, and authentication workflows. The CMS consumes identity information and access tokens without directly handling user credentials.

### Consequences

- Good, because credential storage and authentication logic are removed from the CMS, reducing security risk  
- Good, because the system can leverage established security practices and updates provided by the identity service  
- Good, because future support for SSO or federation can be introduced without changes to core CMS logic  
- Good, because authentication concerns are clearly separated from business functionality  
- Bad, because the CMS becomes dependent on the availability of an external service  
- Bad, because integration and configuration require additional setup and monitoring  

## Pros and Cons of the Options

### Custom authentication within the CMS

- Good, because it provides full control over authentication logic  
- Bad, because it significantly increases security risk and implementation complexity  
- Bad, because ongoing maintenance of authentication mechanisms is required  
- Bad, because supporting SSO or federation requires substantial additional effort  

### External authentication and identity service

- Good, because it reduces security responsibility within the CMS  
- Good, because it supports industry-standard authentication protocols  
- Good, because it enables future extensibility for identity federation  
- Neutral, because it introduces an external dependency  

### Hybrid authentication approach

- Good, because it allows gradual migration or partial externalisation  
- Bad, because responsibilities can become unclear between internal and external systems  
- Bad, because it increases architectural complexity without clear benefit  
