# Real House Price Index (RHPI) Analysis Dashboard

A comprehensive data analysis project that creates an interactive dashboard for analyzing UK house price trends adjusted for inflation, with baseline comparisons to savings accounts and S&P 500 returns.

## 🏠 Project Overview

This project analyzes UK House Price Index (HPI) data by adjusting it for inflation using the Consumer Price Index including Housing (CPIH) to create a Real House Price Index (RHPI). The analysis provides insights into whether house prices have truly grown faster than the general economy and compares property investment performance against alternative investments.

### Key Features

- **Inflation-Adjusted Analysis**: Converts nominal house prices to real prices using CPIH data
- **Multiple Base Years**: Analysis with 2005, 2015, and 2020 base years for different time perspectives
- **Property Type Breakdown**: Analysis for Detached, Semi-Detached, Terraced, and Flat properties
- **Investment Comparison**: Baseline comparisons with savings accounts and S&P 500 returns
- **Interactive Visualizations**: Time series charts and geographical heat maps
- **Regional Coverage**: All English regions and districts

## 📊 Dashboard Features
[View RHPI Dashboard](RHPI%20Dashboard.png)
**[View Interactive Dashboard on Tableau Public](https://public.tableau.com/app/profile/bilal.ahmed.little/viz/RealHousePriceIndexRHPIAnalysisDashboard/Dashboard1#1)**

The final Tableau dashboard includes:

1. **Interactive Time Series**: Compare RHPI trends across different areas with baseline investments
2. **Geographical Heat Map**: Visual representation of RHPI performance across UK regions
3. **Flexible Time Periods**: Toggle between Last 5, 10, and 20 years
4. **Property Type Analysis**: Drill down by specific property types
5. **Economic Context**: Key economic events highlighted (2008 Financial Crisis, COVID-19)

## 🛠️ Technical Stack

- **SQL/SQLite**: Data storage and complex queries
- **Tableau**: Advanced dashboard creation with multi-source data integration, calculated fields, and interactive filtering
- **Excel**: Minor data formatting tasks

## 📁 Project Structure

```
RHPI-Analysis/
│
├── data/
│   ├── UK-HPI-full-file-2025-03.csv
│   ├── Local_Authority_District_to_Region_Lookup.csv
│   ├── CPIH1.xlsx
│   ├── snp500.csv
│   ├── Dividends.csv
│   └── Bank_Rate_history.csv
│
├── notebooks/
│   └── RHPI.ipynb
│
├── output/
│   ├── housing_data_tableau_ready_FIXED.csv
│   ├── all_combined.csv
│   └── house_prices_1.db
│
├── dashboard/
│   └── RHPI_Dashboard.twbx
│
└── README.md
```

## Links to Data Sources


## 🔧 Development Process & Technical Challenges

### Tableau Dashboard Development

The interactive dashboard development presented several technical challenges, particularly around integrating multiple data sources with different structures:

**Dual-Axis Complexity**: Creating the time series with both RHPI and baseline data required extensive calculated field configuration. The challenge arose from needing to filter and display data from different tables (housing vs. baseline) on the same visualization while maintaining interactivity across all filters.

**Data Structure Lessons**: The initial data formatting created bottlenecks during visualization development. Combining housing data (with geographical dimensions) and baseline data (time-series only) in a single dataset led to complex filtering logic and longer development cycles than anticipated.

**Technical Solutions Implemented**:
- Custom calculated fields to handle null values across different data types
- Separate data source management with careful join strategies
- Parameter controls to toggle between different baseline comparisons

### Key Technical Learnings
- **Data Structure Planning**: Future projects will prioritize visualization requirements during the data preparation phase
- **Audience-Driven Design**: The importance of defining a single, clear target audience before beginning development
- **Tableau Proficiency**: Significant improvement in handling complex multi-source visualizations and calculated fields

## 🔄 Data Processing Pipeline

### 1. Data Loading and Cleaning
- Load UK HPI data from ONS
- Import LAD to Region lookup table
- Correct district code mismatches between datasets
- Join regional information to HPI data

### 2. HPI Rebasing
Create rebased HPI tables for three base years:
- **2005 Base**: 20-year perspective
- **2015 Base**: 10-year perspective  
- **2020 Base**: 5-year perspective

### 3. CPIH Processing
- Load Consumer Price Index including Housing data
- Rebase CPIH to match HPI base years
- Prepare for inflation adjustment calculations

### 4. RHPI Calculation
```sql
RHPI = (HPI / CPIH) * 100
```
This formula adjusts house prices for general inflation, showing real price changes.

### 5. Baseline Data Processing

#### Bank of England Interest Rates
- Process historical interest rate changes
- Calculate compound savings returns
- Adjust for inflation using CPIH

#### S&P 500 Analysis
- Incorporate dividend yields for total returns
- Calculate monthly compound returns
- Convert to GBP equivalent (inflation-adjusted)

### 6. Data Integration
- Union all datasets with consistent structure
- Create final analysis-ready dataset
- Generate Tableau-compatible output

## 📈 Key Insights

### Economic Context
- **Great Recession (2007-09)**: Major impact on house prices across all regions
- **COVID-19 (2020)**: Smaller impact compared to 2008 financial crisis
- **Regional Variations**: London significantly outperformed other regions; North East lagged

### Property Performance
- **Flats**: Generally underperformed other property types over 20-year period
- **Detached Properties**: Showed strongest long-term performance
- **Regional Divergence**: Significant performance gaps between regions

### Investment Comparison
- **2008 Crisis**: Created long-term drag on returns, making recent COVID dip appear smaller
- **Savings vs Property**: Property significantly outperformed savings accounts when adjusted for inflation
- **S&P 500**: Provided competitive returns, especially in recent years

## 📊 Data Sources

1. **UK House Price Index**: ONS official HPI data (March 2025)
2. **CPIH Data**: Consumer Price Index including Housing
3. **Regional Lookup**: LAD to Region mapping (December 2023)
4. **Bank Rate**: Bank of England historical interest rates
5. **S&P 500**: Historical price and dividend data
6. **Population Data**: For regional analysis context

## 🎯 Use Cases

### For Property Buyers
- Understand real house price trends in target areas
- Compare property investment against alternatives
- Identify optimal timing based on historical patterns

### For Investors
- Analyze property as an asset class
- Regional investment opportunity assessment
- Risk-adjusted return comparisons

### For Researchers
- Economic impact analysis on housing markets
- Regional development studies
- Inflation-adjusted market analysis

## 🔧 Setup Instructions

### Prerequisites
```bash
pip install pandas sqlite3 openpyxl
```

### Data Preparation
1. Download required datasets (links provided in notebook)
2. Place files in `/data/` directory
3. Ensure Excel files are in correct format

### Running the Analysis
1. Open `RHPI.ipynb` in Jupyter Notebook
2. Run all cells sequentially
3. Final output: `housing_data_tableau_ready_FIXED.csv`

### Dashboard Setup
1. Open Tableau
2. Import the final CSV file
3. Load the provided `.twbx` dashboard file
4. Refresh data connections if needed

## 📝 Technical Notes

### Data Quality Considerations
- **Missing Districts**: Isles of Scilly excluded (no HPI data)
- **Code Corrections**: Barnsley and Sheffield district codes corrected
- **Date Alignment**: All datasets normalized to first-of-month format

### Calculation Methods
- **Compound Returns**: Geometric mean for multi-period returns
- **Inflation Adjustment**: Division method (Index/CPIH)*100
- **Base Year Rebasing**: Proportional adjustment to selected base periods

### Performance Optimizations
- SQLite indexing for large dataset queries
- Efficient pandas operations for data transformations
- Memory-optimized data structures

## 🤔 Project Retrospective & Lessons Learned

### Strategic Design Decisions

**Target Audience Clarity**: This project revealed the critical importance of defining a single, specific target audience before beginning development. The analysis attempted to serve both property investors and potential homebuyers, leading to feature complexity that may not fully optimize for either use case.

**Resource Allocation**: Significant development time was invested in baseline comparisons (S&P 500, savings accounts) which provide limited value for homebuyers but are essential for investors. Similarly, the geographical analysis is crucial for homebuyers but less relevant for portfolio investors.

### Alternative Approaches Identified

**For Homebuyer-Focused Tool**:
- Integration of regional salary and cost-of-living data
- Combined affordability scoring system
- Mortgage affordability calculators
- Commute time and local amenity analysis

**For Investor-Focused Tool**:
- Rental yield analysis and rent-to-price ratios
- Transaction cost modeling
- Portfolio optimization features
- Tax implications calculator
- Detailed ROI comparisons with alternative investments

### Technical Lessons

**Data Architecture**: Future projects will prioritize end-use visualization requirements during the initial data modeling phase. The challenges encountered with dual-axis charts and multi-source filtering could have been minimized with better upfront planning.

**Development Efficiency**: Clear scope definition and audience targeting would have enabled deeper analytical insights rather than broader but shallower coverage across multiple use cases.

These learnings significantly informed the approach for subsequent data analysis projects, emphasizing the value of focused scope and audience-driven design decisions.


