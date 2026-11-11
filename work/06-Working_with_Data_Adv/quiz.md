# 📝 Quiz: 06 - Working with Data (Advanced)

47 questions covering Pandas Series/DataFrames, loading/exploring data, indexing/selection, cleaning, column operations, sorting/filtering/searching, grouping and combining tables, and a "going further" bonus. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first — the Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Series and DataFrames

**1.** (Short Answer) What's the difference between a Pandas `Series` and a `DataFrame`?
Answer: a series is one dimensional and a dataframe is 2d

**2.** (Code Tracing) What prints?
```python
s = pd.Series({'a': 1, 'b': 2})
print(s['a'])
```
Answer: 1

**3.** (Short Answer) What does `df.shape` return?
Answer: (rows, columns) tuples

**4.** (Short Answer) If you add two `Series` together and one has a label the other doesn't, what happens at that label?
Answer: NaN

**5.** (Short Answer) You have a list of dictionaries, one per student (the way you stored records in Module 03b). What does `pd.DataFrame(that_list)` turn each dictionary into?
Answer: Each dict becomes a row

**6.** (Code Tracing) What prints?
```python
scores = pd.Series([70, 95, 88])
print(scores[scores > 80].tolist())
```
Answer: [95, 88]

---

## Section B — Loading and Exploring Data

**7.** (Multiple Choice) Which method shows summary statistics (mean, std, min/max) for numeric columns?
A) `.head()`  B) `.columns`  C) `.describe()`  D) `.shape`
Answer: C

**8.** (Short Answer) What's the difference between what `.head()` and `.info()` each tell you about a DataFrame?
Answer: .head() shows the first 5 rows of actual data. .info() shows the row counts

**9.** (Short Answer) How do you count how many missing values are in *each column* of a DataFrame?
Answer: df.isnull().sum()

**10.** (Short Answer) What do `df.duplicated().sum()` and `df['col'].value_counts(dropna=False)` each tell you?
Answer: df.duplicated().sum() counts rows that exactly repeat an earlier row. value_counts(dropna=False) counts how often each distinct value appears, including missing values.

**11.** (Short Answer) Titanic's `Age` column holds whole numbers, but its dtype is `float64`. Why?
Answer: NaN only exists as a float, so the missing values force the whole column to float64.

---

## Section C — Indexing and Selection

**12.** (Short Answer) What's the difference between `.loc[]` and `.iloc[]`?
Answer: .loc[] selects by label (index values and column names), and .iloc[] selects by position (0, 1, 2, ...).

**13.** (Short Answer) Is `df.loc[0:4]` inclusive or exclusive of row `4`? What about `df.iloc[0:4]` and position `4`?
Answer: df.loc[0:4] includes row 4. df.iloc[0:4] stops before position 4.

**14.** (Short Answer) What symbols does Pandas require for combining conditions when filtering a DataFrame (instead of the `and`/`or` keywords)?
Answer: & for and, | for or, and ~ for not

**15.** (Short Answer) What does `df[df['Age'] < 10]` return?
Answer: A DataFrame containing only the rows where Age is under 10, with all columns. Rows with missing Age are excluded.

**16.** (Short Answer) Rewrite `df[(df['Embarked'] == 'C') | (df['Embarked'] == 'Q')]` using `.isin()`. Does `df['Age'].between(13, 19)` include ages 13 and 19?
Answer: df[df['Embarked'].isin(['C', 'Q'])]. Yes, .between(13, 19) includes both 13 and 19

**17.** (Multiple Choice) Which one returns a `DataFrame` rather than a `Series`?
A) `df['Age']`  B) `df[['Age']]`  C) `df.Age`  D) `df.loc[0]`
Answer: B

**18.** (Short Answer) After `by_id = df.set_index('PassengerId')`, what does `by_id.loc[2]` select, and how is that different from `df.loc[2]`?
Answer: by_id.loc[2] is the row whose PassengerId is 2

