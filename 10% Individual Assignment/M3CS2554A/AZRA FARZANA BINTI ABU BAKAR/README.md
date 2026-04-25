# 📊 Parallel Student Attendance Counter

## 📌 Overview
This project demonstrates the comparison between **three programming techniques**:
- Sequential
- Concurrent (Threading)
- Parallel (Multiprocessing)

The system processes a large dataset of student attendance (over 300,000 records) and measures execution time for each technique.

---

## 🎯 Objectives
- To understand differences between sequential, concurrent, and parallel programming  
- To implement all three techniques using Python  
- To analyze performance when handling large-scale data  
- To visualize execution time using a graph  

---

## ⚙️ Techniques Explanation

### 1. Sequential Processing
Sequential processing executes tasks **one by one** using a single flow.

✔ Simple  
✔ Low overhead  
❌ Cannot utilize multiple cores  

---

### 2. Concurrent Processing (Threading)
Threading allows multiple tasks to run **at the same time (logically)**.

✔ Better responsiveness  
✔ Suitable for lightweight tasks  
❌ Limited by Python GIL (Global Interpreter Lock)  

---

### 3. Parallel Processing (Multiprocessing)
Multiprocessing uses **multiple CPU cores** to run tasks simultaneously.

✔ True parallel execution  
✔ Suitable for heavy computations  
❌ Higher overhead (process creation)  

---

## 📥 Input Used

```
Present: 245090  
Absent: 89700  
```

---

## 📤 Output Result

```
Total Students: 334790

Sequential Time: 0.009078025817871094
Threading Time: 0.014542579650878906
Multiprocessing Time: 0.08580613136291504

Present: 245090
Absent: 89700
```

---

## 📊 Performance Analysis

Based on the result:

- **Sequential** is the fastest (0.0090s)  
- **Threading** is slightly slower (0.0145s)  
- **Multiprocessing** is the slowest (0.0858s)  

This happens because:
- The task (counting attendance) is simple  
- Overhead of creating threads and processes is higher than the task itself  

---

## 📈 Graph Visualization

The system generates a bar chart to compare execution time between:
- Sequential  
- Threading  
- Multiprocessing  

📌 *Graph image is shown below.*

---

## 🧠 Conclusion

This project shows that:

> Parallel and concurrent techniques are not always faster than sequential execution.

For simple operations, sequential processing performs better, while parallel techniques are more useful for complex computations.

---

## 🎥 Demonstration Video

👉 YouTube link here:  
[Click to watch presentation](YOUTUBE_LINK_HERE)

---

## 💻 Source Code (Click to Expand)

<details>
<summary>👉 Click here to view full code</summary>

```python
import time
import threading
from multiprocessing import Pool
import matplotlib.pyplot as plt

# =========================
# GENERATE DATA (MANUAL INPUT)
# =========================
def generate_attendance(present_count, absent_count):
    return ["Present"] * present_count + ["Absent"] * absent_count

# =========================
# SEQUENTIAL
# =========================
def count_sequential(data):
    present = data.count("Present")
    absent = data.count("Absent")
    return present, absent

# =========================
# THREADING (CONCURRENT)
# =========================
def count_threading(data, num_threads=4):
    threads = []
    results = [None] * num_threads
    chunk_size = len(data) // num_threads

    def worker(i, sub_data):
        present = sub_data.count("Present")
        absent = sub_data.count("Absent")
        results[i] = (present, absent)

    for i in range(num_threads):
        start = i * chunk_size
        end = (i + 1) * chunk_size if i != num_threads - 1 else len(data)

        t = threading.Thread(target=worker, args=(i, data[start:end]))
        threads.append(t)
        t.start()

    for t in threads:
        t.join()

    total_present = sum(r[0] for r in results)
    total_absent = sum(r[1] for r in results)

    return total_present, total_absent

# =========================
# MULTIPROCESSING (PARALLEL)
# =========================
def count_part(data):
    return data.count("Present"), data.count("Absent")

def count_multiprocessing(data, num_processes=4):
    chunk_size = len(data) // num_processes
    chunks = []

    for i in range(num_processes):
        start = i * chunk_size
        end = (i + 1) * chunk_size if i != num_processes - 1 else len(data)
        chunks.append(data[start:end])

    with Pool(processes=num_processes) as pool:
        results = pool.map(count_part, chunks)

    total_present = sum(r[0] for r in results)
    total_absent = sum(r[1] for r in results)

    return total_present, total_absent

# =========================
# MAIN PROGRAM
# =========================
if __name__ == "__main__":
    print("=== Student Attendance System ===")

    # INPUT
    present_count = int(input("Enter number of Present students: "))
    absent_count = int(input("Enter number of Absent students: "))

    # GENERATE DATA
    data = generate_attendance(present_count, absent_count)

    print("\nTotal Students:", len(data))

    # SEQUENTIAL
    start = time.time()
    p, a = count_sequential(data)
    seq_time = time.time() - start
    print("Sequential Time:", seq_time)

    # THREADING
    start = time.time()
    p, a = count_threading(data)
    thread_time = time.time() - start
    print("Threading Time:", thread_time)

    # MULTIPROCESSING
    start = time.time()
    p, a = count_multiprocessing(data)
    process_time = time.time() - start
    print("Multiprocessing Time:", process_time)

    # FINAL RESULT
    print("\nPresent:", p)
    print("Absent:", a)

    # =========================
    # GRAPH
    # =========================
    methods = ["Sequential", "Threading", "Multiprocessing"]
    times = [seq_time, thread_time, process_time]

    plt.bar(methods, times)
    plt.xlabel("Method")
    plt.ylabel("Time (seconds)")
    plt.title("Performance Comparison")

    plt.show()
```
