---
name: hibernate-nplus1-optimizer
description: >-
  Diagnoses and fixes JPA/Hibernate N+1 query performance bugs by collapsing repeating SQL SELECTs into set-based JOIN FETCH or native projections. Trigger on user prompt ("fix N+1 queries", "too many queries", "optimize this query", "fetch join") or workflow events (slow endpoint with repeating SQL logs). Do NOT trigger for raw SQL or NoSQL database query tuning.
disable-model-invocation: true
---

# Hibernate N+1 Optimizer

The classic performance bug: loading a collection triggers **1 query for the parents +
N queries for each parent's association**. Confirm it from the logs first, then collapse
it into one set-based query.

## Step 1 — Prove it (don't guess)

Turn on SQL logging and count queries for one request:

```properties
spring.jpa.properties.hibernate.show_sql=true
spring.jpa.properties.hibernate.format_sql=true
logging.level.org.hibernate.SQL=DEBUG
# optional: see bound params
logging.level.org.hibernate.orm.jdbc.bind=TRACE
```

If you see the **same SELECT repeated once per parent row**, it's N+1. Record the count
with [evidence-ledger](../evidence-ledger/SKILL.md) (`[Evidenced: 1 + 50 queries for 50 rows]`).

## Step 2 — Pick the fix

| Situation | Fix |
|---|---|
| You need the full entity graph | **`JOIN FETCH`** in JPQL, or an **`@EntityGraph`** on the repository method |
| You only need a few columns for a response | **native query projected into a DTO/interface projection** — don't hydrate full entities |
| Paginating + fetching a collection | avoid `JOIN FETCH` with pagination (in-memory paging); fetch ids first, then the collection, or use `@BatchSize` |
| Many-to-one shown in a list | make it `LAZY` and batch, or project just the needed fields |

**Preferred for read-heavy endpoints:** a single native query that joins everything and
maps columns straight to the response shape via a projection — it avoids loading and
discarding full entities.

## Step 3 — Examples (generic)

Fetch join (JPQL):

```java
@Query("select o from Order o join fetch o.items where o.id in :ids")
List<Order> findWithItems(@Param("ids") List<Long> ids);
```

Interface projection from a native query (only the columns you return):

```java
public interface OrderSummary {
  Long getOrderId();
  String getCustomerName();
  Long getItemCount();
}

@Query(value = """
  select o.id as orderId, c.name as customerName, count(i.id) as itemCount
  from orders o
  join customers c on c.id = o.customer_id
  left join items i on i.order_id = o.id
  where o.id in (:ids)
  group by o.id, c.name
""", nativeQuery = true)
List<OrderSummary> findSummaries(@Param("ids") List<Long> ids);
```

## Step 4 — Verify

Re-run with SQL logging: confirm the query count dropped to **1 (or a small constant)**.
Remove any now-redundant repository/fetch paths. Add/adjust a test so the behavior is
covered and the shape still matches the response contract.

## Workflow

```
N+1 Progress:
- [ ] Enable SQL logging; reproduce; count queries (prove N+1)
- [ ] Choose fetch-join / entity-graph / native-projection per the table
- [ ] Implement the single set-based query; map to the response shape
- [ ] Re-run: confirm constant query count; drop redundant fetches
- [ ] Add/adjust tests; verify response is unchanged
```

## Cautions

- `JOIN FETCH` + pagination on a collection paginates **in memory** — avoid it; page ids
  first.
- Multiple collection `JOIN FETCH`es cause a cartesian product — fetch one collection at
  a time or split queries.
- Keep the projection field names aligned with the response DTO/contract.