**19.** (Code Tracing) After `by_id = titanic.set_index('PassengerId')`, do `by_id.loc[3]` and `by_id.iloc[3]` select the same passenger? Why or why not?
Answer: by_id.loc[3] is the row labeled PassengerId 3

**20.** (Short Answer) Write a filter for passengers who did **not** board at Southampton (`'S'`), using `~` and `.isin()`.
Answer: df[~df['Embarked'].isin(['S'])]

**21.** (Short Answer) What's wrong with `df[df['Age'] < 10]['child'] = True`, and what should you write instead?
Answer: It’s chained assignment. The first step filters into a copy, so the assignment changes that copy and the original is untouched. you should 
write df['child'] = False
df.loc[df['Age'] < 10, 'child'] = True

---

## Section D — Cleaning

**22.** (Short Answer) What's the difference between `.dropna()` and `.fillna()`?
Answer: .dropna() removes rows (or columns) with missing values. .fillna() replaces missing values with something else.

**23.** (Short Answer) What does `pd.to_numeric(col, errors='coerce')` do to a value like `'ninety'` in that column?
Answer: It becomes NaN instead of raising an error

**24.** (True/False) `NaN` and an empty string `""` are always treated identically by `.isnull()`.
Answer: False

**25.** (Short Answer) Two rows have the same `order_id` but different `amount`s. Does `df.drop_duplicates()` remove one of them? What would you write to keep only the last row for each `order_id`? 
Answer: No. The rows differ in amount, so they aren’t exact duplicates. Use df.drop_duplicates(subset=['order_id'], keep='last').

**26.** (Short Answer) A survey stores missing ages as `-1`. Why is that a problem for `df['age'].mean()`, and how do you fix it?
Answer: Pandas treats -1 as a real number, which drags the mean down. Turn it into a real missing value with df['age'].replace(-1, np.nan), and .mean() will skip it.

**27.** (Short Answer) A date column holds `'2022-01-01'`, `'2022/03/01'`, and `'April 5, 2022'`. Why can `pd.to_datetime(col, errors='coerce')` turn two perfectly valid dates into `NaT`, and how do you fix it?
Answer: Since pandas 2.0, it guesses the format from the first value and turns anything that doesn’t match into NaT, silently. Fix it with format='mixed'.

**28.** (Short Answer) Why does `.astype('int64')` fail on a column with missing values, while `.astype('Int64')` works?
Answer: int64 can’t hold missing values. The nullable Int64 type can, and shows them as <NA>.

**29.** (Short Answer) Before deleting rows with a repeated `order_id`, why would you look at `df[df.duplicated(subset=['order_id'], keep=False)]` first?
Answer: So you can see every copy side by side and decide whether they’re true duplicates, corrections, or different purchases before deleting anything.

---

## Section E — Column Operations, Sorting, Filtering, and Searching

**30.** (Short Answer) How do you create a new column that's the sum of two existing numeric columns?
Answer: df['total'] = df['a'] + df['b']

**31.** (Short Answer) What does `.apply()` do that you could also do with a `for` loop over rows — and why is `.apply()` usually preferred?
Answer: .apply() runs a function on every value in a column (or every row with axis=1), like a loop would. It’s shorter and gives back a result aligned to the column, with no list to build. A whole-column operation is better still when one exists.

**32.** (Short Answer) What does `ascending=False` do inside `df.sort_values(by='score', ascending=False)`?
Answer: It sorts from highest to lowest instead of the default lowest to highest.

**33.** (Short Answer) What's the main advantage of `.query()` over bracket-based boolean filtering (`df[df['col'] > 5]`)?
Answer: Readability.

**34.** (Code Tracing) `bonus` is a brand-new column. What value do the rows with `score >= 80` get in it?
```python
df.loc[df['score'] < 80, 'bonus'] = 5
```
Answer: NaN. The rule only assigns where score < 80, and nothing was ever assigned to the other rows. Create the column with a default first to avoid this.

