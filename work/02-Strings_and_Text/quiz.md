# 📝 Quiz: 02 - Strings and Text

20 questions covering string basics, string methods, formatted strings (f-strings), and the "going further" topics from the Challenge sections. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first — the Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — String Basics

**1.** (Multiple Choice) Which of these lets you write a string that spans multiple lines without using `\n`?
A) `'...'`  B) `"..."`  C) `'''...'''`  D) `f'...'`
answer: C

**2.** (Code Tracing) What prints?
```python
word = 'Python'
print(word[-1])
```
answer: d

**3.** (Code Tracing) What prints?
```python
word = 'Python'
print(word[::-1])
```
answer: drow

**4.** (True/False) Writing `'It's a test'` (an unescaped apostrophe inside single quotes) causes an error.
answer: true

**5.** (Short Answer) Why can't you run `word[0] = 'J'` if `word` is a string?

strings in python are immuatable, you'd have to make a new string and then change it

**6.** (Code Tracing) What does this print (describe the spacing)?
```python
print('Hi\tThere')
```
Hi <tab> There

---

## Section B — String Methods

**7.** (Code Tracing) What prints?
```python
print('  Ada  '.strip())

```
answer: Ada

**8.** (Code Tracing) What prints?
```python
print('the quick brown fox'.split())
```
answer: ['the', 'quick', 'brown', 'fox']

**9.** (Short Answer) What's the difference between using `.find()` and using the `in` keyword to check whether a substring is present?
answer: find returns the indexed location of the found string while in returns a bool value

**10.** (Multiple Choice) Which method checks whether a string contains only digit characters?
A) `.isdigit()`  B) `.isalpha()`  C) `.find()`  D) `.strip()`
answer: A

**11.** (Code Tracing) What prints?
```python
print('hello.py'.endswith('.py'))
```
answer: true

**12.** (Short Answer) What does `'a,b,c'.split(',')` return?
answer: ['a', 'b', 'c']

---

## Section C — Formatted Strings

**13.** (Code Tracing) What prints?
```python
price = 9.5
print(f'{price:.2f}')
```
answer: 9.50

**14.** (Code Tracing) What prints?
```python
print(f'{1234567:,}')
```
answer 1,234,567
The f tells python to perform any operations in {}.

**16.** (Multiple Choice) Which format spec right-aligns a value in a 10-character field?
A) `:<10`  B) `:>10`  C) `:^10`  D) `:10>`

answer: B

**17.** (Code Tracing) What prints?
```python
x = 5
print(f'{x * 2}')
```
answer: 10

**18.** (Short Answer) Name the two older string-formatting styles that predate f-strings (still seen in older code).
answer: % and .format

---

## Section D — Going Further (Bonus)

**19.** (Short Answer) What does prefixing a string with `r` (a raw string) do, and why is it especially useful for Windows file paths?

**20.** (Code Tracing) What prints?
```python
x = 7
print(f'{x=}')
```
