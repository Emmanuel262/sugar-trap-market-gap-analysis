# The "Sugar Trap" Market Gap Analysis

**Author:** Emmanuel ASIFIWE · **Client:** Helix CPG Partners · **Data:** Open Food Facts

Where is the "Blue Ocean" in the snack aisle? In other words, which snack categories sell plenty of products
but almost none that are **low in sugar and high in protein**?

Open Food Facts is a catalog. It lists what shops and brands offer, not what people buy. So a gap found here
is a gap on the shelf, not proof that shoppers want the missing product. The result is therefore called a
**catalog white-space candidate**, and the recommendation says in the same paragraph where its evidence
stops.

---

## A. Executive summary

Of the first 500,000 rows of the Open Food Facts export, 433,181 survived cleaning and were sorted into 17
readable categories, seven of which form the snack aisle. Across the whole catalogue 15.2% of products are
low in sugar and high in protein (5 g or less and 15 g or more per 100 g), but in the snack aisle only 5.1%
of 84,200 products are — and almost all the healthy products sit in meat, fish, eggs and dairy rather than
in snacking. **Based on the data, the biggest market opportunity is in Chocolate & Candy, specifically
targeting products with 15 g of protein and less than 5 g of sugar per 100 g**: it is the largest snack shelf
at 25,399 listings, yet only 57 of them (0.2%) clear both limits, and it ranks first on the white-space score
in 9 of 9 settings that keep category size, and first again when size is removed. Among the qualifying
products that carry a readable ingredient list, the protein comes most often from cocoa (27 of 39 labels),
milk protein or casein (17) and soy (17). This is a gap on the shelf, not proven demand: Open Food Facts
records what brands offer, not what shoppers buy, so demand should be tested with sales or survey data before
R&D commits.

*The full summary, with provenance and every caveat, is in [`outputs/executive_summary.md`](outputs/executive_summary.md)
and in Section 8 of the notebook. These figures come from the export dated 7 November 2026 (slice fingerprint
`9b4c59b97ce5`); in that run the hand-written category and product-format reviews were not loaded, so the
protein target is the 15 g screening level rather than a value read off confirmed sweets. Re-running the
notebook with `outputs/category_audit_labeled.csv` and `outputs/format_review_labeled.csv` in place reports a
measured 85.6% category accuracy and derives the target from the 11 confirmed chocolate products.*

---

## B. Project links

| Deliverable | Link |
|---|---|
| Notebook (Google Colab) | https://colab.research.google.com/drive/1P6Q1VPalPjZKl4qBOt28y_1tgFjdaf7u?usp=sharing |
| Dashboard (Looker Studio) | https://datastudio.google.com/reporting/5e52052f-856d-4360-892b-6b8951080faf |
| Repository | https://github.com/Emmanuel262/sugar-trap-market-gap-analysis |
| Presentation | `The_Sugar_Trap_Presentation.pptx` in this repository |
| Notebook export | `sugar_trap_market_gap_analysis.html` in this repository |

> ⚠️ **Still to confirm before submitting:** open the Colab link in an Incognito window to check it is shared
> as "Anyone with the link can view" — the sharing setting cannot be verified from the link alone. The brief
> rejects "permission error" excuses.

---

## C. Technical explanation

### The data

Open Food Facts publishes one very large file that changes daily. The notebook reads the **first 500,000
rows** and only the columns it needs. Those rows are a convenient slice, not a random sample of the market,
and that limit is repeated wherever numbers are reported.

The first download records two separate things, so any figure can be traced later:

- **Which version of the source file was read** — the date the server last changed it, its ETag and its size.
- **Which rows were analysed** — a SHA-256 fingerprint of the slice itself.

A saved copy is reused only while its fingerprint still matches.

### Cleaning

Rows must have a product name, a sugar value and a protein value. Anything else may stay empty, and nothing
empty is turned into a zero, because "not written down" is not the same as "none".

