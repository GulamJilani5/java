⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ CompletableFuture

- `java.util.concurrent.CompletableFuture`
- **CompletableFuture<T>**
  - Task -> produces result later
  - Future result of type **T**

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

- THIS is the real power of CompletabelFuture
- Every callback has async version.
- Example:

```java
thenApply()
thenApplyAsync()
```

##### 🟦 thenApply()

- Transforms result.

```java

```

##### 🟦 thenRun()

```java

```

##### 🟦 allOf()

```java

```

##### 🟦 anyOf()

```java

```

##### 🟦 thenAccept()

```java

```

##### 🟦 thenCompose()

```java

```

##### 🟦 thenCombine()

```java

```

### ➡️ Exception Handling

##### 🟦

```java

```

##### 🟦

```java

```

##### 🟦

```java

```
