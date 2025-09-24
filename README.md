# Customer Segmentation Pipeline - IT2011 Group Assignment

## Project Overview
Data preprocessing pipeline for customer segmentation using RFM analysis on Online Retail II dataset with sequential data processing steps to prepare clean, scaled data for clustering algorithms.

## Team Members & Responsibilities

| Member | ID | Task | Preprocessing Technique | EDA Visualization | Output File |
|--------|-------|------|------------------------|-------------------|-------------|
| **Kavinsan** | IT24100269 | **De-duplication** | Remove exact duplicate rows using `drop_duplicates()` | Line chart of unique invoices per day (2009-2010 & 2010-2011) | `cleaned_dataset.xlsx` |
| **Layanga** | IT24100344 | **Missing Value Handling** | Remove rows with missing CustomerID for RFM analysis | Bar chart showing revenue share: With vs Without CustomerID | `IT24100344_missing.csv` |
| **Kulas** | IT24100323 | **Outlier Handling** | Cap extreme Quantity values using IQR method with Winsorization | Boxplot comparison: Before vs After outlier capping | `02_outlier_capped_quantity.csv` |
| **Kavindu** | IT24100257 | **RFM Feature Engineering** | Calculate R,F,M per customer (exclude returns for F&M) | Three histograms showing R, F, M distributions | `IT24100257_rfm_table.csv` |
| **Shahly** | IT24100322 | **Scaling & Normalization** | Apply StandardScaler to R,F,M features (mean=0, std=1) | Before/After scaling comparison for Monetary values | `05_rfm_scaled.csv` |
| **Pasan** | IT24100258 | **Customer Filtering** | Remove noise customers: F>1 AND M>0 (exclude one-time buyers) | Bar chart: Customers kept vs removed + Frequency histograms | `06_filtered_customers_enhanced.csv` |

## Technical Pipeline Flow

```
Raw Data (Excel) → De-duplication → Missing Values → Outlier Handling → RFM Engineering → Scaling → Customer Filtering → Final Clean Dataset
```

### Detailed Processing Steps:

1. **📊 Data Loading & De-duplication** (Kavinsan)
   - Load Online Retail II dataset from Excel sheets
   - Normalize column names (lowercase, underscores)
   - Remove exact duplicate rows
   - **EDA**: Daily unique invoice trends analysis

2. **🔍 Missing Value Analysis** (Layanga)
   - Identify records with missing CustomerID
   - Calculate revenue impact of missing data  
   - Filter dataset for RFM-ready records only
   - **EDA**: Revenue distribution analysis

3. **⚡ Outlier Management** (Kulas)
   - Calculate IQR bounds for Quantity column
   - Apply Winsorization capping to extreme values
   - Flag returns (negative quantities) separately
   - **EDA**: Distribution comparison visualization

4. **🎯 RFM Feature Creation** (Kavindu)
   - **Recency**: Days since last purchase from snapshot date
   - **Frequency**: Count of unique invoice dates (non-returns)
   - **Monetary**: Total spend amount (non-returns, clipped ≥0)
   - **EDA**: Individual RFM feature distributions

5. **⚖️ Feature Scaling** (Shahly)
   - Apply StandardScaler for equal feature importance in clustering
   - Transform R,F,M to mean=0, std=1 distribution
   - Maintain original + scaled versions
   - **EDA**: Scaling effect visualization

6. **🎯 Customer Quality Filtering** (Pasan)
   - Remove one-time buyers (Frequency = 1)
   - Remove zero-spend customers (Monetary = 0)
   - Keep only engaged, repeat customers
   - **EDA**: Filtering impact analysis

## Project Structure
```
├── README.md
├── requirements.txt
├── data/
│   └── online_retail_II.xlsx
├── notebooks/
│   ├── group_pipeline_full.ipynb          # Complete integrated pipeline
│   ├── IT24100269_De-duplication.ipynb    # Kavinsan's individual work
│   ├── IT24100344_missing_value_handling.ipynb # Layanga's individual work  
│   ├── IT24100323_outlier_handling.ipynb  # Kulas's individual work
│   ├── IT24100257_RFM.ipynb              # Kavindu's individual work
│   ├── IT24100322_Scaling.ipynb          # Shahly's individual work
│   └── IT24100258_Customer_Fitlering.ipynb # Pasan's individual work
└── results/
    ├── outputs/                           # Sequential pipeline data files
    │   ├── cleaned_dataset.xlsx           # After de-duplication
    │   ├── IT24100344_missing.csv         # After missing value handling
    │   ├── 02_outlier_capped_quantity.csv # After outlier handling
    │   ├── IT24100257_rfm_table.csv       # After RFM engineering
    │   ├── 05_rfm_scaled.csv              # After scaling
    │   └── 06_filtered_customers_enhanced.csv # Final clean dataset
    └── eda_visualization/                 # Individual member EDA plots
        ├── IT24100269_unique_invoices_*.png
        ├── IT24100344_revenueshares.png
        ├── boxplot_Quantity_*.png
        ├── IT24100257_rfm_histograms.png
        ├── IT24100322_shahly_scaling_effect.png
        └── IT24100258_Pasan_*.png
```

## How to Run

### Prerequisites
```bash
pip install -r requirements.txt
```

### Run Complete Pipeline
```bash
jupyter notebook notebooks/group_pipeline_full.ipynb
```

### Run Individual Components
Each team member's notebook can be run independently in sequence:
```bash
# Step by step execution
jupyter notebook notebooks/IT24100269_De-duplication.ipynb
jupyter notebook notebooks/IT24100344_missing_value_handling.ipynb  
jupyter notebook notebooks/IT24100323_outlier_handling.ipynb
jupyter notebook notebooks/IT24100257_RFM.ipynb
jupyter notebook notebooks/IT24100322_Scaling.ipynb
jupyter notebook notebooks/IT24100258_Customer_Fitlering.ipynb
```

## Key Technical Decisions

### **Why These Preprocessing Steps?**

1. **StandardScaler vs RobustScaler**: Chose StandardScaler for equal feature weight in clustering
2. **IQR Outlier Handling**: Preserves data while managing extreme values  
3. **Customer Filtering**: Removes noise to improve clustering quality
4. **Sequential Processing**: Each step builds on the previous, ensuring data consistency

### **Expected Final Output**
Clean dataset optimized for customer segmentation with:
- ✅ No duplicates or missing CustomerIDs
- ✅ Outlier-managed Quantity values  
- ✅ Properly engineered RFM features (R, F, M)
- ✅ Standardized features for clustering (R_scaled, F_scaled, M_scaled)
- ✅ High-engagement customers only (F>1, M>0)
- ✅ ~5,000+ quality customer records ready for K-means/clustering

---
**IT2011 - Artificial Intelligence and Machine Learning**  
**Sri Lanka Institute of Information Technology (SLIIT)**
