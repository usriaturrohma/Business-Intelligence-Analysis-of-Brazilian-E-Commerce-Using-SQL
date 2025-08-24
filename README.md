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

<details>
  <summary>Click to view SQL Queries</summary>

```sql
QUERY INPUT TABEL
CREATE TABLE customer_dataset (
	customer_id VARCHAR(50),
	customer_unique_id VARCHAR(50),
	customer_zip_code_prefix VARCHAR(50),
	customer_city VARCHAR(50),
	customer_state VARCHAR(50)
);

CREATE TABLE geolocation_dataset (
	geolocation_zip_code_prefix VARCHAR(50),
	geolocation_lat DECIMAL(9,6),
	geolocation_lng DECIMAL(9,6),
	geolocation_city VARCHAR(50),
	geolocation_state VARCHAR(50)
);

CREATE TABLE order_items_dataset (
	order_id VARCHAR(50),
	order_item_id VARCHAR(50),
	product_id  VARCHAR(50),
	seller_id VARCHAR(50),
	shipping_limit_date TIMESTAMP,
	price DECIMAL(9,6),
	freight_value DECIMAL(9,6)
);

CREATE TABLE order_payments_dataset (
	order_id VARCHAR(50),
	payment_sequential INT,
	payment_type VARCHAR(50),
	payment_installments INT,
	payment_value DECIMAL(9,6)
);

CREATE TABLE order_reviews_dataset (
	review_id VARCHAR(50),
	order_id VARCHAR(50),
	review_score INT,
	review_comment_title VARCHAR(50),
	review_comment_message VARCHAR(1000),
	review_creation_date TIMESTAMP,
	review_answer_timestamp TIMESTAMP
);

CREATE TABLE orders_dataset (
    order_id VARCHAR(50), -- Order ID
    customer_id VARCHAR(50), -- Customer ID
    order_status VARCHAR(20), -- Order status
    order_purchase_timestamp TIMESTAMP, -- Order purchase timestamp
    order_approved_at TIMESTAMP, -- Order approval timestamp
    order_delivered_carrier_date TIMESTAMP, -- Delivery date by carrier
    order_delivered_customer_date TIMESTAMP, -- Customer received date
    order_estimated_delivery_date TIMESTAMP -- Estimated delivery date
);

CREATE TABLE products_dataset (
    product_id VARCHAR(50), -- Product ID
    product_category_name VARCHAR(50), -- Product category name
    product_name_length INT, -- Product name length
    product_description_length INT, -- Product description length
    product_photos_qty INT, -- Number of product photos
    product_weight_g DECIMAL(10,2), -- Product weight (grams)
    product_length_cm DECIMAL(10,2), -- Product length (cm)
    product_height_cm DECIMAL(10,2), -- Product height (cm)
    product_width_cm DECIMAL(10,2) -- Product width (cm)
);

CREATE TABLE sellers_dataset (
    seller_id VARCHAR(50), -- Seller ID
    seller_zip_code_prefix VARCHAR(20), -- Seller's zip code prefix
    seller_city VARCHAR(50), -- Seller's city
    seller_state VARCHAR(10) -- Seller's state
);

--Add Primary Key
ALTER TABLE customer_dataset ADD CONSTRAINT customer_dataset_pkey PRIMARY KEY (customer_id);
ALTER TABLE geolocation_dataset ADD CONSTRAINT geolocation_dataset_pkey PRIMARY KEY (geolocation_zip_code_prefix);
ALTER TABLE orders_dataset ADD CONSTRAINT orders_dataset_pkey PRIMARY KEY (order_id);
ALTER TABLE products_dataset ADD CONSTRAINT products_dataset_pkey PRIMARY KEY (product_id);
ALTER TABLE sellers_dataset ADD CONSTRAINT sellers_dataset_pkey PRIMARY KEY (seller_id);

ALTER TABLE orders_dataset 
ADD CONSTRAINT fk_orders_customers
FOREIGN KEY (customer_id) REFERENCES customer_dataset (customer_id);

ALTER TABLE order_payments_dataset 
ADD CONSTRAINT fk_payments_order
FOREIGN KEY (order_id) REFERENCES orders_dataset (order_id);

ALTER TABLE order_reviews_dataset
ADD CONSTRAINT fk_reviews_order
FOREIGN KEY (order_id) REFERENCES orders_dataset (order_id);

ALTER TABLE order_items_dataset
ADD CONSTRAINT fk_items_order
FOREIGN KEY (order_id) REFERENCES orders_dataset (order_id);

ALTER TABLE order_items_dataset
ADD CONSTRAINT fk_items_product
FOREIGN KEY (product_id) REFERENCES products_dataset (product_id);

ALTER TABLE order_items_dataset
ADD CONSTRAINT fk_items_sellers
FOREIGN KEY (seller_id) REFERENCES sellers_dataset (seller_id);

ALTER TABLE customer_dataset
ADD CONSTRAINT fk_customer_geolocation
FOREIGN KEY (customer_zip_code_prefix) REFERENCES geolocation_dataset (geolocation_zip_code_prefix);
```

</details>

![ERD](https://i.imgur.com/HRhd2Y0.png) 

---

## 📂 **Data Analysis**

### Customer Distribution & Retention

<details>
  <summary>Click to view SQL Queries</summary>

```sql

```

</details>

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

