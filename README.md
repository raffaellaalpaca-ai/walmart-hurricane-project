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
│   ├── Walmart Midterm Notebook Draft.ipynb           # Draft Notebook
|   └── Walmart Midterm Notebook.ipynb                 # Final Consolidated Notebook
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
1. Categories with the Highest Percent Increase:
Our analysis displays the top five categories by percent increase in the surge period. The surge period refers to the seven days before landfall. We use the seven days before that period as our baseline. We calculated landfall as 2024-09-26 using wind speed as the determining metric. We utilized wind speed as the proxy for landfall since it typically coincides with the storm's approach. The landfall day is not included in the time periods themselves, since it may skew the results. Each category showed an increase, but the five highest were breakfast foods (308.6%), emergency supplies (160.7%), electronics (135.7%), games and entertainment (113.6%), and alcoholic beverages (109.8%). In the Daily Net Unit Sales graph, we notice that there is a significant increase in emergency supplies after the start of the surge period. In addition, breakfast food also begins to rise after the start of the surge period. However, it is important to note the significant difference between the peaks of the top two categories after the start of the surge period. We notice a significant increase in emergency supplies; in addition, breakfast foods also begin to rise. Emergency supplies peak at approximately 1,500 units sold, compared to approximately 700 for breakfast foods. Although breakfast had the largest percent increase, the emergency supplies had more sales volume. We recommend that Walmart prioritize emergency supplies while also increasing the breakfast foods supplies when they anticipate future storms. 

2. Pop-Tart Data Fragmentation:
This section addresses the issue of data fragmentation in the Pop-Tart product. It appears under four different SKU codes, causing the data to inaccurately reflect its sales. The code builds a SKU map to combine "pop tart", "pop-tart", "pop_tart", and "poptart" into one item under the moniker "poptarts." Each of the four variants had relatively low individual sales, but together totaled 5,025 units.
The four variants rank among the lowest in revenue, despite ranking 16th through 19th in units sold. However, after consolidation, "poptarts" ranks highest in both revenue and units sold. The analysis demonstrates the importance of SKU standardization before ranking products. While each variant appears to be a relatively low performer on its own, together they generate approximately $17,500 in revenue. Without consolidation, Walmart may mistakenly classify these products as low performers and reduce their inventory. By addressing this fragmentation, Walmart can recognize the product's strong demand and prioritize keeping it in stock in anticipation of a storm.

3. Sales and Weather Correlation:
Our analysis shows that sales across all ten categories peak in the two-day window before landfall. The wind and rain corerlation coefficent is low. The wind speed correlation coefficient is 0.268, indicating a weak positive relationship between wind speed and daily sales. Similarly, the precipitation correlation coefficient is -0.365 and the pressure one -0.283, indicating a weak negative relationship between precipitation/pressure and daily sales. Despite the relatively weak correlations displayed in the scatterplots, the surge window before landfall remains evident. The latter may suggest that shoppers respond more to the anticipation and progression of the storm rather than the individual conditions on a given day. Additionally, the two-day purchasing surge suggests customer's typically stock up before the storm reaches its most severe condition.

5. Geographic Correlation to Sales:
This section analyzes the relationship between proximity to landfall and sales during the pre-storm periods. For each store, the code compares the average daily revenue in the surge window (7 days before landfall) and the baseline period (14 days before landfall), using Perry, Florida, as the landfall location. The bar chart is ordered from closest to furthest, from top to bottom. There does not appear to be a direct relationship between the distance from landfall and the magnitude of the sales surge. All stores show relatively similar increases in average daily revenue, ranging from 94.6% to 129%. The only notable outlier is fl-239, which experienced a 94.6% increase, approximately 22.38 percentage points below the average increase of 116.98%. These findings suggest that stores across Florida experience relatively consistent purchasing surges, regardless of proximity to landfall. Walmart should anticipate an increase in demand across all Florida locations. 

6. Signal vs. Artifact — The Board Games Investigation:
Our analysis suggests that the increase in Entertainment sales is a genuine sales signal, but the exact size of the increase is uncertain due to data-quality issues. We compared the SQLite daily sales summary with the cleaned transaction dataset. Using September 1–20 as the baseline and September 21–26 as the surge period, the SQL data showed a 160.26% increase in average daily revenue, while the transaction data showed a 167.60% increase. Both datasets showed similar trends, with sales peaking around September 24–25. However, we identified several possible data artifacts. Monopoly and playing cards appeared under multiple SKU identifiers, and the transaction SKU `BG-MONO` required a provisional mapping to `GAME-MONO` in the inventory database. Only 598 of 2,538 board-game-related transactions matched an exact inventory record using store, date, and SKU. We also found four Entertainment records with negative revenue in the SQL summary. These issues suggest that reporting differences and incomplete inventory coverage could affect our interpretation of sales. Our inventory analysis also showed some signs of low stock. For example, GAME-MONO was at or below its reorder point in 27.17% of its recorded inventory observations. However, we did not find any recorded zero-stock values for the four entertainment-related SKUs. This suggests that inventory availability may have been a concern, but we cannot confirm actual stockouts from these records alone. Walmart should consider a modest, targeted increase in board-game inventory before future hurricanes rather than a large increase based solely on the reported 250% surge. The consistent sales pattern across both datasets supports preparing for higher demand, but Walmart should first improve SKU standardization and inventory reporting. Additional historical sales and inventory data would help determine the appropriate stocking levels. Since the Entertainment category includes both Monopoly and playing cards, the overall category increase does not necessarily mean Monopoly sales increased by the same percentage.

