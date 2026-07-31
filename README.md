# Daa-LabTask

# Lab Task 

Solved 3 of 4 parts as permitted by the assignment. Part 3 was skipped.

## Part 1. Trace It Yourself

Input: `[8, 3, 15, 6, 2]`
Output (largest): `15`
Comparisons made: `4`

Dry Run:
```
i = 1, A[i] = 3,  max = 8,  comparisons = 1
i = 2, A[i] = 15, max = 15, comparisons = 2
i = 3, A[i] = 6,  max = 15, comparisons = 3
i = 4, A[i] = 2,  max = 15, comparisons = 4
```

Sorting method used: Bubble Sort
Sorting steps:
```
Step 1: swapped 8 and 3   -> [3, 8, 15, 6, 2]
Step 2: swapped 15 and 6  -> [3, 8, 6, 15, 2]
Step 3: swapped 15 and 2  -> [3, 8, 6, 2, 15]
Step 4: swapped 8 and 6   -> [3, 6, 8, 2, 15]
Step 5: swapped 8 and 2   -> [3, 6, 2, 8, 15]
Step 6: swapped 6 and 2   -> [3, 2, 6, 8, 15]
Step 7: swapped 3 and 2   -> [2, 3, 6, 8, 15]
```
Output (sorted): `[2, 3, 6, 8, 15]`

Explanation:
To find the maximum you must check every element once, since the biggest value could be
anywhere in the list — skipping any element risks missing the true max. That's why finding
the max always takes n-1 comparisons for a list of size n, no more, no less.

## Part 2. Stack or Queue

Stack order: `Task5, Task4, Task3, Task2, Task1`
Queue order: `Task1, Task2, Task3, Task4, Task5`
Printer should use: **Queue**
Reason: a printer must serve jobs in the order they were submitted (first-come-first-served);
a stack would print the most recently added job first, which is unfair to earlier jobs.

Dry Run:
```
Stack (LIFO): push Task1, Task2, Task3, Task4, Task5 then pop in reverse
              -> completion order: Task5, Task4, Task3, Task2, Task1

Queue (FIFO): enqueue Task1 to Task5 then dequeue in same order
              -> completion order: Task1, Task2, Task3, Task4, Task5
```

Explanation:
A printer needs first-come-first-served order so that whoever submits a job first gets it
printed first. A Queue guarantees this (FIFO), while a Stack would reverse the order (LIFO)
and is therefore the wrong structure for this job.

## Part 4. Count the Steps

Single loop runs: `5`
Nested loop total prints: `25`

Dry Run:
```
Single loop, i = 1 to 5, prints 5 times

Nested loop, i = 1 to 5 and j = 1 to 5:
  inner print runs 5 times for each i, total 5 * 5 = 25 times
```

For n = 20 (single loop) / n = 10 (nested loop):
```
Single loop runs (n=20):    20
Nested loop runs (n=10):    100
```

Explanation:
The single loop does one fixed amount of work per iteration, so its total work grows
linearly with n (O(n)) — doubling n roughly doubles the runs. The nested loop repeats the
inner loop once for every outer iteration, so total work grows quadratically with n (O(n²))
— doubling n roughly quadruples the runs.

## Acceptance Criteria

1. **Input for each part:**
   - Part 1: list `[8, 3, 15, 6, 2]`
   - Part 2: task arrival sequence `Task1..Task5`
   - Part 4: loop bound `n` (n=5 in the base case, then n=20 / n=10 for the scaled case)

2. **Output for each part:**
   - Part 1: largest value (`15`), comparison count (`4`), sorted list (`[2, 3, 6, 8, 15]`)
   - Part 2: stack completion order, queue completion order, chosen structure for the printer
   - Part 4: single-loop run count, nested-loop total print count

3. **Data structure used:**
   - Part 1: simple array/list (linear scan + bubble sort, no auxiliary structure)
   - Part 2: Stack (LIFO, Python list used as a stack) and Queue (FIFO, `collections.deque`)
   - Part 4: none — pure loop counting, no data structure needed

4. **If the input size grew 100x, would the effort grow slowly, proportionally, or explosively?**
   - Part 1 (find max / bubble sort max scan): finding the max is O(n) — effort grows
     *proportionally*. Bubble sort itself is O(n²), so if we're talking about the sort step,
     effort would grow *explosively* (100x input -> ~10,000x work); but the "find largest"
     comparisons specifically grow proportionally.
   - Part 2 (stack/queue push-pop): each operation is O(1), so total work is O(n) —
     grows *proportionally* with the number of tasks.
   - Part 4 (loop counting): the single loop is O(n) — grows *proportionally*. The nested
     loop is O(n²) — grows *explosively* (100x n -> 10,000x the print calls), which is
     exactly what we see going from n=5 (25 prints) to n=10 (100 prints), a 4x increase for
     only a 2x increase in n.

## How to run
```
python part1_trace.py
python part2_stack_queue.py
python part4_complexity.py
```
