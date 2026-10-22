# 📝 Quiz: 03b - Containers → Functions

24 questions covering container choice, the loop patterns, nested expressions, function basics, `print` vs. `return`, mutation, and pipelines. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, so don't peek. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning, rather than asking it to solve the question for you.

---

## Section A — Containers

**1.** (Short Answer) Why is `scores = [87, 91, 74]` better than `score1 = 87`, `score2 = 91`, `score3 = 74`? Give two reasons.

answer: You won't need a new a new variable for each individual score. Also the list can then be traversed easily without need to perform tasks to individual variables. 

**2.** (Code Tracing) What prints?
```python
scores = [87, 91, 74, 88, 95]
scores.append(60)
scores.remove(91)
print(scores[1], scores[-1], len(scores))
```
answer: 74 60 5

**3.** (Multiple Choice) Which container fits "Student ID → GPA" best?
A) list  B) tuple  C) dictionary  D) set

answer: C

**4.** (Multiple Choice) Which container fits "an RGB color" best?
A) list  B) tuple  C) dictionary  D) set

answer: B

**5.** (Short Answer) Give a better description of a tuple than "an immutable list."

answer: a tuple is like a coordinate in a plane

**6.** (Code Tracing) What prints?
```python
a = {"OOP", "Database", "Algorithms"}
b = {"Database", "Networks"}
print(a & b)
```

answer: {'Database'}

**7.** (Code Tracing) Evaluate one step at a time. What is the value?
```python
students = [
    {"name": "Alice", "grade": 91},
    {"name": "Bob",   "grade": 84}
]
students[-1]["name"][0]
```
answer: B
---

## Section B — Patterns

**8.** (Short Answer) Accumulate and Count both start at `0`. What's the difference in how they update? Accumulate adds the items value to the total while count just adds 1.

**9.** (Code Tracing) What prints?
```python
nums = [4, -2, 7, -5, 3]
x = []
for n in nums:
    if n < 0:
        x.append(n)
print(x)
```
answer: [-2, -5]

**10.** (Multiple Choice) Which pattern is question 9?
A) Accumulate  B) Count  C) Filter  D) Best So Far
answer: C

**11.** (Short Answer) When finding the maximum with the Best So Far pattern, why should `best` start at the first item instead of `0`?

answer: If all the numbers are negative the function doesn't work.

---

## Section C — Function Basics

**12.** (Code Tracing) What prints when this cell runs?
```python
def square(x):
    return x * x
```
answer: nothing prints

**13.** (Short Answer) In `def area(width, height):` and `area(3, 5)`, which are the parameters and which are the arguments?
answer:with and height are the parameters and 3,5 are the arguments

**14.** (Code Tracing) What prints?
```python
def square(x):
    return x * x

print(square(3) + square(square(2)))
```
answer: 25

**15.** (Code Tracing) What prints? (Careful!)
```python
def double(x):
    print(x * 2)

result = double(5)
print(result)
```
answer: 10 None

**16.** (True/False) `print()` gives a value back to the program so it can be used in later calculations.
answer:false

**17.** (Code Tracing) What prints?
```python
def check(x):
    return "big"
    return "small"

print(check(1))
```
answer: big

**18.** (Short Answer) Give three reasons functions are useful *besides* avoiding copy/paste.
answer: Each function can be tested on its own, a good name makes code easier to read, an issue fixed in one place is fixed everywhere.

---

## Section D — Functions + Containers

**19.** (Short Answer) Find the bug:
```python
def total(numbers):
    result = 0
    for n in numbers:
        result += n
        return result
```
answer: return inside the loop

**20.** (Code Tracing) What prints?
```python
def add_one(values):
    values.append(1)
    return values

a = [5]
b = add_one(a)
print(a)
```
answer: [5, 1]

**21.** (Code Tracing) What prints?
```python
nums = [3, 1, 2]
x = nums.sort()
print(x, nums)
```
answer: None [1, 2, 3]

**22.** (Multiple Choice) `frequency(["a", "b", "a"])` from Notebook 05 turns a list into a...
A) number  B) bool  C) list  D) dictionary

answer: D

**23.** (Short Answer) Write the contract (IN / OUT / DOES) for a function `count_above(numbers, threshold)`.
answer: 
def count_above(numbers, threshold):
    """
    IN:   a list of numbers, and a threshold number
    OUT:  an int
    DOES: returns how many numbers are strictly greater than threshold
    """

**24.** (Code Tracing) Given the functions from Notebook 06, what prints?
```python
numbers = [10, -3, 20, 30]
clean = remove_negatives(numbers)
print(above(clean, average(clean)))
```
answer: [30]