SQL Playground & Query Portfolio (Chinook Database)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A structured collection of SQL queries and data manipulation workflows built using SQLite / SQLBud (chinook.db), 
covering text string transformations, conditional logic, datetime extraction, joins, aggregation, and filtering.

🚀 Features
📊 String Manipulation & Formatting: Demonstrates column concatenation, name formatting, and automatic email generation using lower() and upper() functions.   
🧮 Mathematical & Unit Conversion: Computes millisecond conversions to minutes and byte size conversions to megabytes with round().   
🔀 Conditional Logic: Implements CASE WHEN statements and COALESCE() to handle missing values and segment customers (Corporate vs. End Customer).   
📅 Datetime Extraction: Filters and groups dates using SQLite strftime() functions (Year, Month, Day, and MonthID).   
🔗 Relational Joins & Aggregations: Combines multiple related tables (artists, albums, tracks, genres, customers, invoices) using JOIN clauses and aggregate functions (AVG, SUM, MIN, MAX, COUNT, GROUP BY, HAVING).  
🔍 Advanced Filtering: Utilizes pattern matching (LIKE, wildcards _), logical operators (AND, OR, NOT, IN, BETWEEN), and randomized row sorting.   

🛠️ Tech StackDatabase: 
SQLite (Chinook Sample Database via SQLBud project file format)   
Language: SQL (Structured Query Language) 

⚙️ Getting Started
Prerequisites
To open and execute the queries contained within this project:
- Download or clone the repository containing the .sqlb project file and the chinook.db database.
- Open the file using an SQLite-compatible database management tool that supports the SQLBud project structure (such as SQLiteStudio, DB Browser for SQLite, or extension-based SQL environments).

Project Layout
The project contains pre-written queries categorized by functional logic:
- String Functions: Formatting names and emails (customers).   
- Calculated Columns: Unit conversions for track lengths and file sizes (tracks).   
- Conditional Rules: Data cleaning with COALESCE and CASE WHEN.   
- Date Functions: Time-series filtering by year and month (invoices).   
- Joins & Multi-table Queries: Linking artists, albums, and tracks.   
- Aggregations & Grouping: Statistical metrics grouped by genre and country (genres, customers).

📖 Usage Examples
Here are a few sample queries extracted from the project workflows:

1. Conditional Logic & Handling Null Values (COALESCE / CASE)
SELECT 
    Company,
    COALESCE(Company, 'End Customer') AS 'Company Clean',
    CASE 
        WHEN Company IS NULL THEN 'End Customer'
        ELSE 'Corporate'
    END AS 'Company Clean 2'
FROM customers;

2. Extracting Datetime Components
SELECT 
    InvoiceDate,
    strftime('%Y', InvoiceDate) AS Year,
    strftime('%m', InvoiceDate) AS Month,
    strftime('%d', InvoiceDate) AS Day,
    strftime('%Y-%m', InvoiceDate) AS MonthID
FROM invoices 
WHERE strftime('%Y', InvoiceDate) = '2010';

3. Aggregation with GROUP BY and HAVING
SELECT 
    genres.Name AS genre_name, 
    COUNT(*) AS count_song 
FROM genres 
JOIN tracks ON genres.GenreId = tracks.GenreId
GROUP BY genres.Name
HAVING COUNT(*) >= 100
ORDER BY count_song DESC;

