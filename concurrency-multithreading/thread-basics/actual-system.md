⏺️ ➡️ 🟦 🔵 🟢 🔴 ⭕ 🟠 🟣 🟥 🟧 ✔️ ☑️ • ‣ → ⁕

# ⏺️ System Understanding

### ➡️ Actual MAchine/System/Server

- Physical server, VM, EC2 instance & Host system
- This machine provides: CPU, RAM, Disk & Network
- System Consists Below:

```text
16 GB RAM
5 CPU cores
Linux OS
SSD disk
```

- Everything runs INSIDE this machine.

### ➡️ Operating System

- Linux, Windows & Ubuntu & CentOS
- The OS manages:
  - Processes
  - Threads
  - Memory
  - CPU scheduling
  - Networking

### ➡️ JVM (Java Virtual Machine)

- Tomcat runs INSIDE JVM.
- When we start Tomcat: `startup.sh`
- Actually a Java process starts: `java -jar tomcat...`
- So now OS sees: `PID 1001 -> Java Process`
- Java process consumes:
  - RAM from machine
  - CPU from machine
  - Threads from OS

### ➡️ Tomcat

- Tomcat is:
  - A Java application
  - A web server
  - A servlet container
- Tomcat has defualt 200 threads.🔴
- These 200 threads are ultimately running on: SYSTEM SERVER (machine)

##### 🟦 OS scheduler

- Tomcat has 200 threads
- 5 threads → running on 5 CPU core
- 195 threads → waiting/sleeping/blocked/runnable

```text
Request comes
     ↓
Tomcat thread assigned
     ↓
Thread becomes RUNNABLE
     ↓
OS scheduler gives CPU core
     ↓
Thread executes for small time slice
     ↓
CPU switches to another thread
```
