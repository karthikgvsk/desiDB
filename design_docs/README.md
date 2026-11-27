# desiDB Design Documents

This directory contains the system design and implementation plans for desiDB.

## Planned documents

- `01-requirements.md` — goals, non-goals, requirements, and constraints
- `02-architecture.md` — high-level architecture and component responsibilities
- `03-storage-engine.md` — pages, files, record layout, and disk management
- `04-buffer-pool.md` — memory management and page replacement
- `05-indexing.md` — B+ tree design
- `06-query-engine.md` — SQL parsing, planning, and execution
- `07-transactions-and-recovery.md` — concurrency control, WAL, and crash recovery
- `08-testing-and-benchmarks.md` — correctness, failure testing, and performance strategy

We will agree on the requirements and architecture before implementing database components. These documents are a planned outline; details will be added as decisions are made.
