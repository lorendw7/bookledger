# Go and MySQL preparation roadmap

## Preparation target

Aim for ten days of core work and up to four days of consolidation, assuming three to four hours per day. This is a planning estimate. Go is newly selected, so extend the schedule when a concept or verification needs more time.

The target is a small backend that the maintainer can implement, demonstrate, debug, and explain. The current repository supplies process scaffolding only. All business milestones remain planned.

## Daily plan

| Day | Project work | Knowledge and evidence |
| --- | --- | --- |
| 1 | Run the scaffold; practice Go syntax and basic SQL | Explain functions, types, errors, modules, tables, and rows; record versions |
| 2 | Write the catalog schema, fictional data, and queries | Explain primary keys, decimal prices, constraints, filtering, sorting, and aggregates |
| 3 | Introduce a MySQL driver and read-only catalog access | Explain `database/sql`, connection pooling, context, query parameters, and row cleanup |
| 4 | Implement catalog HTTP behavior and validation | Verify success, empty results, invalid input, and errors; explain handlers and JSON |
| 5 | Model customers, orders, and items; implement basic checkout | Explain relationships, joins, captured prices, transaction ownership, and rollback |
| 6 | Verify failed checkout and last-copy contention | Use two connections; explain atomicity, isolation, locks, and race conditions |
| 7 | Implement cancellation and duplicate-request behavior | Verify valid transitions, stock restoration, repeated requests, and conflicting payloads |
| 8 | Investigate a representative query | Record dataset size, plans, index rationale, and measured observations |
| 9 | Practice basic packaging, configuration, and operation | Introduce Docker and a small CI check when ready; explain logs, health, and shutdown |
| 10 | Demonstrate and review the complete implemented path | Present actual features and limitations; answer design questions in English |
| 11-12 | Repair weak areas and practice coding problems | Explain algorithms, complexity, edge cases, and relevant Go concurrency primitives |
| 13-14 | Run mock interviews and revisit failures | Explain tradeoffs and project ownership without claiming unverified results |

Read [Go foundations](lessons/01-go-foundations.md) and [SQL foundations](lessons/02-sql-foundations.md) first. Use [requirements](requirements.md) for business acceptance and [the progress log](progress.md) for evidence.

## Parallel interview practice

- Spend roughly two hours on project implementation, 45 minutes on algorithms, 20-30 minutes on technical English, and 15 minutes on reflection.
- Prioritize arrays, strings, maps, two pointers, stacks, binary search, and complexity before advanced algorithm topics.
- Practice explaining the concrete problem, chosen approach, verification, and limits of each feature.
- Learn how goroutines differ from operating-system threads, how shared data races occur, and how context cancellation helps bound work. Do not assume concurrency automatically makes a database operation correct.

The preparation target is Rakuten CPSD Software Engineer. Use the live job description to confirm priorities; this schedule is not an official interview syllabus. The [2028 position listing](https://www.i-note.jp/rakuten-tech-entry/2028joiners/positionlist/fulltime.html) describes backend APIs and microservices, CS fundamentals, coding assessment, and business-level English. Go is the maintainer's project-language choice; it is not presented here as an explicit language requirement for that listing.

## Completion criteria

- The maintainer can reproduce the catalog and order behavior from documented prerequisites.
- Failed orders leave no partial committed changes.
- A controlled last-copy experiment permits only one successful reservation.
- Cancellation and retries do not apply stock changes twice.
- Performance statements include actual measurements and their conditions.
- The maintainer can distinguish personal implementation from supplied scaffolding.

## Later topics

After core preparation, explore views, stored procedures, triggers, deadlocks, MVCC, undo/redo, backup restoration, notification outboxes, queues, and Kubernetes. Begin with explanations and focused experiments; production-scale distributed-system experience is not implied by this project.

`EXPLAIN ANALYZE` executes the statement it analyzes. Start with a supported read-only query and record the MySQL version. See [the MySQL reference](https://dev.mysql.com/doc/refman/8.0/en/explain.html).
