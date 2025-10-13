# Constraints

Constraints: The rules and policies you use to keep data integrity good

Some Examples

- Primary key (PK): Combination of Not null and unique to identify each row
- Not null: Column can be null
- Foreign key (FK): Ensure that each link in the tables is still exists and valid
- Unique: All values in a column are different
- Check: Check certain conditions, i.e. age value can't be negative
- Default: default value for columns
- Crate Index: Used to crate a retrieve data from the DB quickly

## Content Table

- [Primary Key](#primary-key)
- [Foreign Key](#foreign-key)
- [Check](#check)
- [Unique](#unique)

## Primary Key

Each table must have a primary key to identify each row and link to any other table

Here is how to create a table with PK filed

```sql
create table courses (
  id int not null primary key,
  name nvarchar(100) not null,
  reference nvarchar(100) null
)
```

This will create a table with **_id_** filed as it's PK, you can see it and get it's values

There is another way to create a PK which is composite key

```sql
create table ex2
(
  id int not null
  ,name nvarchar(100) not null
  ,lastName nvarchar(100) null
  ,constraint pk primary key (id, name)
)
```

In the above statement will create a hidden PK called **_pk_** which is a combination of **_id_** + **_name_**

To add PK constraint you can use the **_alter_** command

Ex: Single field PK

```sql
alter table orders add primary key (id);
```

Ex: Composite PK

```sql
alter table people
add constraint pk_person primary key (id, lastName);
```

To Drop a PK constraint you can use the **_drop_** command

```sql
alter table people drop constraint pk_person;
```

---

## Foreign Key

Used to prevent actions that might destroy links between tables

FK: is a one or more fields that refers to row in another table

Ex: Customers and orders tables

```sql
create table customers
(
  id int not null primary key
  ,name nvarchar(150) not null
  ,location nvarchar(50) not null
  ,phoneNumber nvarchar(15) not null
  ,secondPhoneNumber nvarchar (15) null,
)

create table orders
(
  id int not null primary key
  ,item nvarchar(20) not null
  ,amount smallint not null
  ,customerId int foreign key references customers(id)
)
```

Add FK after creating the table using the **_alter_** command

```sql
alter table orders add foreign key (customerID) references customers(id);
```

Or if we want to make it composite

```sql
alter table orders add constraint fk_customer foreign key (customerId) references customers(id);
```

> Note: The table must already contain a field named **_customerId_**

Drop FK with the **_drop_** command

```sql
alter table orders drop constraint fk_customer
```

---

## Not Null

Field can't contain a null value

```sql
create table ex (
  id int not null primary key
)
```

With the **_alter_** command

```sql
alter table ex add name nvarchar(150) not null
```

---

## Default

Set default value for a field if no value provided

```sql
create table employees (
  id int not null primary key,
  fullName nvarchar(150) not null,
  salary float default 500
)
```

Inserting data

```sql
insert into employees values (1, 'Ahmed Mohamed', 800);

insert into employees
  (id, fullName)
values
  (2 ,'Ali Walled');
```

> You must specify the columns to use the default value for the column not specified

Now Ahmed have salary 800 and ali 500 (From the default constraint)

You can use functions as defaults

First lets add the column, You can skip this if you want to add constraint on an existing column

```sql
alter table employees add hireDate date;
```

Now lets add the constraint

```sql
alter table employees add constraint df_hireDate default getDate() for hireDate;
```

Here **_df_hireDate_** is the constraint name if we want to drop it later

Lets add one row

```sql
insert into employees
  (id, fullName)
values
  (3 ,'Mohamed Mahdi');
```

Now **_Mohamed_** have salary 500 and the hiring date is todays date

> The old employees will have a null value

Drop constraint

```sql
alter table employees drop constraint df_hireDate;
```

Tip: You can crete and add constraint in one line

```sql
alter table [table name] add [new field name] [data type] [nullable] constraint [constraint name] default [default value];
```

```sql
alter table employees add language nvarchar(20) not null constraint df_language default 'C++'
```

> This approach will fill the field with the default value for old records

---

## Check

Checks if the Entered value satisfy the conditions

```sql
create table users
(
  id int not null primary key
  ,username nvarchar(20) not null
  ,age int check (age  >= 18)
)
```

Now if we try to insert this record

```sql
insert into users values (1, 'ahmed', 10);
```

Will give an error "conflicted with the CHECK constraint"

```sql
insert into users values (1, 'ahmed', 20);
```

This will work fine

We can name our constraint, to drop it later

```sql
create table users
(
  id int not null primary key
  ,username nvarchar(20) not null
  ,age int not null
  ,constraint check_age check (age >= 18 and age <=50)
)
```

Drop the constraint with **_drop_** command

```sql
alter table users drop constraint check_age;
```

---

## Unique

Unique means the value in the field doesn't duplicate

> PK is unique and not null, Unique is unique and allows null

```sql
create table people
(
  id int not null unique
  ,lastName varchar(255) not null
  ,firstName varchar(255)
  ,age int
);
```

Now our id won't duplicate

We can unique more than one field

```sql
create table students
(
id int not null
,firstName varchar(255) not null
,lastName varchar(255) not null
,Age int
,constraint uc_student unique (id,lastName)
);
```

**_Alter_** command

```sql
alter table students add project nvarchar(50) not null unique;
```

Or

```sql
alter table students add constraint uc_studentProject unique (firstName, project);
```

**_drop_** command

```sql
alter table student drop constraint uc_user;
```

---

## Index

There are two types of indices

**Cluster**: Which order the data based on the PK (The faster)

> We can only have one Cluster index per table

**Normal**: crate another index based on other data, Which creates a table and order the data based on the that field

> Notice that normal indices making the inserting operation slower because has to edit two tables or more

Once you create any table with PK it will create a cluster index based on that PK

To create a normal index

```sql
create index [index name] on [table name](filed name);
```

Ex: create index for peoples table based on their last name

```sql
create index lastNameIndex on people(lastName);
```

We can create multiple indices with ascending or descending order

```sql
create index ageLastNameIndex on people(age, lastName asc);
```

Drop Index

Basic syntax

```sql
drop index [index name]
```

---

Now Read About [Normalization](../normalization.md)
