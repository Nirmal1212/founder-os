# Component / module design

Good internal structure makes a system changeable and testable. The goal: each module does one thing, hides its internals, and depends only in one direction.

## Single responsibility
Each module has one reason to change. If you describe it with "and" ("handles billing **and** sends email"), split it. A module that does one thing is easy to name, test, and replace.

## Interfaces hide internals
- The public interface is a contract: method signatures with typed inputs/outputs. Callers depend on the interface, never on internals.
- If changing an internal detail forces callers to change, the boundary is leaking — tighten it.

## Dependency direction (the most important rule)
- **Domain/business logic depends on nothing external.** Transport (HTTP), persistence (DB), and third-party clients depend on the domain, not the reverse.
- Inject dependencies (pass collaborators in) rather than constructing them inside — this keeps the core unit-testable without a DB or network.
- A simple test: can you unit-test the business rule with no database and no HTTP? If not, the dependency direction is wrong.

## Where logic lives (layering)
- **Transport layer**: parse/validate the request, map to a domain call, format the response. No business rules here.
- **Domain/service layer**: the actual rules and orchestration. The valuable, well-tested core.
- **Infrastructure layer**: DB access, queues, external APIs — behind interfaces the domain defines.
Keep business rules out of controllers and out of the database. They belong in the domain.

## Don't over-abstract
- Build the interface the requirements need now. No plugin systems, generic frameworks, or speculative extension points for futures that may not arrive. YAGNI beats clever.
- Abstraction earns its place when there are ≥2 real implementations or a real seam for testing — not before.

## Naming
- Module, interface, and entity names come from the glossary. One vocabulary across PRD, API, components, and schema.
