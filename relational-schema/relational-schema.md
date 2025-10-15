# Relational Schema

It's a part of the logical diagram
It's the second step after creating the [ERD](../erd/ERD%20Symbols.md)

---

For example this ERD

![Example](./example.svg)

Relational Schema it is a more detailed diagram and tables

After converting this ERD to relational schema it will look like this

```mermaid
  erDiagram
  direction LR
  Student {
    studentID int PK
    firstName string
    lastName string
    date birthdate
    age int
  }

  Phone {
    id int PK
    phone string
    StudentID int FK
  }

  Enroll {
    id int PK
    studentID int FK
    courseID int FK
    enrollDate date
    grade int
    name string
}

  Course {
    courseID int PK
    name string
    hours int
  }

  Student ||--o{ Phone : ""
  Student ||--o{ Enroll : ""
  Enroll }o--|| Course : ""
```

## Converting ERD Relations Into Relational Schema

- [Self-Referential](#self-referential-to-relational-schema)

- [Composite, Multivalued And Derived Attributes](#composite-multi-valued-and-derived-attributes)

- [One To One](#one-to-one)

- [One To Many / Many To One](#one-to-many--many-to-one)

- [Many To Many](#many-to-many)

- [Generalization And Specialization](#generalization-and-specialization)

- [Associative Entity](#associative-entity)

### Self Referential To Relational Schema

Example:

![Ex](./self-referential-ex.svg)

> In the same table we add a foreign key refers to the primary key of the same table

```mermaid
erDiagram
  direction LR
  EMPLOYEE {
    empID int PK
    name string
    salary decimal
    manager int FK "References empID (Self-Reference)"
  }

    EMPLOYEE |o--o{ EMPLOYEE : "Manges"
```

---

### Composite, Multi valued And Derived Attributes

Example

![Example Three](./example-3.svg)

> We ignore the composite attribute and only take it's sub-attributes

> Derived attributes ignored also

> Create a new table for the multivalued attributes

Our relational schema will look like this

```mermaid
  erDiagram
  direction LR
    Student {
    studentID int PK
    firstName string
    lastName string
    date birthdate
  }

  Phone {
    id int PK
    phone string
    StudentID int FK "Refers to the student's phone"
  }

  Student ||--o{ Phone : "Has Phone"
```

---

### One To One

Example

![ERD](./one-to-one-ex.svg)

There are two solution

- Take the primary key of the **_car_** and put it inside the **_driver_** table as foreign key

- Take the primary key of the **_driver_** and put it inside the **_car_** table as foreign key

**First Solution**:

```mermaid
erDiagram
  direction LR
  Driver {
    driverID int PK
    fullName string
    drivingSkill string
    age int
    carID int FK
  }

  Car {
    carID int PK
    number string
  }

  Driver ||--|| Car : "Driving"
```

**Second Solution**:

```mermaid
erDiagram
  direction LR
  Driver {
    driverID int PK
    fullName string
    drivingSkill string
    age int
  }

  Car {
    carID int PK
    number string
    driverID int FK
  }

  Driver ||--|| Car : "Driving"
```

---

### One To Many / Many To One

Example

![ERD](./one-to-many-ex.svg)

> Always look for the **many** side and take the PK and any attributes from the relationship and the **one** side and put them inside the **many** side table

```mermaid
erDiagram
  direction LR
  Employee {
    empID int PK
    name string
    salary int
    depID int FK "Refers to Department"
    startDate date
  }

  Department {
    depID int PK
    name string
  }

  Employee }o--|| Department : "Works in"
```

---

### Many To Many

> There is always a third Table connect the two entities

Let's take the same example we hade before

![Example](./example.svg)

> The third table is **_Enroll_**

> Take the PK from both sides and store them as FK in the third table

```mermaid
  erDiagram
  direction LR
  Student {
    studentID int PK
    firstName string
    lastName string
    date birthdate
    age int
  }

  Phone {
    id int PK
    phone string
    StudentID int FK
  }

  Enroll {
    id int PK
    studentID int FK
    courseID int FK
    enrollDate date
    grade int
    name string
}

  Course {
    courseID int PK
    name string
    hours int
  }

  Student ||--o{ Phone : ""
  Student ||--o{ Enroll : ""
  Enroll }o--|| Course : ""
```

In some places they combine PKs of both sides and make it as PK to the third table

**Students Table**

| studentID | first_name | last_name | birthdate  | age |
| --------- | ---------- | --------- | ---------- | --- |
| 1         | John       | Smith     | 2002-05-15 | 22  |
| 2         | Alice      | Johnson   | 2001-08-22 | 23  |

**Courses Table**

| courseID | name             | hours |
| -------- | ---------------- | ----- |
| 1        | Database Systems | 3     |
| 2        | Data Structures  | 4     |

**Enroll Table**

| enrollID | studentID | courseID | enrollmentDate | grade |
| -------- | --------- | -------- | -------------- | ----- |
| 1        | 1         | 2        | 1/1/2025       | 90    |
| 2        | 1         | 1        | 1/1/2025       | 40    |
| 3        | 2         | 1        | 2/6/2020       | 88    |
| 4        | 1         | 1        | 1/5/2025       | null  |

Take a look at the enrollID number 4

| enrollID | studentID | courseID | enrollmentDate | grade |
| -------- | --------- | -------- | -------------- | ----- |
| 3        | 2         | 1        | 2/6/2020       | null  |

> If we combined the PKs of student and course we will have the same Pk for the table which is a huge mistake

---

### Generalization And Specialization

Example

```mermaid
flowchart TB
  p[Person]
  s[Student]
  e[Employee]
  p --- id(("`_id_`")) & bh((Birthdate)) & age((Age)):::dAttrib & fName((First Name)) & lName((Last Name))

  p --- a[/is A\] --- s & e

  rg((RegestNumber))
  stuID(("`_StudentID_`"))

  s --- rg & stuID

  salary((Salary))
  empID(("`_Employee ID_`"))

  dev[Developer]
  teacher[Teacher]

  e --- b[\is A/] --- teacher & dev
  e --- salary & empID

  devID(("`*DevID*`"))
  lang((Language))
  teacherID(("`_TeacherID_`"))
  deg((Degree))

  dev --- devID & lang
  teacher --- teacherID & deg
```

> Remember that the relationship is always Ont-To-One

> Take the PK of the parent and use it as FK in the child

```mermaid
erDiagram
  direction TB
  Person {
    personID int PK
    firstName string
    lastName string
    age int
    location string
    birthdate date
  }

  Student {
    studentID int PK
    regNumber int
    personID int FK
  }

  Employee {
    empID int PK
    salary decimal
    personID int Fk
  }

  Developer {
    devID int PK
    language string
    empID int FK
  }

  Teacher {
    teacherID int PK
    degree string
    empID int FK
  }

  Person ||--|| Student  : ""
  Person ||--|| Employee  : ""

  Employee ||--|| Developer  : ""
  Employee ||--|| Teacher  : ""

```

---

### Associative Entity

Example

![ERD](./associative-entity-ex.svg)

1. Create a bridge table for the [many to many](#many-to-many) relationship

2. Take PKs for each table and put them in the bridge table, Also take the PK from the associative relation and put it in the bridge table

It will look like this

```mermaid
erDiagram
  direction LR
  Student {
    studentID int PK
    firstName string
    lastName string
    birthdate date
  }

  Enroll {
    enrollID int PK
    studentID int FK
    courseID int FK
    enrollmentDate date
    grade int
    profID int FK
  }

  Course {
    courseID int PK
    hours int
  }

  Prof {
    profID int PK
    name string
  }

  Student }o--|| Enroll : ""
  Enroll }o--|| Course : ""
  Prof  }o--|| Enroll : ""

```

> Associative Entities are always with the [many to many](../erd/many-to-many-relationship.md) relationship

---
