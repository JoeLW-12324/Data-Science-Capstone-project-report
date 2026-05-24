# Data Science Capstone Project Report

## SpaceX Launch Success Prediction

---

## Table of Contents

1.1 - GitHub URL  
1.2 - Presentation Slides  
1.3 - Executive Summary  
1.4 - Introduction  
1.5 - Data Collection (SpaceX API)  
1.6 - Data Collection (Web Scraping)  
1.7 - Data Wrangling Methodology  
1.8 - EDA with Data Visualization  
1.9 - EDA with SQL  
1.10 - Interactive Visual Analytics  
1.11 - EDA Visualization Results  
1.12 - EDA with SQL Results  
1.13 - Folium Maps Analysis  
1.14 - Plotly Dash Analytics  
1.15 - Predictive Analysis Results  

---

## 1.1 - GitHub Repository URL

**Repository:** https://github.com/JoeLW-12324/Data-Science-Capstone-project-report

All project notebooks and code are maintained in this GitHub repository for version control and transparency.

---

## 1.2 - Presentation Slides in PDF Format

All presentation materials have been compiled into PDF format for easy distribution and viewing across all platforms.

**Slides Include:**
- Executive Summary
- Data Collection & Methodology
- Analysis Results
- Predictive Models
- Key Findings & Recommendations

---

## 1.3 - Executive Summary

### Project Overview
This capstone project analyzes SpaceX launch data to predict launch success rates using machine learning. The comprehensive analysis includes data collection, cleaning, exploratory analysis, and predictive modeling.

### Methods Used
- **Data Collection:** SpaceX API REST endpoints and web scraping
- **Data Processing:** Python pandas for cleaning and wrangling
- **Analysis Tools:** SQL queries, Python visualization libraries
- **Machine Learning:** Multiple algorithms for classification

### Key Results
- Successfully collected and processed [NUMBER] launch records
- Identified key factors affecting launch success
- Built multiple predictive models with [ACCURACY]% accuracy
- Generated actionable insights for mission planning

---

## 1.4 - Introduction

### Background
SpaceX has revolutionized the commercial space industry with reusable rocket technology. Understanding the factors that influence launch success is crucial for:
- Mission planning and risk assessment
- Cost estimation and resource allocation
- Continuous improvement of launch procedures

### Problem Statement
**Main Question:** Can we accurately predict SpaceX launch success based on available features?

**Sub-questions:**
- What are the most important factors affecting launch outcomes?
- How do different rocket types perform?
- Is there a geographic advantage to certain launch sites?
- What role does payload mass play in success rates?

### Project Objectives
1. Collect comprehensive SpaceX launch data from multiple sources
2. Perform thorough exploratory data analysis
3. Identify and quantify key success factors
4. Develop and evaluate multiple predictive models
5. Provide actionable insights and recommendations

---

## 1.5 - Data Collection: SpaceX API

### Data Source
**SpaceX Public REST API:** https://api.spacexdata.com/v4/

### API Endpoints Utilized

| Endpoint | Purpose | Data Retrieved |
|----------|---------|-----------------|
| `/launches` | Launch data | [Add details] |
| `/rockets` | Rocket specifications | [Add details] |
| `/launchpads` | Launch site information | [Add details] |
| `/payloads` | Payload data | [Add details] |
| `/landpads` | Landing pad details | [Add details] |

### Collection Process
- Implemented API calls using Python requests library
- Flattened JSON responses into structured DataFrames
- Applied rate limiting to respect API guidelines
- Validated data completeness and consistency

### Data Volume
- **Total Records:** [NUMBER]
- **Date Range:** [START DATE] to [END DATE]
- **Features Collected:** [NUMBER]

### Notebook Reference
📓 See: `jupyter-labs-spacex-data-collection-api.ipynb`

---

## 1.6 - Data Collection: Web Scraping

### Web Scraping Methodology
Web scraping was implemented to supplement API data with additional information not available through REST endpoints.

### Sources Scraped
- Wikipedia SpaceX launch records
- Industry reports and archives
- [Additional sources if applicable]

