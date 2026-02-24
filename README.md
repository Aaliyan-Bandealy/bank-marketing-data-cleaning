#  Bank Marketing Data Cleaning

##  Project Overview

This project cleans and restructures a UK bank marketing campaign dataset into three normalized tables suitable for PostgreSQL database import.

Banks rely on marketing campaigns to promote personal loans. Before storing campaign data in a relational database for future analysis, the raw CSV must be cleaned, standardized, and split into structured tables.

The script transforms the raw dataset into:

- client.csv  
- campaign.csv  
- economics.csv  

Each table follows a structured schema with correct data types and formatting.

---

##  Objectives

- Clean categorical variables for database compatibility  
- Convert binary outcomes to boolean data types  
- Construct proper datetime fields  
- Normalize raw dataset into relational structure  
- Prepare outputs for PostgreSQL ingestion  

---

##  Technologies Used

- Python  
- Pandas  
- NumPy  

---

##  Dataset Transformation

The original dataset contains client details, campaign activity data, and economic indicators in a single CSV file.

This project separates and cleans the data into three logical tables:

---

### 1️) client.csv

| Column | Type | Cleaning Applied |
|----------|----------|----------------|
| client_id | Integer | No change |
| age | Integer | No change |
| job | String | Replaced `.` with `_` |
| marital | String | No change |
| education | String | Replaced `.` with `_`, converted `"unknown"` to NULL |
| credit_default | Boolean | `"yes"` → True, `"no"` → False |
| mortgage | Boolean | `"yes"` → True, `"no"` → False |

Example:
- `high.school` → `high_school`
- `unknown` → NULL

---

### 2️) campaign.csv

| Column | Type | Cleaning Applied |
|----------|----------|----------------|
| client_id | Integer | No change |
| number_contacts | Integer | No change |
| contact_duration | Integer | No change |
| previous_campaign_contacts | Integer | No change |
| previous_outcome | Boolean | `"success"` → True, others → False |
| campaign_outcome | Boolean | `"yes"` → True, `"no"` → False |
| last_contact_date | Datetime | Constructed from month/day + year 2022 |

Date Construction Process:
1. Added a year column (2022)
2. Combined year + month + day
3. Converted to proper datetime format
4. Dropped intermediate columns (month, day, year)

---

### 3️) economics.csv

| Column | Type | Cleaning Applied |
|----------|----------|----------------|
| client_id | Integer | No change |
| cons_price_idx | Float | No change |
| euribor_three_months | Float | No change |

This table isolates macroeconomic indicators for analysis or modeling.

---

##  How to Run

### Install Dependencies

```bash
pip install pandas numpy
