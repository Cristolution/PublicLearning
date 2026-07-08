## 1) Indexes

Indexes make reads faster by giving the database a shortcut for finding rows, but they cost extra storage and can slow down writes because every insert, update, or delete may also update one or more indexes.[
You should usually index columns used in `WHERE`, `JOIN`, `ORDER BY`, and sometimes `GROUP BY` clauses.[]

## Common index types
- **Single-column index**: indexes one field only. Good for queries that filter by one column, such as `WHERE email = ?`.
- **Composite index**: indexes multiple columns in a fixed order. Good when queries use the leftmost columns first, such as `WHERE user_id = ? ORDER BY created_at`.
- **Unique index**: prevents duplicate values and speeds up equality lookups. Best for things like usernames, emails, or product codes.
- **Full-text index**: optimized for searching text content, not exact matching. Useful for search bars, article search, or product descriptions.
- **Covering index**: contains all columns needed by the query, so MySQL can answer from the index alone without reading the table rows.
## Practical rules
- Index columns you filter, join, and sort on.
- Put the most selective columns first in a composite index when the query pattern supports it.
- Avoid indexing low-value columns like boolean flags alone unless they are part of a larger composite index.
- Use `EXPLAIN` to verify whether the index is actually being used.[]

---

## 2) Denormalization

Denormalization means intentionally adding redundancy back into the database to reduce joins and make reads faster. It is often the opposite of strict normalization, especially beyond 3NF, because you trade storage and update complexity for speed.[]

## Normalized design
- **Read speed**: slower because queries often need joins.
- **Write speed**: faster and cleaner because each fact is stored once.
- **Storage**: lower because there are fewer duplicates.
- **Integrity**: higher because there is a single source of truth.

## Denormalized design
- **Read speed**: very fast because fewer joins are needed.
- **Write speed**: slower because one change may need updates in multiple places.
- **Storage**: higher because data is duplicated.
- **Integrity**: weaker if updates drift out of sync.
    

## When to denormalize
- When read performance matters much more than write simplicity.
- When join-heavy queries are causing latency problems.
- When you need dashboard-style queries, feeds, or reports that are read constantly.

## Typical denormalization methods
- Store copied values such as `customer_name` inside `orders`.
- Store counters such as `total_orders` or `comment_count`.
- Use materialized views or precomputed summary tables.
- Use triggers or application logic to keep copies synchronized.

---

## 3) Transactions

Transactions protect groups of database operations so they succeed or fail together. The ACID rules are: **Atomicity**, **Consistency**, **Isolation**, and **Durability**.
## ACID in simple terms
- **Atomicity**: all operations inside the transaction happen, or none of them happen.
- **Consistency**: the database remains valid before and after the transaction.
- **Isolation**: concurrent transactions do not interfere in unsafe ways.
- **Durability**: once committed, data remains saved even after a crash.

## Savepoints
Savepoints let you roll back part of a transaction without canceling everything. This is useful when a long transaction has several steps and only one step fails.

## Locks and isolation
- Databases use row locks, page locks, or table locks depending on the engine and query.
- Isolation levels control how much one transaction can see another transaction’s changes.
- Higher isolation usually means stronger correctness but more blocking and lower concurrency.
    

## Practical advice
- Keep transactions short.
- Avoid waiting for user input inside a transaction.
- Add indexes to reduce lock time and improve concurrency.
- Use retries for deadlock-prone workflows.

---

## 4) Soft vs Hard Delete

A **hard delete** removes the row permanently, while a **soft delete** keeps the row and marks it as deleted, often using a `deleted_at` column.
Soft delete is useful when recovery, audit history, or referential safety matters, but every query must remember to exclude deleted rows.

## Soft delete
- Recoverable.
- Safer for audit trails.
- Better for records that may need restoration.
- Requires careful filtering in queries.
## Hard delete
- Permanently removes the row.
- Simpler and smaller.
- Best for temporary or disposable data.

## Good use cases
- **Soft delete**: financial records, audit logs, user accounts, CMS content.
- **Hard delete**: carts, temporary sessions, cache records, short-lived logs.

## Important note
If you use soft delete with unique fields like email, you often need a special unique rule that ignores deleted rows, otherwise you may block reuse of the same value.

---

## 5) EXPLAIN
`EXPLAIN` shows how the database plans to execute a query. In MySQL, the `type` column describes the access method, and the usual order from worst to best is: `ALL`, `index`, `range`, `ref`, `eq_ref`, `const`.
## Access types
- **ALL**: full table scan, usually the worst case.
- **index**: scans the whole index.
- **range**: scans a range of indexed values, such as `BETWEEN`, `>`, or `LIKE 'abc%'`.
- **ref**: uses a non-unique index lookup.
- **eq_ref**: uses a unique index lookup, typically very efficient.
- **const**: the database resolves the row as a constant, often best for a primary key or unique key lookup.

## What to look for
- Prefer `ref`, `eq_ref`, or `const` when possible.
- `range` is often acceptable if the range is not too large.
- Avoid `ALL` on large tables.
- `Using index` in `Extra` often means a covering index is being used.[]
## Example rule of thumb
If a query shows `ALL`, think about adding or rewriting indexes. If it shows `ref` or `const`, the query is usually in good shape.

###  The Master Table: EXPLAIN Columns

| Column Name         | Purpose                                                                                                                         | Common Options / Values                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **`id`**            | The execution step number. Shows the order in which MySQL executes the steps.                                                   | `1`, `2`, `3`... (Higher numbers execute first in subqueries). `NULL` for derived tables.     |
| **`select_type`**   | The type of SELECT query being executed in this step.                                                                           | `SIMPLE`, `PRIMARY`, `UNION`, `SUBQUERY`, `DERIVED`, `DEPENDENT SUBQUERY`. _(See list below)_ |
| **`table`**         | The table that MySQL is currently accessing in this step.                                                                       | The actual table name (e.g., `users`), or `<unionM,N>`, `<derivedN>`, `<subqueryN>`.          |
| **`partitions`**    | Which table partitions are being accessed (only relevant if you use table partitioning).                                        | Partition names (e.g., `p0`, `p1`) or `NULL`.                                                 |
| **`type` 🏆**       | **(Most Important)** The "Join Type" or "Access Type". It tells you _how_ MySQL is finding the rows.                            | `system`, `const`, `eq_ref`, `ref`, `range`, `index`, `ALL`. _(See list below)_               |
| **`possible_keys`** | The indexes that MySQL _could_ potentially use to find rows in this table.                                                      | Index names, or `NULL` (if no relevant index exists).                                         |
| **`key` 🔑**        | The index MySQL _actually decided_ to use.                                                                                      | The name of the index being used, or `NULL` (meaning it did a Full Table Scan).               |
| **`key_len`**       | The length of the index (in bytes) that MySQL decided to use. Helps you see how many parts of a composite index are being used. | Integer (e.g., `4`, `258`).                                                                   |
| **`ref`**           | Shows which columns or constants are being compared to the index named in the `key` column.                                     | `const` (compared to a hardcoded value), `func`, or `database.table.column`.                  |
| **`rows` 🔢**       | MySQL’s **estimate** of how many rows it must examine to execute this step.                                                     | Integer. (Lower is better! Note: This is an estimate, not an exact count).                    |
| **`filtered`**      | An estimated percentage of the table rows that will be filtered out by the `WHERE` clause.                                      | Percentage (e.g., `10.00` means 10% of rows pass the filter, 90% are discarded).              |
| **`Extra` 📝**      | Additional, detailed information about how MySQL resolves the query.                                                            | `Using index`, `Using where`, `Using filesort`, `Using temporary`. _(See list below)_         |

---

### 🔍 Deep Dive: The Options for the 3 Most Important Columns

#### 1. `select_type` (What kind of query step is this?)
- **`SIMPLE`**: A basic query. No subqueries, no UNIONs.
- **`PRIMARY`**: The outermost SELECT in a complex query (like a UNION or subquery).
- **`UNION`**: The second (or later) SELECT statement in a UNION.
- **`SUBQUERY`**: The first SELECT inside a subquery (e.g., inside an `IN()` clause).
- **`DERIVED`**: A subquery inside the `FROM` clause (creates a temporary "derived" table).
- **`DEPENDENT SUBQUERY`**: 🚨 **Red Flag.** A subquery that depends on a value from the outer query. It means MySQL has to re-run the subquery for _every single row_ of the outer query.

#### 2. `type` 🏆 (How is it accessing the table? _Best to Worst_)
This is the ultimate indicator of query speed. You want to be on the left; avoid the right.
- **`system` / `const`**: 🟢 **Perfect.** The table has at most 1 matching row. Usually happens when you query a Primary Key with an exact match (e.g., `WHERE id = 5`). Read exactly once at the start.
- **`eq_ref`**: 🟢 **Excellent.** Used during JOINs. Exactly one row is read from this table for each combination of rows from the previous tables. (Always uses a Primary Key or Unique Index).
- **`ref`**: 🟢 **Good.** All rows with matching index values are read. Used for normal, non-unique indexes (e.g., `WHERE email = 'test@test.com'`).
- **`range`**: 🟡 **Okay.** Only rows in a given range are retrieved using an index. Happens when you use `>`, `<`, `BETWEEN`, or `IN()`.
- **`index`**: 🟠 **Slow.** The entire index tree is scanned. Better than `ALL` because it reads the index (which is smaller), but still slow for large tables.
- **`ALL`**: 🔴 **Terrible.** **Full Table Scan.** MySQL is reading every single row in the table from start to finish. _You almost always need to fix queries that result in `ALL`.

### Quick Cheat Sheet for Debugging

When you run `EXPLAIN`, scan the output in this exact order:
1. **Look at `type`**: Do you see **`ALL`**? If yes, you are missing an index on your `WHERE` or `JOIN` columns.
2. **Look at `key`**: Is it **`NULL`**? If yes, MySQL is ignoring your indexes. Check if your data types match (e.g., joining an `INT` to a `VARCHAR` will break the index).
3. **Look at `Extra`**: Do you see **`Using filesort`** or **`Using temporary`**? If yes, your `ORDER BY` or `GROUP BY` clauses need to be optimized or indexed.
4. **Look at `rows`**: Multiply the `rows` numbers together for all steps. If the final number is massive, your query is doing too much work.
---

## 6) The Database Universe
Different database types are built for different strengths. SQL databases are best for integrity and transactions, while NoSQL systems often optimize for flexibility or speed.

|Type|Best for|Strengths|Weaknesses|
|---|---|---|---|
|Relational SQL|Payments, orders, inventory, accounts|Strong consistency, joins, transactions|Less flexible schema, joins can be expensive|
|Document NoSQL|Logs, content, flexible user profiles|Flexible schema, easy nested data|Weak cross-document joins, integrity is harder|
|Key-value NoSQL|Sessions, caches, counters|Extremely fast lookups|Very limited querying|
|Graph NoSQL|Social networks, recommendations, fraud paths|Excellent relationship traversal|More specialized, less general-purpose|

## Simple decision guide
- Use **SQL** when integrity and transactions matter.
- Use **document** databases when schema changes often.
- Use **key-value** stores for speed and simple access.
- Use **graph** databases when relationships are the main feature.
