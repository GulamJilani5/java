⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Internal Working of HashSet

- HashSet internally uses HashMap

```java
HashSet<E> set = new HashSet<>();
```

- Internally becomes:

```java
HashMap<E, Object> map = new HashMap<>();
```

- **Hashset** `value` → becomes `key` of the **HashMap**.
- A dummy value → stored as value (usually `PRESENT`)

### ➡️ Insert into Bucket

```java
set.add('A')
```

##### 🟦 Case A: Bucket is empty

- Directly insert element in the Bucket(HashSet)

##### 🟦 Case B: Bucket NOT empty (Collision)

- Compare elements using hash() & equals()
- If element already exists:
  ```text
    hash matches AND equals() matches → Do NOT insert (duplicate not allowed)
  ```
- If element is different:
  ```text
   → Add new node in same bucket
   → Stored as LinkedList initially
  ```
- Increase the Capacity

```text
if (bucket size ≥ 8 AND capacity ≥ 64)
    → convert LinkedList → Red-Black Tree
```

### ➡️ Search Operation (contains)

```text
1. Calculate hash
2. Find bucket index
3. Traverse:
   - Single node → direct check
   - LinkedList → iterate
   - Tree → log(n) search
4. Match condition:
   if hash matches AND equals() matches → FOUND
```

### ➡️ Remove Operation

```text
1. Calculate hash
2. Find bucket index
3. Traverse bucket
4. Match using hash + equals()
5. Remove node
```
