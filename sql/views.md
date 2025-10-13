# Views

Used to store the query statement, Something like a variable

You can see the view in the views directory

Basic syntax

```sql
create view [viewName] as select * from [table]
```

Here any time we call **_viewName_** it will it's statement

Ex: Store all active employees who works in IT department as a view

```sql
create view ITEmps
as
  select e.*
  from Employees e join Departments d on e.DepartmentID = d.ID
  where d.Name = 'IT' and e.ExitDate is null
```

Now we can use ITEmps like every other table

You Can create a view and with certain columns and give it to a user to make him just see this as his permission
