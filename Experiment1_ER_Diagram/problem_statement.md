# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.


## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

*User Requirements:*
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

*User Requirements:*
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Dhivyadharshini S

## Scenario Chosen:
University

## ER Diagram:
## Scenario 1: University Database
![ER-1](https://github.com/user-attachments/assets/a500d7f3-647a-4d50-b717-f572d9bdb59c)



## Entities and Attributes:
# Scenario 1

1.Student
- Attributes: Student_ID, Student_Name, Program
 
2.Faculty
- Attributes: ID, Name, Department, Experience

3.Course
- Attributes: Course_Code, Course_Name, Credits, Syllabus

4.Course-Offers
- Attributes: Time, Venue, Semester, Year, Description


## Relationships and Constraints:
1.Enrolls (Student → Course-Offers)
- Cardinality: Many-to-Many
- Participation: Total (Every Student must enroll in at least one Course)

2.Teaches (Faculty → Course-Offers)
- Cardinality: One-to-Many (One Faculty teaches multiple Course-Offers)
- Participation: Partial (Not every Faculty must teach)

3.Is Offering (Course-Offers → Course)
- Cardinality: Many-to-One (Many Course-Offers are linked to one Course)
- Participation: Total (Each Course-Offer must correspond to a Course)

4.Requires (Course → Course)
- Cardinality: Many-to-Many
- Participation: Partial (Some courses may have prerequisites, others may not)


## Extension (Prerequisite / Billing):
The 'Requires' relationship captures prerequisites, connecting a Course entity back to another Course. "Pre-requisite" and "Maincourse" are labeled to distinguish which course is dependent on which.

## Design Choices:
- Course-Offers as a Separate Entity:
Instead of linking Students and Faculty directly to Courses, an intermediate Course-Offers entity was used to handle dynamic attributes like Semester, Year, Venue, and Time, making the design more flexible for repeated offerings of the same course.

- Modeling Prerequisites Separately:
By adding the Requires relationship between Courses, the model easily allows for complex prerequisite chains (multiple prerequisites for a course and vice-versa).

- Flexibility and Scalability:
This design supports multiple offerings of a course by different faculty members over different semesters, making it adaptable for real-world university systems.

- Simplicity and Readability:
Entities are kept intuitive (Student, Faculty, Course) and attributes are straightforward, ensuring that the schema is easy to understand and expand later.

## RESULT
Thus the concepts of ER modeling by creating an ER diagram for a real-world application was applied successfully.