### Scraping Process
1. Identified target websites with relevant launch information
2. Used BeautifulSoup and Selenium for parsing
3. Extracted structured data (launch dates, outcomes, payloads)
4. Cross-validated with API data to ensure consistency

### Data Validation
- Compared scrapped data with API records
- Resolved discrepancies through manual verification
- Ensured data quality and accuracy

### Notebook Reference
📓 See: `jupyter-labs-spacex-data-collection-api.ipynb`

---

## 1.7 - Data Wrangling Methodology

### Data Cleaning Process

#### Missing Values
- Identified columns with missing data
- Strategy: [Describe imputation or removal approach]
- Result: [Percentage of data retained]

#### Data Type Conversion
- Converted date strings to datetime objects
- Standardized numeric fields
- Encoded categorical variables

#### Duplicate Removal
- Identified and removed exact duplicates
- Handled near-duplicates with fuzzy matching
- Final dataset size: [NUMBER] records

#### Outlier Detection
- Applied statistical methods (IQR, Z-score)
- Investigated outliers for legitimacy
- Decision: [Keep/Remove outliers and reasoning]

#### Feature Engineering
New features created:
- `Days_Since_Program_Start` - Temporal progression
- `Payload_to_Rocket_Ratio` - Physical characteristic
- `Launch_Site_Experience` - Accumulated launches
- [Additional engineered features]

### Data Quality Metrics
- **Completeness:** [PERCENTAGE]%
- **Consistency:** [PERCENTAGE]%
- **Validity:** [PERCENTAGE]%

### Notebook Reference
📓 See: `labs-jupyter-spacex-Data wrangling.ipynb`

---

## 1.8 - EDA with Data Visualization

### Visualization Techniques Employed

#### Scatter Plots
- Variables analyzed: [List pairs]
- Purpose: Identify relationships and correlations
- Key observation: [Main finding]

#### Bar Charts
- Categories analyzed: [List categories]
- Metrics displayed: [Count, percentage, average, etc.]
- Key observation: [Main finding]

#### Time Series Analysis
- Yearly trends in launch frequency
- Success rate evolution over time
- Technology progression visualization

#### Distribution Plots
- Payload mass distribution
- Orbital velocity distributions
- Launch cost analysis

#### Correlation Analysis
- Heatmap of feature correlations
- Identified multicollinearity issues
- Strong correlations: [List top correlations]

### Visualization Libraries
- Matplotlib for static plots
- Seaborn for statistical visualizations
- Plotly for interactive charts

### Key Insights from Visualizations
1. [Finding 1 from scatter plots]
2. [Finding 2 from bar charts]
3. [Finding 3 from time series]
4. [Finding 4 from distributions]

### Notebook Reference
📓 See: `edadataviz.ipynb`

---

## 1.9 - EDA with SQL

### SQL Database Setup
- Database: SQLite
- Tables created from cleaned CSV files
- Relationships defined between tables

### SQL Queries Performed

#### Query 1: Launch Success Rate Analysis
```sql
SELECT launch_site, COUNT(*) as total_launches, 
       SUM(CASE WHEN outcome = 'Success' THEN 1 ELSE 0 END) as successes,
       ROUND(100.0 * SUM(CASE WHEN outcome = 'Success' THEN 1 ELSE 0 END) / COUNT(*), 2) as success_rate
FROM launches
GROUP BY launch_site
ORDER BY success_rate DESC;
```

#### Query 2: Payload Mass Analysis
```sql
SELECT orbit, AVG(payload_mass) as avg_mass, COUNT(*) as count,
       SUM(CASE WHEN outcome = 'Success' THEN 1 ELSE 0 END) as successes
FROM launches
WHERE payload_mass IS NOT NULL
GROUP BY orbit;
```

#### Query 3: Rocket Performance
```sql
SELECT rocket_id, rocket_name, COUNT(*) as launches,
       SUM(CASE WHEN outcome = 'Success' THEN 1 ELSE 0 END) as successes,
       ROUND(100.0 * SUM(CASE WHEN outcome = 'Success' THEN 1 ELSE 0 END) / COUNT(*), 2) as success_rate
FROM launches
GROUP BY rocket_id, rocket_name;
```

