# desiDB — Relational Database Design Plan

**Status:** Draft  
**Purpose:** Define the product goals, requirements, architecture, and engineering plan for desiDB before implementation.

---

## 1. Overview

desiDB is an effort to design and build a relational database management system from first principles. The project will develop a clear understanding of how a database stores data, executes queries, maintains indexes, coordinates concurrent transactions, and recovers from failures.

This document is the central planning document. Detailed component designs and implementation decisions will live in separate documents under `design_docs/`.

## 2. Goals

The design process should:

- Establish a precise scope for the first usable version.
- Identify functional and non-functional requirements.
- Define the major database subsystems and their responsibilities.
- Specify the contracts and interactions between subsystems.
- Evaluate alternative designs and document trade-offs.
- Define correctness, durability, concurrency, and performance expectations.
- Produce an incremental implementation and validation roadmap.

## 3. Non-goals

To be agreed during requirements discovery. Candidate exclusions for an initial version include:

- Distributed consensus and multi-node replication.
- Automatic sharding and horizontal scale-out.
- Full SQL standard compatibility.
- Advanced cost-based query optimization.
- Stored procedures and a large extension ecosystem.

These are proposals, not final decisions.

## 4. Product scope and use cases

To be defined. Candidate baseline use cases:

- Create and open a database.
- Define tables and supported column types.
- Insert, retrieve, update, and delete rows.
- Filter and sort query results.
- Create and use indexes.
- Execute transactions with documented isolation guarantees.
- Recover committed data after an unclean shutdown.

## 5. Requirements

### 5.1 Functional requirements

For each feature, record:
- Requirement ID
- Description
- Priority (P0/P1/P2)
- Acceptance criteria
- Dependencies

Requirements to investigate:

- Database and catalog management
- Table and schema management
- Record insertion, retrieval, update, and deletion
- SQL parsing and execution
- Index creation, lookup, and maintenance
- Transaction boundaries and rollback
- Concurrent access
- Logging and crash recovery

### 5.2 Non-functional requirements

Define measurable targets for:

- Correctness and consistency
- Atomicity, isolation, and durability guarantees
- Recovery behavior
- Performance and latency
- Storage and memory efficiency
- Reliability and error handling
- Observability and debuggability
- Portability and maintainability

No performance targets are committed yet; they should follow workload assumptions and baseline measurements.

## 6. Design principles

Proposed principles:

1. Correctness before optimization.
2. Explicit invariants for persistent data structures.
3. Clear ownership and lifecycle rules for pages, buffers, and transactions.
4. Crash-safe changes to persistent state.
5. Small components with documented interfaces.
6. Deterministic tests for correctness and failure scenarios.
7. Measure performance before introducing complexity.
8. Record important decisions, alternatives, and consequences.

## 7. Architecture — areas to design

The following is a candidate decomposition, not a finalized architecture:

- **SQL interface:** parsing, validation, and command handling.
- **Query engine:** logical and physical plans, operators, execution.
- **Catalog:** databases, tables, schemas, and indexes metadata.
- **Storage engine:** files, pages, records, and page allocation.
- **Buffer pool:** caching, pinning, dirty-page tracking, eviction.
- **Index manager:** index structures and index maintenance.
- **Transaction manager:** transaction lifecycle and isolation.
- **Lock manager:** coordination of concurrent operations.
- **Log manager:** write-ahead logging and recovery.
- **Database API / execution coordinator:** lifecycle and subsystem orchestration.

For each subsystem, specify responsibilities, invariants, APIs, error behavior, and dependencies.

## 8. Key design questions

These questions must be answered before implementation choices are finalized.

### Product and workload
- Is the initial target an embedded, single-process database or a client-server database?
- Which workloads should be supported first: OLTP, analytical queries, or a small mixed workload?
- What are the expected database size, row counts, concurrency, and durability expectations?

### Data model and SQL
- Which data types and SQL features belong in the first version?
- What are the schema and catalog semantics?
- Which constraints and joins must be supported?

### Storage
- What page size and on-disk file format should be used?
- How are pages allocated, identified, and reclaimed?
- What record layout should be used?
- How will format evolution and corruption detection work?

### Execution and indexing
- Which query operators are required initially?
- Which index structure should be implemented first, and why?
- How will the optimizer choose access paths?

### Transactions and recovery
- What isolation level is the initial target?
- Which locking strategy is appropriate?
- What is the WAL protocol and what must be forced to stable storage?
- How are checkpoints, undo/redo, and crash recovery handled?

### Runtime and operations
- How is the database opened, closed, and shut down?
- How are errors surfaced?
- What diagnostics and metrics are required?

## 9. Quality strategy

The design must include a validation plan covering:

- Unit tests for data structures and algorithms.
- Integration tests across subsystem boundaries.
- SQL behavior and semantic tests.
- Persistence tests across close/reopen cycles.
- Crash and recovery tests at critical write points.
- Concurrent transaction and deadlock tests.
- Property-based and randomized testing where useful.
- Benchmarks with documented datasets and workloads.

## 10. Proposed design-document structure

| Document | Scope |
|---|---|
| `01-requirements.md` | Goals, scope, use cases, and requirements |
| `02-architecture.md` | System architecture and subsystem contracts |
| `03-storage-engine.md` | Disk files, pages, records, and allocation |
| `04-buffer-pool.md` | Page cache, pinning, eviction, and flushing |
| `05-indexing.md` | Index structures and index operations |
| `06-query-engine.md` | SQL, planning, operators, and execution |
| `07-transactions-and-recovery.md` | Concurrency, WAL, and recovery |
| `08-testing-and-benchmarks.md` | Correctness, fault injection, and performance |

This plan is the source of truth for scope and cross-cutting decisions. Detailed documents should link back to it.

## 11. Implementation phases

The sequence below is provisional and will be revised after architecture review.

1. Requirements and workload definition.
2. Architecture and persistent-format design.
3. Disk and page primitives.
4. Record storage and catalog.
5. Buffer pool.
6. Indexing.
7. SQL parsing and query execution.
8. Transactions and concurrency control.
9. WAL and crash recovery.
10. Hardening, testing, and benchmarking.

Each phase should have explicit entry criteria, deliverables, and exit criteria.

## 12. Decision log

Record significant decisions here. Include context, options considered, decision, rationale, and consequences.

| ID | Decision | Status |
|---|---|---|
| D-001 | Initial deployment model | Open |
| D-002 | Initial workload and scale assumptions | Open |
| D-003 | SQL and data type scope | Open |
| D-004 | Storage format and page layout | Open |
| D-005 | Transaction isolation target | Open |
| D-006 | Logging and recovery strategy | Open |

## 13. Open items and next steps

1. Agree on the product goals and intended users.
2. Choose the initial deployment model and workload.
3. Define the first-version SQL and data model scope.
4. Set measurable durability, concurrency, and performance expectations.
5. Review and approve the high-level architecture.
6. Expand the component design documents.
7. Begin implementation only after the foundational decisions are documented.

---

**Working agreement:** Treat unapproved items in this document as open questions. Do not convert a proposal into an implementation constraint without recording the decision and its rationale.
