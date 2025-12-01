# Fixed Asset Dashboard – Mock Data Project

This project provides a complete mock dataset to build a **Power BI Fixed Asset Dashboard** that serves as a one-stop view for tracking asset lifecycle and financial health across an imaginary company.

The dataset enables analysis of:
- Asset inventory by **group and location**
- **Acquisition, depreciation, disposal** trends
- **Daily Net Book Value (NBV)** movement
- Overall **Fixed Asset Health** across multi-year periods filtered to NYSE trading days only

---

## Dashboard Objectives

The dashboard supports:

- Monitoring asset value changes over time  
- Comparing asset utilization and health by group and location  
- Identifying assets with high depreciation or disposal activity  
- Tracking capital expenditure (acquisitions) trends  
- Viewing rolling **net book value** by asset category

---

## Dataset Structure

The dataset uses a simple star schema:

### 1. `FIXED_ASSET_DIM.csv`
Asset master data.

| Column | Description |
|--------|--------------|
| `id` | Unique asset ID |
| `date` | Asset in-service date (YYYYMMDD) |
| `name` | Asset name |
| `group` | Asset category |
| `location` | Physical location |

---

### 2. `ASSET_DETAILS_DIM.csv`
Lifetime financial summary per asset.

| Column | Description |
|--------|-------------|
| `id` | Detail ID |
| `fixed_asset_id` | Asset foreign key |
| `beginning_amt` | Opening asset value |
| `acquisition` | Total additions |
| `depreciation` | Total depreciation |
| `disposal` | Total disposals |
| `net_book_value` | Ending NBV |

---

### 3. `BMV_ASSET_FACT.csv`
Daily asset financial metrics on **NYSE trading days only** (3+ years of data).

| Column | Description |
|--------|-------------|
| `id` | Fact row ID |
| `trade_date` | Trading date |
| `fixed_asset_id` | Asset foreign key |
| `asset_detail_id` | Asset detail key |
| `beginning_amt` | Opening value for the day |
| `acquisition` | Acquisition booked that day |
| `depreciation` | Depreciation for the day |
| `disposal` | Disposal posted that day |
| `net_book_value` | Closing NBV |

---

## Data Generation

A Python script generates realistic asset activity data including:
- 20+ assets across multiple categories
- Daily entries based on **NYSE market calendar**
- Randomized but internally consistent financial totals

### Requirements
```bash
pip install pandas numpy pandas_market_calendars
