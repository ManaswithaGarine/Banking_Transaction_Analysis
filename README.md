
# 🏦 Bank System SQL Project

## 📌 Project Overview

This project implements a **basic banking database system using MySQL**.
It manages **customer information and transaction records** and demonstrates multiple SQL concepts used in real database systems.

The project is designed to practice and showcase:

* Database creation
* Table relationships
* SQL querying techniques
* Data analysis using SQL

It covers concepts like **filtering, sorting, aggregation, joins, window functions, and subqueries**.

---

# 🗄️ Database Setup

## Create Database

```sql
CREATE DATABASE bank_system;
USE bank_system;
```

This database stores all tables related to the banking system.

---

# 📋 Tables Used

## 1️⃣ Customers Table

Stores basic information about bank customers.

| Column   | Description                                      |
| -------- | ------------------------------------------------ |
| cus_id   | Unique customer ID (Primary Key, Auto Increment) |
| name     | Customer name                                    |
| email    | Customer email                                   |
| city     | Customer city                                    |
| acc_type | Account type (Savings / Current)                 |
| acc_bal  | Current account balance                          |

### Purpose

Maintains **customer account details**.

---

## 2️⃣ Transactions Table

Stores financial transactions performed by customers.

| Column   | Description                                           |
| -------- | ----------------------------------------------------- |
| tra_id   | Unique transaction ID                                 |
| cus_id   | Customer ID (Foreign Key referencing customers table) |
| amount   | Transaction amount                                    |
| tra_type | Type of transaction (credit / debit)                  |
| tra_mode | Mode of transaction (UPI, ATM, NEFT, IMPS)            |
| tra_date | Date and time of transaction                          |

### Purpose

Records **deposits, withdrawals, and other banking transactions**.

---

# 📥 Sample Data

Sample records are inserted into both tables to simulate **real banking operations**.

### Cities Used

* Hyderabad
* Delhi
* Mumbai
* Chennai
* Bangalore

### Transaction Modes

* UPI
* ATM
* NEFT
* IMPS

---

# 🔍 SQL Queries Explanation

## 1️⃣ View All Customers

```sql
SELECT * FROM customers;
```

Displays all customer records stored in the database.

---

## 2️⃣ View All Transactions

```sql
SELECT * FROM transactions;
```

Displays all transaction records in the system.

---

## 3️⃣ Customers With Balance Greater Than 1500

```sql
SELECT cus_id, name 
FROM customers 
WHERE acc_bal > 1500;
```

Retrieves customers whose account balance is greater than **1500**.

---

## 4️⃣ Sort Transactions by Date

```sql
SELECT * FROM transactions 
ORDER BY tra_date DESC;
```

Displays transactions sorted from **latest to oldest**.

---

## 5️⃣ Show Unique Transaction Modes

```sql
SELECT DISTINCT tra_mode 
FROM transactions;
```

Lists different transaction methods used in the system.

Example results:

```
UPI
ATM
NEFT
IMPS
```

---

## 6️⃣ Top 5 Transactions by Amount

```sql
SELECT * FROM transactions 
ORDER BY amount DESC 
LIMIT 5;
```

Retrieves the **five largest transactions**.

---

## 7️⃣ Customers Whose Name Starts With 'A'

```sql
SELECT * FROM customers 
WHERE name LIKE 'A%';
```

Filters customers whose names begin with the letter **A**.

Example:

* Alice
* Anjali
* Arjun

---

## 8️⃣ Total Transaction Amount Per Customer

```sql
SELECT cus_id, SUM(amount)
FROM transactions
GROUP BY cus_id;
```

Calculates the **total transaction amount for each customer**.

---

## 9️⃣ Customers With Total Transactions Greater Than 2000

```sql
SELECT cus_id, SUM(amount)
FROM transactions
GROUP BY cus_id
HAVING SUM(amount) > 2000;
```

Shows customers whose **total transaction amount exceeds 2000**.

Note:
`HAVING` is used because filtering happens **after aggregation**.

---

## 🔟 Join Customers and Transactions

```sql
SELECT c.name, t.amount, t.tra_type
FROM customers c
JOIN transactions t
ON c.cus_id = t.cus_id;
```

Combines **customer details with transaction records**.

Displays:

* Customer name
* Transaction amount
* Transaction type

---

## 1️⃣1️⃣ Running Total of Transactions

```sql
SELECT cus_id,
       amount,
       SUM(amount) OVER(PARTITION BY cus_id ORDER BY tra_date) AS running_total
FROM transactions;
```

Calculates a **running total of transactions** for each customer.

Concept used:

* Window Functions

---

## 1️⃣2️⃣ Rank Customers by Account Balance

```sql
SELECT name,
       acc_bal,
       DENSE_RANK() OVER(ORDER BY acc_bal DESC) AS rank_no
FROM customers;
```

Ranks customers based on their **account balance from highest to lowest**.

Concept used:

* Window ranking function (`DENSE_RANK`)

---

## 1️⃣3️⃣ Customers With Above-Average Transactions

```sql
SELECT cus_id
FROM transactions
GROUP BY cus_id
HAVING AVG(amount) > (
    SELECT AVG(amount) FROM transactions
);
```

Finds customers whose **average transaction amount is higher than the overall average**.

Concepts used:

* Subqueries
* Aggregation

---

# 🧠 SQL Concepts Demonstrated

This project demonstrates practical usage of:

* Database Creation
* Table Creation
* Primary Keys
* Foreign Keys
* Data Insertion
* Filtering (`WHERE`)
* Sorting (`ORDER BY`)
* Unique Values (`DISTINCT`)
* Aggregation (`SUM`, `AVG`)
* Grouping (`GROUP BY`)
* Filtering Aggregated Data (`HAVING`)
* Table Joins
* Window Functions
* Ranking Functions
* Subqueries

---

# ✅ Conclusion

This project simulates a **basic banking system database** and demonstrates how SQL can be used to:

* Manage customer records
* Track financial transactions
* Perform banking data analysis
* Generate insights using SQL queries

It provides a strong **foundation for database design and SQL analytics** used in real-world applications.

---
