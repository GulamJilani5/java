🔵🟢🔴➡️⭕🟠🟦🟣🟥🟧✔️ ☑️ • ‣ → ⁕ ⏺️

## ➡️ 2. Explain String immutability. Why are String objects immutable?

##### 🟦 Why are Strings Immutable in Java?

This is one of the most commonly asked interview questions - and for good reason! Strings are special in Java, and their immutability is a design choice that makes the language more secure and efficient.

- Here's why

##### 🟦 Security

- Imagine if database URLs, usernames, or passwords stored as Strings could be modified by another class
- It would be a big risk.

##### 🟦 Caching & Performance

The hashcode of a String is cached once created. Since Strings never change, lookups in HashMap/ HashSet are blazing fast.

##### 🟦 Thread-Safety

- Multiple threads can safely use the same String without worrying about synchronization.
- Enables String Constant Pool.
- Since Strings can't change, they can be stored and reused from a special memory area (SCP), saving huge memory.

##### 🟦 In short:

- Immutability = Security + Performance + Reusability
- I'll cover String Constant Pool in the next post, and how it ties directly to immutability

## ➡️ Why is String immutable but StringBuilder mutable?

- **String** immutability ensures security, caching, and thread-safety.
- **StringBuilder** is mutable for performance-faster when doing lots of modifications.

### ➡️ Does substring() always create a new String? We know runtime String operations create new objects on the heap. But what does this print?

- String str = "java"; String s = str.substring(0); System.out.printIn(str == s); // true or false?

- It prints true. When substring(0) covers the entire string, Java is smart enough to return the same reference instead of creating a new object. The optimization many developers don't expect.

### ➡️ Are two Integer objects with the same value always equal with ==?

- Integer a = 127; Integer b = 127; System.out.printIn(a == b); // true

- Integer x = 128; Integer y = 128;

- System.out.printIn(x == y); // false

- Surprised? Java caches Integer objects in the range -128 to 127. Within this range, == works because both variables point to the same cached object. Beyond 127, new objects are created on the heap, and == compares references - not values. This is why.equals() should always be your default for object comparison.
