# Presentation outline — The "Sugar Trap" Market Gap Analysis

A plan for a short deck of about eleven slides, roughly two minutes. One idea per slide. Say the number
first, then show the chart.

Every figure comes from the notebook: `outputs/executive_summary.md`, `outputs/recommendation.txt` and the
tables named on each slide. Replace each *(figure)* with the value from your run.

---

### Slide 1 — Title
The Sugar Trap: where is the Blue Ocean in the snack aisle?
Emmanuel ASIFIWE · date · prepared for Helix CPG Partners

### Slide 2 — The question, and what the data can answer
The client wants a healthy snacking line and believes the aisle is full of sugar.
This data shows what shops **offer**, not what people **buy**. Everything that follows is a view of the
catalog.

### Slide 3 — Data you can trust
Open Food Facts, *(date)*, the first 500,000 rows, fingerprinted so the figures can be traced.
*(kept)* rows of *(read)* passed the cleaning checks. Every removed row is saved with the rule that removed
it: missing fields, impossible values, nutrients that contradict each other, repeated barcodes.

### Slide 4 — Categories you can trust
18 categories built from Open Food Facts tags, read by the last noun, so a chocolate biscuit is a biscuit.
Powders and supplements are kept out of the snack aisle.
Measured accuracy: *(accuracy)*% of *(count)* labels read by hand were correct.

### Slide 5 — The two limits
5 g of sugar or less is the European limit for "low in sugars". 15 g of protein or more is a practical bar.
Add one line: every result was worked out again under seven other settings.

### Slide 6 — The sugar trap
*Show the sugar-against-protein scatter plot, titled as a sample.*
*(all)*% of all products meet both limits. In the snack aisle, only *(snacks)*%.

### Slide 7 — Where the gap is, with the numbers behind it
*Show the category table from `category_summary.csv`.*
Name each category with its count: "*(category)*: *(k)* of *(n)* products qualify."

### Slide 8 — Which gap to work on first
*Show the white-space score bar chart.*
Score = category size × the share that does **not** qualify.
*(category)* comes first in *(k)* of *(n)* settings. Say plainly that the score favours large categories by
design, and give its rank when size is taken out.

### Slide 9 — The recommendation
Paste the sentence from `recommendation.txt`: the category, at least *(X)* g of protein, less than 5 g of
sugar per 100 g.
Where the target comes from: the middle value of the qualifying products that were read and confirmed to be
that kind of product. Show the before and after: *(all qualifying)* g against *(own kind)* g.

### Slide 10 — What to make it from
*Show the top three ingredient sources.*
Give the count and the group size, for example "*(source)* in *(k)* of *(n)* readable labels".
These are mentions on a label, not a measure of how much protein each one provides.

### Slide 11 — Limits, and the next step
A catalog is not a market. The entries are written by volunteers, from one copy of the export.
Next step: test demand with sales, search or survey data before developing anything.
Link to the dashboard. Thank you.

---

**For the two minute video**

Spend most of the time on slides 6 to 9: the gap, where it is, and what to build.
Say the denominator out loud — "*(k)* of *(n)* chocolate products" — because that is what makes the claim
believable.
Finish on the next step, not on the method.
