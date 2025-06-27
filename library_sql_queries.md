
# 📚 Library Management SQL Query Collection

A comprehensive collection of 52 SQL queries grouped by category, written for a PostgreSQL-based Library Management System. These queries are designed to demonstrate Business Analyst-level use cases.

## 🧭 1. Data Exploration Queries

1. Students who registered in 2025
```sql
SELECT * FROM students WHERE registered_date >= '2025-01-01';
```

2. Books in the 'Science' genre
```sql
SELECT * FROM books WHERE genre = 'Science';
```

3. All librarians and their emails
```sql
SELECT name, email FROM librarians;
```

4. Books published before 2000
```sql
SELECT title FROM books WHERE published_year < 2000;
```

5. Genres available in the library
```sql
SELECT genre, COUNT(*) AS count_per_genre FROM books GROUP BY genre;
```

6. Students approved by librarian ID 5
```sql
SELECT * FROM students WHERE approved_by = 5;
```

7. Books with fewer than 3 copies available
```sql
SELECT book_id, title, copies_available FROM books WHERE copies_available < 3;
```

8. Earliest registered student
```sql
SELECT * FROM students ORDER BY registered_date LIMIT 1;
```

9. Students ordered by registration date
```sql
SELECT * FROM students ORDER BY registered_date;
```

10. Student registrations by year
```sql
SELECT EXTRACT(YEAR FROM registered_date) AS year, COUNT(*) AS total_students
FROM students GROUP BY year ORDER BY year;
```

## 🔗 2. JOIN Queries

11. Student names with issued book titles
```sql
SELECT s.name AS student_name, b.title AS book_title
FROM book_issues AS bi
JOIN students AS s ON bi.student_id = s.student_id
JOIN books AS b ON bi.book_id = b.book_id;
```

12. Approvals with processing librarian name
```sql
SELECT a.approval_id, a.approval_type, a.status, l.name AS processed_by
FROM approvals AS a
JOIN librarians AS l ON a.processed_by = l.librarian_id;
```

13. Books and their issue status
```sql
SELECT b.book_id, b.title, bi.issue_id, bi.returned
FROM books b
JOIN book_issues bi ON b.book_id = bi.book_id;
```

14. Logs with book and student details
```sql
SELECT b.title, s.name AS student_name, l.log_id, l.action
FROM logs AS l
JOIN students AS s ON l.student_id = s.student_id
JOIN books AS b ON l.book_id = b.book_id;
```

15. Approval requests with student names
```sql
SELECT a.approval_id, s.name AS student_name, a.approval_type, a.status, a.request_date
FROM approvals AS a
JOIN students AS s ON a.student_id = s.student_id;
```

16. Student approval request history
```sql
SELECT s.name AS student_name, a.approval_type, a.request_date, a.status, a.processed_by
FROM approvals AS a
JOIN students AS s ON a.student_id = s.student_id
ORDER BY s.name, a.request_date;
```

17. Books issued by students approved by librarian 3
```sql
SELECT s.name AS student_name, b.title AS book_title
FROM students s
JOIN book_issues bi ON s.student_id = bi.student_id
JOIN books b ON bi.book_id = b.book_id
WHERE s.approved_by = 3;
```

18. Book issues joined with librarian approval
```sql
SELECT bi.issue_id, s.name AS student_name, l.name AS approving_librarian,
       b.title AS book_title, bi.issue_date, bi.return_date
FROM book_issues bi
JOIN students s ON bi.student_id = s.student_id
JOIN librarians l ON s.approved_by = l.librarian_id
JOIN books b ON bi.book_id = b.book_id;
```

19. Logs involving books in the 'Fiction' genre
```sql
SELECT l.log_id, s.name AS student_name, b.title AS book_title, l.action, l.timestamp
FROM logs l
JOIN books b ON l.book_id = b.book_id
JOIN students s ON l.student_id = s.student_id
WHERE b.genre = 'Fiction';
```

20. Students who never returned books
```sql
SELECT DISTINCT s.name
FROM students s
JOIN book_issues bi ON s.student_id = bi.student_id
WHERE bi.returned = 'false';
```


---

## 📊 3. Aggregation & Grouping

21. Count of books per genre
```sql
SELECT genre, COUNT(*) AS total_books FROM books GROUP BY genre;
```

22. Students approved by each librarian
```sql
SELECT approved_by AS approved_librarian, COUNT(*) AS total_students FROM students GROUP BY approved_by;
```

23. Issues per month
```sql
SELECT DATE_TRUNC('MONTH', issue_date) AS month, COUNT(*) AS issue_count
FROM book_issues
GROUP BY month
ORDER BY month;
```

24. Average number of copies per book
```sql
SELECT AVG(copies_available) AS avg_copies FROM books;
```

