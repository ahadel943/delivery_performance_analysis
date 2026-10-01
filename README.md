# **Delivery Performance Analysis**
## **One Question Projects — Project 04**

## **Project Overview**
Delivery performance is a critical operational metric for measuring how reliably orders reach customers within the expected delivery date. However, the way this performance is aggregated can affect how the overall operation is perceived.

This project examines delivery performance across multiple warehouses and compares unweighted and weighted On-Time Delivery (OTD) calculations to determine whether warehouse size and order volume materially affect the reported performance.

## **Business Problem**
Operations teams may evaluate warehouse delivery performance by calculating the average On-Time Delivery rate across warehouses. This approach gives each warehouse equal influence, regardless of how many orders it handles.

A small warehouse and a high-volume warehouse therefore contribute equally to the overall average, which may produce a different picture from a calculation based on the actual number of orders delivered on time.

The business needs to understand whether this difference is material enough to affect the interpretation of delivery performance.

## **Project Goal**
The goal of this analysis is to compare unweighted and weighted On-Time Delivery rates and determine how the aggregation method affects the reported delivery performance.

The analysis will answer one primary question:

> **Does the average warehouse OTD accurately represent overall delivery performance, or does order volume materially change the picture?**

## **Dataset Description**
**`delivery_performance.csv`**<br>
Contains order-level delivery performance information across multiple warehouses.

| Column                   | Description                                          |
| ------------------------ | ---------------------------------------------------- |
| `order_id`               | Unique identifier for each order                     |
| `warehouse_id`           | Identifier of the warehouse fulfilling the order     |
| `order_date`             | Date when the order was placed                       |
| `expected_delivery_date` | Date by which the order was expected to be delivered |
| `actual_delivery_date`   | Date when the order was actually delivered           |
| `units`                  | Number of units included in the order                |

## **Business Question**
### **How does On-Time Delivery (OTD) performance vary across warehouses and order sizes?**

## **Data Quality Check**
The initial data quality assessment identified the following issues:

| Issue               | Finding                             | Action                  | Reason                                                                                                                                                                       |
| ------------------- | ----------------------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Missing values      | 10 missing values in `warehouse_id` | Exclude affected rows   | `warehouse_id` is a key analytical dimension. Imputing the missing values would introduce an unverified warehouse assignment and could distort warehouse-level OTD analysis. |
| Exact duplicates    | 14 duplicate rows                   | Exclude duplicated rows | Exact duplicate records do not provide additional information and would artificially increase the number of orders.                                                          |
| Duplicate order IDs | 15 duplicated `order_id` values     | Exclude affected rows   | `order_id` is expected to uniquely identify an order. Keeping duplicated order records could lead to double-counting and unreliable OTD calculations.                        |
| `order_date > actual_delivery_date`   |0 |       | No actual delivery occurred before the order date |
| `order_date > expected_delivery_date` |0|       | No expected delivery date precedes the order date |


### **Data Cleaning Approach**
**Rows affected by the identified data quality issues will be excluded from the analytical dataset rather than modifying or imputing their values. The original dataset will be preserved, while the cleaned dataset will be used for subsequent EDA and analysis.**

