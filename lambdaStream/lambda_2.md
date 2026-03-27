⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Interface, functional interface vs Abstract class

- **Interface** = `contract → what a class must do → supports multiple inheritance → now allows default, static & private methods`.
- **Abstract Class** = `partial implementation → shared behavior + state → constructor supported → single inheritance.`

## ➡️ Interface

- Can have more than one **abstract method** (or even zero)
- No **constructor** (you cannot create object directly)
- No instance variables (because interface fields are **static**)
  - All variables are by default: `public static final`
- Can have **default**, **static**, **private** methods with body (Java 8+ private added in Java 9)

#### 🟦 Key Features:

- **until Java 7:**
  - only abstract methods (implicitly public & abstract)
- **From Java 8+:**
  - default methods (with body)
  - static methods
- **From Java 9+:**
  - private methods allowed

- **Normal Interface Example (Multiple Abstract Methods)**

```java
interface Vehicle {

    // variables are by default: public static final
    int MAX_SPEED = 120;

    // abstract methods (multiple allowed)
    void start();
    void stop();

    // default method (has body)
    default void fuelType() {
        System.out.println("Default fuel type: Petrol");
    }

    // static method (has body)
    static void showCompany() {
        System.out.println("Company: Tata Motors");
    }

    // private method (Java 9+)
    private void engineCheck() {
        System.out.println("Engine checked successfully");
    }

    // default method using private method
    default void service() {
        engineCheck();
        System.out.println("Vehicle servicing done.");
    }
}

```

- **Implementation of Normal Interface**

```java
class Car implements Vehicle {

    @Override
    public void start() {
        System.out.println("Car started");
    }

    @Override
    public void stop() {
        System.out.println("Car stopped");
    }
}

```

## ➡️ Functional Interface

- Same as normal interface BUT it must have exactly one **abstract method**
- Can have **default/static/private** methods any number
- Enables **Lambda expression** and method references
- Marked using `@FunctionalInterface` (optional but recommended)
- **Functional Interface Example (Only One Abstract Method)**

```java
@FunctionalInterface
interface Calculator {

    // only ONE abstract method
    int add(int a, int b);

    // default method allowed
    default void show() {
        System.out.println("Calculator is ready");
    }

    // static method allowed
    static void info() {
        System.out.println("This is a Functional Interface");
    }

    // private method allowed (Java 9+)
    private void secret() {
        System.out.println("Secret internal method");
    }
}

```

- **Lambda Example using Functional Interface**

```java
class FunctionalTest {
    public static void main(String[] args) {

        Calculator calc = (a, b) -> a + b;

        calc.show();
        System.out.println("Sum = " + calc.add(10, 20));

        Calculator.info();
    }
}

```

#### 🟦 Why default methods introduced in Java 8

- Problem before Java 8
  - Interface A is having method m1() and class X is implementing interface A and providing method body to the method m1().

```java
interface A {
    void m1();
}
class X implements A {
    public void m1() {}
}
```

- If Java developers add a new method in an existing interface A, then all implementing classes break

```java
interface A {
    void m1();
    void m2();  // newly added
}

```

- Then class X will give error because it must implement m2().

- Solution is `Default` method
- `Default` method provides a method body inside interface, so old classes will not break.

```java
interface A {
    void m1();

    default void m2() {
        System.out.println("Default implementation");
    }
}
```

- Now existing classes are safe.
- Backward compatibility (old code should not break)

#### 🟦 Why static methods introduced in Java 8?

- Problem before Java 8
  - If you want utility/helper methods in interface, you had to create separate utility class.
  - Now you can directly keep utility methods inside interface using static method.

```java
interface MyUtils {
    static void print() {
        System.out.println("Static method inside interface");
    }
}

```

- Utility methods belong logically to interface itself.

#### 🟦 Why private methods introduced in Java 9?

- Problem in Java 8
  - Interfaces had default methods, but if multiple default methods share common code, we had to repeat code.

```java
interface A {
    default void m1() {
        System.out.println("Log");
        System.out.println("Work1");
    }

    default void m2() {
        System.out.println("Log");
        System.out.println("Work2");
    }
}
```

- Problem, Here `"Log"` is repeated.
- Solution, private method inside interface (Java 9) solve that problem

```java
interface A {

    private void log() {
        System.out.println("Log");
    }

    default void m1() {
        log();
        System.out.println("Work1");
    }

    default void m2() {
        log();
        System.out.println("Work2");
    }
}
```

- Avoid code duplication inside interface.

## ➡️ Abstract Class

- Can have any number of **abstract** + **non-abstract methods**
- Can have **constructor**
- Can have **instance variables**
- Can have **static**, **private**, **final**, **protected** members
- **Abstract Class Example (Constructor + Instance Variable + Methods)**

```java
abstract class Animal {

    // instance variable allowed
    String name;

    // constructor allowed
    Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor called");
    }

    // abstract method
    abstract void sound();

    // non-abstract method
    void sleep() {
        System.out.println(name + " is sleeping");
    }

    // protected method allowed
    protected void eat() {
        System.out.println(name + " is eating");
    }

    // static method allowed
    static void category() {
        System.out.println("Animals are living beings");
    }

    // private method allowed
    private void secretMethod() {
        System.out.println("Animal private method");
    }

    // final method allowed
    final void fixedBehavior() {
        secretMethod();
        System.out.println("This behavior cannot be overridden");
    }
}

```

- **Child Class Extending Abstract Class**

```java
class Dog extends Animal {

    Dog(String name) {
        super(name);
    }

    @Override
    void sound() {
        System.out.println(name + " says: Bow Bow");
    }
}

```

### ➡️ Anonymous Class

An anonymous class is a local class without a name. It's used to create a one-time implementation of an
interface or abstract class.

### ➡️Key Features:

- Defined and instantiated in one line.
- Often used with event handling, threading, and functional interfaces.
- Can override methods immediately.

```

```