#### Query 4: Temporal Trends
```sql
SELECT YEAR(launch_date) as year, COUNT(*) as launches,
       SUM(CASE WHEN outcome = 'Success' THEN 1 ELSE 0 END) as successes
FROM launches
GROUP BY YEAR(launch_date)
ORDER BY year;
```

### Key SQL Findings
- Launch success rate by site: [RESULTS]
- Best performing payload type: [RESULT]
- Rocket performance rankings: [TOP 3]
- Time-based success trends: [RESULTS]

### Notebook Reference
📓 See: `jupyter-labs-eda-sql-coursera_sqllite.ipynb`

---

## 1.10 - Interactive Visual Analytics

### Folium Maps
**Purpose:** Geographic visualization of SpaceX launch sites

**Features Implemented:**
- Interactive map with launch site markers
- Popup information displaying site details
- Color coding for success rates
- Clustering of launch attempts
- [Additional features]

**Geographic Insights:**
- Launch site distribution across regions
- Proximity analysis of multiple sites
- Climate and geographic advantages
- Accessibility factors

### Plotly Dash Application
**Purpose:** Interactive dashboard for real-time data exploration

**Dashboard Components:**
1. **Dropdown Filters** - Select by launch site, rocket type, payload
2. **Success Pie Chart** - Outcome distribution
3. **Scatter Plots** - Payload vs outcome relationship
4. **Time Series** - Launch frequency and success trends
5. **Statistics Panel** - Key metrics and KPIs

**User Interactions:**
- Dynamic filtering across all visualizations
- Hover tooltips for detailed information
- Zoom and pan capabilities
- Export functionality

### Notebook Reference
📓 See: `lab_jupyter_launch_site_location.ipynb`

---

## 1.11 - Complete EDA Visualization Results

### Scatter Plot Analysis
**Scatter Plot 1: Payload Mass vs Launch Success**
- Finding: [Your key finding]
- Implication: [Business implication]

**Scatter Plot 2: Rocket Age vs Success Rate**
- Finding: [Your key finding]
- Implication: [Business implication]

**Scatter Plot 3: [Additional scatter plot]**
- Finding: [Your key finding]

### Bar Chart Analysis
**Bar Chart 1: Success Rate by Launch Site**
- Top site: [SITE] with [PERCENTAGE]% success rate
- Observations: [Pattern observed]

**Bar Chart 2: Launch Frequency by Rocket Type**
- Most used rocket: [ROCKET]
- Launch count: [NUMBER]

**Bar Chart 3: Success Rate Over Years**
- Trend: [Describe improvement or decline]
- Notable year: [YEAR] with [FINDING]

### Yearly Trends Analysis
- **2010-2015:** [Trend description]
- **2016-2020:** [Trend description]
- **2021-Present:** [Trend description]

### Correlation Findings
- Strongest positive correlation: [FEATURE1] & [FEATURE2] (r = [VALUE])
- Strongest negative correlation: [FEATURE1] & [FEATURE2] (r = [VALUE])
- Moderate correlations: [List]

### Notebook Reference
📓 See: `edadataviz.ipynb`

---

## 1.12 - Complete EDA with SQL Results