25. Average delay in book returns
```sql
SELECT AVG(return_date - issue_date) AS avg_delay_days FROM book_issues WHERE returned = 'true';
```

26. Total books issued
```sql
SELECT COUNT(*) AS total_issues FROM book_issues;
```

27. Number of unique students who borrowed books
```sql
SELECT COUNT(DISTINCT student_id) AS unique_borrowers FROM book_issues;
```

28. Count books not returned
```sql
SELECT COUNT(*) AS not_returned FROM book_issues WHERE returned = 'false';
```

29. Count of returned books
```sql
SELECT COUNT(*) AS returned_books FROM book_issues WHERE returned = 'true';
```

30. Students with the most approvals
```sql
SELECT student_id, COUNT(*) AS approval FROM approvals GROUP BY student_id ORDER BY approval DESC;
```

---

## 📆 4. Date-Based & Filtering Queries

31. Books issued in the last 60 days
```sql
SELECT * FROM book_issues WHERE issue_date >= CURRENT_DATE - INTERVAL '60 days';
```

32. Students registered more than 1 year ago
```sql
SELECT * FROM students WHERE registered_date < CURRENT_DATE - INTERVAL '1 year';
```

33. Approvals requested in the last 30 days
```sql
SELECT * FROM approvals WHERE request_date >= CURRENT_DATE - INTERVAL '30 days';
```

34. Books issued in 2024
```sql
SELECT * FROM book_issues WHERE EXTRACT(YEAR FROM issue_date) = 2024;
```

35. Students registered before Jan 1, 2024
```sql
SELECT * FROM students WHERE registered_date < '2024-01-01';
```

36. Books with more than 5 copies and published after 2010
```sql
SELECT * FROM books WHERE published_year > 2010 AND copies_available > 5;
```

37. Logs of returned books
```sql
SELECT * FROM logs WHERE action = 'Returned';
```

38. Overdue books (return date is in the past but not returned)
```sql
SELECT * FROM book_issues WHERE return_date < CURRENT_DATE AND returned = 'false';
```

39. Students who registered but never issued books
```sql
SELECT * FROM students WHERE student_id NOT IN (SELECT DISTINCT student_id FROM book_issues);
```

40. Students with more than 2 approvals
```sql
SELECT student_id, COUNT(*) AS approval_count FROM approvals GROUP BY student_id HAVING COUNT(*) > 2;
```

41. Books issued in the last 7 days
```sql
SELECT * FROM book_issues WHERE issue_date >= CURRENT_DATE - INTERVAL '7 days';
```

42. Students registered on a weekend
```sql
SELECT * FROM students WHERE EXTRACT(DOW FROM registered_date) IN (0, 6);
```

---

## 📈 5. Analytical Queries

43. Top 5 most issued books
```sql
SELECT b.title, COUNT(*) AS times_issued
FROM book_issues bi
JOIN books b ON bi.book_id = b.book_id
GROUP BY b.title
ORDER BY times_issued DESC
LIMIT 5;
```

44. Students with more than 3 book issues
```sql
SELECT student_id, COUNT(*) AS issue_count
FROM book_issues
GROUP BY student_id
HAVING COUNT(*) > 3;
```

---

## 🔍 6. Case, Subqueries, Data Validation

45. Book issue records without matching students
```sql
SELECT * FROM book_issues WHERE student_id NOT IN (SELECT student_id FROM students);
```

46. Approvals with invalid status
```sql
SELECT * FROM approvals WHERE status NOT IN ('Approved', 'Pending', 'Rejected');
```

47. Label issues as 'Returned' or 'Pending' using CASE
```sql
SELECT issue_id, student_id, book_id,
  CASE
    WHEN returned = 'true' THEN 'Returned'
    ELSE 'Pending'
  END AS return_status
FROM book_issues;
```

48. Students with both approvals and book issues
```sql
SELECT DISTINCT s.student_id, s.name
FROM students s
WHERE s.student_id IN (SELECT student_id FROM approvals)
  AND s.student_id IN (SELECT student_id FROM book_issues);
```

49. Duplicate email addresses
```sql
SELECT email, COUNT(*) FROM students GROUP BY email HAVING COUNT(*) > 1;
```

50. Books never issued
```sql
SELECT * FROM books WHERE book_id NOT IN (SELECT DISTINCT book_id FROM book_issues);
```

51. Students who returned books late (more than 30 days)
```sql
SELECT s.student_id, s.name, b.return_date
FROM students AS s
JOIN book_issues AS b ON s.student_id = b.student_id
WHERE b.returned = 'true' AND b.return_date > b.issue_date + INTERVAL '30 days';
```

52. Books issued by more than 10 unique students
```sql
SELECT book_id FROM book_issues GROUP BY book_id HAVING COUNT(DISTINCT student_id) > 10;
```

