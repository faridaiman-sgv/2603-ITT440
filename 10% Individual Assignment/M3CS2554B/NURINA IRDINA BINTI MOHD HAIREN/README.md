# ⁶⁹📐𓈒𖹭🔢𓈒»〽⭑🖇๋࣭  PRIME NUMBER FINDER  ⭑⚝📈⊹₊ ⋆📑⚛ྀ

#### STUDENT NAME: NURINA IRDINA BINTI MOHD HAIREN
#### STUDENT ID: 2024239814
#### CLASS: CDCS2554B



## ⋆. 𐙚 ˚ Introduction

This project is a Python-based utility designed to find prime numbers within a specified range. The core objective is to compare three different execution models:

1. Sequential: Standard single-threaded execution.

2. Threading (Concurrent): Splitting the range into chunks handled by different threads.

3. Multiprocessing (Parallel): Distributing the workload across multiple CPU cores.

## ⋆. 𐙚 ˚ Problem Statement

1. The Mathematical Challenge
   
Finding prime numbers is a computationally intensive task. As the range of numbers increases, the 
time required to check each number for primality grows significantly. A standard sequential (one-by-
one) approach becomes inefficient for very large ranges, leading to long execution times.

2. The Technical Bottleneck

Python’s execution is typically single-threaded due to the Global Interpreter Lock (GIL). While this ensures safety, it prevents the program from fully utilizing the power of modern multi-core processors when performing mathematical calculations.

## ⋆. 𐙚 ˚ System Requirements

-Operating System: Windows, macOS, or Linux.

-Python Version: Python 3.7 or higher.

-Hardware: Multi-core processor (recommended to see the benefits of Parallelism).

## ⋆. 𐙚 ˚ Installation Steps

1. Clone the Repository:

    git clone https://github.com/your-username/prime-finder.git
cd prime-finder

2. No External Dependencies: This program uses Python’s standard library (math, threading, multiprocessing). No pip install is required.

   
## ⋆. 𐙚 ˚ How to Run

1. Open your terminal or command prompt.

2. Navigate to the project folder.

3. Run the script:

python prime_finder.py

4. Follow the on-screen prompts to enter the start and end range.

 ## ⋆. 𐙚 ˚ Sample Input/Output

 Input:

 <img width="635" height="76" alt="image" src="https://github.com/user-attachments/assets/8a97a052-bac4-4c53-92e4-80a538baf8c1" />

 Output:

 <img width="1155" height="314" alt="image" src="https://github.com/user-attachments/assets/55799c7c-296f-4bd0-8693-e4db0168ba61" />

## ⋆. 𐙚 ˚ Source code

<img width="791" height="735" alt="Screenshot 2026-04-22 005502" src="https://github.com/user-attachments/assets/12083226-de4c-4480-b394-7791d4452e91" />\

<img width="804" height="385" alt="Screenshot 2026-04-22 005527" src="https://github.com/user-attachments/assets/78f21162-6a24-41e8-9702-071ec18432ba" />\

<img width="802" height="541" alt="Screenshot 2026-04-22 005546" src="https://github.com/user-attachments/assets/a02b3e5e-8470-4f63-a4c3-4e7194a08f7c" />

## ⋆. 𐙚 ˚ Conclusion

This project successfully demonstrated the practical differences between concurrency and parallelism in Python. By benchmarking three execution models, several key conclusions were reached:

-Sequential Execution: Proved inefficient for large-scale calculations as it utilizes only a single CPU core.

-Threading (Concurrency): Provided minimal performance gains. Due to Python’s Global Interpreter Lock (GIL), threads cannot perform CPU-intensive math simultaneously, making this method better suited for tasks that involve "waiting" (like network requests) rather than "calculating."

-Multiprocessing (Parallelism): This was the most effective approach. By creating separate processes, the program bypassed the GIL and utilized the full power of a multi-core processor, significantly reducing the time required to find primes.

##  🎞️✮⋆˙Video Demonstration:








 

