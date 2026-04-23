
## 🎲 PARALLEL DICE SIMULATOR
**NAME:** INTAN NURUL FASIHAH BINTI MOHD LAZIM

**STUDENT ID:** 2024442972

**CLASS:** M3CS2554A

--------------------------------------------------------------------------------------------------------------------------------
## 📝 INTRODUCTION
The Parallel Dice Combination Simulator is a Python-based application that simulates rolling two dice a large number of times to analyze the frequency of each possible outcome (sum = 2 to 12).

This project demonstrates three execution approaches:

- Sequential execution (single process)
- Concurrent execution using threading
- Parallel execution using multiprocessing

The goal is to compare performance and efficiency when processing large-scale data.
  
  ------------
 ## 🎯 OBJECTIVE
 
- Simulate large numbers of dice rolls
- Implement sequential processing as baseline
- Apply threading for concurrent execution
- Apply multiprocessing for parallel execution
- Compare execution time between methods
- Analyze distribution of dice outcomes
-----------

## 💻 SYSTEM REQUIREMENT
Hardware Requirements:
- Minumum 4GB RAM
- Multi-core CPU (recommended for multiprocessing)

Software Requirement
- Operating System: Windows
- Python version : 3.8 and above

Python Libraries (Built-in)
- ```bash  random```
- ```bash  time```
- ```bash  threading```
- ```bash  multiprocessing```
  --------------
  ## ⚙️ INSTALLATION GUIDE
Step 1: Start Virtual Machine
1. Open VMware Workstation
2. Start your Kali Linux virtual machine
3. Log in to Kali Linux
 
 Step 2: Open Terminal
- Click Terminal or press:
```bash  
Ctrl + Alt + T
```
Step 3: Check Python Installation

Kali usually has Python pre-installed.

Run:

```bash  
python3 --version
```
If not installed:
```bash  
sudo apt update
sudo apt install python3 -y
```

Step 4: Create Project Folder
```bash  
mkdir parallel-dice-simulator
cd parallel-dice-simulator
```
Step 5: Create Python File
```bash  
nano main.py
```
Step 6: Paste Your Code
Copy your Python code
Paste into main.py
Save:

In nano:
- Press ```bash CTRL + X```
- Press ```bashY```
- Press ```bashEnter```

 ## ▶️ 5. How It Runs in Kali Linux

Run the program using:
```bash  
python3 main.py
```
What Happens When You Run

Program simulates dice rolls
Executes:
- Sequential method
- Threading (concurrent)
- Multiprocessing (parallel)
- Measures execution time
- Displays analytics:
- Frequency
- Percentage
 Most/least common values

2. Performance in VM

Running in VMware may be:
- Slower than real machine
- Limited by allocated CPU/RAM
👉 Recommended:
- Allocate at least 2–4 CPU cores
- Allocate 4GB RAM or more
  
3. If Program is Too Slow

Change:
```bash
TOTAL_ROLLS = 1_000_000
```
instead of:
```bash
1_000_000_000
```

-------------------
💻 Source Code

```bash
import random
import time
from threading import Thread
from multiprocessing import Process, Manager, cpu_count

def roll_dice():
    return random.randint(1, 6) + random.randint(1, 6)

def print_analytics(result, total):
    print("\n--- Analytics ---")
    print(f"Total Rolls: {total}")

    max_key = max(result, key=result.get)
    min_key = min(result, key=result.get)

    for key in sorted(result):
        percentage = (result[key] / total) * 100
        print(f"{key}: {result[key]} ({percentage:.2f}%)")

    print(f"\nMost common sum: {max_key}")
    print(f"Least common sum: {min_key}")

def run_sequential(n):
    print("\n--- Sequential ---")
    result = {i: 0 for i in range(2, 13)}

    start = time.time()
    for _ in range(n):
        result[roll_dice()] += 1
    end = time.time()

    print(f"Time: {end - start:.2f} seconds")
    print_analytics(result, n)

def thread_worker(n, result):
    local = {i: 0 for i in range(2, 13)}

    for _ in range(n):
        local[roll_dice()] += 1

    for k in local:
        result[k] += local[k]

def run_threading(n, threads=4):
    print("\n--- Threading (Concurrent) ---")
    result = {i: 0 for i in range(2, 13)}

    chunk = n // threads
    threads_list = []

    start = time.time()

    for _ in range(threads):
        t = Thread(target=thread_worker, args=(chunk, result))
        t.start()
        threads_list.append(t)

    for t in threads_list:
        t.join()

    end = time.time()

    print(f"Time: {end - start:.2f} seconds")
    print_analytics(result, n)

def process_worker(n, shared):
    local = {i: 0 for i in range(2, 13)}

    for _ in range(n):
        local[roll_dice()] += 1

    for k in local:
        shared[k] += local[k]

def run_multiprocessing(n):
    print("\n--- Multiprocessing (Parallel) ---")

    manager = Manager()
    result = manager.dict({i: 0 for i in range(2, 13)})

    processes = []
    cores = cpu_count()
    chunk = n // cores

    start = time.time()

    for _ in range(cores):
        p = Process(target=process_worker, args=(chunk, result))
        p.start()
        processes.append(p)

    for p in processes:
        p.join()

    end = time.time()

    print(f"Time: {end - start:.2f} seconds")
    print_analytics(dict(result), n)

def main():
    TOTAL_ROLLS = 1_000_000

    print(f"Simulating {TOTAL_ROLLS:,} dice rolls...")
    run_sequential(TOTAL_ROLLS)
    run_threading(TOTAL_ROLLS)
    run_multiprocessing(TOTAL_ROLLS)

if __name__ == "__main__":
    main()
-------------------


```

-----------------------
#📈 Result Analysis


--------------------------------

# Sample Input / Output


Sample Input




Sample Output

-----------------------
📌 Conclusion

This program demonstrates how:

- Sequential processing works step-by-step
- Threading improves performance using concurrency
- Multiprocessing achieves the best performance using parallel execution

The results also confirm the probability distribution of dice combinations, where 7 is the most frequent outcome.
  

  
 

  




