## 📌 Overview
This repository contains the database design documentation and Entity Relationship Diagram (ERD) for **WitleShop (Pty) Ltd**, a South African online retailer selling electronics, clothing, and home appliances.

The document outlines the logical data model, including all entities, attributes, primary/foreign keys, relationships, and cardinalities required to manage customers, products, orders, payments, deliveries, and suppliers.

## 📂 Repository Contents
*   **`Kgomotso Shabane ERD.pdf`** – The full database design document containing the data dictionary, ERD (Crow's Foot notation), and business rules.

## 🗄️ Database Schema
The design consists of **nine entities**:

| # | Entity | Purpose | Type |
|---|---|---|---|
| 1 | **CUSTOMER** | Registered buyer | Strong |
| 2 | **ADDRESS** | Delivery address belonging to a customer | Dependent |
| 3 | **CATEGORY** | Product grouping (e.g., Electronics) | Strong |
| 4 | **SUPPLIER** | Company that supplies products | Strong |
| 5 | **PRODUCT** | Item for sale | Strong |
| 6 | **ORDERS** | Purchase by one customer (named ORDERS as ORDER is reserved) | Strong |
| 7 | **ORDER_ITEM** | Products contained in an order | Associative (Bridge) |
| 8 | **PAYMENT** | Payment for an order | Strong |
| 9 | **DELIVERY** | Delivery of an order | Strong |

## 🔗 Relationships & Cardinality
*   **1:M (Five relationships):** Customer to Address, Customer to Orders, Category to Product, Supplier to Product, Address to Delivery.
*   **1:1 (Two relationships):** Orders to Payment, Orders to Delivery (enforced by `UNIQUE` foreign keys).
*   **M:N (One relationship):** Orders to Product (resolved via the `ORDER_ITEM` bridge table).

## 🛠️ Key Design Decisions & Business Rules
*   **Keys:** All tables use system-generated integer IDs as primary keys. `ORDER_ITEM` uses a composite primary key (`order_id`, `product_id`) to prevent duplicate products on a single order.
*   **Registration First:** Every order must belong to a registered customer, and customer emails must be unique.
*   **One Payment & Delivery Per Order:** Enforced through `UNIQUE` foreign key constraints (`order_id`) in the `PAYMENT` and `DELIVERY` tables.
*   **Delivery Ownership:** The delivery address must belong to the customer who placed the order (checked via application logic or a database trigger).
*   **Price Integrity:** `unit_price` is stored in `ORDER_ITEM` so later price changes do not alter historical orders.
*   **Allowed Values:** Fixed lists for `order_status` (Pending, Shipped, Delivered, Cancelled) and `payment_method` (Card, EFT, PayFast).

## 🚀 How to Use
1. Clone this repository.
2. Open the PDF document to view the complete data dictionary, ERD, and detailed business rules.
