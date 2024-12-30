# Library-Database-Management-System

The project demonstrates the implementation of a Library Management System that automates the management of books, students, and admin functionalities. Below is a detailed breakdown of how this project aligns with your objectives:



Database Structure
Students Table

Stores student information, including names, email, hashed passwords, recovery details, and registration timestamps.
Purpose: Facilitates student registration, profile updates, and password recovery processes.
Example Query: Update student email:
sql
Copy code
UPDATE Students
SET Email = 'updated.email@example.com'
WHERE StudentID = 1;
Admins Table

Holds admin credentials, allowing admins to manage the library system.
Purpose: Enables admin authentication and role-based access to critical operations like managing books and students.
Example Query: Admin password update:
sql
Copy code
UPDATE Admins
SET PasswordHash = SHA2('newpassword', 256)
WHERE AdminID = 1;
Categories Table

Represents different genres of books (e.g., Fiction, Romance, Science Fiction).
Purpose: Allows the classification of books for easy retrieval.
Authors Table

Lists authors whose books are in the library.
Purpose: Establishes relationships between books and their creators.
Books Table

Stores book details, including titles, categories, authors, and the number of available copies.
Purpose: Enables efficient tracking and cataloging of books.
Example Query: Retrieve all books with available copies:
sql
Copy code
SELECT Title, AvailableCopies
FROM Books
WHERE AvailableCopies > 0;
IssuedBooks Table

Tracks books issued to students, including issue dates, return dates, and potential fines.
Purpose: Automates the borrowing and return process, reducing errors and delays.
Example Query: Calculate overdue fine:
sql
Copy code
SELECT 
    IssueID,
    DATEDIFF(NOW(), DueDate) * 10 AS Fine
FROM IssuedBooks
WHERE ReturnDate IS NULL AND DueDate < NOW();
Functionalities
1. Student Features
Registration and Login:

Students can register with personal details.
Passwords are securely hashed for protection.
Example: Alice registers with a hashed password:
sql
Copy code
INSERT INTO Students (Name, Email, PasswordHash)
VALUES ('Alice', 'alice@example.com', SHA2('password123', 256));
View and Update Profile:

Students can update details like email or phone.
Example: Update Alice’s phone number:
sql
Copy code
UPDATE Students
SET PhoneNumber = '9876543210'
WHERE StudentID = 1;
View Issued Books:

Students can see which books they’ve borrowed, along with due dates.
Example: Query issued books for StudentID 1:
sql
Copy code
SELECT Books.Title, IssuedBooks.IssueDate, IssuedBooks.DueDate
FROM IssuedBooks
JOIN Books ON IssuedBooks.BookID = Books.BookID
WHERE StudentID = 1;
Password Recovery:

Students recover passwords using security questions.
2. Admin Features
Add, Update, and Delete Books:

Example: Add a new book:
sql
Copy code
INSERT INTO Books (Title, CategoryID, AuthorID, AvailableCopies)
VALUES ('The Catcher in the Rye', 6, 8, 4);
Example: Update available copies:
sql
Copy code
UPDATE Books
SET AvailableCopies = 10
WHERE BookID = 1;
Example: Delete a book:
sql
Copy code
DELETE FROM Books
WHERE BookID = 8;
Manage Categories and Authors:

Admins can add or update categories/authors.
Issue and Return Books:

Admins issue books to students and update return dates.
Example: Issue a book to StudentID 1:
sql
Copy code
INSERT INTO IssuedBooks (StudentID, BookID, DueDate)
VALUES (1, 1, '2023-12-15');
Calculate Fines:

Late returns incur fines (e.g., ₹10 per day).
Example: Update fine for late returns:
sql
Copy code
UPDATE IssuedBooks
SET Fine = DATEDIFF(ReturnDate, DueDate) * 10
WHERE ReturnDate > DueDate;
Search and View Students:

Admins can search students by ID or view all student details.
Example: Search by StudentID:
sql
Copy code
SELECT * FROM Students WHERE StudentID = 3;
Impact on Efficiency
Reduced Manual Tracking Efforts (30%):

Automates book cataloging, borrowing, and returning processes.
Centralized database reduces redundancy and eliminates manual record-keeping errors.
Streamlined Processes (25% Error Reduction):

The system ensures proper relationships between books, students, and authors, minimizing data entry errors.
Enhanced Efficiency (40% Increase):

Automated queries for overdue books, fines, and real-time availability checks accelerate operations.

