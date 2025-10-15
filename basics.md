# Basics

Content Table

- [Data, information and knowledge](#difference-between-data-information-and-knowledge)
- [Data Structure VS. Data Base](#data-structure-vs-data-base)
- [What is NULL](#what-is-null)
- [Primary Key / Foreign Key](#primary-key--foreign-key)
- [Redundancy](#redundancy)
- [Data Integrity](#data-integrity)
- [Constraints](#constraints)
- [What is SQL](#what-is-sql)
- [DBMS Vs. RDBMS](#dbms-vs-rdbms)

## Difference Between Data, Information and Knowledge

**Data**: The row things we know about something but we can't use it in useful way

**Information**: Data has been processed and organized to a way that makes it useful of something like knowing if the company is doing a good job or not

**Knowledge**: is a higher level of understanding that goes beyond information. It is the result of assimilating, interpreting, and contextualizing information in a way that allows for the recognition of patterns, relationships, and connections. Knowledge involves not only understanding “what” and “how” but also “why.”

## Data Structure Vs. Data Base

**Data Structure**: The way we organize the data inside the RAM while runtime using famous data structures such as linked lists, Trees, Arrays...

**Data Base**: It's a collection of data that stored in long term memory as tables consist from rows and columns with relations between them

---

## What Is NULL

**NULL**: In database context it represent the absence of a value in table column

---

## Primary Key / Foreign Key

**Primary Key (PK)**: Column or set of columns that uniquely identify the record from any other record even if they both have the same data,Each table in the DB must have a primary key and it can't be null

**Foreign Key (FK)**: Column that contains the value of another table's primary key so it can refers to that table, It enables us to make relationships between the tables

---

## Redundancy

Mean that the same data exists more than one time which can lead to integrity issues

Redundant data takes more space, And it can make the maintain process harder and inconsistent

To avoid redundancy we apply normalization to the data

**Normalization**: The process of organizing the data in the that reduces the redundancy

---

## Data Integrity

It refers to the accuracy, Consistency, And reliability on the data we have

To Keep integration we have to apply policies and procedures and apply appropriate technology techniques such as backups and encryption

Types of integration

- Entity: Ensure that each row is unique this can be achieved using [primary keys](#primary-key--foreign-key)
- Referential: Ensure all the relationships between the tables are valid and exists and there is no orphaned records this mostly achieved through [foreign keys](#primary-key--foreign-key)

---

## Constraints

Rules or conditions that are
applied to the data to ensure its integrity and consistency

Here are some common constraints

1. [Primary Key](#primary-key--foreign-key)
2. [Foreign Key](#primary-key--foreign-key)
3. Unique: This ensure that the data in the column is unique across all rows
4. Not [NULL](#what-is-null): The data in the column can't be null
5. Check: Add certain conditions on fields for example age can't be under 13, Or student grade can't be over 100

Q: What is the difference between [Primary Key](#primary-key--foreign-key) constraint and Unique constraint

Ans: Primary key doesn't allow null unlike the unique constraint

---

## What Is SQL

SQL stands for structure query language
SQL is used to communicate with the database
SQL lets you access and manipulate database

data base management systems that uses SQL: Oracle, Sybase, Microsoft SQL Server, Access, Ingres,

SQL lets you do the following

- Retrieve, Insert, Update, And delete data inside database
- Create and delete databases
- Create tables, Relationships and view them
- Store procedures in the database
- Mange permissions

Types of SQL statements

- Data definition language (DDL)
- Data manipulation Language (DML)
- Data Control Language (DCL)
- Transaction control language (TCL)
- Data query language (DQL)

---

## DBMS Vs. RDBMS

This systems used to manage databases

**DBMS** stands for Data Base Management System
**RDBMS** stands for Relational Data Base Management System

DBMS examples:
RDBMS examples:

Only one user can access DBMS at the same time
Multiple users can access RDBMS at the same time

| DBMS                                    | RDBMS                                       |
| --------------------------------------- | ------------------------------------------- |
| ex: Files systems or XML                | ex: SQLSever or oracle                      |
| Different data structure to store files | Tabular format                              |
| one user have access at the same time   | Multiple users have access at the same time |
| Less secured                            | More secured                                |

---

Go Back to the [README](./README.md) to read about the next section which is [**ERD**](./erd/ERD%20Symbols.md) !
