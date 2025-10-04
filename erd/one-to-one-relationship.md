# One to one Relationship

Means every entity has only one of the other-side entity and the other side only have one

```mermaid
flowchart LR
  Student --- has{Has} --- stdCard[Student Card]
```

In the example above the student only has one university card and the card represents only one student

so the ERD will look like this

```mermaid
flowchart LR
  Student --- |1| has{Has} --- |1| stdCard[Student Card]
```

---

Another Example

```mermaid
flowchart TD
  s[Student] --- r1{is a} --- p[Person]
  emp[Employee] --- r2{is a} --- p
```

> We have to ask our selfs what is the Nature of the relationship between the **Student** and **Person** from the **Student** perspective, and the **Person** perspective

with describing the relationships it will look like this

```mermaid
flowchart TD
  s[Student] --- |1| r1{is a} --- |1| p[Person]
  emp[Employee] --- |1| r2{is a} --- |1| p
```

---

```mermaid
flowchart LR
  p[Head Coach] --- |1| r1{manages} --- |1| team[Football Team]
```
