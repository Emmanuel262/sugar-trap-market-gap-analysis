### Executive summary

*Author: Emmanuel ASIFIWE · Data: Open Food Facts export, last changed Sat, 07 Nov 2026 10:09:24 GMT; first 500,000 rows, read 2026-11-08, fingerprint 9b4c59b97ce5*

**The data.** 433,181 of 500,000 rows passed the cleaning rules, which check for missing fields,
impossible values, nutrients that contradict each other, and repeated barcodes. Every removed row is saved
with the rule that removed it. Products were sorted into 17 categories, 67%
from Open Food Facts tags and 11% from the product name, with 2,575
powders and supplements kept out of the snack aisle. 20.1% could not be placed.
The category labels have not been read by hand in this run. The food group recorded by Open Food Facts agrees with our category for 92% of the products that have one. That check is not fully independent, because the same field settles a few category clashes.

**What we found.** Using 5 g of sugar or less and 15 g of protein or more per 100 g, 15.2% of all
products qualify, most of them in Meat, Fish & Eggs; Yogurt & Dairy; Other / Uncategorised. In the snack aisle only 5.1% of
84,200 products do. The scarcest snack categories are Chocolate & Candy: 57 of 25,399 (0.2%); Cakes & Pastries: 110 of 17,034 (0.6%); Biscuits & Cookies: 81 of 14,708 (0.6%). Across seven different limit
settings the snack-aisle figure stays between 1.6% and 8.7%, so the shortage
is not an effect of where the lines were drawn.

**Recommendation.** Based on the data, the largest catalog white space is in Chocolate & Candy. The suggested product has at least 15 g of protein and less than 5 g of sugar per 100 g.

Evidence: Chocolate & Candy holds 25,399 products in the cleaned catalog, with a middle value of 50 g sugar and 5 g protein per 100 g. Only 57 of them (0.2%) have 5 g of sugar or less and 15 g of protein or more. That makes it the strongest catalog white-space candidate: it is first in 9 of 9 settings that keep the size part (these vary the limits and the category rules, and larger categories score higher by design); with size removed it ranks 1, behind Chocolate & Candy. Before scoring, 2,575 powders and supplements were moved out of the snack aisle. The protein target is the 15 g screening level set before the analysis, because the product format reading is not read yet, so no product is counted towards the target. The sugar figure is the European limit for a 'low in sugars' claim; the product target is set below it, while the counts above use 5 g or less. Limits of this evidence: product counts describe what is offered in Open Food Facts, not what people buy; the entries are written by volunteers; they come from the first 500,000 rows of one copy of the export (Sat, 07 Nov 2026 10:09:24 GMT), which is not a random sample of the market; categories are decided by rules; the category label reading is not loaded. Demand should be tested with sales, search or survey data before any product is developed.

**Where the protein comes from.** Among the qualifying Chocolate & Candy products that are the category's own
kind, 0 have a readable ingredient list, and the most mentioned sources are
none identified. Taking every qualifying product in the category, 39 have a
readable list and the most mentioned are Cocoa or cacao in 27 products (69.2% of readable lists), Milk protein or casein in 17 products (43.6% of readable lists), Soy in 17 products (43.6% of readable lists). The product formats have not been read by hand in this run. The two groups overlap.
A mention only shows the ingredient is on the label, not how much of the protein it provides
(the match examples are not loaded).
