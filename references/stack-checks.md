# Stack-specific checks (select only relevant)

Read only sections implicated by the changed behavior. These are prompts for finding missed failure modes, not requirements to run every listed check. Resolve uncertain versions, runtime targets and commands from the affected project's configuration; inspect shared monorepo configuration when it influences that project.

Combine the relevant language, framework/runtime and cross-cutting sections. For example, use PHP + Laravel, TypeScript + React, C# + .NET, or Java/Kotlin + Spring/JPA. For unlisted stacks, follow repository conventions and version-appropriate official documentation. Use configured tools; do not add dependencies merely to complete these checks.

## Languages

### C#
- Preserve nullable annotations, value/reference semantics, equality and public serialization contracts.
- Check async exception propagation, cancellation tokens, disposal and deferred enumeration at the owning boundary.
- Inspect project files and shared build settings for language version, target frameworks and analyzers; run relevant build/test commands.

### PHP
- Inspect Composer constraints, PHP version, autoloading and configured extensions; preserve strict typing and coercion behavior.
- Check array keys, null/missing values, object mutation, exception paths and serialization at external boundaries.
- Preserve resource cleanup and request/job state isolation, especially in long-lived workers.
- Use the repository's PHPUnit/Pest and static-analysis commands where configured.

### Go
- Inspect go.mod, package boundaries and existing interfaces; keep interfaces near consumers and avoid abstractions without a real substitution need.
- Propagate context cancellation and deadlines through blocking calls; verify goroutine exit paths and channel ownership.
- Preserve error wrapping and errors.Is/errors.As behavior; check nil interfaces and resource cleanup on early returns.
- Check shared state, synchronization and transaction ownership; avoid unbounded goroutines or retries.
- Run focused go test commands; use go test -race for affected concurrent paths when supported, and repository vet/lint checks where configured.

### TypeScript
- Inspect tsconfig, package exports and runtime targets; preserve strictness, module resolution and public declaration compatibility.
- Reuse domain types and runtime validators; validate external data at boundaries instead of relying on assertions or compile-time types.
- Preserve null/undefined, optional property and discriminated union semantics; narrow unknown values rather than introducing any or unchecked casts.
- Check promise rejection handling and async return contracts in the actual runtime; types do not guarantee cancellation or error handling.
- Run the repository's typecheck and relevant runtime tests; inspect emitted declarations when changing exported library types.

### Java
- Inspect the configured JDK, Maven/Gradle setup and runtime targets before choosing language features or libraries.
- Preserve exception contracts, null handling, equals/hashCode behavior, generics and serialization compatibility.
- Trace thread safety, executor ownership, interruption and resource cleanup; check retries around concurrent writes.
- Use the repository's Maven/Gradle wrapper and focused test selection where available.

### Python
- Inspect pyproject.toml or equivalent configuration, lockfiles, Python version and the existing environment/package runner.
- Preserve mutable default, iterator/generator, exception and context-manager behavior; validate external data independently of type annotations.
- Keep blocking work out of async paths; verify task cancellation, cleanup and shared state across worker processes where relevant.
- Preserve import/package boundaries and public call signatures; run configured tests, lint and type checks without imposing new tooling.

### Rust
- Inspect Cargo manifests, lockfile, edition, minimum supported Rust version and feature flags for the affected crate.
- Preserve ownership, borrowing, lifetimes and error contracts; avoid cloning, panics or unsafe code merely to bypass a design constraint.
- Review affected unsafe code against its documented safety invariants; verify FFI layout and ownership where relevant.
- Check async cancellation, blocking work, lock scope and Send/Sync requirements; run focused cargo tests and configured lint/feature checks.

### Kotlin
- Inspect Gradle configuration, Kotlin version and target platforms; do not assume a JVM-only or Android project.
- Preserve null safety across Java/platform boundaries, data-class equality, sealed hierarchies and serialization behavior.
- Respect coroutine scopes, dispatcher ownership and structured concurrency; do not swallow cancellation in broad exception handlers.
- Check shared mutable state and Flow collection/lifecycle behavior where relevant; run configured tests for the affected targets.

### Swift
- Inspect Package.swift or Xcode build settings, Swift language mode, deployment targets and available test schemes.
- Preserve optional, value/reference, protocol and Codable compatibility; check ARC ownership and escaping closure capture cycles.
- Check actor isolation, Sendable boundaries, task cancellation and main-actor requirements under the project's concurrency settings.
- Use configured Swift package or Xcode checks for affected targets; report simulator, SDK or platform limitations when verification cannot run.

## Frameworks and runtimes

### .NET
- Preserve DI lifetimes, middleware ordering, configuration and hosting conventions.
- Verify auth policy and resource ownership inside the authoritative read/write path, not only controllers.
- Track SQL parameters, transaction ownership, rows affected, retries, cancellation tokens and concurrency controls.
- Avoid new interfaces/services without independent substitutions, policy boundaries or demonstrated reuse.
- Test negative security cases and actual endpoint status/response behavior where feasible.

### Laravel
- Reuse routes, middleware, form requests, policies, Eloquent scopes and container bindings; verify ownership at the authoritative data access boundary.
- Check mass assignment, casts, hidden attributes, relationship loading and query counts; preserve response serialization and validation behavior.
- Trace transaction boundaries, model events and queued jobs; verify retries are idempotent and dispatch timing respects transaction commits.
- Cover validation, scoped queries and job failure paths relevant to the change using the existing test setup.

### React
- Search established hooks/components/providers and design patterns before creating new ones.
- Check stale closure, effect dependencies, cleanup, request cancellation, loading/error/empty states.
- Preserve keyboard/screen-reader behavior and existing routing/cache conventions.
- Avoid duplicating server state across local stores; test user interactions rather than implementation internals.
- Where server rendering or server components are used, preserve server/client boundaries and hydration behavior.

### Spring / JPA (only where present)
- Preserve dependency injection scopes, configuration, validation and exception-to-response mappings.
- Inspect transaction proxy boundaries, propagation and rollback rules; verify behavior for internal calls and async execution where relevant.
- Check persistence context lifetime, lazy loading, relationship fetching, query counts and optimistic locking.
- Verify ownership in scoped queries and persistence behavior with relevant integration tests when mocks cannot exercise it.

## Cross-cutting concerns

### SQL / PostgreSQL / SQL Server
- Inspect schema, constraints, indexes and query plans as necessary; verify tenant/provider scope in every relevant access.
- Use parameters; explicit transaction semantics; concurrency and isolation-aware tests.
- For migration, confirm execution authorization and validate backward compatibility, default/nullability, index lock cost, data backfill and rollback limitations.
- Measure actual query workload before adding indexes.

### Distributed systems
- Define producer and consumer guarantees, ownership, retries, backoff, deduplication and dead letters.
- Confirm idempotency keys and atomic writes/outbox if exactly-once effects are required.
- Exercise duplicates, reordering, partial failure, cancellation, restart and timeout paths.
- Respect observability, cardinality, sensitive data policies and existing operational conventions.
