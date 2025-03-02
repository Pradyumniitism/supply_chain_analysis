# Supply Chain Analysis

This repository contains a comprehensive analysis of a supply chain dataset using Python, `pandas`, and `plotly` for data manipulation and visualization. The analysis covers various aspects of the supply chain, including product pricing, revenue generation, sales distribution, shipping carriers, defect rates, and more.

## Project Overview

The analysis is structured around several key components of the supply chain:

- **Descriptive Statistics:** Provides a summary of the dataset, including measures such as mean, median, and standard deviation.
- **Product Type and Price Analysis:** Examines the relationship between product prices and the revenue generated.
- **Sales by Product Type:** Visualizes the sales distribution across different product types.
- **Total Revenue by Shipping Carrier:** Analyzes revenue contributions from different shipping carriers.
- **Product Analysis:** Evaluates average lead times and manufacturing costs for various products.
- **SKU Analysis:** Explores the concept of Stock Keeping Units (SKUs) and their impact on revenue, stock levels, and order quantities.
- **Shipping Costs:** Compares shipping costs across different carriers.
- **Cost Distribution by Transportation Mode:** Analyzes cost allocation across different transportation modes.
- **Defect Rate Analysis:** Investigates defect rates by product type and transportation mode.

## Setup and Installation

To run the analysis, you need to have Python installed along with the following packages:

```python
import pandas as pd
import plotly.express as px
import plotly.io as pio
import plotly.graph_objects as go
```

You can install the required packages using pip:

```bash
pip install pandas plotly openpyxl
```

## Data

The analysis is performed on a dataset stored in an Excel file. The file should be located at the following path:

```python
db = pd.read_excel(r"C:\Users\Pradyumn Sharma\Downloads\kaam\thoda\ml\supplychain\supply_chain_data.xlsx")
```

Make sure to adjust the file path according to your system's directory structure.

## Analysis and Visualizations

### 1. Descriptive Statistics
Provides a summary of the dataset.

```python
print(db.describe())
```

### 2. Product Type and Price Analysis
Analyzes the relationship between product prices and revenue generated.

```python
fig = px.scatter(db, x='Price', y='Revenue generated', color='Product type', hover_data=['Number of products sold'], trendline="ols")
fig.show()
```

### 3. Sales by Product Type
Visualizes sales distribution across different product types.

```python
sales_data = db.groupby('Product type')['Number of products sold'].sum().reset_index()
pie_chart = px.pie(sales_data, values='Number of products sold', names='Product type', title='Sales by Product Type', hole=0.5, color_discrete_sequence=px.colors.qualitative.Pastel)
pie_chart.show()
```

### 4. Total Revenue by Shipping Carrier
Analyzes revenue contributions from different shipping carriers.

```python
total_revenue = db.groupby('Shipping carriers')['Revenue generated'].sum().reset_index()
fig = go.Figure()
fig.add_trace(go.Bar(x=total_revenue['Shipping carriers'], y=total_revenue['Revenue generated']))
fig.update_layout(title='Total Revenue by Shipping Carrier', xaxis_title='Shipping Carrier', yaxis_title='Revenue Generated')
fig.show()
```

### 5. SKU Analysis
Explores Stock Keeping Units (SKUs) and their impact on revenue, stock levels, and order quantities.

```python
# Revenue generated by SKU
revenue_chart = px.line(db, x='SKU', y='Revenue generated', title='Revenue Generated by SKU')
revenue_chart.show()

# Stock Levels by SKU
stock_chart = px.line(db, x='SKU', y='Stock levels', title='Stock Levels by SKU')
stock_chart.show()

# Order Quantity by SKU
order_quantity_chart = px.bar(db, x='SKU', y='Order quantities', title='Order Quantity by SKU')
order_quantity_chart.show()
```

### 6. Shipping Costs
Compares shipping costs across different carriers.

```python
shipping_cost_chart = px.bar(db, x='Shipping carriers', y='Shipping costs', title='Shipping Costs by Carrier')
shipping_cost_chart.show()
```

### 7. Cost Distribution by Transportation Mode
Analyzes cost allocation across different transportation modes.

```python
transportation_chart = px.pie(db, values='Costs', names='Transportation modes', title='Cost Distribution by Transportation Mode', hole=0.5, color_discrete_sequence=px.colors.qualitative.Pastel)
transportation_chart.show()
```

### 8. Defect Rate Analysis
Investigates defect rates by product type and transportation mode.

```python
# Average Defect Rates by Product Type
defect_rates_by_product = db.groupby('Product type')['Defect rates'].mean().reset_index()
fig = px.bar(defect_rates_by_product, x='Product type', y='Defect rates', title='Average Defect Rates by Product Type')
fig.show()

# Defect Rates by Transportation Mode
pivot_table = pd.pivot_table(db, values='Defect rates', index=['Transportation modes'], aggfunc='mean')
transportation_chart = px.pie(values=pivot_table["Defect rates"], names=pivot_table.index, title='Defect Rates by Transportation Mode', hole=0.5, color_discrete_sequence=px.colors.qualitative.Pastel)
transportation_chart.show()
```

## Summary

This analysis provides insights into various components of a supply chain, helping to identify areas for improvement and opportunities to enhance overall efficiency and customer value.

