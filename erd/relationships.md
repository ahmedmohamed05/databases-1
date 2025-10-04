# Relationships

## Normal Relationships

```mermaid
flowchart LR
  student
  Course
```

there is a relationship between the student and the course, we can represent it like this

---

```mermaid
flowchart LR
  student[Student] --- enroll{Enroll Course}
  enroll{Enroll Course} --- Course
```

> an entity can have one or more relationship

```mermaid
flowchart LR
  Employee --- Developer{Develop} --- project
  Employee --- mange{Mange} --- project
  customer --- consume{Consume} --- project
```

## Self Referencing Relationship

An entity that have relation with other entities with the same type

```mermaid
flowchart LR
  emp[Employee] --- m{managerOn} --- emp
```

As a table

| ID  | Name    | ManagerID |
| --- | ------- | --------- |
| 1   | Ahmed   | null      |
| 2   | Ali     | 1         |
| 3   | Mohamed | 1         |
| 4   | Mahdi   | 2         |

now **Ahmed** is the manager of **Ali** and **Ali** is the manager of **Mahdi**

## Relationship Types

### [one-to-one](./one-to-one-relationship.md)

### [one-to-many](./one-to-many-relationship.md)

### [many-to-one](./many-to-one-relationship.md)

### [many-to-many](./many-to-many-relationship.md)

> You have to see the types

## Cardinality Vs. Ordinality

### Cardinality

Refers to the **maximum** number of times an instance of an entity can relate to instances of another

```mermaid
flowchart LR
  c[Customer]:::en --- |1|r1{place} --- |m| o[Order]:::en
  classDef en fill: #00f
```

- The **maximum** number of instances from order a customer can have is $m$
- The **maximum** number of instances from customer an order can have is $1$

### Ordinality

Refers to the minimum number of the instance an entity can have from another instance

it tells if the relation is required, optional or mandatory

```mermaid
flowchart LR
  s[Student]:::en
  c["Course"]:::en
  r1{Enroll}

  s --- |m| r1 --- |m| c
  s --- |0| r1 --- |0| c

  classDef en fill: #00f
```

maybe there is a **Student** with no enrolled **courses**, and maybe there is a course with no **Students** in

```mermaid
flowchart LR
  c[Customer]:::en
  o[Order]:::en
  r1{Place}:::rel

  c --- |1|r1 --- |m|o
  c --- |1|r1 --- |0|o
```

> Better Representation is like this
> $$(ordinality, cardinality)$$

```mermaid
flowchart LR
  c[Customer]
  o[Order]
  r1{Place}

  c ---|"(1, 1)"| r1 ---|"(0, m)"| o
```

## Cardinality Symbols

we can represent the nature of the ordinality and cardinality in a symbols

```mermaid
erDiagram
  direction LR
  CUSTOMER ||--o{ ORDER: "Place"
```

above example show that a **CUSTOMER** with $(1, 1)$ related to **ORDER** as $(0, m)$

---

converting this ERD to use symbols

```mermaid
flowchart LR
  c[Customer]
  o[Order]
  r1{Place}

  c ---|"(1, 1)"| r1 ---|"(0, m)"| o
```

it will look like this

```mermaid
erDiagram
  direction LR
  Customer ||--o{ Order : "Place"
```

- This symbols called _cross-s-fot-notation_

see the image below

![table of all types of notations in cross-s-fot](./images/cros-s-fot-notation.png)

Example

```mermaid
erDiagram
  direction LR
  Lecturer ||--o{ Course : "Lecture"
```

---

Example

```mermaid
erDiagram
  direction LR
  Student }o--o{ Course : "Enroll"
```

---

Example

```mermaid
erDiagram
  EMPLOYEE |o--o{ EMPLOYEE : "manages"
```

Each employee should have zero on one manager, and each employee can only be a manager for zero or many

---

Example

```mermaid
erDiagram
  direction LR
  EMPLOYEE }|--|{ SKILL : "Learns"
```

---

At the end, Here a [guid](./steps-to-erd.md) to crete ERD
