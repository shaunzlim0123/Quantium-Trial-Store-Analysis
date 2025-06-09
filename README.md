# Quantium Analytics: Trial Store Analysis
## Retail Strategy and Analytics

<div align="center">
  <img src="img/quantium-logo.png" alt="Quantium Logo" width="900"/>
</div>


## Project Overview

This project implements a comprehensive retail trial analysis framework to evaluate the effectiveness of in-store trials across multiple locations. Using advanced control group methodology, we analyze chip sales performance during a strategic trial period (February-June 2019) to measure trial impact and provide scaling recommendations.

**Key Finding**: The trial demonstrates significant positive impact in 2 out of 3 stores, with measurable increases in both sales revenue and customer acquisition.

## Business Context

**Client**: Category Manager  
**Objective**: Evaluate trial effectiveness across multiple store locations and provide data-driven scaling recommendations  
**Key Focus**: Statistical validation of trial impact using control group methodology with 95% confidence intervals

## Dataset Description

### Transaction Data (`QVI_data.csv`)
- **Records**: Aggregated monthly store performance metrics
- **Time Period**: July 2018 - June 2019 (12 months total)
- **Key Fields**:
  - `STORE_NBR`: Store identifier
  - `YEARMONTH`: Time period (YYYYMM format)
  - `totSales`: Total monthly sales revenue
  - `nCustomers`: Monthly customer count
  - `nTxnPerCust`: Average transactions per customer
  - `nChipsPerTxn`: Average chips per transaction
  - `avgPricePerUnit`: Average price per unit

### Trial Configuration
- **Trial Stores**: 77, 86, 88 (client-selected locations)
- **Trial Period**: February 2019 - June 2019 (4 months)
- **Pre-trial Period**: July 2018 - January 2019 (8 months)
- **Control Selection**: Automated algorithm using correlation and magnitude distance

## Data Quality & Cleaning

### Issues Identified & Resolved
1. **Missing Data Handling**: Stores with incomplete observation periods excluded from control pool
2. **Time Series Alignment**: All stores normalized to consistent YEARMONTH format
3. **Outlier Detection**: Statistical validation of extreme performance variations
4. **Control Store Validation**: Pre-trial similarity assessment for all matches

### Final Dataset Statistics
- **Trial Stores**: 3 (Stores 77, 86, 88)
- **Control Store Pool**: 100+ eligible stores with complete data
- **Observation Period**: 12 months per store
- **Success Rate**: 67% (2 out of 3 stores showing significant positive impact)

## Key Features Engineered

### Derived Metrics
- **`scaling_factor`**: Baseline adjustment between trial and control stores
- **`percentage_difference`**: Trial vs. scaled control performance difference
- **`confidence_intervals`**: Statistical bounds for expected performance (±2 std dev)
- **`t_values`**: Statistical significance testing values

### Control Store Selection
- **Correlation Analysis**: Trend similarity using Pearson correlation coefficients
- **Magnitude Distance**: Absolute performance differences, normalized to 0-1 scale
- **Composite Scoring**: Combined metric (50% correlation + 50% magnitude similarity)

## Analysis Framework

The analysis employs a sophisticated matching process using correlation analysis and magnitude distance calculations to identify optimal control stores. The methodology establishes baseline compatibility using 8 months of historical data, then applies rigorous statistical testing during the trial period. Performance outside confidence bounds indicates statistically significant trial impact, validated using t-distribution testing with 95% confidence level.

### Trial Store 77 - High Performer ✅

**Pre-trial Validation**

Store 77 demonstrated excellent baseline compatibility with its selected control store (Store 233). The pre-trial analysis shows strong correlation and similar performance patterns across both sales and customer metrics during the 8-month validation period.

![Pre-trial Sales Comparison - Store 77](store77_img1.png)
![Pre-trial Customer Comparison - Store 77](store77_img2.png)

The pre-trial validation confirms that Store 233 provides a credible counterfactual scenario, with consistent parallel trends throughout the baseline period. This strong foundation enables confident interpretation of trial period results.

**Trial Impact Results**

![Sales Impact Analysis - Store 77](store77_img3.png)
![Customer Impact Analysis - Store 77](store77_img4.png)

Store 77 delivered exceptional performance during the trial period, with statistically significant increases in both sales revenue and customer acquisition. The analysis revealed highly significant results with March 2019 showing a t-value of 7.34 and April 2019 achieving a t-value of 12.48, both well above the 1.895 threshold for 95% confidence.

**Business Assessment**: Strong positive trial effect with sustained impact across multiple months. This store represents an ideal candidate for scaling the trial approach across similar market segments.

---

### Trial Store 86 - Mixed Results ⚠️

**Pre-trial Validation**

Store 86 showed reasonable correlation with its control store (Store 155), though with slightly higher baseline variation compared to other trial stores. The pre-trial assessment provides adequate foundation for impact measurement, with generally consistent trends.

![Pre-trial Sales Comparison - Store 86](store86_img1.png)
![Pre-trial Customer Comparison - Store 86](store86_img2.png)

**Trial Impact Results**

Store 86 presents an intriguing case of mixed results that requires careful interpretation. The sales impact analysis shows performance remaining within confidence intervals for the majority of trial months, indicating no statistically significant sales uplift. However, customer acquisition tells a different story.

