# SQL Basics — Introduction

## Why Databases Matter in Cybersecurity

Databases are ubiquitous( everywhere at once) in security — you will rely on
them no matter what area of security you work in.

| Side | Use Case |
|------|----------|
| **Offensive** | Understand SQL injections, tamper/retrieve data from compromised services |
| **Defensive** | Navigate databases, find suspicious activity, implement access restrictions |
| **General** | Web app security, SOC/SIEM work, authentication, malware analysis tools |

---

# SQL Basics — Introducing Databases, Keys & Relationships

## What is a Database?
An organised collection of structured information that is
easily accessible and can be manipulated or analysed.

**Real world examples:**
- User auth data (usernames/passwords) — login systems
- User posts, comments, likes — social media
- Watch history, recommendations — Netflix/streaming

---

## Types of Databases

### Relational Databases
- Stores **structured data** in rows and columns (tables)
- Data follows a fixed structure e.g. `first_name, last_name, email, username, password`
- **Relationships** can be made between tables e.g. `users` ↔ `order_history`

### Non-Relational Databases
- Stores data in **non-tabular format**
- Used when data varies in type/quantity e.g. scanned documents

```json
{
    _id: ObjectId("4556712cd2b2397ce1b47661"),
    name: { first: "Thomas", last: "Anderson" },
    date_of_birth: new Date('Sep 2, 1964'),
    occupation: ["The One"],
    steps_taken: NumberLong(4738947387743977493)
}
```

---

## Primary & Foreign Keys

### Primary Key
- Ensures each record in a table is **uniquely identifiable**
- No two rows can have the same primary key value
- Only **one** primary key per table
- Example: `id` column in a Books table

### Foreign Key
- A column that **exists in another table** — creates a link between tables
- Can have **more than one** foreign key in a table
- Example: `author_id` in Books table links to `id` in Authors table

### Visual Example
```
Books Table                    Authors Table
───────────────                ──────────────
id  (Primary Key)              id  (Primary Key)
title                          name
author_id (Foreign Key) ──────► id
publication_date               nationality
```

---

# SQL Basics — What is SQL & Database Statements

## What is SQL?

**Structured Query Language** — used to interact with databases
through a **DBMS (Database Management System)**.

> DBMS = software interface between the user and the database

**Common DBMS examples:**
- MySQL
- MongoDB
- Oracle Database
- MariaDB

---

## Core Database Statements

### CREATE DATABASE — Create a new database
```sql
CREATE DATABASE database_name;

-- Example
CREATE DATABASE thm_bookmarket_db;
```

### SHOW DATABASES — List all databases
```sql
SHOW DATABASES;
```
> Returns your created databases + default system databases
> (`mysql`, `information_schema`, `performance_schema`, `sys`)

### USE — Select active database
```sql
USE thm_bookmarket_db;
```
> Must run this before running any queries — tells MySQL which database to run against

### DROP DATABASE — Delete a database
```sql
DROP DATABASE database_name;
```
> Permanently deletes the database and all its data

---

# SQL Basics — Table Statements

## CREATE TABLE
```sql
CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```

**Column breakdown:**

| Column | Data Type | Constraints | Meaning |
|--------|-----------|-------------|---------|
| `book_id` | `INT` | `AUTO_INCREMENT PRIMARY KEY` | Auto-numbered unique ID |
| `book_name` | `VARCHAR(255)` | `NOT NULL` | Text up to 255 chars, can't be empty |
| `publication_date` | `DATE` | — | Date format |

---

## SHOW TABLES — List all tables
```sql
SHOW TABLES;
```

## DESCRIBE — View table structure
```sql
DESCRIBE book_inventory;
-- or
DESC book_inventory;
```
**Output:**
```
+------------------+--------------+------+-----+---------+----------------+
| Field            | Type         | Null | Key | Default | Extra          |
+------------------+--------------+------+-----+---------+----------------+
| book_id          | int          | NO   | PRI | NULL    | auto_increment |
| book_name        | varchar(255) | NO   |     | NULL    |                |
| publication_date | date         | YES  |     | NULL    |                |
+------------------+--------------+------+-----+---------+----------------+
```

