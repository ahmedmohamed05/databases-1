# Generalization

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

# Specialization

we take deep more attributes from an entity

![See the diagram](./generalization-specialization.svg)

> We can look at the triangle as the filter in which we remove attributes or add
