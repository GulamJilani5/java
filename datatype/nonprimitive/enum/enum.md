⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Enum

- Enum gives:
  - Type safety
  - Fixed values
  - Better readability

### ➡️ Enum OUTSIDE class

- It is a top-level type like a normal class

```java
public enum Status {
    SUCCESS, FAIL, DO_NOT_SEND
}
```

- Status.SUCCESS

### ➡️ Enum INSIDE class

- It has been used inside my KMP code.
- enum inside class → implicitly static
- Keep enum INSIDE class when:
  - It is specific to that class only

```java
public class MessageResponse {

    private String messageId;
    private String description;
    private Status status;

    // getters, setters, equals, hashCode...

    public enum Status {
        SUCCESS("SUCCESS"),
        FAIL("FAIL"),
        DO_NOT_SEND("DO_NOT_SEND");

        private String text;

        Status(String text) {
            this.text = text;
        }

        public String getText() {
            return text;
        }

        public static Status fromText(String text) {
            return Arrays.stream(Status.values())
                    .filter(s -> s.text.equals(text))
                    .findFirst()
                    .orElse(null);
        }
    }
}
```

- Setting value

```java
MessageResponse response = new MessageResponse();
response.setStatus(MessageResponse.Status.SUCCESS);
```

- Returning from your execute()

```java
public MessageResponse.Status execute(PortalQuery query) {

    if (query == null) {
        return MessageResponse.Status.FAIL;
    }

    if (someCondition) {
        return MessageResponse.Status.SUCCESS;
    }

    return MessageResponse.Status.DO_NOT_SEND;
}
```

- Reading value

```java
if (response.getStatus() == MessageResponse.Status.SUCCESS) {
    // success logic
}
```

### ➡️ Real-World Design (Better Version)

- Instead of String inside enum: `SUCCESS("SUCCESS")`
- We can simplify: Because **Enum** name itself is already a string

```java
public enum Status {
    SUCCESS,
    FAIL,
    DO_NOT_SEND
}
```

`if (status == Status.SUCCESS)` // type-safe
