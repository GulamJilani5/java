⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ throw vs throws

### ➡️ throw

- Written inside a method/block
- Throws one exception object
- used to throw exception manually

```java
  throw new ArithmeticException("Invalid value");

 if(age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
  }
```

### ➡️ throws

- Written in method signature
- Can declare multiple exceptions
- Mostly used for checked exceptions
- used to declare exception to caller

```java
void readFile() throws IOException
```

# ⏺️ final, finally and finalize

### ➡️ Final

- Final variable (field)
  - Value cannot be changed once assigned
- final method
  - Cannot be overridden in child class
- final class
  - Cannot be extended (inherited)

### ➡️ Finally

##### 🟦 Always executes

- whether exception occurs or not
- return inside try/catch

##### 🟦 It may NOT run if:

- JVM is terminated → `System.exit(0)`
- JVM crashes (e.g., `OutOfMemoryError`, fatal error)
- Infinite loop / thread killed abruptly

```java
try {
    // code
} catch (Exception e) {
    // handle exception
} finally {
    // always runs ✅
}
```

### ➡️ finalize

- Deprecated since Java 9
- Use alternatives like:
  - try-with-resources
  - AutoCloseable
- Method called before object is garbage collected
- Used for cleanup (like closing resources)

```java
@Override
protected void finalize() throws Throwable {
    // cleanup code
}
```
