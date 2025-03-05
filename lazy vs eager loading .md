# Eager Loading vs. Lazy Loading in Rails

## 1. Lazy Loading

- By default, Rails follows **lazy loading**, meaning it loads associations only when they are accessed.
- This can lead to the **N+1 query problem**, where for each record in a collection, an additional query is executed for its association.

### **Example (N+1 Query Problem)**
```ruby
@posts = Post.all
@posts.each do |post|
  puts post.comments.count  # Triggers a separate query for each post
end
```

💥 Issue: If there are 100 posts, this results in 101 queries (1 for Post.all and 100 for comments).

2. Eager Loading (includes)

Eager loading preloads associated records in a single query, reducing the number of queries.
This is achieved using .includes(:association), which uses a LEFT OUTER JOIN or separate queries with IN().
### **Example (Fixing N+1 Problem)**

```ruby

@posts = Post.includes(:comments)
@posts.each do |post|
  puts post.comments.count  # No extra queries
end

```
✅ Improvement: This loads all posts and their comments in two queries instead of 101.

3. Preloading vs. Joins (Alternative Eager Loading)

Rails provides different ways to eager load data:

Preloading (preload)
+ Runs separate queries for associations.
+ Good when you don’t need to filter based on associations.

```ruby

@posts = Post.preload(:comments) # Loads comments in a separate query

```

Joins (eager_load)
Uses INNER JOIN to fetch records in one query.
Best when filtering based on associations.

```ruby

@posts = Post.eager_load(:comments).where(comments: { approved: true })

```

4. When to Use Which?

| Strategy      | Use When                                      |
|--------------|----------------------------------------------|
| **Lazy Loading**  | Small datasets, occasional associations.  |
| **`includes`**   | Avoiding N+1 queries, improving efficiency. |
| **`preload`**    | Fetching associations but not filtering.   |
| **`eager_load`** | Querying and filtering based on associations. |


# Conclusion
+ Eager Loading improves performance by reducing queries.
+ Lazy Loading is fine for small data but causes N+1 issues.
+ Choose includes, preload, or eager_load based on the use case.