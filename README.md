# Walmart Hurricane Analytics — Team Wallyworld

**DS2002 · Fall 2026 · Midterm**

## Team

| Name | GitHub | Role / main contributions |
|------|--------|---------------------------|
| Nate Carter | natecarter459-droid | Data cleaning + decision log |
| Jack Lenk | jacklenkk | Weather API + join, Q3, reflection #2 |
| Maya Dias | mayajdias | Analysis, Q1–Q2, slide deck |
| Alex Cho | alexcho2823-del | Q4–Q5, reflection #4, Q4/Q5 + recommendation slides, README |

## Summary

Acting as Walmart's data consultants, we cleaned messy point-of-sale, store, product, and inventory data, joined it with real weather data from the Open-Meteo API, and measured how Florida demand changed before Hurricane Helene's landfall (Sept 26, 2024). In the 7 days before landfall, unit sales ran **2.31x** the normal baseline, led by Breakfast and Emergency supplies; Strawberry Pop-Tarts were the biggest single mover once their four SKUs were combined. The surge was statewide rather than concentrated near the storm, buying peaked about two days ahead of the strongest winds, and the reported +250% board-game surge turned out to be real demand inflated by category lumping, closer to +150%.

## Data

| File | Source | Notes |
|------|--------|-------|
| `data/walmart_transactions.csv` | DS2002 course repo | ~25,000 POS records (Sept 2024); duplicates, mixed timestamps, fragmented SKUs, `$` prices, negative quantities |
| `data/store_locations.csv` | DS2002 course repo | 12 Florida stores; duplicate rows, inconsistent store IDs and state names, missing Tallahassee coordinates |
| `data/product_catalog (1).csv` | DS2002 course repo | Product/SKU reference; inconsistent names, categories, package sizes |
| `data/distribution_centers.csv` | DS2002 course repo | 5 distribution centers; text in numeric columns, one missing cost |
| `data/inventory_and_sales.db` | DS2002 course repo | SQLite: `daily_sales_summary` + `inventory_levels`; mixed date formats, negative revenue, unmapped SKUs |

External API used: **Open-Meteo Historical Weather API** — base URL: `https://archive-api.open-meteo.com/v1/archive` (daily precipitation, max wind speed, and sea-level pressure for Orlando, America/New_York timezone)

## How to run

1. Open `notebooks/team_notebook.ipynb` in Colab: [Open in Colab](https://colab.research.google.com/github/mayajdias/walmart-hurricane-project/blob/main/notebooks/team_notebook.ipynb)
2. Run all cells top to bottom (**Runtime → Restart session and run all**)
3. No login or API key is needed. The first code cell clones this repository so the `data/` files are available, and if the weather API is unreachable the notebook falls back to a saved sample and prints which source was used.

**Analysis windows:** landfall Sept 26, 2024 · baseline Sept 1–18 · surge Sept 19–25 (the 7 days before landfall)

## Key findings

- **Q1 Demand surge:** Daily units rose from 1,181 to 2,724 (**2.31x**) in the week before landfall. The top categories were Breakfast (+328%), Emergency (+164%), Electronics (+138%), Alcohol (+115%), and Entertainment (+114%).
- **Q2 Pop-Tarts:** Strawberry Pop-Tarts were split across **4 SKUs**. Separately, none stood out; combined, Pop-Tarts surged **4.3x** and became the top-surging product.
- **Q3 Weather:** Wind speed was the only weather indicator positively correlated with daily sales (r = 0.21–0.43). Sales correlated most strongly with wind speed **two days later** in every category (r ≈ 0.74–0.86), over 30 days of data.
- **Q4 Stores:** Every store surged **2.13x–2.43x** regardless of distance from landfall (r = 0.19, n = 12). Miami (farthest, highest, earliest) and Orlando (lowest) were the outliers.
- **Q5 Board games:** The +250% only appears using the two peak days and with playing cards lumped into "Entertainment." Board games alone rose about **+150%**, at all 12 stores, with inventory falling the same day sales jumped, so the demand is real but smaller than reported.

## Recommendation

Pre-position storm inventory at **every Florida store**, not only those near the forecast landfall, starting about 5–7 days out, since demand rose statewide and buying led the worst weather by about two days. Prioritize consolidated Pop-Tarts, emergency supplies, and water. For board games, stock about **2.5x** normal volume rather than the 3.5x the headline implied; overstock risk is low because they don't spoil. Before the next storm, fix the SKU mapping and separate board games from playing cards so dashboards report true demand.

## Reflection

All five reflection answers are in the **Reflection Questions** section at the end of `notebooks/team_notebook.ipynb`. Each team member contributed.