Each row then passes through eight checks, and is counted against the first one it fails: the three required
fields; nutrients in grams between 0 and 100; energy between 0 and 900 kcal; saturated fat no more than total
fat; sugar no more than total carbohydrate; and the four main nutrients adding up to no more than 100 g. The
last three allow about 2 g in total, because labels round each value. Where a barcode repeats, the fuller row
is kept; rows with no barcode are kept and counted.

Every removed row is saved with the rule that removed it, and a sample of what each check caught is shown in
the notebook, so no genuine food is thrown away unnoticed.

`health_score` is protein minus sugar. A second score adds fiber, but stays empty when fiber is not reported,
because treating a missing value as zero would punish products that simply did not print it.

### Categories

Open Food Facts tags such as `en:chocolate-biscuits` are grouped into readable categories: sixteen built from
keyword rules, plus **Sports Nutrition & Supplements** for powders and shakes and **Other / Uncategorised**
for products no rule reaches, so eighteen labels are possible. How many actually appear is reported by the
run, because a label with no products in the slice is not shown. The **last noun**
of each tag decides the category, matched on whole words, so *nut* never matches *nutrition*. A few very broad
tags are skipped: `en:seeds` is the parent tag of rice, beans and lentils, and tags ending in
`-and-beverages` also appear on fresh fruit. When tags point at more than one category, the shape of the
product beats its flavour, so a chocolate biscuit is a biscuit. The product name is used only when no tag
matches, and parts of the name that are just the brand are skipped.

Two extra rules keep the snack aisle honest. Products whose name or tags describe a powder, a shake or a
supplement move to **Sports Nutrition & Supplements**, and bars move to **Protein & Cereal Bars**; bars are
checked first, because a protein bar carries supplement tags too. When a snack category clashes with the food
group Open Food Facts itself recorded — meat, fish, eggs or a cooked meal — the food group wins. Inside a
snack category, anything above 45 g of protein per 100 g is also treated as a powder, since no solid sweet
reaches that level; the number of products this moves is reported.

**Seven categories form the snack aisle** this project is about: bars, biscuits, cakes and pastries, chocolate
and candy, crisps and savoury snacks, nuts and seeds, and dried fruit. Ice cream is labelled but kept outside,
because it belongs to the freezer aisle.

The labels are checked three ways: the most common tags among the products left over; agreement with the food
group Open Food Facts recorded, which is a useful but not independent check, since that same field settles a
few clashes; and reading up to ten products from each category by hand and marking each one right or wrong.
The third check gives a measured accuracy rather than an assumed one. Because it reads a fixed number per
category rather than ten per thousand products, it is not weighted by how common each category is, and the
notebook says so.

Those hand-written answers are matched back to the analysis **on the barcode**, so a review stays usable when
a later run cleans or categorises slightly differently and therefore samples a partly different set of
products. Only products the current run actually sampled are counted, and the notebook prints how many of
them carry an answer, so partial coverage is visible rather than silent. Every descriptive field — category,
method, nutrients — is taken from the current run, never from the review file, so an out-of-date label can
never carry a stale category into the results.

### Sugar against protein

A product counts as low sugar and high protein at **5 g of sugar or less** and **15 g of protein or more** per
100 g. The sugar figure is the European limit for calling a solid food "low in sugars". There is no legal
figure for protein per 100 g, so 15 g is used as a practical bar that ordinary sweets do not reach but nuts
and protein bars do.

Because 15 g is a judgement, every result is worked out again under seven other settings, including the
European rule where at least 20% of a product's energy must come from protein. All percentages come from the
full cleaned table; the scatter plot draws a sample so the points stay readable, and its title says so.

### Candidate's Choice: scoring the gap

Each snack category gets a score:

```
white space = (products in category / products in the largest category) x (1 - qualifying share)
```

This rises with the number of listings in a category that have **no** low-sugar, high-protein version. A large
category is an established shelf that many brands already supply; a small qualifying share means the healthy
corner is still empty. Together they point at a large, visible gap in the catalog.

