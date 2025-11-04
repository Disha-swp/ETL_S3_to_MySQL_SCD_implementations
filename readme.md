# 🧠 ETL Pipeline: S3 → MySQL with SCD Type 1 & Type 2

This project demonstrates an **end-to-end ETL pipeline** that extracts JSON data from an **AWS S3 bucket**, transforms it, and loads it into **MySQL** tables while handling **Slowly Changing Dimensions (SCD)** — both **Type 1** and **Type 2**.

---

## 📂 Project Overview

The ETL process involves:
1. **Extracting** data from an S3 bucket.
2. **Transforming** JSON data into structured format using Python.
3. **Loading** the transformed data into MySQL tables.
4. Implementing **SCD Type 1** and **Type 2** logic for maintaining dimension data.

---

## 🧩 Data Model

The project uses a **Star Schema** with:
- **Dimensions:**
  - `Customer`
  - `Product`
- **Fact Table:**
  - `Order`

### 🔹 Product Dimension
- Implemented both **SCD Type 1** and **SCD Type 2**.
- Tracks changes in product details (e.g., name, category, price).
- Includes fields: `product_sk`, `product_id`, `name`, `category`, `price`, `start_date`, and `end_date`.

### 🔹 Customer Dimension
- Captures unique customer information such as `customer_id`, `name`, `email`, and `address`.

### 🔹 Order Fact
- Contains transactional data with foreign keys referencing product and customer dimensions.

---

## ⚙️ ETL Steps

1. **Extract**
   - Read JSON files from the S3 bucket using `boto3`.
   - Merge multiple JSON files into a single dataset.

2. **Transform**
   - Parse nested JSON into flat structures.
   - Prepare dataframes for each dimension and fact table.

3. **Load**
   - Load data into MySQL using `sqlalchemy` or `mysql.connector`.
   - Apply **SCD Type 1** (overwrite old records) and **SCD Type 2** (maintain historical records with date ranges).

---

## 🧠 Key Features

- ✅ Integration with **AWS S3** for data extraction  
- ✅ Automated **data transformations** using Python  
- ✅ Supports **SCD Type 1 & Type 2** in product dimension  
- ✅ **Star schema design** for analytical queries  
- ✅ **MySQL** as target database  

---

## 🧰 Tech Stack

| Component | Technology |
|------------|-------------|
| Programming | Python |
| Cloud Storage | AWS S3 |
| Database | MySQL |
| Libraries | boto3, pandas, sqlalchemy, json |

---

## 📘 Project Structure

├── etl_script.py                # Python ETL logic (extract, transform, load)
├── validator.py                 # Schema and data validation logic
├── sql_scripts/
│   ├── create_tables.sql        # Table creation scripts
│   ├── scd_type1.sql            # SCD Type 1 implementation
│   └── scd_type2.sql            # SCD Type 2 implementation
├── data/                        # Sample data (optional)
├── README.md                    # Project documentation


## Set up your environment
pip install boto3 pandas mysql-connector-python

## Configure AWS and MySQL
s3 = boto3.client(
    's3',
    aws_access_key_id='YOUR_ACCESS_KEY',
    aws_secret_access_key='YOUR_SECRET_KEY'
)

## Run the ETL Script
python -m notebook

## Verify results in MySQL

SELECT * FROM products_ETL_scd2;

## Example Output

After running the ETL pipeline, MySQL database will contain:

Customer dimension with unique customer details

Product dimension with both current and historical versions

Order fact table referencing both dimensions

