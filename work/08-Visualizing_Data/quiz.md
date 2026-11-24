# 📝 Quiz: 08 - Visualizing Data

36 questions covering object-oriented Matplotlib, plotting with pandas, Seaborn distributions, Seaborn relationships and categories, and choosing and designing charts. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Matplotlib, Object-Oriented

**1.** (Short Answer) In `fig, ax = plt.subplots()`, what's the difference between `fig` and `ax`?

Answer: fig shows the whole figure ax shows one chart

**2.** (Short Answer) Why does the object-oriented style scale better than `plt.title()`/`plt.xlabel()` calls when a figure has several charts?

Answer: the style makes it easier to not confuse charts

**3.** (Code Tracing) How many axes does this create, and how do you reach the bottom-right one?
```python
fig, axes = plt.subplots(2, 3)
```

Answer: axes[1, 2]

**4.** (Short Answer) What does `sharey=True` do, and why does it matter when comparing panels?

Answer: All panels share the same y-axis scale. Bar heights and positions can then be compared directly. Without it, each panel scales itself, so a small group can look as big as a large one.

**5.** (Short Answer) When is a log-scale axis a good idea? What value can't it show?

Answer: Use it for skewed data, where a long tail squeezes the crowded part into a few bars. Each step is a multiple (×10) instead of a fixed amount.

**6.** (Multiple Choice) Which formatter displays `0.25` on an axis as `25%`?
A) `StrMethodFormatter('{x:.0%}')`  B) `PercentFormatter(xmax=1)`  C) `PercentFormatter(xmax=100)`  D) `ax.set(percent=True)`

Answer: B

**7.** (Short Answer) Why should you call `fig.savefig()` before `plt.show()`, and why `plt.close(fig)` inside a loop?

Answer: In some environments plt.show() clears the figure, so saving afterward can give a blank file. In a loop, plt.close(fig) stops figures from piling up in memory.

**8.** (Short Answer) In `ax.annotate('Peak', xy=(5, 10), xytext=(7, 12), arrowprops=...)`, what do `xy` and `xytext` each mean?

Answer: xy is the data point being labeled (5, 10). xytext is where the text is placed (7, 12). Both are in data coordinates.

---

## Section B — Plotting with Pandas

**9.** (Short Answer) When pandas plots a DataFrame, what becomes the x-axis, and what becomes each line or set of bars?

Answer: The index becomes the x-axis (or the bar labels). Each column becomes one line or one set of bars.

**10.** (Code Tracing) What kind of chart does this draw, and what are the bar labels?
```python
titanic['Embarked'].value_counts().plot.barh()
```

Answer: A horizontal bar chart. 

**11.** (Short Answer) You plot a `pivot_table` with classes as the index and sexes as the columns. How do you switch the chart to group by sex instead?

Answer: Transpose the table with .T before plotting, so the sexes become the index.

**12.** (Short Answer) What does a 100% stacked bar chart show, and which `crosstab` argument produces the right table for it?

Answer: It shows the composition (share) within each group, and each bar totals 100%. Use pd.crosstab(..., normalize='index').

**13.** (Short Answer) What's the difference between wide and long data? Which does pandas `.plot` expect, and which does Seaborn expect?

Answer: Wide data has one column per series, with x-values in the index. Long (tidy) data has one row per observation, with columns that name things. Pandas .plot expects wide, and Seaborn expects long.

**14.** (Short Answer) Should you sort the bars of an ordinal category (like ticket class) by value? Why or why not?

Answer: No. Ordinal categories keep their natural order (1st, 2nd, 3rd), because the order carries meaning. Only nominal categories get sorted by value.

---

## Section C — Seaborn: Distributions

**15.** (Short Answer) What's the difference between an axes-level and a figure-level Seaborn function? Give one example of each.

Answer: Axes-level functions draw on one ax and accept ax=, e.g. histplot, boxplot. Figure-level functions create a whole figure with panels (col=, row=) and return a FacetGrid, e.g. displot, catplot, relplot.

**16.** (Short Answer) What does `hue='species'` do in `sns.histplot()`?

Answer: It splits the data by species and colors each group differently.

**17.** (Multiple Choice) Two groups have 500 and 50 rows. To compare the **shapes** of their distributions, use:
A) `stat='count'`  B) `multiple='stack'`  C) `stat='percent', common_norm=False`  D) `binwidth=1`

