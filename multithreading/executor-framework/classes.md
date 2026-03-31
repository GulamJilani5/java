⏺️ ➡️ 🟦 🔵 ✔️ 🟣 🟢 🔴 🟡 🟠 ➡️ ⭕ 🟠 ⬛ 🟩 🟪 🟫 ••‣⁎⁕⁜※⁂
⏺️ ExecutorService & Executors

## ➡️ ExecutorService

- It is an interface for managing and executing tasks asynchronously
- Methods

```java
submit()
execute()
shutdown()
invokeAll()
```

```java
ExecutorService executor = Executors.newFixedThreadPool(10);

executor.submit(() -> {
    System.out.println("Running task in thread: " + Thread.currentThread());
});
```

## ➡️ Executors Class (Utility Class)

- `java.util.concurrent.Executors`
- Executors → gives ExecutorService → backed by real pools
- Executors uses ThreadPoolExecutor internally
- Executors.newFixedThreadPool() → internally creates → ThreadPoolExecutor

### 🟦 Factory Methods

#### 🔵 SingleThreadExecutor

- A method `Executors.newSingleThreadExecutor()`
- `ExecutorService executor = Executors.newSingleThreadExecutor();`
- Uses one thread to run tasks one at a time, in order.
- **Good for:** Sequential tasks, like processing a queue of events.
- **Example:** `Executors.newSingleThreadExecutor()`.

#### 🔵 FixedThreadPool

- A method `Executors.newFixedThreadPool(int nThreads)`.
  `ExecutorService executor = Executors.newFixedThreadPool(5);`
- A pool with a fixed number of threads (e.g., 3 threads).
- If all threads are busy, new tasks wait in a queue.
- **Good for:** Applications with a steady number of tasks, like a web server handling client requests.
- **Example:** `Executors.newFixedThreadPool(3)` creates a pool with 3 threads.

#### 🔵 CachedThreadPool

- A method `Executors.newCachedThreadPool()`.
- Creates new threads as needed and reuses idle ones. Idle threads are removed after 60 seconds.
- **Good for:** Short, unpredictable tasks, like handling sudden bursts of user requests.
- **Example:** `Executors.newCachedThreadPool()`.

#### 🔵 ScheduledThreadPool

- A method `Executors.newScheduledThreadPool(int corePoolSize)`.
- Runs tasks after a delay or at regular intervals (like a timer).
- **Good for:** Periodic tasks, like checking for updates every 5 seconds.
- **Example:** `Executors.newScheduledThreadPool(2)`.

#### 🔵 WorkStealingPool

- A method `Executors.newWorkStealingPool() (Java 8+)`.
- Uses multiple threads (based on CPU cores) where idle threads “steal” tasks from busy ones.
- **Good for:** Tasks that split into smaller subtasks, like parallel processing.
- **Example:** `Executors.newWorkStealingPool()`.

## ➡️ ThreadPoolExecutor

- The core class for `SingleThreadExecutor`, `CachedThreadPool`, and `FixedThreadPool`.

## ➡️ ScheduledThreadPoolExecutor:

Extends `ThreadPoolExecutor` for `ScheduledExecutorService`.

## ➡️ ForkJoinPool:

- Used for `WorkStealingPool`, separate from `ThreadPoolExecutor`.
