# 📊 Advanced DAX Sales Analysis (Power BI)

##  Project Overview

This project focuses on performing **data modeling and advanced DAX calculations** in Power BI without building a full dashboard. The objective is to develop a strong understanding of **data relationships, calculated columns, measures, and time intelligence functions**.

---

##  Objectives

* Build a **structured data model (Star Schema)**
* Perform **data transformation and calculations using DAX**
* Implement **Time Intelligence functions**
* Analyze **sales performance and trends**
* Practice **real-world business logic without visualization dependency**

---

##  Dataset Description

###  Fact Tables

* **Sales_Fact** — Contains transactional sales data (SalesAmount, Cost, Date, ProductID, CustomerID)
* **Returns_Fact** — Contains returned transactions (SalesID)

###  Dimension Tables

* **Customer_Dim** — Customer details
* **Product_Dim** — Product information
* **Date_Dim** — Calendar table for time-based analysis
* **Region_Dim** — Geographic details

---

##  Data Model

* Implemented a **Star Schema**
* Relationships:

  * Sales_Fact → Customer_Dim (CustomerID)
  * Sales_Fact → Product_Dim (ProductID)
  * Sales_Fact → Date_Dim (Date)
  * Sales_Fact → Region_Dim (RegionID)
  * Returns_Fact → Sales_Fact (SalesID)

✔ Ensures optimized performance and clean structure

---

##  Calculated Columns

```DAX
Profit = Sales_Fact[SalesAmount] - Sales_Fact[Cost]

Return Flag = 
IF(
    Sales_Fact[SalesID] IN VALUES(Returns_Fact[SalesID]),
    "Returned",
    "Not Returned"
)

Customer Name = Customer_Dim[FirstName] & " " & Customer_Dim[LastName]
```

---

##  Measures (DAX)

###  Core Metrics

```DAX
Total Sales = SUM(Sales_Fact[SalesAmount])
Total Cost = SUM(Sales_Fact[Cost])
Total Profit = SUM(Sales_Fact[Profit])
```

---

###  Performance Metrics

```DAX
Return Rate = 
DIVIDE(
    COUNT(Returns_Fact[SalesID]),
    COUNT(Sales_Fact[SalesID])
)

Avg Sales = 
DIVIDE(
    [Total Sales],
    DISTINCTCOUNT(Sales_Fact[SalesID])
)
```

---

##  Time Intelligence

### Month-to-Date (MTD)

```DAX
MTD Sales = TOTALMTD([Total Sales], Date_Dim[Date])
```

### Last Month Sales

```DAX
Last Month Sales = 
CALCULATE(
    [Total Sales],
    DATEADD(Date_Dim[Date], -1, MONTH)
)
```

---

##  Month-over-Month Analysis

```DAX
Last Month Sales = 
CALCULATE(
    [Total Sales],
    PREVIOUSMONTH(Date_Dim[Date])
)

Sales Difference = 
[Total Sales] - [Last Month Sales]

Sales Growth % = 
DIVIDE(
    [Sales Difference],
    [Last Month Sales]
)
```

---

##  Advanced DAX (Iterator Functions)

```DAX
Total Profit (X) = 
SUMX(
    Sales_Fact,
    Sales_Fact[SalesAmount] - Sales_Fact[Cost]
)

Avg Profit = 
AVERAGEX(
    Sales_Fact,
    Sales_Fact[SalesAmount] - Sales_Fact[Cost]
)
```

---

##  Key DAX Concepts Applied

* CALCULATE and filter context
* Aggregation functions (SUM, AVERAGE)
* Logical functions (IF, SWITCH)
* Time Intelligence functions
* Iterator functions (SUMX, AVERAGEX)
* Relationship-based functions (RELATED)

---

##  Important Considerations

* Use a **dedicated Date Table** for all time calculations
* Mark Date_Dim as **Date Table** in Power BI
* Prefer **Measures over Calculated Columns** for dynamic calculations
* Maintain **clean relationships** in the data model
* Use **DIVIDE() instead of /** to handle errors safely

---

##  Learning Outcomes

* Strong understanding of **Power BI data modeling**
* Ability to write and optimize **DAX calculations**
* Practical knowledge of **Time Intelligence functions**
* Experience in applying **business logic to raw data**

---

##  Conclusion

This project builds a solid foundation in **Power BI and DAX**, focusing on backend logic and analytical thinking rather than visualization. It prepares for real-world scenarios where **data modeling and calculation accuracy** are critical.

---

##  Author

**Nitesh Kumar**

---