Answer: C

**18.** (Short Answer) Explain each part of a box plot: the box, the line inside it, the whiskers, and the dots.

Answer: The box spans Q1 to Q3 (the IQR). The line inside is the median. The whiskers reach the most extreme values inside the IQR fences (1.5×IQR). The dots are outliers beyond the fences.

**19.** (Short Answer) Name one thing a violin plot shows that a box plot hides, and one thing a strip plot shows that a violin hides.

Answer: A violin shows the full shape (e.g. a second peak), which a box hides. A strip plot shows every individual point, and so the sample size, which a violin hides.

**20.** (Short Answer) How do you read a group's median from an ECDF plot?

Answer: Find where the group's curve crosses y = 0.5. The x-value there is the median.

**21.** (True/False) A KDE curve always stays within the actual range of the data.

Answer: False

**22.** (Short Answer) Why does `showfliers=False` make sense when you draw a strip plot on top of a box plot?

Answer: The strip plot already draws every point, so the box plot's outlier dots would draw the same points twice.

---

## Section D — Seaborn: Relationships and Categories

**23.** (Short Answer) Name two ways to reduce overplotting in a scatter plot.

Answer: Any two of: transparency (alpha), a log scale, smaller markers, or splitting into panels.

**24.** (Short Answer) In the penguins data, one `regplot` line through all the points slopes down, but one line per species slopes up. What's this called, and what's the lesson for fitting trend lines?

Answer: Simpson's paradox.

**25.** (Short Answer) Why did the four Anscombe datasets get identical lines from `lmplot`?

Answer: Because the four datasets have the same summary statistics (means, standard deviations, correlation), and a fitted line is just another summary. It hides the shape of the data (a curve, an outlier, one influential point).

**26.** (Short Answer) What's the difference between `countplot` and `barplot`?

Answer: countplot counts the rows in each category. barplot computes a statistic of a numeric column (the mean by default) for each category, with an error bar.

**27.** (Multiple Choice) `sns.barplot(..., errorbar='sd')` draws error bars showing:
A) the 95% confidence interval  B) the standard error  C) one standard deviation of the individual values  D) the IQR

Answer: C

**28.** (Short Answer) What does Seaborn's default error bar on a `barplot` represent?

Answer: A 95% confidence interval of the mean, showing how precisely the group's average is estimated.

**29.** (Short Answer) What does a `pointplot` with crossing or diverging lines tell you?

Answer: The effect of one variable depends on the other (an interaction). Parallel lines would mean no interaction.

**30.** (Short Answer) Should a correlation heatmap use a diverging or a sequential color map? What about a heatmap of survival rates? Why?

Answer: A correlation heatmap uses a diverging map centered on 0, because 0 is a meaningful middle (negative vs. positive). Survival rates use a sequential map (light to dark), because they run from 0 to 1 with no meaningful middle.

---

## Section E — Choosing and Telling

**31.** (Short Answer) Why must bar charts start at zero, when line charts don't have to?

Answer: Bars encode value by length, so cutting off the bottom distorts the comparison. Lines encode position and slope, so a non-zero axis can be fine if it's labeled.

**32.** (Short Answer) Name the chart you'd choose for each: (a) the distribution of one numeric column, (b) the mix of categories within each group, (c) the relationship between two numeric columns.

Answer: (a) Histogram, KDE, or ECDF. (b) 100% stacked bar. (c) Scatter plot, with a trend line and colored by group.

**33.** (Short Answer) What's a palette dictionary, and why use one across a whole report?

Answer: A dictionary mapping each category to a color, built once and passed with palette=. The same category then has the same color in every chart, so readers don't have to re-learn the legend.

**34.** (Short Answer) Rewrite this descriptive title as a finding title: "Mean Body Mass by Species."

Answer: "Gentoo Penguins Are About 1,350 g Heavier Than the Other Two Species."

**35.** (True/False) Every bar in a bar chart should have its own distinct color.

Answer: False

**36.** (Short Answer) Give two reasons to look at a chart **and** the matching numbers, rather than just one of them.

Answer: 1. Charts show shape, patterns, and outliers that numbers hide.
        2. Numbers give exact values and are checkable evidence.

