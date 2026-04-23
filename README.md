# Tesla EV Market Analysis Dashboard

This project presents an end-to-end analysis of Tesla’s electric vehicle performance using publicly available EV population data. The focus is on transforming raw data into structured insights and presenting them through a clean, interactive dashboard built in R.

---


## 📊 Overview

The dashboard highlights key business questions:

- What is Tesla’s market share in the EV space?
- Which Tesla models drive the most volume and revenue?
- How has Tesla’s performance evolved over time?
- How does Tesla compare within the broader EV ecosystem?

The output is a structured dashboard designed to communicate insights clearly and efficiently.

---

## 🧰 Tools & Technologies

- **R**
- **dplyr** – data transformation and aggregation  
- **ggplot2** – data visualization  
- **flexdashboard** – dashboard layout and presentation  
- **tidyr / scales** – data formatting and enhancement  

---

## 🔄 Data Pipeline

### 1. Data Preparation
- Cleaned column names for consistency  
- Standardized categorical variables  
- Converted numeric fields (e.g., MSRP) for analysis  
- Created derived fields such as Tesla vs Other segmentation  

### 2. Feature Engineering
- Calculated key metrics:
  - Total vehicles
  - Tesla vehicle count
  - Market share percentage  
- Aggregated model-level and year-level data  
- Integrated pricing data to estimate revenue per model  

### 3. Data Modeling
- Grouped and summarized data across:
  - Model
  - Year
  - Vehicle type (BEV vs PHEV)  
- Filtered and refined datasets to focus on meaningful comparisons  

---

## 📈 Dashboard Structure

The dashboard is organized into four sections:

### Overview
- High-level KPIs (total vehicles, Tesla share, Tesla count)  
- Market share visualization  

### Performance
- Model-level sales distribution  
- Estimated revenue by model  

### Trends
- Tesla vehicle growth over time  
- BEV vs PHEV adoption trends  

### Insights
- Average electric range comparison  
- Top utility providers supporting Tesla vehicles  

---

## 🎯 Key Insights

- Tesla maintains a strong share of the EV market, driven primarily by a few high-volume models  
- Revenue concentration aligns closely with model popularity  
- EV adoption has accelerated significantly in recent years  
- BEVs dominate over PHEVs in growth trends  
- Infrastructure (utilities) plays a key role in EV distribution patterns  

---

## 📁 Project Structure


---

## 🚀 How to Run

1. Open the `.Rmd` file in RStudio  
2. Ensure required libraries are installed  
3. Update file paths if needed  
4. Click **Knit** to generate the dashboard  

---

## 📌 Notes

This project emphasizes clarity in both analysis and presentation.  
The goal is not just to explore the data, but to structure insights in a way that supports decision-making.

---

## 📬 Contact

For questions, collaboration, or feedback, feel free to connect.
