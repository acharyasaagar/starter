# Guiding principles

Decisions made about the project are (and should be) guided by the following principles:

## Keep core logic independent of frameworks and libraries where possible.

Why?

- Helps me develop the core functionality without needing to think about what framework or library will be used to deliver it.
- Helps me easily test my core without needing to mock or involve external dependencies.
- Helps me easily reason about the core functionality.

## Consistency over flexibility

Why?

- Lowers the cognitive load and makes old projects feel familiar, even after long breaks.
- Allows llms to generate code that fits the existing structure.
- Helps best practices spread naturally because the same patterns repeat across all projects.
- Improves the reliability of refactoring because similar code behaves in predictable ways

> Consistency also carries risk: if a pattern is wrong or poorly chosen, it will be replicated everywhere until corrected.

## Set clear rules for repeated decisions.

Why?

- Don't reinvent the wheel.
- Reduce decision fatigue.
- Maintain consistency across the code-base.
- Removes multiple ways to do the same thing.

## Document decisions (Rules) as they are made.

Why?

- Architectural decisions are easy to forget after months.
- Writing them down preserves the reasoning behind patterns and structure.
- [Bonus] LLMs can follow the documented rules.

## Clean Architecture + DDD should guide most decisions.

Why?

- These principles align with how I think about software design.
- They help keep domain logic pure and focused on business rules.
- They provide a clear guide for organizing code and responsibilities.
- Following these principles naturally enforces separation of concerns.
