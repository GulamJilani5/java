✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

# ⏺️ Executor Framework

### ➡️ Is Executor Framework Preferred?

- **Executor Framework** is Pure Java(**Core Java / JDK level**) concurrency utility (since **Java 5**, `java.util.concurrent`).
- Yes Preferred — but usually through Spring abstractions (`TaskExecutor`, `@Async`, `TaskScheduler`) instead of raw
  `Executors.newFixedThreadPool()` etc. Spring manages the lifecycle of the thread pool for you.
- `Executors` (via Spring’s `TaskExecutor`) are still used internally for things like background jobs, scheduling,
  or CPU-heavy tasks in Spring boot.
  - But for inter-service communication (calling another microservice), we prefer `WebClient` over a thread-blocking
    `RestTemplate/Executor` model.

## ➡️ Core Interfaces

- Executor
- ExecutorService
- ScheduledExecutorService

## ➡️ Executors Utility Class

- Executors class

## ➡️ Core Implementation(Class)

- ThreadPoolExecutor

## ➡️ Specific Thread Pools

- SingleThreadExecutor,
- CachedThreadPool
- FixedThreadPool
- ScheduledExecutorService
- WorkStealingPool

## ➡️ Executor Framework Hierarchy

Executor (`interface`)
└──── ExecutorService (`interface`)
├──── ThreadPoolExecutor (`class`)
│ ├────────── SingleThreadExecutor (`via Executors, wrapped ThreadPoolExecutor`)
│ ├────────── CachedThreadPool (`via Executors, direct ThreadPoolExecutor`)
│ ├────────── FixedThreadPool (`via Executors, direct ThreadPoolExecutor`)
│ └────────── ScheduledThreadPoolExecutor (`extends ThreadPoolExecutor`)
│ └────────────────── ScheduledExecutorService (`interface, implemented by ScheduledThreadPoolExecutor`)
└──── ForkJoinPool (`class`)
└──────────── WorkStealingPool (`via Executors`)

## ➡️ What problem does Executor Framework Resolve

#### 🟦 Avoids Thread Creation Overhead:

Creating a new thread for each task is slow and uses a lot of memory. ExecutorService reuses threads from a pool.

#### 🟦 Simplifies Thread Management:

You don’t need to manually start, stop, or track threads.

#### 🟦 Handles Task Queuing:

If there are more tasks than threads, ExecutorService queues them and processes them when a thread is free.

#### 🟦 Supports Task Results:

Unlike basic threads, ExecutorService can run tasks that return results (using Callable).

#### 🟦 Prevents Resource Overload:

Limits the number of threads to avoid crashing your program.

#### 🟦 Enables Asynchronous Execution:

Tasks run in the background, so your main program doesn’t wait.
