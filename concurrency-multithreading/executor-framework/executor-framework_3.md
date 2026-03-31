✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

# ⏺️ Java Concurrency: The Confusion Between Executor and Executors

- Ever wondered — "We have an Executor interface and also a class named Executors.
- What’s the difference?” - This is one of those Java concurrency confusions that catches even experienced devs!😅.

### ➡️ Executor

- **Executor** — The **Interface**.
- **Executor** is a core interface introduced in Java 5.
- It defines a simple contract:

```java
    public interface Executor {
    void execute(Runnable command);
    }
```

- That’s it! - It just represents something that can run your tasks — it doesn’t say how.
- Think of it as a contract for submitting tasks.

### ➡️ Executors — The Utility Class

- Provides factory methods to create executors.
- Executors is a factory class that helps you create different types of ExecutorService implementations (thread pools).

```java
    Executors.newFixedThreadPool(3);
    Executors.newCachedThreadPool();
    Executors.newSingleThreadExecutor();
```

- Internally, all of these return a `ThreadPoolExecutor`, pre-configured for specific behaviors.
- **ThreadPoolExecutor** -> The real implementation doing the heavy lifting.

## ➡️ Pro Tip:

- In production systems, prefer creating your own **ThreadPoolExecutor** instead of using the factory methods in Executors.
- Why? Because the **factory methods** use `unbounded queues`, which can lead to **OutOfMemoryError** under heavy load.

```java
    ExecutorService pool = new ThreadPoolExecutor(
    2, 4, 60, TimeUnit.SECONDS,
    new ArrayBlockingQueue<>(100)
    );
```