## ALTER — Modify existing table
```sql
-- Add a column
ALTER TABLE book_inventory
ADD page_count INT;
```
> Also used to rename columns, change data types, or remove columns

## DROP TABLE — Delete a table
```sql
DROP TABLE table_name;
```
> Permanently deletes table and all its data

---

# SQL Basics — CRUD Operations

**CRUD** = Create, Read, Update, Delete — the four basic
data management operations.

---

## Create — INSERT
```sql
INSERT INTO books (id, name, published_date, description)
VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
```

---

## Read — SELECT
```sql
-- All columns
SELECT * FROM books;

-- Specific columns
SELECT name, description FROM books;
```

---

## Update — UPDATE
```sql
UPDATE books
SET description = "An In-Depth Guide to Android's Security Architecture."
WHERE id = 1;
```
> Always use `WHERE` — without it, ALL rows get updated

---

## Delete — DELETE
```sql
DELETE FROM books WHERE id = 1;
```
> Always use `WHERE` — without it, ALL rows get deleted

---

# SQL Basics — Clauses

A **clause** specifies criteria for data being retrieved or sorted.

---

## DISTINCT — Remove duplicates
```sql
SELECT DISTINCT name FROM books;
```
> Returns only unique values — filters out duplicate rows

---

## GROUP BY — Aggregate & group results
```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name;
```
> Groups rows with same value — useful with aggregate functions
> like `COUNT()`, `SUM()`, `AVG()`

---

## ORDER BY — Sort results
```sql
-- Ascending (oldest first)
SELECT * FROM books ORDER BY published_date ASC;

-- Descending (newest first)
SELECT * FROM books ORDER BY published_date DESC;
```

---

## HAVING — Filter after grouping
```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name
HAVING name LIKE '%Hack%';
```
> Used with `GROUP BY` — filters **after** aggregation
> Unlike `WHERE` which filters **before** aggregation

---

## WHERE vs HAVING

| | `WHERE` | `HAVING` |
|---|---------|---------|
| Filters | Individual rows | Grouped results |
| Used with | Any query | `GROUP BY` |
| Runs | Before aggregation | After aggregation |

---
# SQL Basics — Operators

---

## Logical Operators

### LIKE — Pattern matching
```sql
SELECT * FROM books WHERE description LIKE "%guide%";
```
> `%` = wildcard (any characters before/after)

### AND — All conditions must be true
```sql
SELECT * FROM books
WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";
```

### OR — At least one condition must be true
```sql
SELECT * FROM books
WHERE name LIKE "%Android%" OR name LIKE "%iOS%";
```

### NOT — Exclude a condition
```sql
SELECT * FROM books WHERE NOT description LIKE "%guide%";
```

### BETWEEN — Value within a range
```sql
SELECT * FROM books WHERE id BETWEEN 2 AND 4;
```

---

## Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `=` | Equal to | `WHERE name = "Ethical Hacking"` |
| `!=` | Not equal to | `WHERE category != "Offensive Security"` |
| `<` | Less than | `WHERE published_date < "2020-01-01"` |
| `>` | Greater than | `WHERE published_date > "2020-01-01"` |
| `<=` | Less than or equal | `WHERE published_date <= "2021-11-15"` |
| `>=` | Greater than or equal | `WHERE published_date >= "2021-11-02"` |

---

# SQL Basics — Functions

---

## String Functions
> Work on text/string values in columns

---

### CONCAT() — Glue strings together
Think of it like joining words into one sentence.

```sql
SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info
FROM books;
```
```
+------------------------------------------------------------------+
| book_info                                                        |
+------------------------------------------------------------------+
| Android Security Internals is a type of Defensive Security book.|
| Bug Bounty Bootcamp is a type of Offensive Security book.        |
| Car Hacker's Handbook is a type of Offensive Security book.      |
| Designing Secure Software is a type of Defensive Security book.  |
| Ethical Hacking is a type of Offensive Security book.            |
+------------------------------------------------------------------+
```
> Takes `name` + your custom text + `category` and
> combines them into one readable sentence per row

