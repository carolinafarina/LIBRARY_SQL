# LIBRARY_SQL
General description
This database is designed to manage the operations of a library, including tracking books and lending to users. It facilitates the consultation of information about available books, active loans, and usage statistics by users.
Database Scheme
Tables and Relationships
Books

Book_ID (INT, primary key): Unique identifier for each book.
Titles (VARCHAR): Title of the book.
Author (VARCHAR): Author of the book.
Year (INT): Year of publication of the book.

Loans

Loan_ID (INT, primary key): Unique identifier for each loan.
Book_ID (INT, foreign key, reference to Books): Identifies the borrowed book.
User_ID (INT): Identifier of the user to whom the book has been lent.
DateLoan (DATE): Date on which the loan was made.
DateReturn (DATE): Date the book was returned.

User

User_ID (INT, primary key): Unique identifier for each user.
FirstName (VARCHAR): Name of the user.
LastName (VARCHAR): User's last name.
Addess(VARVHAR): user address

Important Queries
-- libros que no fueron prestados
--SELECT *
--FROM "books"
--JOIN "Loans" ON "books"."Book_ID" = "Loans"."Book_ID"
--WHERE "Loans"."DateReturn" IS NOT NULL;


-- libro más antiguo
--SELECT * from books order by "Year";

--préstamos por libro,
--SELECT "books"."Book_ID", "books"."Titles", COUNT("Loans"."Loan_ID") AS loan_count
--FROM "books"
--JOIN "Loans" ON "books"."Book_ID" = "Loans"."Book_ID"
--GROUP BY "books"."Book_ID"
--ORDER BY loan_count DESC;

-- libros  prestados en el último mes
--SELECT "books"."Titles"
--FROM "Loans"
--JOIN "books" ON "books"."Book_ID" = "Loans"."Book_ID"
--WHERE "Loans"."DateLoan" >= CURRENT_DATE - INTERVAL '1 month'
--ORDER BY "Loans"."DateLoan" DESC;


--Qué usuarios han realizado más préstamos
--select "User"."FirstName", count("Loans"."User_ID") as loans_count
--from "User"
--join "Loans" on "User"."User_ID" = "Loans"."User_ID"
--GROUP  by "User"."FirstName"
--ORDER BY loans_count DESC;

--libros que nunca han sido prestados
--SELECT "books"."Titles", "Loans"."DateLoan"
--from "books"
--join "Loans" on "books"."Book_ID" = "Loans"."Book_ID"
--WHERE "Loans"."DateLoan"= NULL
--ORDER BY "books","Titles"
