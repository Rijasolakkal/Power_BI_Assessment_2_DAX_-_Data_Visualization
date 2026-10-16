# Power_BI_Assessment_2_DAX_-_Data_Visualization
DAX &amp; Data Visualization 
# Power BI Assignment 2 – DAX & Data Visualization

## E-Commerce Sales Analysis

## Project Overview

This project analyzes e-commerce sales data using Microsoft Power BI. It focuses on DAX calculated columns, measures, data modelling, and visualizations to analyze sales performance, profitability, sales targets, and geographic trends.

## Objectives

- Create calculated columns using DAX.
- Create calculated measures to analyze sales and profit.
- Compare actual sales with sales targets.
- Analyze monthly sales trends.
- Visualize profit, quantity, and order counts.
- Explore geographic sales and sub-category sales distribution.

## Dataset

The assignment uses the following CSV files:

- `List of Orders.csv`
- `Order Details.csv`
- `Sales target.csv`

### Main Tables and Fields

| Table | Fields |
|---|---|
| List of Orders | Order ID, Order Date, CustomerName, City, State |
| Order Details | Order ID, Amount, Profit, Quantity, Category, Sub-Category |
| Sales target | Category, Month of Order Date, Target |

## Calculated Columns

### 1. Category Type

Combines Category and Sub-Category into one column.

```DAX
Category Type =
'Order Details'[Category] & " - " & 'Order Details'[Sub-Category]
```

### 2. Revenue per Order

Calculates Amount multiplied by Quantity.

```DAX
Revenue per Order =
'Order Details'[Amount] * 'Order Details'[Quantity]
```

### 3. Sales Category

Classifies each order as Above Average or Below Average based on Amount.

```DAX
Sales Category =
VAR AverageAmount =
    CALCULATE(
        AVERAGE('Order Details'[Amount]),
        ALL('Order Details')
    )
RETURN
    IF(
        'Order Details'[Amount] > AverageAmount,
        "Above Average",
        "Below Average"
    )
```

## 📐 Calculated Measures

### 1. Order Count

Counts order records in the Order Details table.

```DAX
Order Count =
COUNT('Order Details'[Order ID])
```

### 2. Average Profit in Delhi

Calculates the average profit for orders placed in Delhi.

```DAX
Average Profit in Delhi =
CALCULATE(
    AVERAGE('Order Details'[Profit]),
    'List of Orders'[City] = "Delhi"
)
```

### 3. YTD Sales

Calculates cumulative sales from the earliest order date through the current order date.

```DAX
YTD Sales =
CALCULATE(
    SUM('Order Details'[Amount]),
    FILTER(
        ALL('List of Orders'[Order Date]),
        'List of Orders'[Order Date]
            <= MAX('List of Orders'[Order Date])
    )
)
```

> Note: Verify that table names, relationships, and formulas match your Power BI model and assignment instructions.

## 📊 Data Visualizations

### 1. Sales Target Achievement by Category
- **Visual:** Clustered Column Chart
- **Purpose:** Compare actual sales with sales targets by category.

### 2. Max Profit Margin by Sub-Category
- **Visual:** Donut Chart
- **Purpose:** Display maximum profit margin by sub-category.
- **Validation:** Ensure the visual uses the required profit margin calculation and Maximum aggregation.

### 3. Monthly Sales Trend
- **Visual:** Line Chart
- **Purpose:** Analyze monthly changes in sales.

### 4. Profit and Quantity by Sub-Category
- **Visual:** Scatter Chart
- **Purpose:** Compare profit and quantity across sub-categories.

### 5. Total Sales Amount and Target
- **Visuals:** Card and Multi-row Card
- **Purpose:** Display total sales amount, total sales target, and minimum target for each segment.
- **Validation:** Confirm that the required Segment field is available in the dataset.

### 6. Sales Performance Matrix
- **Visual:** Matrix
- **Purpose:** Compare actual sales with targets across categories and months.
- **Validation:** Confirm that values respond correctly to category and month filters.

### 7. Geographic Sales Analysis
- **Visual:** Map
- **Purpose:** Display sales by city.

### 8. Sales Distribution by Sub-Category
- **Visual:** Treemap
- **Purpose:** Show sales distribution across sub-categories.

### 9. Order Count Analysis by State
- **Visual:** Funnel Chart
- **Purpose:** Compare order counts across states.

## 🔗 Data Modelling

The project uses three tables:

- `List of Orders`
- `Order Details`
- `Sales target`

The order tables should be related using `Order ID`. The Sales target table contains category and month information.

Check relationship cardinality and filter direction so actual sales and target values filter correctly. Avoid unintended many-to-many relationships.

## 🛠️ Tools Used

- Microsoft Power BI Desktop
- DAX (Data Analysis Expressions)
- CSV datasets
- Data modelling and relationships
- Data visualization

## 💡 Key Learning Outcomes

- Creating calculated columns and measures using DAX.
- Applying functions such as `IF`, `CALCULATE`, `AVERAGE`, `COUNT`, and `SUM`.
- Understanding relationships and filter context.
- Comparing actual sales with sales targets.
- Analyzing sales trends, profitability, and order counts.
- Creating and formatting Power BI visualizations.

## 📋 Assignment Checklist

### Calculated Columns
- [ ] Category Type
- [ ] Revenue per Order
- [ ] Sales Category

### Calculated Measures
- [ ] Order Count
- [ ] Average Profit in Delhi
- [ ] YTD Sales

### Visualizations
- [ ] Sales Target Achievement by Category — Clustered Column Chart
- [ ] Max Profit Margin by Sub-Category — Donut Chart
- [ ] Monthly Sales Trend — Line Chart
- [ ] Profit and Quantity by Sub-Category — Scatter Chart
- [ ] Total Sales Amount — Card
- [ ] Total Sales Target — Card
- [ ] Minimum Target for Each Segment — Multi-row Card
- [ ] Sales Performance Matrix
- [ ] Geographic Sales Analysis — Map
- [ ] Sales Distribution by Sub-Category — Treemap
- [ ] Order Count Analysis by State — Funnel Chart
