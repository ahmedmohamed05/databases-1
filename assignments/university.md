# University Assignment

**Q**: Draw ERD for a university that satisfy this requirements

- In a university, a Student enrolls in Courses. A student can enroll in more than one course, Each course can have more than one student.

- Each student has only one mentor (prof), Professor can mentor more than one student.

- Each Professor can teach only one course.

- Each Course can have only one professor.

- Course can have un-assigned professor.

- Professor can teach no courses.

**Solution**:

```mermaid

erDiagram
  direction LR
  %% Entities
  s[Student]:::entity
  c[Course]:::entity
  p[Prof]:::entity

  %% Attributes
  s {
    int ID PK
    string first_name
    string second_name
    string last_name
    Date birthdate
    int age*
  }

  c {
    int ID PK
    string name
    int hours
  }

  p {
    int ID PK
    string full_name
    string degree
  }


  %% Relationships
  s }o--o{ c : "Enroll"
  s }o--|| p : "Mentor"
  p |o--o| c : "Teach"

  classDef entity fill:purple
```
