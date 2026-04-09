# Banking_Transaction_Analysis
Bank System SQL Project
Project Overview

This project demonstrates the implementation of a simple banking database system using MySQL.
It includes tables for customers and transactions, sample data insertion, and multiple SQL queries that analyze customer accounts and transaction activities.

The goal of this project is to practice core SQL concepts such as:

Database creation
Table relationships using foreign keys
Data insertion
Filtering and sorting data
Aggregation functions
Joins
Window functions
Subqueries
Database Structure
1. Database Creation

A database named bank_system is created to store all banking related tables.

CREATE DATABASE bank_system;
USE bank_system;
Tables
1. Customers Table

Stores information about bank customers.

Column	Description
cus_id	Unique ID for each customer (Primary Key, Auto Increment)
name	Customer name
email	Customer email address
city	City where the customer lives
acc_type	Type of account (Savings / Current)
acc_bal	Current account balance

Purpose:

Maintains customer account information.
2. Transactions Table

Stores all financial transactions performed by customers.

Column	Description
tra_id	Unique transaction ID
cus_id	Customer ID (Foreign Key referencing customers table)
amount	Transaction amount
tra_type	Transaction type (credit / debit)
tra_mode	Transaction method (UPI, ATM, NEFT, IMPS)
tra_date	Date and time of transaction

Purpose:

Records every financial activity linked to customers.
Insert Sample Data

Sample records are inserted into both tables to simulate real banking operations such as deposits and withdrawals.

Customers include people from cities like:

Hyderabad
Delhi
Mumbai
Chennai
Bangalore

Transactions include payment modes such as:

UPI
ATM
NEFT
IMPS
SQL Queries Explanation
1. View All Customers
SELECT * FROM customers;

Displays all customer records stored in the database.

2. View All Transactions
SELECT * FROM transactions;

Shows the complete transaction history of all customers.

3. Customers With Balance Greater Than 1500
SELECT cus_id, name FROM customers WHERE acc_bal > 1500;

Purpose:

Retrieves customers whose account balance exceeds 1500.

Use Case:

Identifying high balance customers.
4. Transactions Sorted by Date
SELECT * FROM transactions ORDER BY tra_date DESC;

Purpose:

Displays transactions from most recent to oldest.

Use Case:

Viewing latest transaction activity.
5. Unique Transaction Modes
SELECT DISTINCT tra_mode FROM transactions;

Purpose:

Lists unique payment methods used by customers.

Expected Results:

UPI
ATM
NEFT
IMPS
6. Top 5 Transactions by Amount
SELECT * FROM transactions ORDER BY amount DESC LIMIT 5;

Purpose:

Retrieves the five largest transactions.

Use Case:

Detecting large deposits or withdrawals.
7. Customers Whose Name Starts With "A"
SELECT * FROM customers WHERE name LIKE 'A%';

Purpose:

Filters customers whose names begin with the letter A.

Examples:

Alice
Anjali
Arjun
8. Total Transaction Amount Per Customer
SELECT cus_id, SUM(amount) FROM transactions GROUP BY cus_id;

Purpose:

Calculates the total transaction amount for each customer.

Use Case:

Understanding customer transaction volume.
9. Customers With Total Transactions Above 2000
SELECT cus_id, SUM(amount)
FROM transactions
GROUP BY cus_id
HAVING SUM(amount) > 2000;

Purpose:

Shows customers whose total transaction amount exceeds 2000.

Difference:

HAVING is used because aggregation is involved.
10. Join Customers and Transactions
SELECT c.name, t.amount, t.tra_type
FROM customers c
JOIN transactions t ON c.cus_id = t.cus_id;

Purpose:

Combines customer data with transaction details.

Output Includes:

Customer name
Transaction amount
Transaction type
11. Running Total of Transactions
SELECT cus_id, amount,
SUM(amount) OVER (PARTITION BY cus_id ORDER BY tra_date) AS running_total
FROM transactions;

Purpose:

Calculates cumulative transaction totals per customer.

Concept Used:

Window Functions

Use Case:

Tracking how transaction amounts accumulate over time.
12. Rank Customers by Account Balance
SELECT name, acc_bal,
DENSE_RANK() OVER (ORDER BY acc_bal DESC) AS rank_no
FROM customers;

Purpose:

Ranks customers based on account balance.

Concept Used:

Window Ranking Function

Difference:

DENSE_RANK does not skip rank numbers when ties occur.
13. Customers With Above Average Transactions
SELECT cus_id
FROM transactions
GROUP BY cus_id
HAVING AVG(amount) >
      (SELECT AVG(amount) FROM transactions);

Purpose:

Finds customers whose average transaction amount is greater than the overall average.

Concepts Used:

Aggregation
Subquery
SQL Concepts Used

This project demonstrates practical usage of:

CREATE DATABASE
CREATE TABLE
PRIMARY KEY
FOREIGN KEY
INSERT
SELECT
WHERE
ORDER BY
DISTINCT
LIMIT
GROUP BY
HAVING
JOIN
WINDOW FUNCTIONS
SUBQUERIES
Conclusion

This project simulates a basic banking transaction system and demonstrates how SQL can be used to:

Manage customer data
Track financial transactions
Perform analytical queries
Generate insights from banking data

It provides a strong foundation for learning database design and SQL analytics.
