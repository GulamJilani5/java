🔵🟢🔴➡️⭕🟠🟦🟣🟥🟧✔️ ☑️ • ‣ → ⁕ ⏺️

# ⏺️Java 21 (September 2023)

Java 21, an LTS release, introduced significant concurrency and expressiveness improvements, building on preview features from earlier versions.

### ➡️ Virtual Threads (Finalized):🟠

- Like async functions in java

### ➡️ Structured Concurrency (Preview):

#### 🟦 `Promise.all()` Similar to `StructuredTaskScope.ShutdownOnFailure`

- ###### 🔵 Promise.all()
  - If one fails → everything fails immediately

```js
await Promise.all([p1, p2, p3]);
```

- ###### 🔵 StructuredTaskScope.ShutdownOnFailure
  - Parallel execution
  - Fail fast
  - Clean cancellation

```java
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {

    Future<String> f1 = scope.fork(() -> task1());
    Future<String> f2 = scope.fork(() -> task2());

    scope.join();
    scope.throwIfFailed(); // fails if any task failed

    return f1.resultNow() + f2.resultNow();
}
```

- ###### 🔵 ShutdownOnSuccess (Java-specific)
  - This is something JS doesn’t directly have
  - Returns first successful result
  - Cancels others

```java
try (var scope = new StructuredTaskScope.ShutdownOnSuccess<String>()) {

    scope.fork(() -> fastService());
    scope.fork(() -> slowService());

    scope.join();

    return scope.result(); // first successful result
}
```

#### 🟦 `Promise.allSettled()` Similar to `StructuredTaskScope.ShutdownOnSuccess (or custom handling)`

- ###### 🔵 Promise.allSettled()
  - Waits for ALL tasks
  - Doesn't fail early
  - Returns success + failure results

```js
await Promise.allSettled([p1, p2, p3]);
```

- ###### 🔵 StructuredTaskScope.ShutdownOnSuccess (or custom handling)
  - No automatic failure
  - You decide what to do

```java
try (var scope = new StructuredTaskScope<>()) {

    Future<String> f1 = scope.fork(() -> task1());
    Future<String> f2 = scope.fork(() -> task2());

    scope.join(); // wait for all

    // manually check results
    try {
        System.out.println(f1.resultNow());
    } catch (Exception e) {
        System.out.println("f1 failed");
    }

    try {
        System.out.println(f2.resultNow());
    } catch (Exception e) {
        System.out.println("f2 failed");
    }
}
```

### ➡️ Record Patterns (Finalized):🟠

- Find `D:\Jilani\learning\java-fundamentals\javaVersions\java17.md`

### ➡️ Pattern Matching for switch (Finalized):

### ➡️ Sequenced Collections(Finalized)::🟠

#### 🟦 1. SequencedCollection<E> Interface

- Introduced in Java 21 (Preview)
- Superinterface for ordered collections (like List, Deque, LinkedHashSet, etc.)

###### 🔵Methods

- `E getFirst()`;
- `E getLast()`;
- `void addFirst(E e)`;
- `void addLast(E e)`;
- `E removeFirst()`;
- `E removeLast()`;
- `SequencedCollection<E> reversed()`;

#### 🟦 2. SequencedList<E> Interface

- Extends `List<E>` and `SequencedCollection<E>`
- Meant for lists with a defined order (like ArrayList, LinkedList)
- Inherits all SequencedCollection methods

#### 🟦 3. SequencedSet<E> Interface

- Extends `Set<E>` and `SequencedCollection<E>`
- Ensures no duplicates and maintains order
- Typical implementation: `LinkedHashSet`

### ➡️ Unnamed Patterns & Variables(Preview)

### ➡️ Vector API (Finalized):

### ➡️ Foreign Function & Memory API (Finalized):

### ➡️ Multi-File Source Launch

### ➡️ String Templates(Preview)
