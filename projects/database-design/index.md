---
layout: single
title: Database Design
permalink: /projects/database-design/
author_profile: true
sidebar:
  nav: "side_nav"
---

---
**Goal:**  
<!--  I wanted to make sure I understood the fundamentals of how data is deployed in production environments. I decided to take a raw dataset from an unprocessed `.csv` and bring it through all design phases into a working, queryable database. -->
To take a raw dataset and bring it through all design phases into a working, queryable database.

---

**Data:**  
I found a dataset about used car sales in the U.S. between 2014 and 2015. The data gives information about the vehicle, and where and when it was sold.

| Column | Description | Example Value |
|-----------|----------|---------|
| year      | Model year of the vehicle sold | 2014 |
| make       | Manufacturer of the vehicle      | Kia      |
| model       | Model of the vehicle      | Rio     |
| trim       | Identifies included features      | LX     |
| body       | Type of vehicle      | Sedan     |
| transmission       | Transmission style of vehicle      | automatic     |
| vin       | Vehicle Identification Number      | knadm4a35e6327128     |
| state       | U.S. State car was sold in      | tx     |
| condition       | Rating of vehicle condition      | 39     |
| odometer       | Odometer reading at time of sale      | 27187     |
| color       | Exterior paint color      | silver     |
| interior       | Interior finish color      | black     |
| seller       | The entity that sold the vehicle      | tdaf remarketing     |
| mmr       | Manheim Market Report, an estimated market value      | 10650     |
| sellingprice       | Price vehicle sold for      | 10200     |
| saledate       | Date of sale      | Wed Feb 11 2015 02:15:00 GMT-0800 (PST)     |

This dataset was authored by [Syed Anwar](https://www.kaggle.com/syedanwarafridi) and [published to Kaggle](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data/data).
{: .notice}

---

**Approach:**  
I used the standard layered approach, which consisted of:
- Conceptual Design (High Level ER Diagrams)
- Logical Design (Define tables, columns and keys)
- Physical Model (DDL)
- Deployment (Loading and transforming data)


---

**Results:**  
Metrics *or* business insights, plus 2–4 bullets.

---

**What I’d do next:**  
1–3 bullets (shows maturity).

---

**Code:**  
https://github.com/USERNAME/REPO1
