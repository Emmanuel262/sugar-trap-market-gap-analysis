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

> ⚠️ **The generated files currently in this folder are from a superseded run and do not all match the
> current notebook.** `executive_summary.md` in particular was written before the hand-written reviews were
> wired up, so it reports the category accuracy as not read and the protein target as the 15 g screening
> level. Run the notebook top to bottom to replace them, then refresh the executive summary in the top-level
> `README.md` from the new `executive_summary.md`.

The large ones — `all_clean_products.csv.gz`, `removed_rows.csv.gz`, `dashboard_products.csv` — are excluded
by `.gitignore`, because they are rebuilt from the source data rather than edited.
