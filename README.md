# Supply Chain Management for Car - Data Pipeline

A complete Python-based data pipeline that automates downloading a car supply chain dataset from Kaggle, processing and transforming it using **Pandas**, exporting it for **Power BI** visualizations, and loading the structured data directly into a **MySQL** database.

---

## Features

* **Automated Data Retrieval:** Downloads the dataset directly from Kaggle using the Kaggle API and extracts the zipped contents.
* **Data Processing & Transformation:** Cleans and formats the dataset using Pandas, dropping unnecessary index columns to maintain data integrity.
* **Business Intelligence Ready:** Exports the cleaned dataset into an Excel workbook (`supply-chain-final.xlsx`) tailored for **Power BI** dashboards.
* **Database Integration:** Automatically creates a structured SQL table and inserts records into a local **MySQL** database using PyMySQL.

---

## Prerequisites & Dependencies

Make sure you have the following Python libraries installed before running the script:

```bash
pip install pandas kaggle pymysql numpy openpyxl

```

> **Note:** You must have a valid Kaggle API token (`kaggle.json`) configured in your environment (typically under `~/.kaggle/`) to download the dataset successfully.

---

## Configuration & Setup

1. **MySQL Credentials:**
Update the MySQL connection parameters in the script with your local database credentials:
```python
myconnection = pymysql.connect(
    host='localhost',
    user='root',
    passwd='your_password',  # Replace with your actual MySQL password
    database='youtube'       # Replace with your target database name
)

```


2. **Dataset Source:**
The script pulls data from the Kaggle dataset: `prashantk93/supply-chain-management-for-car`.

---

## Project Workflow

1. **Download & Extract:** Connects to Kaggle, downloads `supply-chain-management-for-car.zip`, and unzips `Car_SupplyChainManagementDataSet.csv`.
2. **Pandas Processing:** Reads the CSV into a DataFrame, inspects data types (`info()`), and exports it to an Excel file (`supply-chain-final.xlsx`).
3. **Database Population:**
* Connects to MySQL.
* Removes redundant index columns using Pandas `iloc`.
* Dynamically generates an SQL `CREATE TABLE` query for the `cars` table with appropriate schema fields (Supplier details, Car specs, Customer info, Orders, and Shipping data).
* Inserts records iteratively with transaction commits.



---

## Output Files

* `Car_SupplyChainManagementDataSet.csv` — Raw extracted dataset.
* `supply-chain-final.xlsx` — Cleaned dataset ready for Power BI consumption.
* **MySQL Table (`cars`)** — Relational storage of all supply chain records.
