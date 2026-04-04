⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ InputStream, FileInputStream & BufferedInputStream

### ➡️ InputStream(Abstract class)

- **InputStream** is the parent (abstract) class for reading byte data in Java.
- Works with byte streams (8-bit)
- Cannot be instantiated directly
- Provides basic methods:
  - `read()`
  - `close()`

```java
InputStream is = new FileInputStream("file.txt");
int data = is.read();
```

### ➡️ FileInputStream (Concrete Class, Extends InputStream)

- **FileInputStream** is used to read data from a file.
- Reads raw bytes from files
- No buffering → slower for large data

```java
FileInputStream fis = new FileInputStream("file.txt");

int data;
while ((data = fis.read()) != -1) {
    System.out.print((char) data);
}

fis.close();
```

### ➡️ BufferedInputStream (Performance Wrapper)

- BufferedInputStream wraps another input stream and adds buffering for better performance.
- Uses internal buffer (default 8KB)
- Reduces number of disk reads 🔴
- Much faster for large files

```java
FileInputStream fis = new FileInputStream("file.txt");
BufferedInputStream bis = new BufferedInputStream(fis);

int data;
while ((data = bis.read()) != -1) {
    System.out.print((char) data);
}

bis.close();
```
