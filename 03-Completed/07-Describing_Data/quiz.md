# 📝 Quiz: 07 - Describing Data

36 questions covering types of data, center and spread, shape and outliers, comparing groups, and relationships and correlation. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Types of Data

**1.** (Short Answer) What's the difference between a column's **dtype** and its **measurement scale**?

Answer: The dtype is how pandas stores the values (int64, float64, str, bool, category). The measurement scale is what the values mean (nominal, ordinal, interval, ratio).

**2.** (Multiple Choice) Titanic's `Pclass` is stored as `1`, `2`, `3`. Its measurement scale is:

A) Nominal  B) Ordinal  C) Interval  D) Ratio

Answer: B

**3.** (Multiple Choice) Which scale has a true zero that means "none of it"?
A) Nominal  B) Ordinal  C) Interval  D) Ratio

Answer: D

**4.** (True/False) Temperature in °C is ratio data, because 20°C is twice 10°C.

Answer: False

**5.** (Short Answer) Is "number of siblings aboard" discrete or continuous? How can you tell?

Answer: Discrete, people are countable. Can't have pi people.

**6.** (Code Tracing) What prints?
```python
s = pd.Series([True, False, True, True])
print(s.mean())
```

Answer: 0.75

**7.** (Short Answer) Why is `titanic['PassengerId'].mean()` meaningless, even though pandas computes it without complaint?

Answer: PassengerId is an identifier.

**8.** (Short Answer) What does `ordered=True` in `pd.CategoricalDtype([...], ordered=True)` let you do that a plain `str` column can't?

Answer: It lets pandas know the order, so you can use min()/max(), comparisons like > and >=, and counts in logical order, all following your order rather than alphabetical order.

---

## Section B — Center and Spread

**9.** (Short Answer) Which is more robust to outliers, the mean or the median? Why?

Answer: The median. It depends only on the middle position, while the mean uses every value’s size, so one extreme value drags it.

**10.** (Code Tracing) What prints?
```python
s = pd.Series([2, 4, 4, 6, 100])
print(s.median(), s.mode()[0])
```

Answer: 4.0.4

**11.** (Short Answer) A column's mean is much larger than its median. What does that suggest?

Answer: The data are right-skewed or have large outliers pulling the mean up.

**12.** (Multiple Choice) `pd.Series(data).std()` and `np.std(data)` give slightly different answers because:
A) NumPy rounds  B) pandas skips NaN  C) they use different default `ddof`  D) one is variance

Answer: C

**13.** (Short Answer) What's the IQR, and how do you compute it in pandas?

Answer: IQR = Q3 − Q1, the width of the middle half of the data. In pandas: s.quantile(0.75) - s.quantile(0.25).
 
**14.** (Short Answer) In `.describe()`, a column's `count` is 714 but the DataFrame has 891 rows. What does that tell you?

Answer: 177 values are missing in that column (891 − 714). count only counts non-missing values.

**15.** (Short Answer) You fill 177 missing ages with the median age. What happens to the standard deviation, and why?

Answer: The std shrinks. The median doesn’t move, but the quartiles go toward the middle.

**16.** (Short Answer) Which spread statistic pairs naturally with the median, and which with the mean?

Answer: The median pairs with the IQR (both robust). The mean pairs with the std. 


---

## Section C — Shape and Outliers

**17.** (Multiple Choice) A column with `.skew()` of 4.8 is:
A) roughly symmetric  B) strongly left-skewed  C) strongly right-skewed  D) heavy-tailed but symmetric

Answer: C

**18.** (Short Answer) Write the formulas for the lower and upper fences of the 1.5 × IQR rule.

Answer: Lower fence = Q1 − 1.5 × IQR. Upper fence = Q3 + 1.5 × IQR.

**19.** (Short Answer) On Titanic fares, the IQR rule flags 116 values but the |z| > 3 rule flags only 20. Why are z-scores less sensitive on a skewed column?

