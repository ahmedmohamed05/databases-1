# Generalization / Specialization

## Generalization

If we have two or more entities with many same attributes we can group them up into a new entity and use a special symbol to say the the two old entities have this same attributes

Ex:

```mermaid
flowchart TD
  s[Student] --- id(("`_id_`")) & bh((Birthdate)) & age((Age)):::dAttrib & fName((First Name)) & lName((Last Name)) & regNumber((RegNumber))

  classDef dAttrib stroke-dasharray: 5 5
```

```mermaid
flowchart BT
  e[Employee] --- id(("`_id_`")) & bh((Birthdate)) & age((Age)):::dAttrib & fName((First Name)) & lName((Last Name)) & ss((Salary))

  classDef dAttrib stroke-dasharray: 5 5
```

Notice that **id**, **First name**, **Last name**, **Birthdate**, And **Age** are in both **Student** and **Employee**

we can generalize this as the following

```mermaid
flowchart TD
  p[Person]
  s[Student]
  e[Employee]
  p --- id(("`_id_`")) & bh((Birthdate)) & age((Age)):::dAttrib & fName((First Name)) & lName((Last Name))

  p --- a[/is A\] --- s & e

  s --- rp((RegNumber))
  e --- sa((Salary))
```

it is a bottom-top approach

> Tip: it's like inheritance in OOP

## Specialization

we take deep more attributes from an entity

<!-- ![See the diagram](./generalization-specialization.svg) -->

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

> We can look at the triangle as the filter in which we remove attributes or add

Now we can move into [Relational Schema](../../relational-schema/relational-schema.md)
