⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

## ➡️ Executors Class (Utility Class)

- `java.util.concurrent.Executors`
- Executors → gives ExecutorService → backed by real pools
- Executors uses ThreadPoolExecutor internally
- Executors.newFixedThreadPool() → internally creates → ThreadPoolExecutor

### 🟦 Factory Methods

#### 🔵 SingleThreadExecutor

- Uses one thread to run tasks one at a time, in order.
- **Good for:** Sequential tasks, like processing a queue of events.
- **Example:**

```java
import java.util.concurrent.*;

public class SingleThreadExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        executor.submit(() -> System.out.println("Task 1"));
        executor.submit(() -> System.out.println("Task 2"));
        executor.submit(() -> System.out.println("Task 3"));

        executor.shutdown();
    }
}
```

- Output (always in order):
  - Task 1
  - Task 2
  - Task 3

#### 🔵 FixedThreadPool

- A pool with a fixed number of threads (e.g., 3 threads).
- If all threads are busy, new tasks wait in a queue.
- **Good for:** Applications with a steady number of tasks, like a web server handling client requests.
- **Example:**

```java
import java.util.concurrent.*;

public class FixedThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        for (int i = 1; i <= 5; i++) {
            int task = i;
            executor.submit(() -> {
                System.out.println("Task " + task + " executed by " + Thread.currentThread().getName());
            });
        }

        executor.shutdown();
    }
}
```

- Behavior:
  - Only 2 threads run at a time
  - बाकी tasks queue में wait करते हैं

#### 🔵 CachedThreadPool

- Creates new threads as needed and reuses idle ones. Idle threads are removed after 60 seconds.
- **Good for:** Short, unpredictable tasks, like handling sudden bursts of user requests.
- **Example:**

```java
import java.util.concurrent.*;

public class CachedThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newCachedThreadPool();

        for (int i = 1; i <= 5; i++) {
            int task = i;
            executor.submit(() -> {
                System.out.println("Task " + task + " executed by " + Thread.currentThread().getName());
            });
        }

        executor.shutdown();
    }
}
```

- Behavior:
  - Threads dynamically create होते हैं
  - Idle threads reuse होते हैं

#### 🔵 ScheduledThreadPool

- Runs tasks after a delay or at regular intervals (like a timer/Periodic Tasks).
- **Good for:** Periodic tasks, like checking for updates every 5 seconds.

```java
import java.util.concurrent.*;

public class ScheduledThreadPoolExample {
    public static void main(String[] args) {
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);

        // Run after 3 seconds delay
        scheduler.schedule(() -> {
            System.out.println("Executed after 3 seconds");
        }, 3, TimeUnit.SECONDS);

        // Run every 2 seconds
        scheduler.scheduleAtFixedRate(() -> {
            System.out.println("Running periodically: " + System.currentTimeMillis());
        }, 0, 2, TimeUnit.SECONDS);
    }
}
```

- Use cases:
  - Cron jobs
  - Polling APIs
  - Background monitoring

#### 🔵 WorkStealingPool

- Java 8+.
- Uses multiple threads (based on CPU cores) where idle threads “steal” tasks from busy ones.
- **Good for:** Tasks that split into smaller subtasks, like parallel processing.
- **Example:**

```java
import java.util.concurrent.*;

public class WorkStealingPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newWorkStealingPool();

        for (int i = 1; i <= 10; i++) {
            int task = i;
            executor.submit(() -> {
                System.out.println("Task " + task + " executed by " + Thread.currentThread().getName());
            });
        }

        // No need to shutdown immediately (ForkJoinPool handles lifecycle differently)
    }
}
```

- Behavior:
  - Uses ForkJoinPool internally
  - Idle threads steal tasks → better CPU utilization