---

### GROUP_CONCAT() — Merge multiple rows into ONE cell
Instead of showing each book on its own row,
it groups them together in one cell separated by commas.

```sql
SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
FROM books
GROUP BY category;
```
```
+--------------------+-------------------------------------------------------------+
| category           | books                                                       |
+--------------------+-------------------------------------------------------------+
| Defensive Security | Android Security Internals, Designing Secure Software       |
| Offensive Security | Bug Bounty Bootcamp, Car Hacker's Handbook, Ethical Hacking |
+--------------------+-------------------------------------------------------------+
```
> Instead of 5 rows, we get 2 rows — one per category
> with all book names joined together by ", "

---

### SUBSTRING() — Cut out part of a string
Like cutting a specific piece from a word or date.
You tell it WHERE to start and HOW MANY characters to take.

```sql
-- Start at position 1, take 4 characters = just the year
SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
```
```
+----------------+
| published_year |
+----------------+
| 2014           |
| 2021           |
| 2016           |
| 2021           |
| 2021           |
+----------------+
```
> `published_date` stores `2014-10-14`
> `SUBSTRING(published_date, 1, 4)` extracts just `2014`

---

### LENGTH() — Count how many characters in a string
Like counting letters in a word — includes spaces too.

```sql
SELECT LENGTH(name) AS name_length FROM books;
```
```
+-------------+
| name_length |
+-------------+
|          26 |  ← "Android Security Internals" = 26 chars
|          19 |  ← "Bug Bounty Bootcamp" = 19 chars
|          21 |  ← "Car Hacker's Handbook" = 21 chars
|          25 |  ← "Designing Secure Software" = 25 chars
|          15 |  ← "Ethical Hacking" = 15 chars
+-------------+
```

---

## Aggregate Functions
> Work across MULTIPLE rows and return ONE result

---

### COUNT() — Count total number of rows
Like counting how many items are in a list.

```sql
SELECT COUNT(*) AS total_books FROM books;
```
```
+-------------+
| total_books |
+-------------+
|           5 |   ← there are 5 books in the table
+-------------+
```
> `*` means count ALL rows regardless of content

---

### SUM() — Add up all values in a column
Like using a calculator to total up all prices.

```sql
SELECT SUM(price) AS total_price FROM books;
```
```
+-------------+
| total_price |
+-------------+
|      249.95 |   ← all book prices added together
+-------------+
```
> Ignores NULL values automatically

---

### MAX() — Find the biggest/latest value
Like finding the most recent date or highest score.

```sql
SELECT MAX(published_date) AS latest_book FROM books;
```
```
+-------------+
| latest_book |
+-------------+
| 2021-12-21  |   ← most recently published book
+-------------+
```

---

### MIN() — Find the smallest/earliest value
Opposite of MAX — finds the lowest value.

```sql
SELECT MIN(published_date) AS earliest_book FROM books;
```
```
+---------------+
| earliest_book |
+---------------+
| 2014-10-14    |   ← oldest published book
+---------------+
```

---

## Quick Reference

| Function | Type | Purpose | Simple Analogy |
|----------|------|---------|----------------|
| `CONCAT()` | String | Join strings | Glue words together |
| `GROUP_CONCAT()` | String | Merge rows into one | Combine a list into one line |
| `SUBSTRING()` | String | Extract part of string | Cut a piece out |
| `LENGTH()` | String | Count characters | Count letters |
| `COUNT()` | Aggregate | Count rows | How many items? |
| `SUM()` | Aggregate | Total of values | Add everything up |
| `MAX()` | Aggregate | Highest value | What's the biggest? |
| `MIN()` | Aggregate | Lowest value | What's the smallest? |

---
