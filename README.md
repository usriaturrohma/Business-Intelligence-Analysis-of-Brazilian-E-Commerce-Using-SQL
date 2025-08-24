# 🛍️ **Business Intelligence Analysis of Brazilian E-Commerce Using SQL**

![PostgreSQL](https://img.shields.io/badge/database-PostgreSQL-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/project-complete-brightgreen)

---

## 📂 **Table of Contents**

1. [Project Overview](#-project-overview)
2. [Data Preparation](#-data-preparation)

   * [Database Construction & ERD](#database-construction--erd)
3. [Data Analysis](#-data-analysis)

   * [Customer Distribution & Retention](#customer-distribution--retention)
   * [Seller Performance](#seller-performance)
   * [Product Category Insights](#product-category-insights)
4. [Business Insights Summary](#-business-insights-summary)
5. [Business Implications](#-business-implications)
6. [Tools & Environment](#-tools--environment)
7. [Reproducibility Guide](#-reproducibility-guide)

---

## 📂 **Project Overview**

### Background

Evaluating e-commerce performance is crucial to understand both market concentration and business sustainability. This project explores the **Brazilian e-commerce market** through SQL-based analysis to assess customers, sellers, and product categories.

### Project Goals

This project aims to derive actionable insights through SQL analysis with a focus on three main dimensions:

1. **Customer Distribution & Retention**

   * Analyze customer concentration across states.
   * Compare one-time vs repeat buyers and spending concentration (top spenders).
   * Identify retention challenges and highlight loyalty opportunities.

2. **Seller Performance**

   * Evaluate revenue distribution among sellers.
   * Assess performance based on review scores and order volume.
   * Uncover seller concentration in specific regions, especially São Paulo.

3. **Product Category Insights**

   * Identify top-selling product categories.
   * Detect problematic categories with high demand but poor ratings.
   * Provide insights on category trends and product quality implications.

---

## 📂 **Data Preparation**

The dataset is sourced from the **Brazilian E-Commerce Public Dataset by Olist (Kaggle)**.

Steps performed:

1. Created a PostgreSQL database and defined schemas using `CREATE TABLE`.
2. Imported datasets into tables (`customers`, `orders`, `sellers`, `products`, `reviews`, `payments`, `items`, `geolocation`).
3. Added primary and foreign key constraints to establish table relationships.
4. Generated the Entity Relationship Diagram (ERD) for visualization.

![ERD](https://i.imgur.com/HRhd2Y0.png) 

---

## 📂 **Data Analysis**

### Customer Distribution & Retention

**Key findings:** 
* Customer distribution is highly concentrated; São Paulo clearly dominates.
* A small set of states (São Paulo, Rio de Janeiro, Minas Gerais) lead, while the rest form a long tail with modest contributions.
* The pattern reflects regional concentration of demand and uneven penetration across states.
![Distribution of Unique Customers by State](assets/Output%201.png)

**Key findings:** 
* Customer mix is skewed toward first-time buyers; repeat purchasing is limited.
* Retention underperforms, suggesting growth relies more on acquisition than loyalty.
* Priority: drive second purchases and loyalty initiatives to raise lifetime value and improve acquisition payback.
![Output 2](assets/Output%202.png)

**Key Findings:**
* Highly concentrated spending: The top customer spends significantly more than others, with the highest spender contributing the majority of the total spend.
* Top 10 customers dominate: The top 10 customers account for a substantial portion of the overall spending, indicating a small number of customers are driving revenue.
* Significant spending disparity: There is a sharp drop-off in total spending after the top spender, highlighting the unequal distribution of spending among customers.
![Output 3](assets/Output%203.png)

### Seller Performance

**Key findings:**
* Top 2 sellers dominate: The top 2 sellers contribute the majority of the total revenue, with the highest seller generating over $249,640.
* Skewed revenue distribution: A few sellers generate significantly more revenue compared to others, indicating that revenue is not evenly distributed.
* Seller performance variability: Despite the top sellers driving revenue, there is significant variation in revenue between the remaining sellers, with the bottom sellers contributing much less.
![Output 4](assets/Output%204.png)

**Key findings:**
* São Paulo dominates with a seller count far above all other provinces, highlighting a strong concentration of sellers in one region.
* Sharp drop-off after São Paulo, with the next provinces (Paraná, Minas Gerais, Santa Catarina, Rio de Janeiro, Rio Grande do Sul) contributing significantly fewer sellers but still forming the second tier of activity.
* Long tail distribution: Most other provinces host very few sellers (many with fewer than 10), showing a highly uneven geographic distribution of seller presence.
![Output 5](assets/Output%205.png)

**Key findings:**
* Several sellers achieved perfect or near-perfect review scores (≈5.0), even with a substantial number of completed orders.
* The top seller not only maintained a 5.0 rating but also had the highest order volume (33 orders), showing consistent customer satisfaction.
* Overall, sellers with sufficient transaction volume demonstrated very high review averages, indicating strong service quality and positive customer experiences. 
![Output 6](assets/Output%206.png)

### Product Category Insights

**Key findings:**
* Beleza_saude leads as the top-selling category with over 36.6M in total sales, well ahead of other categories.
* Esporte_lazer and relogios_presentes follow, contributing more than 30M and 24.6M respectively, showing strong consumer demand.
* The distribution highlights a clear dominance of lifestyle and household-related categories (beauty, sports, home, and electronics accessories) in driving overall sales.
![Output 7](assets/Output%207.png)

**Key findings:**
* Several product categories (e.g., beleza_saude, utilidades_domesticas) received very low ratings (≈1.0–2.0) yet still had relatively high order volumes.
* This pattern indicates potential problem products: despite high demand, customers consistently gave poor reviews.
* Such categories may reflect quality issues, mismatch with expectations, or service-related problems, making them priority areas for investigation and improvement. 
![Output 8](assets/Output%208.png)

---

## 📊 **Business Insights Summary**

### 🧍‍♂️ Customer Distribution & Retention

Customer presence is highly concentrated:
* São Paulo leads by a wide margin, followed by Rio de Janeiro and Minas Gerais, while most other states contribute modestly.
* The customer mix is skewed toward one-time buyers (~97%), with repeat purchases very limited.
* Spending is also concentrated: the top 10 customers account for a substantial share, with the top spender far exceeding the rest.
This suggests low retention and heavy reliance on acquisition, highlighting the need for:
* Loyalty and re-engagement programs
* Incentives for second purchases
* Personalized campaigns for high-value customers

### 🏪 Seller Performance

Seller activity also shows strong concentration:
* The top 2 sellers dominate revenue, each exceeding $200K+, while the rest contribute less.
* São Paulo hosts the majority of sellers, with other provinces forming a long tail of limited presence.
* Some sellers achieved near-perfect review scores (≈5.0) while handling high order volumes, indicating strong and consistent service quality.
This emphasizes opportunities to:
* Support mid- and lower-tier sellers to boost competitiveness
* Replicate best practices from high-rated, high-volume sellers

### 🛒 Product Category Insights

Product sales are driven by lifestyle and household-related categories:
* Beleza_saude leads with over 36.6M in sales, followed by esporte_lazer and relogios_presentes.
* However, some categories (e.g., beleza_saude, utilidades_domesticas) show high demand but low ratings (≤2), signaling possible quality or expectation gaps.
This calls for:
* Deeper quality and fulfillment checks on popular categories
* Prioritization of customer feedback loops for problematic products
* Continuous monitoring of product category trends

---

## 📂 **Business Implications**

* Strengthen customer retention by introducing loyalty programs, personalized promotions, and post-purchase engagement to convert one-time buyers into repeat customers and improve CLV relative to CAC.
* Mitigate revenue dependency on top sellers by expanding seller development programs, recruiting in underrepresented regions outside São Paulo, and sharing best practices from high-performing sellers to elevate overall service quality.
* Address product quality gaps by closely monitoring categories with high demand but low ratings, such as beleza_saude and utilidades_domesticas, and implementing stronger quality assurance and customer feedback mechanisms to ensure satisfaction and reduce churn.

---

## 📂 **Tools & Environment**

* **PostgreSQL** for database & queries
* **pgAdmin** for schema/ERD management
* **Microsoft Excel 2019** for visualization

---

## 🚀 **Reproducibility Guide**

1. Clone this repository:

   ```bash
   git clone https://github.com/username/repo-name.git
   ```
2. Create a new PostgreSQL database.
3. Run the provided `CREATE TABLE` scripts in `/schema`.
4. Import each dataset into the corresponding table.
5. Execute SQL queries from `/queries`.
6. Export results and visualize them using Excel or BI tools.

---

