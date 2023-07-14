i8887# A bit more CSharp and SQL

1. What does **_inheritance_** accomplish for us in C#?

> It allows code from one class to be reused in another

2. How does **_member inheritance_** work in C#? Does a `Class` inherit all members of the base `Class`?

> | ANSWER HERE |

3. How does **_accessibility_** affect inheritance?

> It affects inheritance by determining whether an inherited member is public, protected, or private

4. What is the difference between a `PRIMARY KEY` and a `FOREIGN KEY`

> Primary Key cant' have a value of NULL, Foreign Key can

5. What is an **_alias_**?

> When the same data collection can be accessed using different names

6. Demonstrate how you would query a join statement that would get all of a doctors patients from the following collections:

```SQL
CREATE TABLE doctors (
  id INT NOT NULL AUTO_INCREMENT,
  -- CODE OMITTED
  PRIMARY KEY (id)
)

CREATE TABLE patients (
  id INT NOT NULL AUTO_INCREMENT,
  -- CODE OMITTED
  PRIMARY KEY (id)
)

CREATE TABLE patient_doctors (
  id INT NOT NULL AUTO_INCREMENT,
  doctorId INT NOT NULL,
  patientId INT NOT NULL,

  FOREIGN KEY (doctorId)
    REFERENCES doctors(id),
  FOREIGN KEY (patientId)
    REFERENCES patients(id),
)

```

> SELECT patients p.\*
> FROM doctors d
> JOIN patient_doctors ON d.id = patient_doctors.doctorId
> JOIN patients p ON patientId = p.id
> WHERE d.id = doctor.id
