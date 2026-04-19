# STUDENT NAME: NURUL NABILAH BINTI HISHAM
# STUDENT ID: 2024290614
# TITLE: PARALLEL WORKFORCE PAYROLL ENGINE

# 1. Introduction
The Parallel Workforce Payroll Engine is a high-performance Python application designed to streamline large-scale salary computations. By utilizing Parallel Processing via Python’s multiprocessing module, this engine bypasses the Global Interpreter Lock (GIL) to execute tasks across multiple CPU cores simultaneously. This approach significantly reduces processing time, ensuring high efficiency for organizational payroll management.

# 2. Tools & Environment
To ensure a lightweight yet powerful setup, the following tools were utilized:

Visual Studio Code (VS Code): The primary IDE used for writing, debugging, and executing the Python script.

Python 3.12 (Microsoft Store Version): The core programming language. This version was selected to ensure compatibility with Windows security policies.

Python Extension for VS Code: An essential tool that provides IntelliSense and debugging support.

# 3. Implementation Logic
The system follows a Process-Pool Model:

Data Ingestion: A list containing employee IDs, hourly rates, and hours worked is provided.

Parallel Mapping: The multiprocessing.Pool().map() function distributes the workload.

Independent Execution: Each worker process calculates the net pay (including an 11% EPF deduction) in its own dedicated memory space.

Process Identification: Each calculation logs a unique Process ID (PID) to prove that tasks are running in parallel across different CPU cores.

# 4. The Python Code
```python
import multiprocessing
import time
import os

# Function to calculate salary in parallel
def calculate_salary(data):
    emp_id, rate, hours = data
    # Calculate gross and net pay (minus 11% EPF)
    gross_pay = rate * hours
    net_pay = gross_pay - (gross_pay * 0.11) 
    
    # Log showing unique Process IDs (PID) for parallelism proof
    print(f"[PROCESS {os.getpid()}] Processing Employee ID: {emp_id} | Net Pay: RM{net_pay:.2f}")
    return (emp_id, net_pay)

if __name__ == "__main__":
    print("-----------------------------------------------")
    print("      PARALLEL WORKFORCE PAYROLL ENGINE        ")
    print("       Course: ITT440 - Network Programming    ")
    print("-----------------------------------------------")

    # Workforce Data: (Employee ID, Rate, Hours)
    workforce = [(202301, 50.0, 160), (202302, 45.0, 175), (202303, 65.0, 150), (202304, 55.0, 165)]

    start = time.time()

    # Initializing worker pool
    with multiprocessing.Pool() as pool:
        final_results = pool.map(calculate_salary, workforce)

    end = time.time()
    
    print("-----------------------------------------------")
    print(f"[SUCCESS] Parallel processing finished in {end - start:.4f} seconds.")
    print("-----------------------------------------------")
    for emp_id, salary in final_results:
        print(f"ID: {emp_id} | Final Salary (after EPF): RM{salary:.2f}")
```

# 5. Video Presentation Script
