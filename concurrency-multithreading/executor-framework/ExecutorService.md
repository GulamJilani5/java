⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Executor & ExecutorService

### ➡️ Executor

- It is a core interface introduced in Java 5 and It has only one method
- It is simple fire-and-forget execution

##### 🟦 Disadvantage:

- no return value
- no checked exception handling
- no task status tracking

```java
    public interface Executor {
    void execute(Runnable command);
    }
```

### ➡️ ExecutorService

- It is an interface for managing and executing tasks asynchronously.
- **ExecutorService** extends **Executor**.
- In real applications, developers mostly use **ExecutorService** because it is more powerful than **Executor**.

- Methods
  - submit()
  - execute()
  - shutdown()
  - invokeAll()

##### 🟦 execute()

- Since **ExecutorService** extends **Executor** so **ExecutorService** inherits the `execute()` method from **Executor**.
- `execute()` is still useful for:
  - simple fire-and-forget tasks
  - when no return value is needed

##### 🟦 submit()

- It is better replacemnt of the **Executor**'s `execut()` method.
- returns value using Future
- exception handling support
- can check task completion
- can cancel task
- supports graceful shutdown methods

```java
ExecutorService executor = Executors.newFixedThreadPool(10);

executor.submit(() -> {
    System.out.println("Running task in thread: " + Thread.currentThread());
});
```

##### 🟦 shutdown()

- Used to gracefully stop **ExecutorService**.
  - stops accepting new tasks
  - already submitted tasks continue and finish

```java
ExecutorService executor = Executors.newFixedThreadPool(2);
executor.submit(() -> System.out.println("Task running"));
executor.shutdown();
```

- After shutdown:

```java
executor.submit(...)
```

- will throw exception because pool is closed.

##### 🟦 invokeAll()

- Used to submit multiple tasks together and wait until ALL complete.
- Returns: `List<Future<T>>`
- Useful when:
  - multiple parallel tasks
  - need all results before proceeding

```java
List<Callable<String>> tasks = List.of(
    () -> "Task1",
    () -> "Task2"
);

List<Future<String>> results =
        executor.invokeAll(tasks);

for(Future<String> f : results) {
    System.out.println(f.get());
}
```
