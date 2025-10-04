# Many to many relationship

single entity can have many other entities and the other entities can relate to more than single entity

```mermaid
flowchart LR
  s[Student] --- r1{Enroll} --- c[Course]
```

now the Student can enroll many courses, and the course can be shown to many students, so to describe the nature of the relationship

```mermaid
flowchart LR
  s[Student] --- |m| r1{Enroll} --- |m| c[Course]
```

**Example**: draw an ERD for the following entities

- Customer
- Order
- Products

Relationships requirements:

1. One customer can order many orders
2. many orders can contains many products
3. there are a lot of products can be taken to a lot of orders

**Solution**:

```mermaid
flowchart TD
  c[Customer]
  r1{Place}
  o[Order]
  r2{Contains}
  p[Product]
  c:::entity --- |1| r1 --- |m| o:::entity
  o --- |m| r2 --- |m| p:::entity

  classDef entity fill:#00f
```

one customer can order many orders and many orders can contains many products at the same time many products can be inside may other orders
