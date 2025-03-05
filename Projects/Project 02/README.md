# Library Management System (SQL Project)

## Introduction
The Library Management System is a database project designed to efficiently manage the records of a library, including books, members, and transactions. This project utilizes SQL to store, retrieve, and manage library data effectively.

## Features
- **Book Management:** Add, update, delete, and view book details.
- **Member Management:** Maintain records of library members.
- **Borrowing & Returning:** Track books issued and returned by members.
- **Fine Calculation:** Calculate overdue fines for late returns.
- **Admin Operations:** Manage the entire library system with SQL queries.

## Database Structure
The project includes the following tables:
1. **Branch** - Stores branch details of the library.
2. **Employees** - Contains information about library employees.
3. **Books** - Stores information about available books.
4. **Members** - Holds details of registered library members.
5. **Issued Status** - Logs book borrowing and return details.
6. **Fines** - Records overdue fine details.

## SQL File
The provided SQL file (`p2_library.sql`) contains:
- Table creation scripts.
- Insert statements with sample data.
- Queries for managing the system.

## Setup Instructions
1. Install MySQL or any SQL database management system.
2. Open your SQL client and create a new database:
   ```sql
   CREATE DATABASE LibraryDB;
   USE LibraryDB;
   ```
3. Import the `p2_library.sql` file:
   ```sql
   SOURCE path/to/p2_library.sql;
   ```
4. Run SQL queries to interact with the database.

## SQL Code
```sql
-- Creating Library Management System Database

-- Drop tables if they exist
DROP TABLE IF EXISTS branch;
CREATE TABLE branch (
    branch_id VARCHAR(20) PRIMARY KEY,
    manager_id VARCHAR(20),
    branch_address VARCHAR(50),
    contact_no VARCHAR(20)
);

DROP TABLE IF EXISTS employee;
CREATE TABLE employee (
    emp_id VARCHAR(20) PRIMARY KEY,
    emp_name VARCHAR(50),
    position VARCHAR(20),
    salary INT,
    branch_id VARCHAR(20) -- Foreign key
);

DROP TABLE IF EXISTS book;
CREATE TABLE book (
    isbn VARCHAR(20) PRIMARY KEY,
    book_title VARCHAR(75),
    category VARCHAR(30),
    rental_price FLOAT,
    status VARCHAR(10),
    author VARCHAR(30),
    publisher VARCHAR(30)
);

DROP TABLE IF EXISTS members;
CREATE TABLE members (
    member_id VARCHAR(30) PRIMARY KEY, -- Foreign key
    member_name VARCHAR(30),
    member_address VARCHAR(50),
    reg_date DATE
);

DROP TABLE IF EXISTS issued_status;
CREATE TABLE issued_status (
    issued_id VARCHAR(30) PRIMARY KEY,
    issued_member_id VARCHAR(30), -- Foreign key
    issued_book_name VARCHAR(50),
    issued_date DATE,
    return_date DATE
);

DROP TABLE IF EXISTS fines;
CREATE TABLE fines (
    fine_id VARCHAR(20) PRIMARY KEY,
    member_id VARCHAR(30), -- Foreign key
    amount FLOAT,
    status VARCHAR(10)
);

-- Sample Data Insertion
INSERT INTO branch VALUES ('B001', 'M001', 'Downtown Library', '1234567890');
INSERT INTO employee VALUES ('E001', 'John Doe', 'Librarian', 50000, 'B001');
INSERT INTO book VALUES ('ISBN001', 'Database Systems', 'Education', 10.99, 'Available', 'C.J. Date', 'Pearson');
INSERT INTO members VALUES ('M001', 'Alice Smith', '123 Elm St', '2023-01-10');
INSERT INTO issued_status VALUES ('I001', 'M001', 'Database Systems', '2024-02-01', '2024-02-15');
INSERT INTO fines VALUES ('F001', 'M001', 5.00, 'Unpaid');
```

## Usage
- Use `SELECT` queries to fetch book and member details.
- Use `INSERT` statements to add new books and members.
- Issue and return books using appropriate SQL transactions.
- Calculate fines using `JOIN` queries.

## Future Enhancements
- Implement a front-end interface.
- Add role-based authentication for admin and users.
- Automate overdue notifications.

Author
Rudresh P


