# Mastering the technical interview

*August 21, 2022*

Kappa Theta Pi Technical Development

with Neha Desaraju

---

## What is a technical interview question?

* Typically variation of a common problem such as sorting a certain kind of vector or inserting/finding item in binary search tree
* 1-2 per interview
* Problem may take 15-30 minutes (for a total 30-60 min interview)

---

## Keep in mind

* Don't panic - you don't always need the answer
* Always keep talking
* Ask questions
* Talk about what you're thinking, it's a conversation

---

### 1. Clarify

* What other info do we need? Space/time constraints? Empty/null possibility?
* Arrays duplicate, sorted, or negatives?
* Linkedlists single or double?

---

### 2. Consider examples/edge cases

* Define them clearly
* Write out expected behavior
* Be sure to handle 0/null, 1, and many for num of elements
* Sometimes many-even is different than many-odd

---

### 3. Brute force

1. Don't overthink
2. Check it against simple inputs & outputs (including edge cases)
3. Large O complexity is fine for now
4. Don't code

---

### 4. Optimize

* Spend lots of time here
* Talk through specific places you think you can optimize (develop this intuition)
* Ask targeted questions (e.g. "I'm not sure how to fix <specific problem>..."), your interview can give you nudges in the right direction
* Improve on how LONG or how MANY steps you take
* You can ask your interviewer if they think you're on the right track!
* Try hash tables, recursion, priority queues, dynamic programming, and sorting first

---

### 5. Write code

* Mention what language you're using (Python recommended, Java ok)
* Use pseudocode (especially in case you run out of time)
* Code can be correct-ish

---

### 6. Check

* Step through like you're a debugger
* Think of additional edge cases and test
* Go back until you run out of time
* "And I think that works"

---

## Examples <!-- .element: class="r-fit-text" -->

--

Given an array of integers and an additional integer x, print out pairs of numbers that sum to x.

--

```python
def print_pairs_sum_to_x(arr, x):
    seen = set()
    for num in arr:
        complement = x - num
        if complement in seen:
            print(complement, num)
        seen.add(num)
```

--

Given k sorted arrays, each containing n elements, combine them in sorted order.

--

```python
import heapq

def merge_sorted_arrays(arrays):
    heap = [(array[0], i, 0) for i, array in enumerate(arrays) if array]
    heapq.heapify(heap)
    merged = []
    while heap:
        val, arr_idx, elem_idx = heapq.heappop(heap)
        merged.append(val)
        if elem_idx + 1 < len(arrays[arr_idx]):
            next_val = arrays[arr_idx][elem_idx + 1]
            heapq.heappush(heap, (next_val, arr_idx, elem_idx + 1))
    return merged
```

---

This presentation was made with ❤️ and `revealjs` by Neha Desaraju.