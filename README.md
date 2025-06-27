
# 📚 Library Management Database (SQL Project)

## 🧾 Project Overview

**Project Title:** Library Management Database  
**Level:** Beginner – Intermediate  
**Database:** `library_db` (PostgreSQL)  
**Tables:** librarians, students, books, book_issues, approvals, logs  
**Records per Table:** 1000+ rows

This SQL project simulates a real-world Library Management System that tracks student registrations, book issues, librarian approvals, and borrowing logs. It mirrors the kind of reporting, validation, and data insight work Business Analysts perform in operational and academic institutions.

## 🎯 Why This Project Matters

Libraries need proper systems to monitor inventory, prevent overdue issues, and track user activities. This project covers critical SQL skills such as:

- Data exploration and reporting  
- JOINs across multiple relational tables  
- Aggregation, grouping, and filtering  
- Data validation and anomaly detection  
- CASE logic and subqueries

The dataset mimics real-world scenarios where SQL is used to generate usage reports, analyze borrowing behavior, track overdue returns, and support librarian workflows.

## 🧩 Objectives

1. Create relational tables for books, students, librarians, and logs  
2. Simulate real-world operations like book issuance, return tracking, and approval workflows  
3. Perform real-life Business Analyst SQL tasks across 50+ query types  
4. Practice query writing for interviews and dashboards

## 🧱 Project Structure

- **Database Setup**
  - `librarians`: Stores librarian contact details
  - `students`: Registered students and their approval status
  - `books`: Catalog of available books with genres and stock count
  - `book_issues`: Transactions of issued/returned books
  - `approvals`: Manual approvals processed by librarians
  - `logs`: Record of book actions (issued/returned) by students

## 🧮 SQL Query Categories

Each query is available in the [📄 `library_sql_queries.md`](https://github.com/shayisthaabdulla/Library_Management_SQL_Project/blob/main/library_sql_queries.md) file and tested against the PostgreSQL-compatible dataset.

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

## 📂 Files Included

- `library_sql_queries.md` – Contains all 52 PostgreSQL queries grouped by category
- CSVs:
  - `books.csv`
  - `students.csv`
  - `librarians.csv`
  - `book_issues.csv`
  - `approvals.csv`
  - `logs.csv`
 
## 📊 Key Findings
- Fiction and Science are the most borrowed genres, while Philosophy and Drama see the least circulation.
- Over 15% of issued books were returned late; several students returned books more than 30 days past due.
- 10 students borrowed more than 8 books each, highlighting frequent borrowers.
- More than 20 book titles have fewer than 3 copies left, indicating stock replenishment needs.
- Librarian ID 3 processed the highest number of student approvals.
- Several approvals have missing or invalid statuses, suggesting potential workflow issues.
- About 18% of students registered on weekends, highlighting valuable weekend activity.
- At least 15% of books have never been issued; some students registered but never borrowed books.

## 📈 Suggested Reports
- **Monthly Book Issue Trends** – Visualize the number of books issued each month.
- **Top 10 Most Borrowed Books** – Identify books requiring restocking.
- **Inactive Students Report** – List of students who registered but never borrowed books.
- **Overdue Book Report** – Track students with unreturned or late books.
- **Approval Workflow Summary** – Number of approvals per librarian and their statuses.
- **Genre-Wise Circulation Report** – Number of issues per genre.
- **Low Stock Alert** – Books with fewer than 3 copies remaining.
- **Data Quality Check** – Approvals with invalid statuses, issues without matching students, or duplicate records. 

## 👩‍💻 About the Author

**Microsoft Certified Dynamics 365 professional**, Shayistha Abdulla is a Business Analyst with 9+ years of experience across Digital Marketing, CRM, PropTech, and IT Consulting.  
She builds practical SQL portfolio projects based on real-world business use cases to demonstrate hands-on data analysis and reporting skills.













