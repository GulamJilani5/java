⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Java Generics — Syntax & Official Names

```java
| Syntax                            | Official Name                                      |
|---------------------------------- | ---------------------------------------------------|
| `<T>`                             | **Type Parameter**                                 |
| `<T extends X>`                   | **Bounded Type Parameter**                         |
| `?`                               | **Unbounded Wildcard**                             |
| `? extends X`                     | **Upper-Bounded Wildcard**                         |
| `? super X`                       | **Lower-Bounded Wildcard**                         |
| `List<T>`                         | **Parameterized Type**                             |
| `class Box<T>`                    | **Generic Class / Generic Type**                   |
| `<S extends T> S`                 | **Bounded Type Parameter with `S` as Return Type** |
| `<S extends T> S methodName(...)` | **Generic Method with a Bounded Type Parameter**   |
----------------------------------- | ----------------------------------------------------
```

### ➡️ Type Parameters

- These occur when declaring a generic class or generic method.

```java
<T>
<S extends T>
```

##### 🟦 Generic Class

```java
class Box<T>
```

##### 🟦 Gneric

```java
<S extends T> S save(S entity)
```

### ➡️ Type Arguments / Parameterized Types

- These occur when using a generic type.

```java
List<T>
List<String>
Optional<T>
```

- `List<String>`
  - **List** parameterized with **String**.

##### 🟦 Type Parameter

```java
<T>
```

##### 🟦 Parameterized Type

```java
List<T>
```

### ➡️ Wildcards

- These represent an **unknown type**.

```java
?
? extends T
? super T
```

##### 🟦 Unbounded Wildcard

```java
?

```

##### 🟦 Upper-Bounded Wildcard

```java
? extends X

```

##### 🟦 Lower-Bounded Wildcard

```java
? super X
```