Answer: The z-score is built from the mean and std, which the outliers themselves inflate. On a skewed column the extreme values stretch the yardstick that measures them, so fewer of them look extreme. The IQR rule uses quartiles, which aren’t distorted.

**20.** (True/False) Any value flagged as an outlier should be removed before analysis.

Answer: False

**21.** (Short Answer) Name two things you can do with a real-but-extreme value instead of deleting it.

Answer: keep it and use robust statistics (median, IQR),  or report it separately, 

**22.** (Short Answer) Why can a value be an outlier within its group but not in the whole dataset (or the other way around)? 

Answer: Outlier status depends on the comparison group. A £100 fare is extreme for 3rd class but normal in 1st class. In the penguins, a value can be ordinary across the pooled data but unusual within its own species, because the pooled fences are wide.

---

## Section D — Comparing Groups

**23.** (Short Answer) More 3rd-class passengers survived than 2nd-class passengers, but 3rd class had the lower survival rate. How can both be true?

Answer: Counts depend on group size. 3rd class was much bigger, so it can have more survivors in total while a smaller share of its passengers survived. Compare rates, not counts.

**24.** (Code Tracing) What does this compute?
```python
titanic.groupby('Sex')['Survived'].mean()
```

Answer: The survival rate

**25.** (Multiple Choice) In `pd.crosstab(df['class'], df['Sex'], normalize='index')`, what adds up to 100%?
A) each row  B) each column  C) the whole table  D) nothing; it's counts

Answer: A

**26.** (Short Answer) What's the difference between what `pd.crosstab()` and `pivot_table()` compute?

Answer: crosstab() counts combinations of two categorical columns. pivot_table() computes any statistic of a third column for every combination of two others.

**27.** (Short Answer) Why should a group summary always include the group's size?

Answer:  A rate or mean from a tiny group is unreliable, and size tells the reader how much to trust it. It also shows whether a difference comes from a few rows.

**28.** (Short Answer) Cherbourg passengers survived at a higher rate than other ports. Explain how ticket class could be a **confounder** here.

Answer: About half of the Cherbourg passengers were 1st class, far more than at other ports. Class affects survival, and class also differs by port, so part of Cherbourg’s higher rate is really a class effect. Comparing within each class shrinks the port differences.

**29.** (Short Answer) What does `observed=True` do in a `groupby` on a categorical column?

Answer: It shows only the categories that actually have rows, so empty groups don’t appear in the result.

---

## Section E — Relationships and Correlation

**30.** (Short Answer) Why is covariance hard to interpret on its own, and how does correlation fix that?

Answer: Covariance depends on the units (dividing a column by 10 changes it by 10× with no change in the relationship). Correlation rescales it to always fall between −1 and 1 with no units, so the size is comparable.

**31.** (Multiple Choice) r = −0.85 means:
A) a weak negative linear relationship  B) a strong negative linear relationship  C) 85% of y is caused by x  D) no relationship

Answer: B

**32.** (Short Answer) Give two situations where Spearman is a better choice than Pearson.

Answer: Any two of: ordinal data, a curved but always rising or falling (monotonic) relationship, or data with outliers or heavy skew.

**33.** (True/False) If r = 0, the two columns have no relationship at all.

Answer: False

**34.** (Short Answer) Name three explanations for a correlation besides "A causes B."

Answer: Any three of: reverse causation (B causes A), a confounder (C causes both), or coincidence (especially from testing many pairs and reporting the strongest).

**35.** (Short Answer) What is Anscombe's quartet, and what lesson does it teach?

Answer: Four small datasets with the same means, standard deviations and correlation (r ≈ 0.82) but completely different shapes. The lesson is that summary statistics compress data and hide information, so always plot the data.

**36.** (Short Answer) In the penguins data, bill length and depth correlate at −0.24 overall but +0.39 to +0.65 within each species. What's this called?

Answer: Simpson's paradox. 

