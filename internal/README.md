# Future application packages

This directory is reserved for maintainer-authored application packages. No business implementation is present.

Introduce packages when real responsibilities emerge: HTTP handlers interpret requests, services coordinate business rules, and database access executes the maintainer's SQL. Keep transaction ownership explicit. Avoid adding empty abstractions before a working path exists.

Read [the design proposal](../docs/database-design.md) and [requirements](../docs/requirements.md) before implementation. See [the ownership agreement](../AGENTS.md) for assistant boundaries.
