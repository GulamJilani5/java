⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Functional Interfaces

### ➡️ Built-in(Standard) Functional Interfaces (from 🔵java.util.function package)

- Find `D:\Jilani\learning\java-fundamentals\lambdaStream\lambda_2.md`

  | Interface             | Method Signature         | Description                        |
  | --------------------- | ------------------------ | ---------------------------------- |
  | ➡️`Function<T,R>`     | `R apply(T t)`           | Takes input, returns output        |
  | ➡️`Predicate<T>`      | `boolean test(T t)`      | Returns true/false                 |
  | ➡️`Consumer<T>`       | `void accept(T t)`       | Performs action, returns nothing   |
  | ➡️`Supplier<T>`       | `T get()`                | Supplies a value, takes nothing    |
  | ➡️`UnaryOperator<T>`  | `T apply(T t)`           | Function where input = output type |
  | ➡️`BinaryOperator<T>` | `T apply(T t1, T t2)`    | Takes 2 inputs, returns 1 output   |
  | ➡️`BiFunction<T,U,R>` | `R apply(T t, U u)`      | 2 inputs, 1 output                 |
  | ➡️`BiPredicate<T,U>`  | `boolean test(T t, U u)` | 2 inputs, true/false               |
  | ➡️`BiConsumer<T,U>`   | `void accept(T t, U u)`  | Takes 2 inputs, no return          |

### ➡️ Different ways to create the lambda expression

##### 🟦 1. No Parameter Lambda

- Used when the method has no arguments.
- Often used with Runnable, event listeners, etc.
- **Example:**

```java
Runnable r = () -> System.out.println("Hello World");
r.run();
```

##### 🟦 2. Single Parameter Lambda

- If only one parameter, parentheses are optional
- **Example:**

```java
 Consumer<String> printer = message -> System.out.println(message);
 printer.accept("Lambda with one parameter");
```

##### 🟦 3. Multiple Parameters Lambda

- Parentheses required when there is more than one parameter.
- **Example:**

```java
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
System.out.println(add.apply(5, 10)); // Output: 15
```

##### 🟦 4. With Block Body (Curly Braces and Return)

- Use this when the logic has multiple lines or return statements.
- **Example:**

```java
Function<Integer, String> evenOdd = (n) -> {
   if (n % 2 == 0) return "Even";
   else return "Odd";
};
System.out.println(evenOdd.apply(4)); // Even

```

### ➡️ Lambda Forms

##### 🟦 Lambda with Type Inference (MOST COMMON — 90% of real projects)

- Java automatically infers the type from the interface method.

```java
(a, b) -> a + b               // type inference (preferred)

```

- We don’t write the types.
- Java checks the functional interface and guesses them.
- If Java can guess the type, you don’t write it.

##### 🟦 Lambda with Explicit Type

- When your code becomes confusing or inference fails
- You write the parameter type yourself:

```java
  ( int a, int b ) -> a + b;

```

- When used?
  - When parameters need annotations
  - When overloading causes ambiguity
- Write type only when required, otherwise skip it.

##### 🟦 Lambda with Return Type Inference

- `ONE line = NO return`
- `MULTI line = MUST write return`

- **If the body is ONE expression**
  - No return keyword needed
  - Java infers the return type

```java
  (a, b) -> a + b

```

- This returns an int automatically.

- **If the body is MULTI-LINE**
  - No return keyword needed
  - Java infers the return type

```java
   (a, b) -> {
    int sum = a + b;
    return sum;        // mandatory
}

```

##### 🟦 Inline Lambda

- Directly passed as an argument

```java
  list.forEach(item -> System.out.println(item));
  // Thread
  Thread t = new Thread(() -> System.out.println("Running..."));

```

- Inline lambda = write the lambda directly inside a method call.
