# Adoption of the Controller–Service–Repository Pattern

## Context and Problem Statement

The Backend API encapsulates all core complaint management logic and must support a growing set of user-facing features while remaining maintainable and testable.  
As the system evolves, there is a risk that business logic becomes tightly coupled to API endpoints or persistence mechanisms, increasing complexity and reducing clarity.

The architectural decision concerns how responsibilities within the backend should be structured to ensure clear separation of concerns, consistent enforcement of business rules, and ease of testing.  
Several organisational patterns are available, ranging from tightly coupled controller-driven logic to more layered and modular approaches.

## Decision Drivers

- Separation of concerns between API handling, business logic, and data access  
- Maintainability as the codebase grows  
- Testability of business logic independent of web and persistence layers  
- Consistent enforcement of business rules across all API endpoints  
- Alignment with common enterprise and framework conventions  

## Considered Options

- Controller-centric design (business logic embedded in controllers)  
- Controller–Service–Repository (CSR) pattern  
- Domain-centric architecture with rich domain models  

## Decision Outcome

**Chosen option:** Controller–Service–Repository pattern  

The backend is structured using the Controller–Service–Repository pattern, where controllers act as thin API adapters, services encapsulate business workflows, and repositories abstract persistence concerns. This separation ensures that business logic remains independent of both transport and storage mechanisms.

### Consequences

- Good, because responsibilities are clearly separated and easier to reason about  
- Good, because business logic can be tested independently of API and database layers  
- Good, because changes to persistence or API contracts have minimal impact on business logic  
- Good, because the structure aligns naturally with the C4 component decomposition  
- Bad, because additional abstraction layers introduce some boilerplate  
- Bad, because strict layering must be enforced to prevent architectural erosion  

## Pros and Cons of the Options

### Controller-centric design

- Good, because it is simple for small or prototype systems  
- Bad, because controllers quickly become large and difficult to maintain  
- Bad, because business rules are duplicated across endpoints  
- Bad, because testing requires web-layer setup  

### Controller–Service–Repository pattern

- Good, because it enforces clear separation of concerns  
- Good, because business logic is isolated from infrastructure concerns  
- Good, because it supports unit testing and modular evolution  
- Neutral, because it introduces additional layers and conventions  

### Domain-centric architecture

- Good, because it models complex business rules explicitly  
- Good, because it can reduce duplication in highly complex domains  
- Bad, because it introduces significant design and learning overhead  
- Bad, because it is unnecessary for the current complexity of the CMS  

