
# 📚 Library Management Database (SQL Project)

## 🧾 Project Overview

**Project Title:** Library Management Database  
**Level:** Beginner – Intermediate  
**Database:** `library_db` (PostgreSQL)  
**Tables:** librarians, students, books, book_issues, approvals, logs  
**Records per Table:** 1000+ rows

This SQL project simulates a real-world Library Management System that tracks student registrations, book issues, librarian approvals, and borrowing logs. It mirrors the kind of reporting, validation, and data insight work Business Analysts perform in operational and academic institutions.

---

## 🎯 Why This Project Matters

Libraries need proper systems to monitor inventory, prevent overdue issues, and track user activities. This project covers critical SQL skills such as:

- Data exploration and reporting  
- JOINs across multiple relational tables  
- Aggregation, grouping, and filtering  
- Data validation and anomaly detection  
- CASE logic and subqueries

The dataset mimics real-world scenarios where SQL is used to generate usage reports, analyze borrowing behavior, track overdue returns, and support librarian workflows.

---

## 🧩 Objectives

1. Create relational tables for books, students, librarians, and logs  
2. Simulate real-world operations like book issuance, return tracking, and approval workflows  
3. Perform real-life Business Analyst SQL tasks across 50+ query types  
4. Practice query writing for interviews and dashboards

---

## 🧱 Project Structure

- **Database Setup**
  - `librarians`: Stores librarian contact details
  - `students`: Registered students and their approval status
  - `books`: Catalog of available books with genres and stock count
  - `book_issues`: Transactions of issued/returned books
  - `approvals`: Manual approvals processed by librarians
  - `logs`: Record of book actions (issued/returned) by students

- **Sample Data**
  - 1000+ rows per table
  - Includes intentionally missing or invalid records (e.g. books never returned, students with no issues)

---

## 🧮 SQL Query Categories (53 Total)

| Category | Description | # Queries |
|---------|-------------|-----------|
| Data Exploration | Basic filtering and selections | 10 |
| JOINs | Multi-table relationships | 9 |
| Aggregation & Grouping | Summary stats and counts | 11 |
| Date Filtering | Time-based insights | 12 |
| Analytical | Top performers, frequent borrowers | 2 |
| Case, Subqueries & Validation | Data quality, logic-based labels | 9 |

Each query is available in the [📄 `library_sql_queries.md`](./library_sql_queries.md) file and tested against the PostgreSQL-compatible dataset.

---

## 📌 Sample Queries

✅ List all books in the 'Fiction' genre:
```sql
SELECT * FROM books WHERE genre = 'Fiction';
```

✅ Find overdue books not yet returned:
```sql
SELECT * FROM book_issues
WHERE return_date < CURRENT_DATE AND returned = 'false';
```

✅ Top 5 most issued books:
```sql
SELECT b.title, COUNT(*) AS times_issued
FROM book_issues bi
JOIN books b ON bi.book_id = b.book_id
GROUP BY b.title
ORDER BY times_issued DESC
LIMIT 5;
```

✅ Students with late returns (over 30 days):
```sql
SELECT s.student_id, s.name, b.return_date
FROM students s
JOIN book_issues b ON s.student_id = b.student_id
WHERE b.returned = 'true' AND b.return_date > b.issue_date + INTERVAL '30 days';
```

---

## 📂 Files Included

- `library_sql_queries.md` – Contains all 53 PostgreSQL queries grouped by category
- CSVs:
  - `books.csv`
  - `students.csv`
  - `librarians.csv`
  - `book_issues.csv`
  - `approvals.csv`
  - `logs.csv`

---

## 👩‍💻 About the Author

**Microsoft Certified Dynamics 365 professional**, Shayistha Abdulla is a Business Analyst with 9+ years of experience across Digital Marketing, CRM, PropTech, and IT Consulting.  
She builds practical SQL portfolio projects based on real-world business use cases to demonstrate hands-on data analysis and reporting skills.

---

## 🏁 Final Notes

This project is ideal for:
- Practicing SQL queries as a Business Analyst or Data Analyst
- Interview preparation with real-case scenarios
- Building a PostgreSQL-based SQL portfolio for GitHub