**35.** (Short Answer) To compute `price * qty` for every row, why should you write `df['price'] * df['qty']` instead of looping with `.iterrows()`? When *is* a loop (preferably `.itertuples()`) the right tool?
Answer: The vectorized version is shorter, clearer, and faster. A loop is the right tool when each row triggers an action rather than a calculation, such as writing a file per row, sending a message, or calling a website.

**36.** (Short Answer) What do `case=False` and `na=False` each do in `df['name'].str.contains('an', case=False, na=False)`?
Answer: case=False ignores capitalization. na=False treats missing values as “no match”, so the mask has no NaN and the filter doesn’t fail.

**37.** (Code Tracing) A student has `math = 95` and `average = 91`. What is their `award` after these three lines, and what would it be if the last two lines were swapped?
```python
df['award'] = 'None'
df.loc[df['average'] >= 85, 'award'] = 'Honor Roll'
df.loc[df['math'] >= 90, 'award'] = 'Math Star'
```
Answer: 'Math Star', because the last matching rule wins. If the last two lines were swapped, it would be 'Honor Roll'.

**38.** (Short Answer) What does `pd.cut(df['score'], bins=[0, 70, 90, 101], labels=['Low', 'Mid', 'High'], right=False)` do, and why is it usually better than `.apply()` with an `if`/`elif` function for the same job?
Answer: It sorts scores into labeled bands: [0, 70) is Low, [70, 90) is Mid, and [90, 101) is High. right=False includes each left edge and excludes the right. It’s better than .apply() with if/elif because it’s one whole-column operation that’s shorter, faster, and states the bands directly.

**39.** (Short Answer) What's the difference between `df.query('math_score >= minimum')` and `df.query('math_score >= @minimum')`?
Answer: Without @, pandas looks for a column named minimum and raises an error. With @, it uses the value of your Python variable minimum.

**40.** (Code Tracing) What does each line return, and why are they different?
```python
books = pd.Series(['C++ Primer', 'C Programming'])
books.str.contains('C++').tolist()
books.str.contains('C++', regex=False).tolist()
```
Answer: The first returns [True, True]. The second returns [True, False]. By default, .str.contains() treats the text as a pattern, and + is special in patterns, so 'C++' matches any C. With regex=False, it searches for the literal text C++.

---

## Section F — Grouping and Combining

**41.** (Code Tracing) What does this return?
```python
df = pd.DataFrame({'team': ['A', 'B', 'A', 'B'], 'points': [10, 4, 20, 6]})
df.groupby('team')['points'].mean()
```
Answer:  
team
A    15.0
B     5.0
Name: points, dtype: float64

**42.** (Short Answer) Write a `groupby` with `.agg()` that gives, for each `team`, the number of rows and the total `points`, as columns named `games` and `total`.
Answer: df.groupby(‘team’).agg(games=(‘points’, ‘count’), total=(‘points’, ‘sum’))

**43.** (Short Answer) When would you use `pd.concat()` instead of `.merge()`? What does `ignore_index=True` do?
Answer: concat stacks more rows of the same data while merge adds related columns

**44.** (Short Answer) In `orders.merge(prices, on='product_id', how='left')`, what happens to an order whose `product_id` isn't in `prices`? What would `how='inner'` do instead? And why does a merge on state codes fail when one table uses `'tx'` and the other uses `'TX'`?
Answer: With `how='left'`, the order stays, and its columns from `prices` are `NaN`. With `how='inner'`, that order is dropped.

**45.** (Short Answer) In Titanic, `groupby('Pclass').size()` gives 216 for 1st class, but `groupby('Pclass')['Age'].count()` gives 186. Why are they different?
Answer: size counts the rows 

**46.** (Short Answer) `purchases` has 6 rows. After `purchases.merge(buyers, on='buyer_id', how='left')`, it has 8. What probably happened, and how can `validate=` protect you?
Answer: it produces an error for duplicate values instead of just performing the task anyway.

---

## Section G — Going Further (Bonus)

**47.** (Short Answer) What do the `usecols` and `nrows` arguments to `pd.read_csv()` do, and when would you reach for them?
Answer:

