# Normalization

Used to reduce redundancy and split data into tables, It improve data consistency

Normalization is achieved by applying a set of steps called **Normal Forms(NFs)**

1. [First Normal Form (1NF)](#first-normal-form-1nf)
2. [Second Normal Form (1NF)](#second-normal-form-2nf)
3. [Third Normal Form (1NF)](#third-normal-form-3nf)

## First Normal Form (1NF)

**Rules**:

1. Primary key: The table must have a primary key (PK)
2. Atomic Values: Each column should only contain single indivisible value
3. No Repeating Groups: Each column should have a distinct name
4. No multi-value attributes such as FullName

---

## Second Normal Form (2NF)

> You must apply 1NF first

**Rules**:

1. No partial dependencies: Each non-key column must be dependent on the entire primary key

| courseID | courseName | studentID | studentName | grade |
| -------- | ---------- | --------- | ----------- | ----- |
| 1        | Physics    | 1         | John        | A     |
| 1        | Physics    | 2         | doe         | A+    |
| 2        | CS         | 1         | john        | B     |

This table doesn't satisfy 2NF because the attribute **_courseName_** depend on courseID and studentID at the same time

To fix this we can change the table to this

**Courses**:

| courseID | courseName |
| -------- | ---------- |
| 1        | Physics    |
| 2        | CS         |

**Enrollments**:

| courseID | studentID | grade |
| -------- | --------- | ----- |
| 1        | 1         | A     |
| 1        | 2         | A+    |
| 2        | 1         | B     |

---

## Third Normal Form (3NF)

> You must apply 1NF and 2NF first

**Rules**:

1. No transitive dependencies: Each non-key column in the table must depend on the primary key and not any other column

Ex:

| book ID | Book Title | Author Name   | Author Email |
| ------- | ---------- | ------------- | ------------ |
| 1       | C++ Basics | Ahmed Mohamed | <m1@g.c>     |
| 2       | Algorithms | John Doe      | <john@g.c>   |
| 3       | OS         | Ahmed Mohamed | <m1@g.c>     |
| 4       | OOP        | John Doe      | <john@g.c>   |

In this example the **_Author Email_** depends on **_Author Name_** as it's key but the values are duplicated

So we must split it into two tables

**Authors Tables**:

| ID  | Author Name   | Author Email |
| --- | ------------- | ------------ |
| 1   | Ahmed Mohamed | <m1@g.c>     |
| 2   | John Doe      | <john@g.c>   |

**Books Table**:

| Book ID | Book Title | AuthorID |
| ------- | ---------- | -------- |
| 1       | C++ Basics | 1        |
| 2       | Algorithms | 2        |
| 3       | OS         | 1        |
| 3       | OOP        | 2        |

Now Less redundancy

---
