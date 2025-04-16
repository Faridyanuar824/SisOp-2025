# Chapter 4 Exercise – Threads & Concurrency

## 4.1
**Provide three programming examples in which multithreading provides better performance than a single-threaded solution.**

**Answer:**
1. **Web Server Handling Multiple Clients:** Each client request can be handled by a separate thread, allowing concurrent responses and improving responsiveness.
2. **Matrix Multiplication:** Each row or block can be computed in parallel threads to significantly reduce computation time.
3. **Image Processing:** Applying filters or transformations to different parts of an image simultaneously using separate threads.

---

## 4.2
**Using Amdahl’s Law, calculate the speedup gain of an application that has a 60 percent parallel component for:**
- **(a)** two processing cores  
- **(b)** four processing cores

**Answer:**

Amdahl's Law:  
Speedup = 1 / [(1 - P) + (P / N)]

Where:  
- \( P = 0.60 \) (parallel fraction)  
- \( N \) = number of cores

**(a) Two cores:**  
Speedup = 1 / [(1 - 0.60) + (0.60 / 2)] = 1 / [0.40 + 0.30] = 1 / 0.70 ≈ 1.43

**(b) Four cores:**  
Speedup = 1 / [(1 - 0.60) + (0.60 / 4)] = 1 / [0.40 + 0.15] = 1 / 0.55 ≈ 1.82

---

## 4.3
**Does the multithreaded web server described in Section 4.1 exhibit task or data parallelism?**

**Answer:**  
It exhibits **task parallelism**. Each thread handles a different client connection, performing similar tasks but on different data.

---

## 4.4
**What are two differences between user-level threads and kernel-level threads? Under what circumstances is one type better than the other?**

**Answer:**
- **Management:** User-level threads are managed in user space, kernel-level threads by the OS.
- **System Call Visibility:** User-level threads are invisible to the kernel; kernel-level threads are known and scheduled by the OS.

**User-level threads** are better when context switching speed is more important.  
**Kernel-level threads** are better when threads must block independently (e.g., I/O).

---

## 4.5
**Describe the actions taken by a kernel to context-switch between kernel-level threads.**

**Answer:**  
- Save the current thread’s state (registers, stack pointer).
- Load the new thread’s state from its control block.
- Update memory maps or CPU state if needed.
- Resume execution of the new thread.

---

## 4.6
**What resources are used when a thread is created? How do they differ from those used when a process is created?**

**Answer:**  
Creating a **thread** allocates a stack, register state, and thread control block.  
Creating a **process** allocates all of the above **plus** a separate address space, page tables, and OS resources like file descriptors. Thread creation is thus lighter and faster.

---

## 4.7
**Is it necessary to bind a real-time thread to an LWP in a many-to-many model? Explain.**

**Answer:**  
Yes. In real-time systems, **binding a real-time thread to an LWP** ensures that it is directly scheduled by the kernel without delay from user-level scheduling. This guarantees timely execution and meets real-time constraints.