The score contains no sales, prices or shopper preferences. It also favours large categories by design,
because it counts listings. So a category that stays top across the settings is robust to those settings, not
independent of its own size, and the notebook reports the ranking with size removed separately.

### The recommendation

A qualifying product only says something about a workable recipe if it really is the kind of product the
category is named after. Among products labelled chocolate or candy there are protein bars, powders, and a
few items that are not sweets at all. Each qualifying product in the chosen category is therefore read and
marked as one of four kinds: the category's own kind, a bar or bite, a powder or supplement, or something
else. The protein target is the middle value of the first group only, and the notebook reports how many
products were read and how many of them are the category's own kind.

A product with no hand-written answer is counted as **not read**, not as "something else", so an unread
product can never be mistaken for evidence that the category's own kind is scarce. If fewer than ten
qualifying products are confirmed to be the category's own kind, the target stays at the 15 g screening
level rather than resting on too few products, and the recommendation says which of the two it is using.

### Bonus: where the protein comes from

The top three protein sources are reported twice for the chosen category: once for the category's own kind of
product, and once for every qualifying product in it. Each group reports how many products it holds and how
many have a readable ingredient list. Matching reads the ingredient text first and stops before the "may
contain" part, so allergy warnings are not counted. Whole-word matching keeps *pea protein* apart from
*peanut*, and oils, flavourings and lecithins are removed first, since they carry almost no protein. A mention
only shows the ingredient is on the label, not how much of the protein it provides.

### What this analysis cannot show

Sales or demand. How accurate the nutrition figures are, beyond what volunteers typed in. The market outside
the first 500,000 rows of one copy of the export. Categories come from rules, and their accuracy is measured
by the hand check rather than assumed.

---

## Running the notebook

Open `sugar_trap_market_gap_analysis.ipynb` in Google Colab and choose **Runtime ▸ Run all**. The first run
downloads the data slice and saves a copy, so later runs start quickly.

For the hand-written reviews to be counted, upload `outputs/category_audit_labeled.csv` and
`outputs/format_review_labeled.csv` into the `outputs/` folder of the Colab session before running. Without
them the analysis still completes, but the category accuracy is reported as not read and the protein target
falls back to the 15 g screening level.

To run it locally instead, `pip install -r requirements.txt` first. The notebook is written for pandas 2.x;
pandas 3.0 changes enough CSV and groupby behaviour to be worth avoiding. The HTML export is produced with:

```
jupyter nbconvert --to html --execute sugar_trap_market_gap_analysis.ipynb
```

The last cell writes two archives:

- **`sugar_trap_dashboard_data.zip`** — the three tables the dashboard reads: `dashboard_products.csv` (a
  50,000 product sample, for the scatter plot), `category_summary.csv` (every category, from the full data)
  and `overall_summary.csv` (one row of headline figures, from the full data).
- **`sugar_trap_evidence.zip`** — the working behind the numbers: the cleaning audit, the removed rows, the
  category checks, the sensitivity tables, the hand-checked review files, the recommendation and the summary.

The dashboard is built from the first archive by following `Looker_Studio_Dashboard_Build_Guide.pdf`.

## Files in this folder

```
sugar_trap_market_gap_analysis.ipynb     the analysis, run from top to bottom
sugar_trap_market_gap_analysis.html      an export of the notebook after it has been run  (TO BE ADDED)
Looker_Studio_Dashboard_Build_Guide.pdf  how to build the dashboard
The_Sugar_Trap_Presentation.pptx         the slides, eleven of them, with speaker notes
PRESENTATION_OUTLINE.md                  the slide plan the deck was built from
outputs/                                 the tables and hand-checked files behind the numbers
requirements.txt                          the packages a local run needs
.gitignore                                keeps the data and the rebuilt tables out of the repository
README.md                                this file
```

The HTML export is marked **TO BE ADDED** because it is produced by the run, not written by hand. The brief
requires it, so export it after the run finishes and commit it.

Large files are not kept in the repository: the downloaded slice, the full product table and the two archives
are all rebuilt by running the notebook.
