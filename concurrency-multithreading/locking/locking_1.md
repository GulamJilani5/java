⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Locking

- Having key(lock) to enter the method and perform execution
- Others should wait

### ➡️ Types Of Lock

##### 🟦 Object-level Lock (Intrinsic Lock) - 80% used 🔴

- Every Java object has One intrinsic lock (monitor)

```java
class A {
    synchronized void method1() { }
    synchronized void method2() { }
}
```

```java
A obj = new A();
Thread 1 → calls obj.method1()
Thread 2 → calls obj.method2()
```

- Execution Flow:
  - Thread 1 enters method1()
  - It acquires lock on obj
  - Thread 2 tries method2()
  - ❌ Blocked → because lock already taken
  - Thread 2 waits until Thread 1 exits
- Even though: Methods are different & Logic is different
  - Still cannot run in parallel, Because lock is on OBJECT, not METHOD

###### 🔵 When CAN they run in parallel?

- Case 1: Different Objects

```java
A obj1 = new A();
A obj2 = new A();

Thread 1 → obj1.method1()
Thread 2 → obj2.method2()
```

- Case 2: Use different locks manually

```java
class A {
    private final Object lock1 = new Object();
    private final Object lock2 = new Object();

    void method1() {
        synchronized(lock1) {
            // critical section
        }
    }

    void method2() {
        synchronized(lock2) {
            // critical section
        }
    }
}
```

##### 🟦 Explicit Locks (java.util.concurrent.locks)

- More powerful & flexible than synchronized

###### 🔵 ReentrantLock

- Manual lock/unlock
- Try lock without blocking:

```java
import java.util.concurrent.locks.ReentrantLock;

ReentrantLock lock = new ReentrantLock();

lock.lock();
try {
    // critical section
} finally {
    lock.unlock();
}
```

###### 🔵 ReadWriteLock (ReentrantReadWriteLock)

- Many readers ✅
- One writer ❌ (exclusive)
- Use when: Read-heavy systems (e.g., cache, configs)

```java
ReentrantReadWriteLock rwLock = new ReentrantReadWriteLock();

rwLock.readLock().lock();   // multiple readers allowed
rwLock.writeLock().lock();  // only one writer
```

###### 🔵 StampedLock (Advanced)

- Optimistic locking (very fast reads)
- Better performance than ReadWriteLock
- Use when:
  - High-performance systems
  - Complex concurrency control

```java
StampedLock lock = new StampedLock();

long stamp = lock.readLock();
lock.unlockRead(stamp);
```

##### 🟦 Class-Level Lock (Static Synchronization)

- Shared across ALL objects
- Only one thread across JVM class

```java
static synchronized void method() { }
```

- Lock Used `ClassName.class`

##### 🟦 Custom Lock Objects

- Fine-grained locking
- Avoid blocking entire object

```java
Object lock1 = new Object();

synchronized(lock1) {
    // critical section
}
```

##### 🟦 Semaphore (Not exactly lock, but control access)

- Used when, Limit concurrent access (DB connections, APIs)

```java
Semaphore semaphore = new Semaphore(3); // 3 threads allowed
```

##### 🟦 Spin Locks (Conceptual / Low-level)

- Thread keeps checking lock (busy waiting)
- Used internally (not common in normal Java code)