### Why is it useful? What is the impact?
Building a trustworthy data pipeline allows Walmart to combine fragmented datasets and uncover trends that would otherwise remain hidden. By making the data consistent and analysis-ready, Walmart can make more informed decisions about inventory management and supply chain operations.

The expected impact includes improved customer satisfaction through better product availability, increased supply chain efficiency through strategic stocking and fewer last-minute emergency shipments, and stronger financial performance through increased sales and protected profit margins.

### Data Limitations
- Historical sales data may not fully represent customer behavior during an actual hurricane.
- Missing values and inconsistencies in the original datasets may affect certain analyses.
- Recommendations are based on the available data and should be interpreted within these limitations.
- Weather conditions and hurricane forecasts can change.

### Reflection Questions
- Question 1: One data quality issue we encountered was the inconsistent product naming within the datasets. For example, the same product could be "first aid kit" and "first-aid kit" or "pop-tarts strawberry" and "strawberry pop-tart". These variants are the same product. The naming conventions and formatting differences cause the products to be treated as separate items in the analysis. To address this discrepancy, we standardized the product names. This allows us to see that the variations are referring to the same item by grouping them. By cleaning the unstandardized values, we created a better representation of the product-level sales trends, as shown by the fragmented sales visualization compared with the consolidated sales visualization. Standardizing the product names makes it easier to recognize patterns that were unclear or would have been dispersed across multiple product labels if we did not clean the data. If we did not resolve this issue, the same product's sales could have been spread across multiple names. The latter could cause an individual product trend to look smaller or less consistent, thus causing our analysis to overlook a meaningful trend/pattern. By standardizing the product names, we improved data consistency and ensured the accuracy of our analysis.
  
- Question 2: In the walmart_transactions.csv file, there were originally 886 missing timestamp values. The original data type of the timestamp column was object. To make downstream analysis easier, we decided to convert the column into datetime objects. Initially, we used pd.to_datetime(df[column_name], errors='coerce'). However, errors='coerce' tells pandas to convert valid timestamp strings into datetime objects and convert both missing values and unparseable timestamp values into NaT. This last case is what caused our missing value count to increase from 884 to 23,028. This indicated that many timestamp values that were not originally missing could not be interpreted using pandas' default datetime parsing behavior. In other words, many of the original timestamp values may not be compatible with pandas' datetime parsing rules. To address this issue, we included the format='mixed' parameter. This allows pandas to infer the format of each timestamp individually, which is useful because our dataset contains multiple timestamp formats. After applying this approach, we were able to successfully parse the existing timestamp values while preserving the original missing values as NaT. Additionally, we decided to keep the missing timestamps rather than fill them with estimated or dummy values because we did not have enough information to determine what the original dates and times should have been. One alternative decision would have been to keep the original errors='coerce' implementation without specifying format='mixed'. However, this would have resulted in 23,028 missing timestamps out of 25,562 transactions, leaving only 2,534 transactions with usable timestamps. This would have significantly reduced the amount of data available for time-based analysis, potentially making our conclusions about transaction trends less reliable. Another alternative decision would have been to fill the missing timestamps with dummy or estimated values. Although this would have reduced the number of missing values, it could have introduced inaccurate information and distorted our analysis of transaction patterns over time. Ultimately, we decided that preserving missing values was better than introducing information that we could not verify.

- Question 3: I agree with the Walmart CDO that the biggest risk is the data pipeline rather than the model itself. When working on the Weather API portion of our project, I realized how much our results depend on having reliable and correctly matched data. One of the biggest challenges we encountered was when the Open-Meteo API became overloaded and returned a 503 error, preventing us from retrieving the weather data. We also had missing store coordinates and transaction timestamps, which meant that not every sales record could be matched with weather information. Another concern was that the original sales timestamps did not specify a timezone, so we had to document our assumption about using Florida local time. I think the most fragile part of our pipeline was integrating the weather data with the sales transactions because even a small issue with dates or store locations could affect our analysis. This experience taught us that checking data quality and validating joins are just as important as the analysis itself, since unreliable data can lead to misleading conclusions.

- Question 4: For Question 5, I tried to balance what our data showed with the risks Walmart could face by ordering too much inventory. Both our SQL database and transaction data showed an increase in Entertainment sales of about 160–168%, which suggested that demand was increasing. However, we also found issues with inconsistent SKU names, missing inventory matches, and differences in reported sales totals. Because of these limitations, I wouldn't recommend that Walmart significantly increase its board-game inventory based only on the reported 250% surge. Instead, I would recommend a smaller, targeted increase to avoid having too much unsold inventory after the storm. If we had more time or data, I would want to compare sales across multiple hurricane seasons and look at more complete inventory records. This would help us determine whether the increase happens consistently and make a more confident recommendation.

- Question 5: We divided the work into data cleaning, API calls, analytical questions/ visualizations, and each person completed a reflection question based on their assignment. If we had another week, we would look further into the data cleaning process to ensure each step was done correctly, as well as further into the analysis. By looking further into the analysis, we can ensure an understanding of the trends vs. what is noise. In addition, we could create more in-depth visualizations to better model the trends and to attempt to make them easier to understand for viewers with less context. For data cleaning and the API call, the members primarily used their Python knowledge and SQL (inventory & sales data). For the analytical questions and visuals, they used Python and their knowledge of data visualization.
