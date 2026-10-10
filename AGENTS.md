# Collaboration instructions

## Ownership

The human maintainer writes all core implementation code. This includes database schemas, migrations, seed scripts, business SQL, database access, application logic, and executable business tests.

Assistants may write and maintain English documentation, describe exercises and acceptance criteria, explain concepts, and review implementation when requested. Do not generate, modify, or complete core implementation unless the maintainer explicitly changes this agreement. If asked for help with an exercise, begin with conceptual guidance and hints.

The maintainer has authorized assistants to build and maintain non-business scaffolding: editor settings, dependency manifests, startup configuration, server bootstrap, generic request parsing, and a process health endpoint. This does not authorize database connection/query implementations, business routes, domain models, transaction logic, or executable business tests. The selected stack is Go with the standard-library HTTP server and MySQL for future data persistence.

Generic setup commands and small teaching examples are allowed in documentation. Do not include a complete solution to a BookLedger implementation task.

## Documentation

- Keep all repository documentation in English.
- Distinguish planned behavior from implemented and verified behavior.
- Teach from foundations before introducing advanced terminology.
- Keep the roadmap, requirements, design proposal, and progress log consistent.
- Use relative links within repository documentation.
- Cite official MySQL documentation for version-sensitive behavior.
- Record actual measurements and versions; do not invent benchmark results.

## Git and project scope

- Keep BookLedger separate from the maintainer's personal website repository.
- Use `codex/` as the prefix for assistant-created feature branches.
- Add completed features to the README only after verification.
- Use synthetic customer data and keep local credentials out of commits.
- Add a website showcase when the maintainer requests that work.
- Retain the MIT License and its copyright notice.
