# Layers and Their Responsibilities

The project uses a layered structure to keep responsibilities clear and predictable. Each layer has a specific purpose, and understanding these layers helps keep the architecture simple, testable, and easy to reason about.

## Domain Layer

The Domain layer contains the core business logic: entities, value objects, and domain rules. It should be completely free of frameworks and external dependencies.

**Purpose**

- Define how the system behaves.
- Enforce invariants and business rules.
- Represent the true source of business truth.

## Application Layer

The Application layer coordinates actions. It uses the domain to perform work and defines the **interfaces** that `infrastructure` must implement.

**Purpose**

- Orchestrate use-cases.
- Define input/output schemas.
- Describe what needs to happen without knowing how it happens.

## Infrastructure Layer

The Infrastructure layer provides actual implementations for the **interfaces** defined in the application layer. It deals with databases, external APIs, file systems, and other technical concerns.

**Purpose**

- Integrate with external systems.
- Implement repositories, clients, and services.
- Keep technical details out of business logic.

## API Layer

The API layer is the entry and exit point of the application. It accepts input (HTTP, CLI, events) and produces output for end users or other systems.

**Purpose**

- Adapt external requests into use-case calls.
- Map results or errors back into user-facing responses.
- Keep delivery mechanisms separate from core logic.
