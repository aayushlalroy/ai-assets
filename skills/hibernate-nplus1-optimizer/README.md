# Hibernate N+1 Optimizer (`hibernate-nplus1-optimizer`)

> [!NOTE]
> **Pre-requisites**:
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — used to record exact query count benchmarks)

---

## What This Skill Does
Diagnoses JPA/Hibernate N+1 query performance bugs from SQL logs, proves query duplication, and collapses multiple SELECT queries into a single set-based `JOIN FETCH`, `@EntityGraph`, or native projection DTO query.

---

## When to Use

### Triggers & Scenarios
- **N+1 Performance Bugs**: When SQL logs show 1 parent query + N association queries repeating per row.
- **Query Optimization**: When asked `"fix N+1 queries"`, `"too many queries"`, or `"optimize query"`.

### When NOT to Use
- Do NOT use for raw SQL tuning outside JPA/Hibernate or NoSQL databases.

---

## Examples

### Example Optimization
```java
// BEFORE (N+1 queries):
List<Post> posts = repository.findAll(); // triggers N queries for comments

// AFTER (1 set-based query):
@Query("SELECT DISTINCT p FROM Post p JOIN FETCH p.comments")
List<Post> findAllWithComments();
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/hibernate-nplus1-optimizer
```
