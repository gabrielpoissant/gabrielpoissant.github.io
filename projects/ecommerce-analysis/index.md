---
layout: single
title: E-Commerce Analysis
permalink: /projects/ecommerce-analysis/
author_profile: true
sidebar:
  nav: "side_nav"
---

---
**Goal:**

To answer key business questions by cleaning, processing, and analyzing real-world e-commerce transaction data. 

---

**Data:**

I used a dataset that details e-commerce sales and returns, taken from a UK-based online store which primarily sells gift items to wholesalers. The dates of sales range from 12/01/2009 to 12/09/2010.

| Column    | Description                                   | Example Value |
|--------   |--------                                       |--------|
|Invoice    |Invoice number. Cancellations begin with 'C'|  491633| 
|StockCode  |Code that uniquely identifies product ordered|48195|
|Description|Description of product ordered                 |DOOR MAT GREEN PAISLEY|
|Quantity   |Number of units ordered per transaction        |2|
|InvoiceDate|Date and time of invoice                       |2009-12-11 15:37:00|
|Price      |Per-unit price in sterling                     |6.75|
|Customer ID|Number that uniquely identifies customer       |17958.0|
|Country    |The country the customer ordered from          |United Kingdom|

This dataset was authored by [Daqing Chen](https://scholar.google.com/citations?user=D827XxMAAAAJ&hl=en) and [published by University of California, Irvine](https://archive.ics.uci.edu/dataset/502/online+retail+ii).

---

**Business Questions**

I sought to answer the following critical business questions:
- How has monthly revenue evolved over time?
- Is there evidence of seasonality in sales?
- What is the average order value, and how has it changed?
- What share of revenue comes from repeat customers?
- How concentrated is revenue among customers?
- Which products drive the majority of revenue?
- Which products have disproportionately high return rates?
- How is revenue distributed geographically?
- Are certain markets growing faster than others?
- What percentage of gross revenue is lost to returns?

---

**Approach**

Analyzing this dataset required several data cleaning steps, and repair before analysis.
- **Exploratory Data Analysis**
- **Missing Data** (repaired using other row information)
- **Cleaning** (data types, additional columns, trimming rows)
- **Business Insights**

Missing value analysis before and after processing:

{: .text-center}
![Missing-Analysis](/assets/missing_analysis.png){: .align-center}

```
def product_concentration(df):
    df2 = df[df['Type'] != 'Cancellation'].copy()
    code_revenue = df2[['StockCode','TotalPrice']].groupby('StockCode').sum().sort_values('TotalPrice', ascending=False)
    code_description = df2[['StockCode','Description']].drop_duplicates(subset='StockCode')
    units_sold = df2[['StockCode','Quantity']].groupby('StockCode').sum().sort_values('Quantity', ascending=False)

    product_revenue = pd.merge(code_revenue, code_description, on='StockCode', how='outer')
    product_revenue = pd.merge(product_revenue, units_sold, on='StockCode', how='outer')
    product_revenue['Percentage'] = product_revenue['TotalPrice']/product_revenue['TotalPrice'].sum()
    product_revenue = product_revenue[['StockCode','Description','TotalPrice','Percentage','Quantity']].sort_values('TotalPrice', ascending=False).reset_index(drop=True)
    product_revenue = product_revenue.rename(columns={'TotalPrice':'Revenue'})
    return product_revenue
```

{: .text-center}
![Product-Concentration-Table](/assets/product_concentration_table.png){: .align-center}




{: .text-center}
![Top-Performing-Products](/assets/Top_Performing_Products.png){: .align-center}


<img src="/assets/Top_Performing_Products.png" alt="" width="200"/>


---

