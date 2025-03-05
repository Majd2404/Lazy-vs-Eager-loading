# Loading Strategies in Rails

In Rails, handling data efficiently is crucial for application performance. This document covers different **loading strategies** in Active Record, including **lazy loading, eager loading, and preloading**.

---

## 1. Lazy Loading (Default Behavior)

Lazy loading means that Rails loads associated records **only when they are accessed**. While this can work fine for small datasets, it often leads to the **N+1 query problem**, which slows down performance.

## 2. Eager Loading (includes)

Eager loading loads associated records in advance to reduce the number of queries and improve performance.

## 3. Preloading vs. Joins (Alternative Eager Loading)

Active Record provides different ways to efficiently load associations:

Preloading (preload)
+ Loads associated records in separate queries.
+ Best when you don’t need to filter based on associations.

Joins (eager_load)
+ Uses INNER JOIN to fetch data in one query.
+ Useful when filtering based on associations.

## Conclusion

+ Lazy Loading is the default but can cause performance issues.
+ Eager Loading (includes) is useful for reducing queries.
+ Preloading (preload) works best when you don’t filter based on associations.
+ Eager Loading with Joins (eager_load) is best when filtering.