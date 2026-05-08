⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ CompletableFuture

- `java.util.concurrent.CompletableFuture`
- **CompletableFuture<T>**
  - Task -> produces result later
  - Future result of type **T**
- Future + Callback + Composition + Combination + Error Pipelines

##### 🟦 Internal States

- A **CompletableFuture** has 3 major states:

```text
1. Incomplete
2. Completed normally
3. Completed exceptionally
```

### ➡️ Creation Methods

##### 🟦 supplyAsync()

- Runs task asynchronously and returns value.
- Used for:
  - APIs
  - DB calls
  - service calls
- Equivalent to `Callable`

```java
CompletableFuture<String> future =
    CompletableFuture.supplyAsync(() -> {
        return "Hello";
    });
```

- ###### 🔵 Without executor

```java
CompletableFuture.supplyAsync(...)
```

- Used `ForkJoinPool.commonPool()` a Shared JVM pool.

- ###### 🔵 With Executor or Custom Executor
  - Real-world preferred approach.

```java
ExecutorService executor =
    Executors.newFixedThreadPool(10);

CompletableFuture<String> future =
    CompletableFuture.supplyAsync(
        () -> fetchData(),
        executor
    );
```

##### 🟦 runAsync()

- Async task without return value.
- Equivalent to `Runnable`

```java
CompletableFuture<Void> future =
    CompletableFuture.runAsync(() -> {
        System.out.println("Task");
    });
```

##### 🟦 completedFuture()

- Already completed future.
- No async here.

```java
CompletableFuture<String> future =
    CompletableFuture.completedFuture("Hello");
```

### ➡️ Consuming Results

##### 🟦 get()

- blocks thread
- checked exceptions
- Throws:
  - `InterruptedException`
  - `ExecutionException`

```java
String result = future.get();
```

##### 🟦 join()

- Same as get but:
  - unchecked exception
  - cleaner syntax
- Preferred in modern code.

```java
String result = future.join();
```

### ➡️ Callback Methods

- This is the real power of **CompletableFuture**
- Do Something when finished.
- Every callback has async version. 🔴

```java
thenApply()
thenApplyAsync()
```

##### 🟦 thenApply()

- Transforms Result.

```java
CompletableFuture<String> future =
    CompletableFuture.supplyAsync(() -> "hello")
                     .thenApply(result -> result.toUpperCase());
```

```text
hello -> HELLO
```

- It is quite equivalent to `map()`

##### 🟦 thenRun()

- Runs next task without using previous result.

```java
future.thenRun(() -> {
    System.out.println("Done");
});
```

##### 🟦 allOf()

- Wait for ALL futures.

```java
CompletableFuture.allOf(f1, f2, f3);
```

- Returns:

```java
CompletableFuture<Void>
```

- **Used for:**
  - parallel orchestration
  - microservices aggregation

##### 🟦 anyOf()

- Returns first completed future.

```java
CompletableFuture.anyOf(f1, f2, f3);
```

- **Useful for:**
  - fastest response wins
  - fallback systems

##### 🟦 thenAccept()

- Consumes result but returns nothing.

```java
future.thenAccept(result -> {
    System.out.println(result);
});
```

- Return type

```java
CompletableFuture<Void>
```

##### 🟦 thenCompose()

- Flattens nested futures.
- Without compose: `CompletableFuture<CompletableFuture<String>>`

- ###### 🔵 Example

```java
getUser()
    .thenCompose(user ->
        getOrders(user)
    );
```

- Equivalent to `flatMap()`
- Used when second async depends on first result.

##### 🟦 thenCombine()

- Combine 2 independent futures.

```java
future1.thenCombine(future2,
    (a, b) -> a + b);
```

- **Example:**
  - user service
  - inventory service
- parallel execution.

### ➡️ Exception Handling

##### 🟦 exceptionally()

- Fallback on error.

```java
future.exceptionally(ex -> {
    return "default";
});
```

##### 🟦 handle()

- Access both:
  - success
  - failure

```java
future.handle((result, ex) -> {
    if (ex != null)
        return "fallback";

    return result;
});
```

##### 🟦 whenComplete()

- Observe result/error without changing output.

```java
future.whenComplete((result, ex) -> {
    log.info("completed");
});
```

- Mostly logging/monitoring.

##### 🟦 Manual Completion

- You can complete future manually.

```java
CompletableFuture<String> future =
    new CompletableFuture<>();
future.complete("done");
```

- **Useful in:**
  - adapters
  - event systems
  - callbacks integration

##### 🟦 completeExceptionally()

```java
future.completeExceptionally(
    new RuntimeException()
);
```

##### 🟦 Cancellation

```java
future.cancel(true);
```

- Marks cancelled.
