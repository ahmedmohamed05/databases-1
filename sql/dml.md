# DML (Data Manipulation Language)

Content Table

- [Insert](#insert)
- [Update](#update)
- [Delete](#delete)
- [Select Into](#select-into)
- [Insert Into Select From](#insert-into-select-from)

## Insert

Allows me to insert data to the table

Syntax:

```sql
insert into [table name] values (...values)
```

Lets say we have this table

```sql
create table employees (
  id int not null,
  name nvarchar(50) not null,
  phone nvarchar(15) null,
  salary smallint null,
  primary key (id)
)
```

and want to add this data
ID = 1, name = "Ahmed", phone = "+9641212", salary = 4000

we write the following

```sql
insert into employees values (1, 'Ahmed', '+9641212', 4000)
```

> You must write the values in the same order as the table

Now if you try to run the same code again it won't work because you have to change the id to stay uniq

---

We can enter multiple records

```sql
insert into [table name] values
(...values1),
(...values2),
(...values3),
(...values4)
```

**Ex:**

```sql
insert into employees values
(2, 'Ali', '+9642323', 2000),
(3, 'Mustafa', '+9643434', 1000),
(4, 'Ali', '+9644545', 2500),
(5, 'Mohamed', null, 7000)
```

---

We can insert certain values into certain columns

Syntax would be like this

```sql
insert into [table name] ([...column names]) values ([...values])
```

**Ex:**

```sql
insert into employees (id, name) values (7, 'Mahdi');
```

any other nullable filed will be null

---

## Update

Lets say we have this table

| id  | name    | phone    | salary |
| --- | ------- | -------- | ------ |
| 1   | Ahmed   | +9641212 | 4000   |
| 2   | Ali     | +9642323 | 2000   |
| 3   | Mustafa | +9643434 | 1000   |
| 4   | Ali     | +9644545 | 2500   |
| 5   | Mohamed | null     | 7000   |

Basic syntax

```sql
update [table name] set [filed name] = [new value] where [condition]
```

Ex: We want to change the salary of the employee with id 3

update employees set salary = 3000
where id = 3;

the result would be

| id  | name    | phone    | salary |
| --- | ------- | -------- | ------ |
| 1   | Ahmed   | +9641212 | 4000   |
| 2   | Ali     | +9642323 | 2000   |
| 3   | Mustafa | +9643434 | 3000   |
| 4   | Ali     | +9644545 | 2500   |
| 5   | Mohamed | null     | 7000   |

> You must add a condition, If no condition provided the update will effect all the entities

You can update multiple things

```sql
update employees set salary = 6000, name = 'Maher'
where id = 3;
```

Output

| id  | name    | phone    | salary |
| --- | ------- | -------- | ------ |
| 1   | Ahmed   | +9641212 | 4000   |
| 2   | Ali     | +9642323 | 2000   |
| 3   | Maher   | +9643434 | 6000   |
| 4   | Ali     | +9644545 | 2500   |
| 5   | Mohamed | null     | 7000   |

Ex: lets say we want to add 500 to any employee with salary < 4000

We will write this statement

```sql
update employees set salary = salary + 500
where salary < 4000
```

Result:

| id  | name    | phone    | salary |
| --- | ------- | -------- | ------ |
| 1   | Ahmed   | +9641212 | 4000   |
| 2   | Ali     | +9642323 | 2500   |
| 3   | Maher   | +9643434 | 6000   |
| 4   | Ali     | +9644545 | 3000   |
| 5   | Mohamed | null     | 7000   |

---

Ex: lets we want to add 10% for all employees

Solution

```sql
update employees set salary = (salary / 10) + salary;
```

Result:

| id  | name    | phone    | salary |
| --- | ------- | -------- | ------ |
| 1   | Ahmed   | +9641212 | 4400   |
| 2   | Ali     | +9642323 | 2750   |
| 3   | Maher   | +9643434 | 6600   |
| 4   | Ali     | +9644545 | 3300   |
| 5   | Mohamed | null     | 7700   |

---

## Delete

Basic syntax

```sql
delete from [table name] where [condition]
```

> If no condition specified all the table will be **deleted**

Lets say i have this table

| id  | name    | phone    | salary |
| --- | ------- | -------- | ------ |
| 1   | Ahmed   | +9641212 | 4400   |
| 2   | Ali     | +9642323 | 2750   |
| 3   | Maher   | +9643434 | 6600   |
| 4   | Ali     | +9644545 | 3300   |
| 5   | Mohamed | NULL     | 7700   |
| 6   | Fadel   | NULL     | NULL   |
| 7   | karem   | +9645656 | NULL   |

And i want to delete all the employees with phone number null

```sql
delete from employees where phone is null
```

| id  | name  | phone    | salary |
| --- | ----- | -------- | ------ |
| 1   | Ahmed | +9641212 | 4400   |
| 2   | Ali   | +9642323 | 2750   |
| 3   | Maher | +9643434 | 6600   |
| 4   | Ali   | +9644545 | 3300   |
| 7   | karem | +9645656 | NULL   |

---

## Select Into

We can select a whole table and copy it into a new table for ex

```sql
select * into [new table name] from [old table name];
```

**Ex**:

### employees

| id  | name  | phone    | salary |
| --- | ----- | -------- | ------ |
| 1   | Ahmed | +9641212 | 4400   |
| 2   | Ali   | +9642323 | 2750   |
| 3   | Maher | +9643434 | 6600   |
| 4   | Ali   | +9644545 | 3300   |
| 7   | karem | +9645656 | NULL   |

To copy it to **_employeesCopy_** for example write this statement

```sql
select * into employeesCopy from employees;
```

This will create a new table called **_employeesCopy_** and copy all the data from **_employees_** table

Now if we try to run the same code again it will give us an error saying the table already exist

**Practice:** You can write a statement to copy the table if not exists

The code will copy all the fields, To copy certain data we can specify what to copy

```sql
select [fields] into [new table name] from [old table name];
```

**Ex:** Lets say i want the id and the phone

```sql
select id, phone into employeesCopy2 from employees;
```

The table would be

### employeesCopy2

| id  | phone    |
| --- | -------- |
| 1   | +9641212 |
| 2   | +9642323 |
| 3   | +9643434 |
| 4   | +9644545 |
| 7   | +9645656 |

Now if you just want a new table with the same field(Not the data) we can write a condition and make it always returns false

Ex:

```sql
select * into testingEmployees from employees where 1=0;
```

### testingEmployees

| id  | name | phone | salary |
| --- | ---- | ----- | ------ |
|     |      |       |        |
|     |      |       |        |
|     |      |       |        |
|     |      |       |        |
|     |      |       |        |
|     |      |       |        |
|     |      |       |        |

---

## Insert Into Select From

Used to select data from any table and copy it to new table

Basic syntax

```sql
insert into [target table] select * from [source table];
```

Lets say we have this two tables

### people

| id  | name    | age |
| --- | ------- | --- |
| 1   | Ahmed   | 20  |
| 2   | Ali     | 14  |
| 3   | Mohamed | 30  |

### friends (it's empty)

| id  | name | age |
| --- | ---- | --- |
|     |      |     |
|     |      |     |
|     |      |     |
|     |      |     |
|     |      |     |
|     |      |     |
|     |      |     |

We write the following

```sql
insert into friends select * from people;
```

### friends

| id  | name    | age |
| --- | ------- | --- |
| 1   | Ahmed   | 20  |
| 2   | Ali     | 14  |
| 3   | Mohamed | 30  |

Also we can copy data based on condition

```sql
insert into [target table] select * from [source table] where [condition];
```

**_Ex:_**copy only people with age <= 20

```sql
insert into youngPeople select * from people where age <= 20;
```

### youngPeople

| id  | name  | age |
| --- | ----- | --- |
| 1   | Ahmed | 20  |
| 2   | Ali   | 14  |

Now Let's take some [miscellaneous](./misc.md) things
