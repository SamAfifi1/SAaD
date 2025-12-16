# Selection of Technology Stack

## Context and Problem Statement

The CMS system must support a multi-tenant complaint management system with requirements for scalability, availability, security, and maintainability.  
The technology stack must align with the chosen hybrid architectural style, support asynchronous processing, and integrate cleanly with external services.

The architectural decision concerns the selection of core technologies for the backend, client applications, data persistence, and messaging infrastructure. The chosen stack must be suitable for enterprise and regulated environments while remaining accessible and maintainable within an academic development context.

## Decision Drivers

- Alignment with the selected hybrid architectural style  
- Scalability and performance for both synchronous and asynchronous workloads  
- Maturity and stability of the technology stack  
- Security and suitability for regulated environments  
- Developer productivity and familiarity within the academic context  

## Considered Options

- .NET-based technology stack  
- JavaScript / PHP-based technology stack  
- Python-based technology stack  

## Decision Outcome

**Chosen option:** .NET-based technology stack  

The backend is implemented using **ASP.NET Core (.NET 8)**, providing a high-performance, cross-platform runtime well-suited to stateless API services and modular application design. Web and mobile clients are implemented using **React** and **React Native**, enabling consistent user experience across platforms.

For data persistence, **PostgreSQL** is used as the primary relational database, supporting strong consistency, transactional integrity, and compatibility with the database-per-tenant and clustered deployment strategies.  
Asynchronous communication between the core backend and supporting microservices is enabled through a dedicated message broker, supporting the event-driven architecture described elsewhere.

### Consequences

- Good, because the stack aligns well with the selected architectural style and C4 decomposition  
- Good, because the technologies are mature, stable, and widely supported  
- Good, because performance and scalability requirements can be met without unnecessary complexity  
- Good, because the stack supports secure deployment in regulated environments  
- Bad, because familiarity with the .NET ecosystem is required  
- Bad, because alternative stacks may be more accessible to developers with different backgrounds  

## Pros and Cons of the Options

### .NET-based technology stack

- Good, because it provides strong performance and tooling support  
- Good, because it aligns naturally with layered and modular backend designs  
- Good, because it integrates well with relational databases and messaging systems  
- Neutral, because it requires familiarity with the .NET ecosystem  

### JavaScript / PHP-based technology stack

- Good, because it is widely taught and commonly used in web development  
- Good, because it supports rapid development of web applications  
- Bad, because long-term maintainability for large, modular backends can be more challenging  
- Bad, because performance and scalability characteristics vary significantly across frameworks  

### Python-based technology stack

- Good, because it offers a simple and expressive programming model  
- Good, because it is widely used in academic and data-oriented contexts  
- Bad, because performance for high-throughput API workloads can be limited  
- Bad, because ecosystem support for large-scale, modular service architectures is less consistent  
