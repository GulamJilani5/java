⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Internal Working of HashMap

### ➡️ Creation of HashMap

```java
HashMap<K,V> map = new HashMap<>();
```

- No array created yet ❗
- table = null
- Default values ready: 🔴
  - capacity(buckets) = 16 (used later)
  - loadFactor = 0.75, if 12 buckets filled then capacity becomes 32 and again 64 etc...

### ➡️ First put() → Array (Buckets) Created

```java
map.put("A", 1);
```

- Now HashMap initializes:
  - Creates array of size 16 → buckets 🔴
  - bucket is index base(0, 1, 2 ....15)
- This is called lazy initialization

### ➡️ Hash Calculation

- Hash of key is calculated

```java
hash = hash(key)
index = (n - 1) & hash
```

- Determines which bucket (index) to use

### ➡️ Insert into Bucket

##### 🟦 Case A: Bucket empty

- Directly store node at calculated index

##### 🟦 Case B: Bucket NOT empty ( Collision)

- If same index already has elements
- then compare the keys(Using `equlas()`)
  - If keys are same then replace(update) the existed value with the new value.
  - If keys are different then adding the next to the existed node and existed node will point to the new node.

### ➡️ Check for Tree Conversion

- After insertion in that bucket:

```java
if (bucket size ≥ 8 AND capacity ≥ 64)
    → convert LinkedList → Red-Black Tree
```

### ➡️ get() Operation (Retrieval)

```java
map.get("A");
```

- Hash Calculation & Find bucket index

```java
hash = hash(key)
index = (n - 1) & hash
```

- If hash matches AND `key.equals()` matches→ return value
  ```text
   if (node.hash == hash && (node.key == key || key.equals(node.key)))
   → return value
  ```
- Else:
  - If LinkedList → traverse list
  - If Tree → search in tree
  - If found → return value
  - If not found → return null
