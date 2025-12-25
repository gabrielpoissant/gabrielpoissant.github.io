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
I used the standard layered approach, consisting of:
- **Conceptual Design** (High Level ER Diagram)
- **Logical Design** (Define tables, columns and keys)
- **Physical Model** (DDL)
- **Deployment** (Loading and transforming data)


Conceptual diagram describing preliminary structure and cardinality:
{: .text-center}
![Conceptual-Model](/assets/Conceptual_Diagram.png){: .align-center}
<figcaption>This is the image caption.</figcaption>

Physical model diagram created using reverse-engineer method:
{: .text-center}
![Physical_Diagram](/assets/Physical_Diagram.png){: .align-center}

SQL excerpt defining tables, primary keys and foreign keys:
{: .text-center}
```
CREATE TABLE MAKE
(Make_ID INT AUTO_INCREMENT,
Make VARCHAR(50),
Created_Date DATETIME DEFAULT NOW(),
Modified_Date DATETIME DEFAULT NOW(),
CONSTRAINT PK_MAKE PRIMARY KEY (Make_ID));

ALTER TABLE CAR_SALE
ADD CONSTRAINT FK_CAR_SALE_Make_ID FOREIGN KEY (Make_ID)
REFERENCES MAKE(Make_ID);
```

---

**Results:**  
After data input and configuration, I'm able to define queries:
```
SELECT 
    seller,
    COUNT(*) AS cars_sold,
    ROUND(AVG(mmr - sellingprice), 2) AS avg_discount_vs_mmr,
	  ROUND(AVG(car_condition),2) AS average_condition,
    ROUND(AVG(odometer),2) AS average_odometer
FROM vw_CARS
GROUP BY seller
HAVING COUNT(*) > 100
ORDER BY avg_discount_vs_mmr DESC
LIMIT 10;
```

Output:

| seller | cars_sold | avg_discount_vs_mmr | average_condition | average_odometer |
|-----------|----------|---------|----------|---------|
| hertz/tra | 500 | 6630.09 | 1.78 | 32143.31 |
| fox rent a car tra | 115 | 5212.17 | 2.47 | 35468.75 |
| hertz damaged liquidation | 112 | 4636.38 | 2.50 | 46183.85 |
| enterprise vehicle exchange / tra / rental / tulsa | 2395 | 4454.55 | 2.26 | 24533.00 |
| mercedes-benz usa | 154 | 2670.78 | 36.89 | 20526.31 |
| hyundai buybacks | 125 | 2665.80 | 33.67 | 22535.38 |
| enterprise fm exchange/tra/lease | 102 | 1931.13 | 4.11 | 131590.00 |
| security service fcu (sscu) | 133 | 1852.82 | 24.92 | 78381.17 |
| excell auto center | 316 | 1764.00 | 30.33 | 77011.25 |
| navy federal credit union | 139 | 1482.37 | 26.81 | 82929.74 |

This table is a short guide to high-volume sellers who regularly price below Manheim Market Report value, sorted by greatest savings.  
{: .notice}

Metrics *or* business insights, plus 2–4 bullets.

---

**What I’d do next:**  
- Dive deeper into integrity
- Improve efficiency with indexes
- Anticipate team usage (roles, backups, deployment)

---

**Code:**  
[https://github.com/gabepoissant/used-car-database-design](https://github.com/gabepoissant/used-car-database-design)
