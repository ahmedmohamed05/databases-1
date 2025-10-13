# Joins

restore this DB from the link [Here](https://uploads.teachablecdn.com/attachments/BQo1eBhaRr6iLUDVrXVp_Shop_Database.bak)

**Join:** Lets you combine rows from two or more tables based on relations between their columns

## Content Table

- [Inner Join](#inner-join)
- [Left Outer Join](#left-join-outer)
- [Right Outer Join](#right-join-outer)

## Inner Join

Takes only the data that have a relationship between the tables

Basic Syntax

```sql
select [columns from tables] from [table1] inner join [table2] on [table1.column] = [table2.column]
```

Ex: Get the customers with their orders

```sql
select Customers.CustomerID ,Customers.Name ,Orders.Amount
from Customers inner join Orders on Customers.CustomerID = Orders.OrderID
```

Ex: Show the first 10 employees and their first and last name and the department he works in

```sql

select top 10
  Employees.FirstName ,Employees.LastName ,DepartmentName = Departments.Name
from Employees inner join Departments on Employees.DepartmentID = Departments.ID
```

You can generate select queries just write click on the empty space in the file and select Design in query editor or press `ctrl+shift+q`

and select the table and the columns you want to show click ok, It will generate the query for you

Ex: Show Employee name and department and country

```sql

select top 10
  Employees.FirstName ,Employees.LastName ,DepartmentName = Departments.Name ,CountryName = Countries.Name
from Employees inner join Departments on Employees.DepartmentID = Departments.ID inner join Countries on Employees.CountryID = Countries.ID
```

> You can edit a query in the designer just highlight it and press the right click than click design in query editor

the keyword **_inner_** is optional

---

## Left Join (Outer)

Returns ALL rows from the LEFT table + matching rows from the RIGHT table. If no match, shows NULL for right table columns.

Basic Syntax

```sql
select [columns from tables] from [table1] left outer join [table2] on [table1.column] = [table2.column]
```

Ex: Show all the customers even the ones without orders

```sql
select Customers.CustomerID ,Customers.Name ,Orders.Amount
from Customers left outer join Orders on Customers.CustomerID = Orders.CustomerID
```

> the keyword **_outer_** is optional

you can open the designer and right click on the relationship and select where the columns comes from

---

## Right Join (Outer)

Same as left join but it shows all data from right table(table 2) and only matches data from left table(table 1)

Basic Syntax

```sql
select [columns from tables] from [table1] right outer join [table2] on [table1.column] = [table2.column]
```

Ex: Show all orders and only the customers with orders

```sql
select Customers.CustomerID ,Customers.Name ,Orders.Amount
from Customers right outer join Orders on Customers.CustomerID = Orders.CustomerID
```

---

## Full Outer Join

Return all data from both table

Basic syntax

```sql
select [columns from tables] from [table1] full join [table2] on [table1.column] = [table2.column];
```

Ex: Get all data from both customers and orders tables

```sql
select Customers.CustomerID ,Customers.Name ,Orders.Amount
from Customers full join Orders on Customers.CustomerID = Orders.CustomerID
```