### Launch Site Analysis Results
| Site | Total Launches | Successes | Success Rate | First Launch |
|------|---|---|---|---|
| [Site 1] | [#] | [#] | [%] | [DATE] |
| [Site 2] | [#] | [#] | [%] | [DATE] |
| [Site 3] | [#] | [#] | [%] | [DATE] |

### Payload Analysis Results
| Payload Type | Avg Mass (kg) | Count | Successes | Success Rate |
|---|---|---|---|---|
| [Type 1] | [#] | [#] | [#] | [%] |
| [Type 2] | [#] | [#] | [#] | [%] |
| [Type 3] | [#] | [#] | [#] | [%] |

### Rocket Performance Rankings
1. **[Rocket A]** - [NUMBER] launches, [PERCENTAGE]% success rate
2. **[Rocket B]** - [NUMBER] launches, [PERCENTAGE]% success rate
3. **[Rocket C]** - [NUMBER] launches, [PERCENTAGE]% success rate

### Temporal Analysis Results
**Overall Success Rate:** [PERCENTAGE]%

**Success Rate Progression:**
- 2010-2015: [PERCENTAGE]%
- 2016-2018: [PERCENTAGE]%
- 2019-2021: [PERCENTAGE]%
- 2022+: [PERCENTAGE]%

### Key Insights from SQL Analysis
1. [Insight 1]
2. [Insight 2]
3. [Insight 3]
4. [Insight 4]
5. [Insight 5]

### Notebook Reference
📓 See: `jupyter-labs-eda-sql-coursera_sqllite.ipynb`

---

## 1.13 - Folium Maps with Launch Site Markers, Launch Records, and Proximity Analysis

### Geographic Visualization Overview
Interactive maps created showing SpaceX launch sites globally with detailed information and analysis.

### Launch Site Markers
Each marker displays:
- **Site Name and Location** (Latitude, Longitude)
- **Launch Count** - Total launches from this site
- **Success Rate** - Percentage of successful launches
- **Active Status** - Currently operational or inactive
- **Orbit Types** - Types of orbits launched from site

### Launch Records
- **Clickable Info Windows** showing:
  - Historic launches from each site
  - Recent launch information
  - Site status and capabilities
  - Contact and facility details

### Proximity Analysis
**Analysis Results:**
- Closest sites: [SITE 1] and [SITE 2] - [DISTANCE] km apart
- Isolated site: [SITE] - [DISTANCE] km from nearest
- Clustered region: [REGION] with [NUMBER] sites

**Implications:**
- Logistics and resource sharing between proximate sites
- Backup launch capabilities in regional clusters
- Geographic risk distribution

### Map Features
- **Zoom Levels:** Detailed view at all scales
- **Popup Information:** Click markers for site details
- **Clustering:** Automatic clustering at lower zoom levels
- **Basemap Options:** Multiple map styles available

### Findings
1. Geographic concentration of launches in coastal areas
2. [Additional finding from proximity analysis]
3. [Additional finding from marker distribution]

### Notebook Reference
📓 See: `lab_jupyter_launch_site_location.ipynb`

---

## 1.14 - Plotly Dash Application with Success Pie Charts and Payload vs Launch Outcome Scatter Plots

### Dashboard Overview
Interactive web application built with Plotly Dash for comprehensive data exploration.

### Dashboard Components

#### Component 1: Success Outcome Pie Chart
- **Visual:** Pie chart showing success vs. failure breakdown
- **Data:** [PERCENTAGE]% Success, [PERCENTAGE]% Failure
- **Interactive:** Hover for exact counts and percentages
- **Filtering:** Updates based on dropdown selections

#### Component 2: Payload vs Launch Outcome Scatter Plot
- **X-Axis:** Payload Mass (kg)
- **Y-Axis:** Orbit Type or Mission Status
- **Color-Coding:** Green for success, red for failure
- **Size:** Represents rocket type or mission importance
- **Interactive:** Hover for detailed mission information

#### Component 3: Site Selection Dropdown
```
Options:
- All Sites
- [Site 1]
- [Site 2]
- [Site 3]
- [Site 4]
```

#### Component 4: Payload Range Slider
- Minimum: [VALUE] kg
- Maximum: [VALUE] kg
- Allows filtering by payload mass range

#### Component 5: Rocket Type Filter
- Multi-select dropdown
- Options: [List rocket types]
- Filters all visualizations simultaneously

#### Component 6: Time Period Selector
- Range slider for date selection
- Enables temporal analysis within custom date ranges

### Dashboard Interactions
1. Select launch site → All charts update
2. Adjust payload range → Scatter plot and pie chart filter
3. Choose rocket types → Data reflects selection
4. Set time period → Temporal filtering applied

### Key Metrics Displayed
- Total launches: [NUMBER]
- Success rate: [PERCENTAGE]%
- Average payload: [VALUE] kg
- Most used site: [SITE]

### Dashboard Deployment
- **Framework:** Plotly Dash
- **Server:** [Specify deployment platform]
- **Accessibility:** [URL or access method]

### Notebook/Code Reference
📓 See: Application code and visualization notebooks

---

## 1.15 - Predictive Analysis with Multiple Models, Evaluation Results, Confusion Matrix, and Clear Conclusion with Creative Insights

### Predictive Models Developed

#### Model 1: Logistic Regression
**Algorithm:** Linear classification with sigmoid function
**Hyperparameters:** [Specify]
**Training Time:** [TIME]
**Accuracy:** [PERCENTAGE]%

#### Model 2: Decision Tree Classifier
**Algorithm:** Tree-based hierarchical decision model
**Max Depth:** [VALUE]
**Min Samples Split:** [VALUE]
**Accuracy:** [PERCENTAGE]%

#### Model 3: Random Forest Classifier
**Algorithm:** Ensemble of decision trees
**Number of Trees:** [NUMBER]
**Max Depth:** [VALUE]
**Accuracy:** [PERCENTAGE]%

#### Model 4: Support Vector Machine (SVM)
**Algorithm:** Kernel-based classification
**Kernel Type:** [rbf/linear/polynomial]
**C Parameter:** [VALUE]
**Accuracy:** [PERCENTAGE]%

#### Model 5: K-Nearest Neighbors (KNN)
**Algorithm:** Instance-based nearest neighbor
**K Value:** [NUMBER]
**Distance Metric:** [Euclidean/Manhattan]
**Accuracy:** [PERCENTAGE]%

### Model Performance Comparison

| Model | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|-------|----------|-----------|--------|----------|---------|
| Logistic Regression | [%] | [%] | [%] | [%] | [%] |
| Decision Tree | [%] | [%] | [%] | [%] | [%] |
| Random Forest | [%] | [%] | [%] | [%] | [%] |
| SVM | [%] | [%] | [%] | [%] | [%] |
| KNN | [%] | [%] | [%] | [%] | [%] |

### Best Performing Model: [MODEL NAME]
**Why This Model Performs Best:**
- Highest accuracy: [PERCENTAGE]%
- Excellent precision: [PERCENTAGE]% (minimizes false positives)
- Strong recall: [PERCENTAGE]% (captures most true positives)
- Best F1-Score: [VALUE] (balanced performance)
- Highest AUC-ROC: [VALUE]

### Confusion Matrix Analysis for Best Model

```
                    Predicted Success    Predicted Failure
Actual Success      [True Positives]     [False Negatives]
Actual Failure      [False Positives]    [True Negatives]
```

**Interpretation:**
- **True Positive Rate (Sensitivity):** [PERCENTAGE]% - Of actual successes, we correctly predict [X]%
- **True Negative Rate (Specificity):** [PERCENTAGE]% - Of actual failures, we correctly identify [X]%
- **False Positive Rate:** [PERCENTAGE]% - Incorrectly predict success [X]% of the time
- **False Negative Rate:** [PERCENTAGE]% - Miss actual successes [X]% of the time

**Business Impact:**
- Missing a successful launch (FN): [Cost/Risk]
- Predicting failure when success occurs (FP): [Cost/Risk]
- [Strategic recommendation based on matrix]

### Feature Importance Analysis

#### Top 10 Most Important Features:
1. **[Feature 1]** - Importance: [0.XXX]
   - Impact: [Explain why this feature is important]

2. **[Feature 2]** - Importance: [0.XXX]
   - Impact: [Explain significance]

3. **[Feature 3]** - Importance: [0.XXX]
   - Impact: [Explain significance]

4. **[Feature 4]** - Importance: [0.XXX]
5. **[Feature 5]** - Importance: [0.XXX]
6. **[Feature 6]** - Importance: [0.XXX]
7. **[Feature 7]** - Importance: [0.XXX]
8. **[Feature 8]** - Importance: [0.XXX]
9. **[Feature 9]** - Importance: [0.XXX]
10. **[Feature 10]** - Importance: [0.XXX]

#### Feature Importance Visualization
[Description of visualization showing top features]

### Model Validation Strategy
- **Train-Test Split:** [PERCENTAGE]% train, [PERCENTAGE]% test
- **Cross-Validation:** [K-fold with K=[NUMBER]]
- **Stratification:** Applied to maintain class distribution

### Hyperparameter Tuning
- **Method:** Grid Search / Random Search
- **Parameters Optimized:** [List parameters]
- **Best Parameters Found:** [Specify]
- **Improvement:** [PERCENTAGE] increase in performance

### Creative and Innovative Insights

#### Insight 1: Feature Synergy Effects
The combination of [Feature A] and [Feature B] shows unexpected synergistic effects. When both are optimized, success probability increases by [X]% more than the sum of individual improvements. This suggests [business implication].

#### Insight 2: Temporal Learning Pattern
The model's prediction confidence increases with [temporal variable]. This indicates that SpaceX operations show consistent patterns that improve over time, particularly in [specific domain]. Recommendation: [Action item]

#### Insight 3: Risk Clustering
Payload types in the [orbit type] category cluster into two distinct risk profiles. High-risk payloads could be [description], while low-risk payloads are [description]. Strategic insight: [Business strategy]

#### Insight 4: Hidden Feature Interactions
[Feature X] interacts with [Feature Y] in a non-linear manner that traditional analysis misses. The model captures this, enabling [specific prediction improvement]. Innovation: [How to leverage this]

#### Insight 5: Predictive Power Asymmetry
The model predicts success [PERCENTAGE]% accurately but failures only [PERCENTAGE]% accurately. This asymmetry reveals that [root cause]. Recommendation: [How to address]

### Model Limitations and Considerations
- Potential bias: [Describe any bias in training data]
- Data imbalance: [Success rate %] success vs [%] failure
- Generalization: Model tested on [time period/geographic region]
- Future data drift: [Anticipated challenges]

### Recommendations for Deployment
1. Monitor model performance in production
2. Retrain quarterly with new launch data
3. Set alert thresholds for confidence scores
4. Use ensemble predictions for critical missions

### Conclusion
The [BEST MODEL] achieved [ACCURACY]% accuracy in predicting SpaceX launch success. The model demonstrates strong discriminative ability, particularly for [scenario]. The identified features provide actionable insights for mission planning and risk assessment. Future improvements could include [specific recommendations].

### Notebook Reference
📓 See: `SpaceX_Machine Learning Prediction_Part_5.ipynb`

---

## Final Summary and Recommendations

### Project Achievements
✅ Successfully collected [NUMBER] launch records  
✅ Identified [NUMBER] key success factors  
✅ Built [NUMBER] predictive models  
✅ Achieved [PERCENTAGE]% prediction accuracy  
✅ Created interactive visualizations and dashboards  
✅ Generated actionable business insights  

### Key Takeaways
1. [Major finding 1]
2. [Major finding 2]
3. [Major finding 3]
4. [Major finding 4]
5. [Major finding 5]

### Recommendations for Future Work
1. **Enhanced Data Collection**
   - Incorporate weather data for launch conditions
   - Add satellite imagery for site conditions
   - Include detailed mission parameters

2. **Advanced Modeling**
   - Develop neural network models (LSTM, CNN)
   - Implement ensemble methods
   - Explore anomaly detection techniques

3. **Real-time Application**
   - Deploy prediction system for upcoming launches
   - Create alert system for mission-critical decisions
   - Develop API for stakeholder access

4. **Deeper Analysis**
   - Investigate feature interactions
   - Perform causal inference analysis
   - Conduct scenario planning studies

### Project Impact
This analysis provides SpaceX and space industry stakeholders with data-driven insights for:
- Mission planning and scheduling
- Risk assessment and mitigation
- Resource allocation optimization
- Technology advancement planning

---

## Repository Information

**GitHub Repository:** https://github.com/JoeLW-12324/Data-Science-Capstone-project-report

**Project Files:**
- `jupyter-labs-spacex-data-collection-api.ipynb` - Data collection via API
- `labs-jupyter-spacex-Data wrangling.ipynb` - Data cleaning and preprocessing
- `edadataviz.ipynb` - Exploratory data analysis and visualizations
- `jupyter-labs-eda-sql-coursera_sqllite.ipynb` - SQL-based analysis
- `lab_jupyter_launch_site_location.ipynb` - Geographic analysis with Folium
- `SpaceX_Machine Learning Prediction_Part_5.ipynb` - Predictive modeling

---

*Report Generated: [DATE]*  
*Data Period: [START DATE] to [END DATE]*  
*Analysis Complete*
