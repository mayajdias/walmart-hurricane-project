# Walmart Hurricane Analytics — Team Wallyworld
**DS 2002 Data Science Systems · Midterm Project · Fall 2026**

Walmart's data science team discovered that Strawberry Pop-Tart sales surged before hurricanes. Acting as Walmart's data consultants, we cleaned messy point-of-sale, store, product, and inventory data, joined it with real weather data from a free API, and analyzed demand before Hurricane Helene's landfall in Florida (Sept 26, 2024) to answer five business questions and make a stocking recommendation.

## Team
| Member | GitHub | Role |
|---|---|---|
| Nate Carter | natecarter459 | Data cleaning + decision log |
| Jack Lenk | jacklenkk | Weather API + join, Q3 |
| Maya Dias | mayajdias | Analysis, Q1–Q2 |
| Alex Cho | alexcho2823-del | Q4–Q5, charts + presentation, README |

## How to run
1. Open `notebooks/team_notebook.ipynb` in Google Colab: [Open in Colab](https://colab.research.google.com/github/mayajdias/walmart-hurricane-project/blob/main/notebooks/team_notebook.ipynb)
2. Click **Runtime → Restart session and run all**.
3. The first code cell clones this repository so the data files in `data/` are available. No API key is needed.

The notebook runs top to bottom with no manual steps. If the weather API is unreachable, it falls back to a saved sample and prints which source was used.

## Repository structure
```
walmart-hurricane-project/
├── README.md
├── CHARTER.md                             team charter (roles, goals, how we work)
├── data/
│   ├── walmart_transactions.csv           ~25,000 messy POS records (Sept 2024)
│   ├── store_locations.csv                12 Florida stores
│   ├── product_catalog (1).csv            product/SKU reference
│   ├── distribution_centers.csv           5 distribution centers
│   └── inventory_and_sales.db             SQLite: daily_sales_summary + inventory_levels
└── notebooks/
    ├── team_notebook.ipynb                FINAL DELIVERABLE
    ├── walmart_transactions_cleaned.csv   cleaned transactions exported by the notebook
    ├── scratch/                           individual working notebooks
    └── (lab checkpoints)
```

## Notebook contents
1. **Data cleaning + decision log:** duplicates, SKU and category consolidation (45 raw SKUs → 20 products), price and timestamp fixes, store ID standardization, negative quantities, missing values
2. **Weather API + join:** Open-Meteo daily weather joined to sales by date (America/New_York timezone), with all 24,648 rows preserved
3. **Analytical questions**
   - Q1: Demand surge by category
   - Q2: Pop-Tarts SKU consolidation
   - Q3: Weather correlation and lag
   - Q4: Store-level geographic patterns
   - Q5: Board games — signal vs. artifact
4. **Reflection questions** (answers are at the end of the notebook)

## Key windows
- **Landfall:** Hurricane Helene, Sept 26, 2024 (Big Bend, near Perry FL)
- **Baseline:** Sept 1–18 · **Surge:** Sept 19–25 (the 7 days before landfall)

## Data and API sources
- Supplied data: DS 2002 course repository (`06-midterm-walmart`)
- Weather: [Open-Meteo Historical Weather API](https://open-meteo.com/), base URL `https://archive-api.open-meteo.com/v1/archive`
