# 🛒 Zepto E-commerce SQL Data Analyst Portfolio Project

A complete, real-world SQL Data Analytics Portfolio Project based on an e-commerce dataset scraped from Zepto — one of India’s fastest-growing quick-commerce startups.  
This project demonstrates how analysts use SQL for data cleaning, exploration, and deriving business insights from real-world data.

---

## 📌 Project Overview

The goal of this project is to simulate how data analysts in e-commerce work with messy real-world datasets to:  
✅ Build and manage a structured SQL database  
✅ Perform Exploratory Data Analysis (EDA) to explore product categories, stock, and pricing  
✅ Implement data cleaning to fix missing or invalid records  
✅ Write business-focused SQL queries to analyze pricing, discounts, inventory, and revenue

---

## 📁 Dataset Overview

Source: Kaggle — dataset scraped from Zepto’s product listings.  
Each record represents a unique SKU (Stock Keeping Unit) for a product. Duplicate names occur due to multiple sizes, weights, or package variations — just like real catalog data.

### Columns Description

- **sku_id**: Unique identifier for each product (Primary Key)  
- **name**: Product name as listed on the app  
- **category**: Product category (e.g., Fruits, Snacks, Beverages)  
- **mrp**: Maximum Retail Price (originally in paise, converted to ₹)  
- **discountPercent**: Discount percentage applied on MRP  
- **discountedSellingPrice**: Final selling price after discount  
- **availableQuantity**: Units available in stock  
- **weightInGms**: Product weight in grams  
- **outOfStock**: Boolean flag (TRUE = out of stock)  
- **quantity**: Number of units per package

---

## 🧱 1. Database & Table Creation

Created the base SQL table with correct data types:

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
```

---

## 📥 2. Data Import

Loaded data into PostgreSQL using pgAdmin or the `\copy` command:

```sql
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');
```

💡 If you face encoding errors, re-save the file as “CSV UTF-8” before importing.

---

## 🔍 3. Data Exploration

Performed initial data exploration using SQL:  
- Counted total records and viewed sample data  
- Checked for null values  
- Listed distinct categories  
- Compared in-stock vs out-of-stock products  
- Found duplicate product names across SKUs

---

## 🧹 4. Data Cleaning

- Removed rows where **mrp** or **discountedSellingPrice** = 0  
- Converted **mrp** and **discountedSellingPrice** from paise to rupees

```sql
UPDATE zepto 
SET mrp = mrp / 100.0,
    discountedSellingPrice = discountedSellingPrice / 100.0;
```

---

## 📊 5. Business Insights (SQL Queries)

- Q1. Find top 10 best-value products based on highest discount percentage  
- Q2. Identify high-MRP products that are currently out of stock  
- Q3. Estimate potential revenue for each product category  
- Q4. Filter expensive products (MRP > ₹500) with minimal discount  
- Q5. Rank top 5 categories offering highest average discounts  
- Q6. Calculate price per gram to identify value-for-money products  
- Q7. Group products based on weight into Low, Medium, and Bulk categories  
- Q8. Measure total inventory weight per product category  
- Q9. List categories where average selling price per gram exceeds ₹2  
- Q10. Identify products that contribute most to overall revenue (top 10 by revenue share)

---

## 🧠 Example Insights

- Beverages and Snacks contribute the highest revenue.  
- Dry Fruits offer the highest average discounts.  
- Around 12% of products are out of stock.  
- High-MRP products often have low discounts — an opportunity for promotions.

---

## 🧩 Tools & Technologies Used

- **PostgreSQL** — for database management  
- **pgAdmin 4** — for running SQL queries  
- **Kaggle** — as the data source  
- **SQL** — for data cleaning, analysis, and insights

---

## 🏁 Key Takeaways

- Realistic e-commerce data experience  
- End-to-end SQL workflow (import → cleaning → insights)  
- Strong analytical and querying skills  
- Simulation of real-world data analyst tasks

---

## 💼 Author

**Rajat Bhatia**  
📧 brajat909@gmail.com  
🌐 [GitHub Profile](https://github.com/brajat170)

---

⭐ If you found this project helpful, give it a star and connect with me for more SQL projects!
