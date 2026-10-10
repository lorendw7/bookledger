# Planned system requirements

These are planned business behaviors. The current Go scaffold only responds to process health; it does not satisfy the requirements below.

## Scope

Build a fictional bookstore backend using Go and MySQL. Payment is simulated. Choose and record one currency before loading sample prices. Authentication, shipping, taxes, external payment services, and a frontend are outside the first preparation milestone.

## Catalog and customers

- A book edition has an identifier, unique textual ISBN, title, author, price, and stock quantity.
- Price and stock cannot be negative. Required text must have meaningful content; `NOT NULL` alone does not reject an empty string.
- A customer has an identifier, name, and unique email under a documented comparison policy.
- Use synthetic records and preserve book/customer references needed by historical orders.

## Orders and stock

- Each committed order belongs to one customer and contains at least one item.
- Items contain a book identifier, positive quantity, and captured unit price.
- Combine repeated book selections so an order contains at most one item per book.
- Derive totals from quantities and captured prices. Later catalog price changes must not alter history.
- Order creation commits the header, items, and stock reservation together, or commits none of them.

| State | Meaning | Stock effect |
| --- | --- | --- |
| `pending` | Created, with stock reserved | Decrease once during creation |
| `paid` | Simulated payment confirmed | No further stock change |
| `cancelled` | Pending order cancelled | Restore once during cancellation |

Allowed transitions are `pending -> paid` and `pending -> cancelled`. Cancellation changes state and restores stock in the same transaction. Paid and cancelled orders cannot be cancelled again.

## Repeated requests

Define an operation identifier and scope. A retry of the same logical operation reuses its identifier; a separate operation uses another. Concurrent requests for one identifier must not create multiple orders. Reusing an identifier for a different payload must produce a documented conflict. Store enough information to distinguish an existing result from an operation that has not completed.

## HTTP behavior

Before implementing each route, document its method, path, request shape, success response, and errors. Validate input and use parameterized SQL. Avoid exposing credentials or internal database error details in responses. The exact business API remains a maintainer design task.

## Acceptance scenarios

| Scenario | Required observation |
| --- | --- |
| Empty catalog | Successful, documented empty result |
| Invalid price or stock | Rejected without invalid persisted data |
| Buy two copies with five available | One pending order; three remain |
| Request six copies with five available | No committed order or stock change |
| Later item fails during checkout | All checkout changes roll back |
| Two connections compete for the last copy | Exactly one reservation succeeds |
| Cancel a pending order | Stock restored once and state changed |
| Cancel again | No additional restoration |
| Confirm simulated payment | State changes without additional reservation |
| Retry the same order request | No duplicate order or stock effect |
| Same identifier, different payload | Documented conflict without new effects |
| Change a catalog price | Historical captured price unchanged |
| Remove a referenced customer/book | Historical relationships preserved |

Record fixtures, connection ordering, expected outcome, actual outcome, and cleanup. Constraints cover local rules; transactions and concurrency design cover operations spanning multiple records. See [the design proposal](database-design.md).
