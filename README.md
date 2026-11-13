# Walmart_Midterm_DS2002

#### Group Members: Emma Kee (hvh6ng), Kylie Sharp (dhq4mr), Raffaella Alpaca (bet3at), Miriam Ahmadd (zzx6jb)

### Project Background
In 2004, Walmart discovered that Strawberry Pop-Tart sales increased sevenfold before hurricanes, demonstrating how data analysis can uncover valuable business insights from fragmented data.

### Project Description
We have been hired as Walmart's data science consultants. A new hurricane is approaching Florida, and leadership needs answers fast. We have been given raw transaction data, store records, product catalogs, distribution center info, and an inventory database, but the data is messy (fragmented SKUs, incomplete data, and more) and needs to be cleaned before analysis. Moreover, we will use real weather data pulled from a free API to enrich our analysis. The goal is to make data-driven inventory and distribution recommendations ahead of the hurricane.

### Project Objectives
Our analysis aims to answer the following questions:
1) Sales trends: Which product categories experienced the greatest sales surge in the seven days before hurricane landfall compared to the previous baseline period?
2) SKU standardization: After consolidating all Pop-Tart SKU variants into a single product, what is the true daily sales volume? How does the fragmented, uncleaned view compare to the consolidated, cleaned view, and how might these differences affect business decisions?
3) Weather and sales relationships: How do weather indicators (wind speed, precipitation, and barometric pressure) correlate with daily sales volume across product categories? Is there a detectable lag between worsening weather conditions and increases in purchasing?
4) Store-level trends: Do all Florida store locations experience similar sales surges, or do stores closer to the predicted hurricane path experience earlier and larger increases? Are there any notable store-level outliers?
5) Inventory and data validation: The board games/entertainment category shows a +250% sales increase. Using the SQLite inventory and sales database, investigate whether this is a genuine demand signal or a data artifact (e.g., SKU miscoding, category lumping, inventory reporting lag). Based on the evidence, should Walmart increase board game inventory before future storms?

### How are we going to do this?
ETL (Extract, Transform, and Load) pipelines
- Extract: Retrieve raw transaction, store, product, distribution center, and inventory data, along with external weather data.
- Transform: Clean missing values, address duplicates, standardize SKUs and identifiers, and integrate weather data.
- Load: Combine the cleaned datasets into a unified, analysis-ready dataset for querying and analysis.

### What data are we working with?

| File | Format | Description | Approximate Size |
|------|--------|-------------|-----------------|
| `walmart_transactions.csv` | CSV | Point-of-sale transaction records across Florida stores (Sept 2024) | ~25,000 rows |
| `store_locations.csv` | CSV | Walmart store metadata (Florida locations) | ~14 rows |
| `product_catalog.csv` | CSV | Master product/SKU reference list | ~45 rows |
| `distribution_centers.csv` | CSV | Distribution center capacity and logistics | 5 rows |
| `inventory_and_sales.db` | SQLite | Database with `daily_sales_summary` and `inventory_levels` tables | ~7,900 rows total |

### Tools and Technologies
- Python: Primary programming language
- Pandas: Data cleaning, manipulation, and transformation
- NumPy: Numerical operations
- SQLite: Database storage and querying
- Matplotlib: Data visualization
- Requests: Retrieving weather data from an external API
- OS: File and directory management
- Time: Managing API request timing and delays
- GitHub: Version control and collaboration

### Repository Structure
```
Walmart_Midterm_DS2002/
│
├── data/
│   ├── distribution_centers.csv
│   ├── inventory_and_sales.db
│   ├── product_catalog.csv
│   ├── store_locations.csv
│   └── walmart_transactions.csv
│
├── notebooks/
│   ├── class content/
│       ├── 2026-10-19 — Midterm Kickoff and Team Formation - Lecture.ipynb
│       ├── 2026-10-21 — Weather API Join - Studio.ipynb
│       └── 2026-10-23 — Midterm Checkpoint - Lab.ipynb
│    ├── Walmart Midterm Notebook Draft.ipynb           # Draft Notebook
|    └── Walmart Midterm Notebook.ipynb                 # Final Consolidated Notebook
│
├── scratch/
│
├── .gitignore
├── CHARTER.md                                          # Project Goals and Expectations
├── DS2002_Midterm_Project_Brief.md                     # Midterm Project Brief
├── README.md                                           # Project Overview
└── Walmart Case.pdf                                    # Walmart Case Description
```

### How to Run the Project
1) Clone the GitHub repository: Run the following command to download the project repository

  ```bash
   git clone https://github.com/ekee7/walmart-hurricane-project.git
   ```

3) Open the project notebook: Navigate to the `notebooks` directory and open `Walmart Midterm Notebook.ipynb`.
4) Import the datasets: The notebook automatically imports the required datasets directly from GitHub.
5) Run the notebook: In Google Colab, select Runtime → Run all to execute the entire notebook sequentially.

**Disclaimer: The necessary code and dataset import steps are already included in the notebook. No additional code needs to be written.**

### Key Findings
- 

### Why is it useful? What is the impact?
Building a trustworthy data pipeline allows Walmart to combine fragmented datasets and uncover trends that would otherwise remain hidden. By making the data consistent and analysis-ready, Walmart can make more informed decisions about inventory management and supply chain operations.

The expected impact includes improved customer satisfaction through better product availability, increased supply chain efficiency through strategic stocking and fewer last-minute emergency shipments, and stronger financial performance through increased sales and protected profit margins.

### Data Limitations
- Historical sales data may not fully represent customer behavior during an actual hurricane.
- Missing values and inconsistencies in the original datasets may affect certain analyses.
- Recommendations are based on the available data and should be interpreted within these limitations.
- Weather conditions and hurricane forecasts can change.

### Reflection Questions
- 