![Sales Impact Analysis - Store 86](store86_img3.png)
![Customer Impact Analysis - Store 86](store86_img4.png)

The customer impact analysis reveals significant increases across all trial months, with performance consistently above the 95% confidence interval. This creates a paradox: more customers visiting the store but not generating proportional sales increases.

**Business Hypothesis**: The trial may have included promotional pricing or discounts that attracted customers but reduced average transaction values. This suggests different trial execution compared to successful stores or competitive responses affecting purchasing behavior.

**Recommended Actions**: Conduct pricing strategy review, analyze competitive environment, and investigate implementation differences to understand the disconnect between customer acquisition and sales performance.

---

### Trial Store 88 - High Performer ✅

**Pre-trial Validation**

Store 88 achieved the strongest control store match with Store 237, demonstrating excellent correlation and minimal deviation throughout the pre-trial period. This represents the highest quality baseline for counterfactual analysis.

![Pre-trial Sales Comparison - Store 88](store88_img1.png)
![Pre-trial Customer Comparison - Store 88](store88_img2.png)

**Trial Impact Results**

![Sales Impact Analysis - Store 88](store88_img3.png)
![Customer Impact Analysis - Store 88](store88_img4.png)

Store 88 demonstrated clear positive trial impact with performance outside confidence intervals for 2 out of 3 trial months. Both sales and customer metrics showed significant positive responses, indicating successful trial implementation with sustainable growth patterns rather than temporary spikes.

**Business Assessment**: Strong positive trial effect with consistent improvement across both revenue and customer acquisition metrics. This store, combined with Store 77, provides strong evidence for scaling the trial approach.

## Strategic Recommendations

### 1. Immediate Scaling (Stores 77 & 88)
- **Action**: Implement trial approach across 10-15 similar market segments
- **Timeline**: Phased rollout over 6-month period
- **Expected Impact**: 15-20% sales uplift based on trial results

### 2. Store 86 Investigation
- **Root Cause Analysis**: 30-day deep dive into implementation differences
- **Pricing Strategy Review**: Analyze promotional pricing vs. other stores
- **Customer Research**: Focus groups to understand behavior changes

### 3. Financial Impact Quantification
- **Conservative Estimate**: 15% sales increase across 50 stores
- **ROI Analysis**: 3-6 month payback period based on current performance
- **Success Metrics**: Monitor both sales revenue and customer acquisition

### 4. Long-term Strategy Development
- **Advanced Analytics**: Deploy real-time trial performance tracking
- **Best Practice Documentation**: Create standardized trial execution playbooks
- **Organizational Capability**: Upskill store managers on trial implementation

## Technical Implementation

### Tools & Libraries Used
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
from datetime import datetime
```

### Analysis Workflow
1. **Data Loading & Preparation**: Monthly aggregation and time series creation
2. **Control Store Selection**: Correlation and magnitude distance calculations
3. **Pre-trial Validation**: Visual and statistical baseline assessment
4. **Trial Impact Measurement**: Scaling and confidence interval construction
5. **Statistical Testing**: t-distribution significance testing
6. **Visualization Generation**: Automated figure creation and saving
7. **Results Interpretation**: Business recommendations and scaling guidance

## Files Structure
```
trial-store-analysis/
├── LICENSE
│
├── README.md                           # This comprehensive project documentation
│
├── data/
│   └── QVI_data.csv                   # Aggregated monthly store performance data
│
├── notebooks/
│   └── store_analysis.ipynb          # Main analysis notebook with complete workflow
│
│
└── requirements.txt                   # Python dependencies
```

## Usage Instructions

1. **Environment Setup**: Install dependencies from requirements.txt
2. **Data Preparation**: Ensure QVI_data.csv is in data/ folder
3. **Launch Analysis**: Open store_analysis.ipynb in Jupyter
4. **Execute Workflow**: Run cells sequentially for complete analysis
5. **Review Results**: Generated figures save automatically to figures/ folder
6. **Interpret Findings**: Use confidence interval plots for business decisions

### Key Analysis Parameters
```python
trial_stores = [77, 86, 88]           # Trial store numbers
trial_start_month = 201902            # February 2019
trial_end_month = 201905              # May 2019 (inclusive)
confidence_level = 0.95               # 95% statistical confidence
correlation_weight = 0.5              # Equal weighting for correlation vs magnitude
```

## Business Impact

This analysis provides the Category Manager with:
- **Statistical validation** of trial effectiveness with 95% confidence
- **Specific scaling recommendations** for successful store formats
- **Investigation framework** for underperforming trial locations
- **Visual decision tools** with confidence interval methodology
- **Financial projections** for scaling across store network

## Next Steps

1. **Scale Successful Implementation**: Rollout to 10-15 similar stores over 6 months
2. **Store 86 Deep Dive**: Investigate pricing strategy and competitive responses
3. **Real-time Monitoring**: Deploy automated trial performance tracking
4. **Advanced Segmentation**: Identify store characteristics predicting trial success
5. **Extended Trial Design**: Consider 6-month trials for seasonal effect analysis

---

*Analysis completed using control group methodology and statistical confidence interval testing for retail trial evaluation*
