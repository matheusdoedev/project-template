---
name: hexagonal-architecture
description: 'Design and improve software using hexagonal architecture principles. Use for isolating business logic from external concerns, improving testability, and structuring ports/adapters around domain behavior.'
argument-hint: 'What part of the system do you want to refactor around ports, adapters, or domain boundaries?'
user-invocable: true
disable-model-invocation: false
---

# Hexagonal Architecture

## When to Use
- Design new application boundaries or modules
- Refactor a system where business logic is coupled to frameworks, databases, or UI code
- Improve testability by isolating the domain from infrastructure concerns
- Define ports and adapters for persistence, APIs, messaging, and external integrations
- Create maintainable architectures where business rules remain stable despite changing delivery mechanisms

## Core Objective
Keep the core domain independent from external systems. Business rules should be expressed clearly, be easy to test, and remain stable even when frameworks, databases, or interfaces change.

## Procedure

### 1. Define the business purpose and domain model
Start from the actual business behavior, not the infrastructure.

Identify:
- the core use case or domain capability
- the business rules that must always hold
- the actors, inputs, and expected outputs
- the events or side effects that matter to the domain

The domain should describe the problem, not the implementation details of a database, HTTP framework, or UI.

### 2. Separate core logic from infrastructure
Map the system into these layers:
- core/domain: business logic, use cases, rules, and entities
- ports: interfaces or contracts that the core depends on
- adapters: implementations for databases, HTTP, messaging, file systems, and other external systems

The core should depend on abstractions, not concrete frameworks. Infrastructure should adapt to the domain model, not vice versa.

### 3. Design ports around behavior, not technology
Ports describe what the application needs from the outside world.

Prefer ports such as:
- repository interfaces for persistence
- notification or messaging interfaces
- external service gateways
- clock, id generator, or event publisher contracts

Port design should emphasize behavior and capability, not implementation details like SQL, REST, or a specific library.

### 4. Keep adapters thin and implementation-specific
Adapters convert between the outside world and port contracts.

Examples:
- database adapters implement repository interfaces
- HTTP controllers adapt requests/responses into domain commands
- messaging listeners translate external events into domain operations
- file-system adapters handle storage concerns without spreading them across the core

Adapters should be as thin as possible; they are translators, not business logic owners.

### 5. Make the domain testable
The core should be testable without database or framework dependencies.

Good patterns:
- drive the domain with pure use cases and explicit inputs
- inject interfaces at the boundary
- test business rules in isolation
- keep infrastructure concerns outside the domain logic

When possible, validate the domain with unit tests that do not depend on external services.

### 6. Respect dependency direction
The dependency rule is critical:
- inner layers should not depend on outer layers
- infrastructure should implement the domain contracts
- the domain should not know about controllers, repositories, or framework types

If a dependency points inward in the wrong direction, refactor the boundaries before continuing.

## Decision Points

### If business logic is mixed with HTTP or database code
- move the logic into the core/use-case layer
- define a port for the required interaction
- implement that interaction in an adapter

### If tests require infrastructure to run
- introduce a port contract
- keep the business rule in the core layer
- drive behavior via test doubles or fake implementations

### If the codebase is hard to change when frameworks change
- reduce framework-specific types in the domain
- express behavior through interfaces and domain primitives
- move infrastructure-only concerns to adapters

### If a feature spans multiple systems
- model the use case in the domain
- define how the system communicates through ports
- implement each integration in its own adapter

## Completion Checklist
Before finishing, confirm:
- the core business logic is independent from UI, database, and framework concerns
- ports represent required behavior, not implementation details
- adapters are thin and do not contain business rules
- the domain can be tested without infrastructure dependencies
- dependency direction flows from outer adapters toward inner domain contracts
- changes in persistence or delivery channels do not require rewriting business rules
- the design remains understandable and maintainable for future changes

## Quality Bar
A hexagonal design is healthy when:
- business rules are explicit and centralized
- external systems are isolated behind ports
- tests focus on behavior rather than framework wiring
- the application can evolve without forcing domain churn
- infrastructure can change without destabilizing core logic

## Example Prompts
- /hexagonal-architecture refactor this service to keep business logic independent from the database layer
- /hexagonal-architecture design ports and adapters for this payment workflow
- /hexagonal-architecture review this module for dependency inversion and infrastructure leakage
- /hexagonal-architecture restructure this codebase around a domain-driven hexagon

## Related Customizations
- create a domain-driven-design skill
- create a ports-and-adapters review checklist
- create a clean-code skill for implementation-level refactors
