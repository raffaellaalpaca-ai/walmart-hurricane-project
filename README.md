# Walmart_Midterm_DS2002

#### Group Members: Emma Kee (hvh6ng), Kylie Sharp (dhq4mr), Raffaella Alpaca (bet3at), Miriam Ahmadd (zzx6jb)

### Project background
In 2004, Walmart discovered that Strawberry Pop-Tart sales increased sevenfold before hurricanes, demonstrating how data analysis can uncover valuable business insights from fragmented data.

### Project description
We have been hired as Walmart's data science consultants. A new hurricane is approaching Florida, and leadership needs answers fast. We have been given raw transaction data, store records, product catalogs, distribution center info, and an inventory database, but the data is messy (fragmented SKUs, incomplete data, and more) and needs to be cleaned before analysis. Moreover, we will use real weather data pulled from a free API to enrich our analysis. The goal is to make data-driven inventory and distribution recommendations.

### Project objectives


### How are we going to do this?
ETL (Extract, Transform, and Load) pipelines
- Extract: Raw input data.
- Transform: Remove duplicates, standardize SKU codes across regions, weather alerts were aligned with store-level sales data, and more.
- Load: Cleaned data is loaded into Walmart's enterprise warehouse, making it usable for querying and analysis.

### Why is it useful? What is the impact?
Building a trustworthy data pipeline allows Walmart to combine fragmented datasets and uncover trends that would otherwise remain hidden. By making the data consistent and analysis-ready, Walmart can make more informed decisions about inventory management and supply chain operations.

The impact is customer satisfaction (the products they wanted were in stock), supply chain efficiency (strategic stocking reduced last-minute emergency shipments), and financial gains (sales increased and margins were protected).

### Tools and technologies
- Python, Pandas, SQLite, APIs, GitHub

### What data are we working with?

| File | Format | Description | Approximate Size |
|------|--------|-------------|-----------------|
| `walmart_transactions.csv` | CSV | Point-of-sale transaction records across Florida stores (Sept 2024) | ~25,000 rows |
| `store_locations.csv` | CSV | Walmart store metadata (Florida locations) | ~14 rows |
| `product_catalog.csv` | CSV | Master product/SKU reference list | ~45 rows |
| `distribution_centers.csv` | CSV | Distribution center capacity and logistics | 5 rows |
| `inventory_and_sales.db` | SQLite | Database with `daily_sales_summary` and `inventory_levels` tables | ~7,900 rows total |
