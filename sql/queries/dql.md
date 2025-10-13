# DQL

To start with this lesson, Download and restore the sample database from this link [hr db](https://uploads.teachablecdn.com/attachments/QyyG7eKQqWrOMBWbKshk_HR_Database.bak)

## Content Table

- [Select Statement](#select-statement)
- [Select Distinct Statement](#select-distinct-statement)
- [Where Statement](#where-statement)
- [In Operator](#in-operator)
- [Order By](#order-by)
- [Select Top](#select-top)
- [Between Operator](#between-operator)
- [Count, Sum, Avg, Min and Max](#count-sum-avg-min-and-max)
- [Group By](#group-by)
- [Having](#having)
- [Like](#like)
- [Joins](#now-see-joins-in-this-tutorial)
- [Exists Query](#exists)
- [Unions](#union)
- [Case](#case)
- [More About Constraints](#constraints)

## Select Statement

```sql
select * from [table]
```

Returns all the columns and values from the table

Ex:

```sql
select * from Employees
```

This will return the table with all it's columns

```sql
select ID, FirstName, LastName from Employees;
```

This will only return the table with the specific columns

## Select Distinct Statement

It return the data without duplicates, Just if you want to know for example what are the departments

```sql
select distinct departmentID from Employees;
```

Also works on more than one column

```sql
select distinct departmentID, FirstName from Employees;
```

## Where Statement

Basic Syntax

```sql
select * from [table name] where [condition]
```

Ex: Select only male employees

```sql
select * from Employees where Gender = 'M';
```

Ex: Select only female employees and their salary is less than 500

```sql
select * from Employees where MonthSalary < 500 and Gender = 'F';
```

You Can Choice columns

```sql
select [columns names] from [table];
```

Ex: Print the first and last name from employees

```sql
select FirstName ,LastName
from Employees
where MonthlySalary <= 500 and Gender = 'M';
```

**_Not_** Keyword used to reverse the condition

syntax

```sql
select * from [table name] where not [condition]
```

Ex: Select the female employees

```sql
select FirstName ,Gender
from Employees
where not Gender = 'M';
```

> Not equal sign is `<>` in **_SQL_** server

```sql
select *
from Employees
where CountryID <> 1;
```

Selecting employees work in any other country than number 1

### OR

syntax

```sql
select * from [table] where [condition 1] or [condition 2] ... or [condition n];
```

Ex: Select the employees who works in department number 1 and 2

```sql
select *
from Employees
where DepartmentID = 1 or DepartmentID = 2
```

using **_OR_** and **_AND_**

```sql
select *
from Employees
where (DepartmentID = 1 or DepartmentID = 2) and Gender = 'M';
```

using **_NOT_**, **_OR_**, and **_AND_**

Ex: select the employees who are not in the departments 1 or 2, and if they in the 1 or 2 they must be not males

```sql
select *
from Employees
where not ((DepartmentID = 1 or DepartmentID = 2) and Gender = 'M');
```

### NULL Checking

Syntax

```sql
select * from [table] where [column name] is null;
```

Ex: Select all employees they don't have exit date

```sql
select * from Employees where ExitDate is null
```

using not

```sql
select *
from Employees
where ExitDate is not null
```

---

## IN Operator

it used to check if the filed value is exists inside the given values

The problem: imagine if we want to get the employees works in departments 1, 2, 5, 6, 9, and 10 we must write this code

```sql
select * from Employees where DepartmentID = 1 or DepartmentID = 2 or DepartmentID = 5 or DepartmentID = 6 or DepartmentID = 9 or DepartmentID = 10;
```

To prevent the repeating process we can use the **_IN_** operator

```sql
select *
from Employees
where DepartmentID in (1, 2, 5, 6, 9, 10);
```

you can use them with any datatype

```sql
select *
from Employees
where FirstName in ('Kai', 'Robert', 'Cameron')
```

You can still use the other statements we learned

```sql
select *
from Employees
where FirstName in ('Kai', 'Robert', 'Cameron') and Gender = 'M' and ExitDate is not null;
```

> Note that the In operator takes a set of elements

```sql
select DepartmentID from Employees where MonthlySalary <= 210
```

This statement will return a set of departments IDs that give salary >= 210

Lets say it will return: (1, 4, 8)

We can use this set inside another **_IN_** operator

```sql
select name
from Departments
where ID in (select DepartmentID
from Employees
where MonthlySalary <= 210)
```

we put the result of the select statement inside the parentheses, Like we are saying like this

```sql
select name
from Departments
where ID in (1, 4, 8)
```

We can still using **_not_** operator

```sql
select name
from Departments
where ID not in (select DepartmentID
from Employees
where MonthlySalary <= 210)
```

## Order By

Sorting Results
By default the ordering is ascending

```sql
select * from [table] order by [filed name] [ASC or desc]
```

Ex: Get all employees ordered by their salary

```sql
select ID ,FirstName ,MonthlySalary
from Employees
order by MonthlySalary
```

Can be used with string values

```sql
select ID ,FirstName ,MonthlySalary
from Employees
where DepartmentID = 1
order by FirstName
```

we can order the results based on more than one thing

```sql
select ID ,FirstName ,MonthlySalary
from Employees
where DepartmentID = 1
order by FirstName, MonthlySalary desc;
```

It will check every entity with the same **_FirstName_** and than it will order them by salary descending

## Select Top

Helps you selecting a number $n$ from the table

```sql
select top [n] [Fields] from [table];
```

Ex: Selecting first 5 employees

```sql
select top 5 * from Employees;
```

We can use percentage like return 25% of the all results, If we have 200 Employees it will return just 50 of them

```sql
select top [n] percent [fields] from [table];
```

Ex:

```sql
select top 25% percent * from Employees;
```

Ex: Lets get top 3 employees with highest salary without duplicates

**Sol:**

```sql
select distinct top 3 MonthlySalary
from Employees
order by MonthlySalary desc
```

Ex: Now find all the employees who takes this salaries

**Sol:**

```sql
select *
from Employees
where MonthlySalary
in
(select distinct top 3
  MonthlySalary
from Employees
order by MonthlySalary desc
)
order by MonthlySalary desc
```

## Select As

Select statement accepts expressions

```sql
select a = 2 * 3, b = 18 / 9;
```

this will display this table

| a   | b   |
| --- | --- |
| 6   | 2   |

Now if we added a table like this

```sql
select a = 2 * 3, b = 18 / 9 from [table];
```

This will return the same results but as the table records number, if we had 100 record, than the results will be 100

We can combine this feature to a lot of things, For example

```sql
select MonthlySalary ,halfSalary = MonthlySalary / 2
from Employees
```

this way we can create a table with the salary and half the salary

We can use the **_as_** keyword to do the same thing

```sql
select ID ,FirstName + ' ' + LastName as FullName
from Employees
```

this will combine **_FirstName_** and **_LastName_** as a field named **_FullName_**

Ex: Finding the yearly salary of an employee

**Sol:**

```sql
select ID ,Name = FirstName + ' ' + LastName ,YearlySalary = MonthlySalary * 12
from Employees;
```

Ex: Calculate the age of the employee

**Sol:**

```sql
select ID ,Name = FirstName + ' '+LastName ,age = dateDiff(year, DateOfBirth, getDate())
from Employees;
```

dateDiff function takes three arguments

1. type of the result year, months or days
2. fromDate or the old date
3. newDate

Ex: Find the number of months every employee had since their hiring date

```sql
select Name = FirstName + ' '+LastName ,MonthsHere = dateDiff(year, HireDate, getDate())
from Employees;
```

---

## Between Operator

To check if the values is between two values, reduce redundancy

Ex: Find all employees achieve the condition $200 \le salary \le 500$

```sql
select *
from Employees
where MonthlySalary >= 200 and MonthlySalary <= 500;
```

We can write this

```sql
select *
from Employees
where MonthlySalary between 200 and 500;
```

This much more readable

> You can use it with dates

---

## Count, Sum, Avg, Min and Max

### Count

Counts the number of rows matches the statement

Ex: Number of employees their age is 30

```sql
select x = count(*)
from Employees
where dateDiff(year, DateOfBirth, getDate()) = 30;
```

### Sum

Sum the values of the field

Ex: sum the **_MonthlySalary_** given each month

```sql
select MonthSalarySum=Sum(MonthlySalary)
from Employees;
```

### Avg

get the sum of the average of the field

Ex: Average of the ages

```sql
select AgeAvg = avg(dateDiff(year, DateOfBirth, getDate()))
from Employees;
```

### Min and Max

Ex: get the minimum and maximum monthly salary

```sql
select MaxSalary = max(MonthlySalary) ,MinSalary = min(MonthlySalary)
from Employees;
```

> Count and Avg doesn't count the null values

---

## Group By

Used to group the results of the whole table by a specific field

Ex: Lets say i want to know the following for each department

1. Number of employees
2. Total monthly salary
3. Average salary
4. Highest salary
5. lowest salary
6. Number of males
7. Number of females

**Sol:**

```sql
select DepartmentID ,gender
  ,numberOfEmployees = count(ID)
  ,totalMonthlySalary = sum(MonthlySalary)
  ,averageSalary = avg(MonthlySalary)
  ,highestSalary = max(MonthlySalary)
  ,lowestSalary = min(MonthlySalary)

from Employees

group by gender, DepartmentID
order by DepartmentID, Gender desc
```

Now this statement mean to select the fields per **_DepartmentID_** and **_Gender_**

Which mean it will make tow records for each department, because we have two genders (male and female)

> Make sure that your statements are logical and not like the example blow

```sql
select
  DepartmentID
  ,numberOfEmployees = count(ID)
  ,totalMonthlySalary = sum(MonthlySalary)
  ,averageSalary = avg(MonthlySalary)
  ,highestSalary = max(MonthlySalary)
  ,lowestSalary = min(MonthlySalary)

from Employees
```

This will return an error because it don't know what record of DepartmentID to display

---

## Having

It used to filter the results from the [group by](#group-by) statements

It's like the **_where_** statement for the [group by](#group-by) results

```sql
select
  numberOfEmployees = count(ID)
  ,totalMonthlySalary = sum(MonthlySalary)
  ,averageSalary = avg(MonthlySalary)
  ,highestSalary = max(MonthlySalary)
  ,lowestSalary = min(MonthlySalary)

from Employees

group by DepartmentID
order by DepartmentID
```

You can't add the where statement here to show departments with number of employees grater than 100 for example

using the **_having_** our statement will look like this

```sql
select
  numberOfEmployees = count(ID)
  ,totalMonthlySalary = sum(MonthlySalary)
  ,averageSalary = avg(MonthlySalary)
  ,highestSalary = max(MonthlySalary)
  ,lowestSalary = min(MonthlySalary)

from Employees

group by DepartmentID
having count (ID) >= 100
order by DepartmentID
```

> You can also use everything you learned about conditions

You can still use **_where_** to get the same results by playing around like this

```sql
select *
from (select
    numberOfEmployees = count(ID)
  ,totalMonthlySalary = sum(MonthlySalary)
  ,averageSalary = avg(MonthlySalary)
  ,highestSalary = max(MonthlySalary)
  ,lowestSalary = min(MonthlySalary)

  from Employees

  group by DepartmentID) result
where result.numberOfEmployees >= 100
```

---

## Like

It's used to filter data based on patterns

```sql
select *
from Employees
where Employees.FirstName like 'a%'
```

Return all the employees with firstName starts with 'a'

```sql
select *
from Employees
where Employees.FirstName like '%a'
```

Return all the employees with firstName ends with 'a'

```sql
select *
from Employees
where Employees.FirstName like '%er%'
```

Return all the employees with firstName contains 'er' in the middle

```sql
select *
from Employees
where Employees.FirstName like 'a%z'
```

Return all the employees with firstName starts with an 'a' and ends with a 'z'

```sql
select *
from Employees
where Employees.FirstName like '_a%'
```

Return all the employees their firstName has an 'a' in the second place

```sql
select *
from Employees
where Employees.FirstName like 'a___%'
```

Return all the employees their firstName starts with an 'a' and the name is 4 characters long

> You can still combine conditions because **_like_** operators is the same as the **_in_** operator

```sql
select *
from Employees
where FirstName like 'a___%' or FirstName like 'b___%'
```

The Wiled Cards

Now update this two records for testing

```sql
update Employees set FirstName = 'Ahmed', LastName = 'Mohamed'
where ID = 285

update Employees set FirstName = 'Ahmed', LastName = 'Mohamad'
where ID = 286

```

Now both names are correct it's just a way of naming
but the problem if we want to search we must get both

```sql
select *
from Employees
where LastName like 'moham[ae]d';
```

This will check if the letter in the position is an 'a' or an 'e'

```sql
select *
from Employees
where FirstName like '[abc]%';
```

Check if the name starts with a, b or c

```sql
select *
from Employees
where FirstName like '[a-h]%';
```

Check if the name starts with the letters from a to h

```sql
select *
from Employees
where FirstName like '[^abc]%';
```

Check if the name doesn't starts with the letters a, b and c

> Search for more wildcard they are very useful

---

## Now see joins in this [tutorial](../joins.md)

---

## Exists

Exists check if the results of a select statement has at least one record

Basic syntax

```sql
select ret = 'Yes' where exists (select [columns] from [table] where [conditions])
```

Ex: Returns all customers who have at least one order with an amount less than 600.

```sql
select *
from Customers c
where exists (select *
from orders
where orders.CustomerID = c.CustomerID and Amount < 600)
```

If This example feels hard to understand you can think about it like nested loops in programming

```js
// Outer loop - goes through each customer
for (let customer of customers) {
  // Inner loop - checks orders for THIS customer
  let foundMatch = false;
  for (let order of orders) {
    if (order.CustomerID === customer.CustomerID && order.Amount < 600) {
      foundMatch = true;
      break; // EXISTS stops at first match!
    }
  }

  // If we found a match, include this customer
  if (foundMatch) results.push(customer);
}
```

> Keep in mind that once the exists find's one row it stop executing the sub-query which makes it very fast, So it doesn't matter what are you selecting from the sub-query

---

## Union

It used to combined tables to one single result set

Basic syntax

```sql
select [columns] from [table1]
union
select [columns] from [table2]
```

> You have to return the same columns from both tables

```sql
select * from activeEmps
union
select * from resignedEmps
```

This will return all the employees combined into one table

> Union removes the duplicates, it's like distinct

If you really want to get the data with duplicates you can use the **_all_** keyword

```sql
  select *
  from Customers
union all
  select *
  from Customers
```

This will duplicate the table

---

## Case

Helps you to return data based on cases

Basic syntax

```sql
select [columns], [new column] =
case
  when [field value] [condition] then [returned value]
  when [field value] [condition] then [returned value]
  .
  .
  .
end
from [table name]
```

Ex: Get the full name of the departments

```sql
select * ,FullName = case
when Name = 'IT' then 'Information Technology'
when Name = 'HR' then 'Human Resources'
else name
end
from Departments
```

You can also use it to order date

```sql
select * ,FullName = case
when Name = 'IT' then 'Information Technology'
when Name = 'HR' then 'Human Resources'
else name
end
from Departments d
order by case
when d.Name = 'IT' then 1
else 2
end
```

This will put the it departments in the firs

Ex: find the age and tell if the employee is old or young

```sql
select e.ID ,e.FirstName ,e.DateOfBirth ,age = dateDiff(year, e.DateOfBirth, getDate())
  ,Old = case
when dateDiff(year, e.DateOfBirth, getDate()) <= 35 then 'Young'
else 'old'
end
from Employees e;
```

---

## Constraints

Now About [Constraints](../constraints.md)
