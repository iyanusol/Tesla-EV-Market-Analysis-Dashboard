# Tesla EV Market Analysis Dashboard

This project presents an end-to-end analysis of Tesla’s electric vehicle performance using publicly available EV population data. The focus is on transforming raw data into structured insights and presenting them through a clean, interactive dashboard built in R.

---

### 🧠 Overall Dashboard
![Dashboard Overview](https://raw.githubusercontent.com/iyanusol/Tesla-EV-Market-Analysis-Dashboard/main/images/graph%20sample.png)
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

![Models Sold](https://raw.githubusercontent.com/iyanusol/Tesla-EV-Market-Analysis-Dashboard/main/images/output-1.png)

```
make_model_sold <- clean_df  %>%
  filter(Tesla == "TESLA") %>%
  group_by(Make, Model) %>%
  summarise(count_sold = n(), .groups = "drop") %>%
  arrange(desc(count_sold))


msrp_per_year <- clean_df %>%
  filter(Base_MSRP > 0) %>%
  filter(Tesla == "TESLA") %>%
  group_by(Model_Year, Make, Model) %>%
  summarise(min(Base_MSRP)) %>%
  arrange(Model_Year, Make, Model)
```

### 2. Feature Engineering
- Calculated key metrics:
  - Total vehicles
  - Tesla vehicle count
  - Market share percentage  
- Aggregated model-level and year-level data  
- Integrated pricing data to estimate revenue per model  

![Trends](https://raw.githubusercontent.com/iyanusol/Tesla-EV-Market-Analysis-Dashboard/main/images/output-3.png)

### 3. Data Modeling
- Grouped and summarized data across:
  - Model
  - Year
  - Vehicle type (BEV vs PHEV)  
- Filtered and refined datasets to focus on meaningful comparisons  

---
```
market_df <- data.frame(
  Group = c("TESLA", "OTHER"),
  Market_Share = c(tesla_market_share, 100 - tesla_market_share)
)

market_df <- market_df %>%
  mutate(
    Label = paste0(Market_Share, "%"),
    ypos = cumsum(Market_Share) - 0.5 * Market_Share
  )

ggplot(market_df, aes(x = "", y = Market_Share, fill = Group)) +
  geom_col(width = 1) +
  coord_polar("y") +
  geom_text (aes(y = ypos, label = Label))+
  labs(title = "Tesla Market Share in Washington (%)")+
  theme_void()

```


## 📈 Dashboard Structure

The dashboard is organized into four sections:

### Overview
- High-level KPIs (total vehicles, Tesla share, Tesla count)  
- Market share visualization  

```
df_tesla_prices <- df_tesla_prices %>%
  mutate(
    Model = toupper(Model)
  )
  

Top_Tesla_Models_Priced <- make_model_sold %>%
  left_join(df_tesla_prices, by = "Model") %>%
  mutate(
    Estimated_revenue = as.numeric(count_sold) * as.numeric(Base_Price_USD)
  )

Top_Tesla_Models_Priced <- Top_Tesla_Models_Priced %>%
  filter(!is.na(Estimated_revenue)) %>%
  group_by(Model) %>%
  slice_min(Base_Price_USD) %>%
  ungroup()


tesla_sold_by_year <- clean_df %>%
  filter(Tesla == "TESLA") %>%
  group_by(Model_Year) %>%
  summarise(count = n()) %>%
  arrange(Model_Year)

```

### Performance
- Model-level sales distribution  
- Estimated revenue by model  

```
Avg_Range_For_EVs <- clean_df %>%
  filter(Electric_Vehicle_Type == "Battery Electric Vehicle (BEV)",
         Electric_Range != 0,
         Base_MSRP != 0) %>%
  group_by(Tesla) %>%
  summarise(AVG_Range = mean(Electric_Range),
            AVG_MSRP =mean(Base_MSRP))



Median_Range_For_EVs <- clean_df %>%
  filter(Electric_Vehicle_Type == "Battery Electric Vehicle (BEV)",
         Electric_Range != 0,
         Base_MSRP != 0) %>%
  group_by(Tesla) %>%
  summarise(Median_Range = median(Electric_Range),
            Median_MSRP =median(Base_MSRP))
```


### Trends
- Tesla vehicle growth over time  
- BEV vs PHEV adoption trends
  
![Revenue](https://raw.githubusercontent.com/iyanusol/Tesla-EV-Market-Analysis-Dashboard/main/images/output-2.png)  

### Insights
- Average electric range comparison  
- Top utility providers supporting Tesla vehicles

### ⚡ EV Insights
![Insights](https://raw.githubusercontent.com/iyanusol/Tesla-EV-Market-Analysis-Dashboard/main/images/output-4.png)
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
