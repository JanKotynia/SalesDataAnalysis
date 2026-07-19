# Amazon Products Sales Cleaning & Analysis (2025)

Exploratory data analysis of a 42,000-item Amazon Electronics sales dataset, focused on
process of cleaning this messy dataset, alongside with analysis of what actually drives product sales price, discounts, sponsorship,
coupons, or customer ratings.

- **Source:** Amazon Electronics Products Sales Dataset (Kaggle)
- **Size:** ~42,000 records, 17 raw features
- **Version used:** raw / uncleaned, chosen deliberately to demonstrate a full cleaning pipeline
- **Content:** product prices, discounts, coupons, ratings, review counts, sponsorship status,
delivery details, and best-seller flags

I was using:
** pandas · NumPy · seaborn · matplotlib · kagglehub **

🛠️ Data cleaning:
- Vectorized string processing: extracting numeric values from messy text fields
using .str.replace(), .str.extract(), and .str.match() with regular expressions
- Boolean masking with .loc: targeted conditional updates (e.g. filling
listed_price from discounted_price only for "No Discount" rows) without mutating
unrelated data.
- Custom transformation logic with .apply(): a dedicated function
(compute_coupon_profit) that parses mixed percentage/dollar coupon formats into a
single comparable numeric column.
- NumPy for numerical transforms: np.log(), np.where()
- Type coercion pipelines: converting cleaned string columns to float/bool in
a loop over a column list, rather than repeating the same code per column
- Deliberate missing-value strategy: different fillna() logic per column
depending on what "missing" actually means
- Datetime parsing: pd.to_datetime() with custom formats and errors="coerce"
to safely extract delivery dates from unstructured text
- Duplicate handling & data integrity checks: drop_duplicates() with before/after
row counts, isna().sum() audits at multiple pipeline stages
- Feature engineering: derived columns (discount_amount, coupon_profit,
last_month_revenue) computed from cleaned base columns for downstream analysis.


📈 Key findings:
- **Rating and sales volume:** a weak positive relationship, high-selling products
consistently have ratings above 4.5, but rating alone is a poor predictor of sales
volume overall.
- **Discounts:** no meaningful correlation between discount size and units sold.
- **Sponsorship:** sponsored listings sell slightly more on average, but the effect is
small.
- **Best sellers:** products flagged as "Best Seller" have marginally higher ratings
(~0.1 higher on average) than the rest of the catalog.
- **Coupons:** no visible relationship between coupon value and sales volume.
- **Rating distribution** is strongly left-skewed, most products cluster between 4.0
and 4.8, which limits rating's usefulness as a differentiator between products.

<img width="1561" height="873" alt="copies_corr" src="https://github.com/user-attachments/assets/3b04a780-7a6d-4604-9839-e19f4ff9dade" />
<img width="1473" height="872" alt="rating" src="https://github.com/user-attachments/assets/0cb8d4a4-da02-453f-8795-08aefbd39a64" />
<img width="2223" height="872" alt="num_copies_sold_monthly_sales" src="https://github.com/user-attachments/assets/f82ef71e-3864-4abe-944b-93900b2eae21" />

