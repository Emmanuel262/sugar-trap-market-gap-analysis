# What is in this folder

Two kinds of file live here, and the difference matters.

## Hand-written input — keep these

These hold human judgements that the notebook cannot reproduce. They are the only files here that must be
kept and committed by hand.

| File | What it holds |
|---|---|
| `category_audit_labeled.csv` | 180 products read by hand, each marked `Y` or `N` for whether its category is right. 154 of 180 were correct (85.6%). |
| `format_review_labeled.csv` | 60 qualifying products read by hand and marked `c` (the category's own kind), `b` (bar or bite), `s` (powder or supplement) or `o` (something else). |

The notebook matches these back to the analysis **on the barcode**, so they stay usable when a later run
samples a partly different set of products. It prints how many of the products it sampled carry an answer, so
partial coverage is visible rather than silent.

## Produced by the run — these are overwritten

Everything else in this folder is written by the notebook and is replaced the next time it runs. A full run
writes 23 files here.

> ⚠️ **This folder is incomplete: it holds a handful of files rather than the full set.** The ones here come
> from the run dated 7 November 2026, which is the run the slides and the executive summary in the top-level
> `README.md` are built from, so those three agree with each other. That run did not load the hand-written
> reviews, so it reports the category accuracy as not read and the protein target as the 15 g screening
> level.
>
> Running the notebook top to bottom — with the two labelled files above in place — fills the folder, reports
> the measured 85.6% category accuracy and derives the protein target from confirmed sweets. After that run,
> refresh the executive summary in the top-level `README.md` from the new `executive_summary.md` so the two
> stay in step.

The large ones — `all_clean_products.csv.gz`, `removed_rows.csv.gz`, `dashboard_products.csv` — are excluded
by `.gitignore`, because they are rebuilt from the source data rather than edited.
