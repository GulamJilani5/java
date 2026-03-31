# ThreadPoolExecutor

A ThreadPoolExecutor manages a pool of threads to execute tasks (Runnable or Callable) efficiently. It maintains a set of worker threads that execute tasks from a queue. You can think of it as a kitchen with a team of cooks (threads) preparing orders (tasks) from a queue, with rules for how many cooks to keep, how to handle too many orders, and what to do when the kitchen is overwhelmed.

- For custom thread pools with specific settings (e.g., limited queue size).
- It is concrete implementation of the **ExecutorService** interface in the java.util.concurrent package.
- It provides a flexible and customizable thread pool for executing tasks concurrently, allowing fine-grained control over thread management, task queuing, and task rejection policies.
- Unlike the higher-level Executors factory methods (e.g., newFixedThreadPool or newCachedThreadPool), ThreadPoolExecutor lets you configure details like the number of threads, queue size, and how to handle excess tasks. This makes it ideal for advanced use cases where you need precise control over concurrency.

### Key Features:

### Why Use ThreadPoolExecutor

- **Customization:** Unlike `Executors.newFixedThreadPool`, which has a fixed size and unbounded queue, `ThreadPoolExecutor` lets you set queue limits and rejection policies.
- **Performance Tuning:** You can optimize thread count and queue size for your application’s needs.
- **Resource Control:** Prevents resource exhaustion by limiting threads and queue size.
- **Flexibility:** Supports custom thread factories and rejection handlers for advanced use cases.

### ThreadPoolExecutor Parameters

- **corePoolSize (int):** The number of threads to keep in the pool, even when idle.
- **maximumPoolSize (int):** The maximum number of threads allowed in the pool.
- **keepAliveTime (long):** The time that extra threads (beyond `corePoolSize`) remain idle before being terminated.
- **unit (TimeUnit):** The time unit for `keepAliveTime` (e.g., seconds, milliseconds).
- **workQueue (BlockingQueue<runnable>)</runnable>:** The queue that holds tasks waiting to be executed when all threads are busy.
- **threadFactory (ThreadFactory):** An object that creates new threads for the pool.
- **handler (RejectedExecutionHandler):** A policy for handling tasks when the executor cannot accept them (queue full and `maximumPoolSize` reached).

```java
ThreadPoolExecutor(int corePoolSize,
                  int maximumPoolSize,
                  long keepAliveTime,
                  TimeUnit unit,
                  BlockingQueue<Runnable> workQueue,
                  ThreadFactory threadFactory,
                  RejectedExecutionHandler handler)
```
