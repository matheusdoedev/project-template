# System Architecture

> **Status:** Draft | **Owner:** TBD | **Updated:** YYYY-MM-DD  
> **System:** Name | **Architecture state:** Current / Proposed

## 1. Purpose and Scope

Describe the system's purpose, this document's audience, and the architectural scope. State what is out of scope.

## 2. Architecture Overview

Summarize the main architectural approach, major boundaries, and important principles in a few sentences.

## 3. Architecture Views

Each view should state the concern it addresses. Label diagram elements and relationships; identify the system boundary and distinguish current from proposed behavior.

### 3.1 System Context (C4)

```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master

Person(client, "Client")
System(system, "System", "Description of the system")
Rel(client, system, "Uses")

@enduml
```

### 3.2 Containers and Components (C4)

```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master
System_Boundary(system, "System") {
    Container(webapp, "Web Application", "Description of the web app")
    ContainerDb(database, "Database", "Description of the database")
    Rel(webapp, database, "Reads from and writes to")
}
@enduml
```

| Element | Responsibility | Technology | Interfaces or dependencies |
|---|---|---|---|
| TBD | TBD | TBD | TBD |

### 3.3 Interactions (UML)

Choose a representative scenario. Describe its trigger and important success or failure paths; add a UML sequence or activity diagram.

**Scenario:** TBD  
**Diagram source or link:** TBD  
**Important behavior:** TBD

### 3.4 Deployment and Runtime

Show environments, nodes or services, network boundaries, and relevant runtime relationships. Mark this view TBD if deployment is not yet decided.

**Diagram source or link:** TBD  
**Operational notes:** TBD

## 5. Interfaces and Data

Record the important component or external-system contracts. Include direction, protocol, data exchanged, and ownership where known.

| From | To | Interface / data | Protocol | Notes |
|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD |

## 6. Quality and Security Considerations

Capture only architecture-significant requirements and decisions. Reference detailed requirements rather than duplicating them.

| Concern | Requirement or target | Architectural response / status |
|---|---|---|
| Availability, performance, security, privacy, or other | TBD | TBD |

## 7. Key Decisions

Link to an Architecture Decision Record (ADR) when available. Record unresolved choices as open questions, not settled decisions.

| Decision | Rationale | Consequence | ADR / status |
|---|---|---|---|
| TBD | TBD | TBD | TBD |

## 8. Risks and Open Questions

- TBD

## 9. References and Notation

- ISO/IEC/IEEE 42010:2022, *Software, systems and enterprise - Architecture description*. Use as guidance for organizing stakeholders, concerns, viewpoints, and views; this template alone does not establish conformance. [ISO catalog](https://www.iso.org/standard/74393.html)
- C4 model, official guidance for software architecture abstractions and diagrams. C4 is a model, not a formal standard. [C4 model](https://c4model.com/)
- OMG, *Unified Modeling Language (UML)*, Version 2.5.1, formal specification, December 2017. Use UML notation where a UML view is needed. [OMG specification](https://www.omg.org/spec/UML/2.5.1/About-UML)

**Diagram formats/tools used:** TBD
