Experiment 1: Entity-Relationship (ER) Diagram
🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

🧪 Choose One Scenario:
🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

User Requirements:

Academic programs grouped under departments.
Students have admission number, name, DOB, contact info.
Instructors with staff number, contact info, etc.
Courses have number, name, credits.
Track course enrollments by students and enrollment date.
Add support for prerequisites (some courses require others).
🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

User Requirements:

Patient details including contact and insurance.
Doctors and their departments, contact info, specialization.
Appointments with reason, time, patient-doctor link.
Medical records with treatments, diagnosis, test results.
Billing and payment details for each appointment.
📝 Tasks:
Identify entities, relationships, and attributes.
Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
Include:
Cardinality & participation constraints
Prerequisites for University OR Billing for Hospital
Explain:
Why you chose the entities and relationships.
How you modeled prerequisites or billing.
ER Diagram Submission - Rahul V
Scenario Chosen:
University

ER Diagram:
Screenshot 2025-05-06 112346

Entities and Attributes:
Student-(Register No, Name, dob, EmailId, Mobile No)

Department -(department name, hod)

Course-(course name, course no, no. of credits)

Faculty- (Staff Id, mobile no, name, email)

Prerequisite Courses- (course name, credits)

Relationships and Constraints:
Belongs to (Student, Department)
Enrolls in (Student, Course)
Offers (Department, Course)
Handled by (Course, Faculty)
Has prerequisites (Course, Prerequisite Courses)
Belongs to (Faculty, Department)
Extension (Prerequisite / Billing):
The ER diagram models prerequisites using the has prerequisites relationship connecting Course to the Prerequisite Courses entity. This separate entity stores details like course name and credits for each prerequisite. This design allows a course to have multiple prerequisites, each with specific attributes, avoiding multi-valued attributes in the Course entity. The implied Many-to-Many relationship signifies that one course can have several prerequisites, and a course can be a prerequisite for many others. This approach ensures a flexible and normalized representation of prerequisite dependencies within the database.
Design Choices:
The entities in this ER diagram—Student, Department, Course, and Faculty—were chosen as they represent the core organizational units and actors within a typical academic institution. Students are the primary subjects of study, Departments are the administrative and academic groupings, Courses are the units of instruction, and Faculty are the educators and researchers. The relationships model the natural interactions between these entities: students belong to departments and enroll in courses; departments offer courses and faculty belong to and handle them; and courses have prerequisites. The inclusion of "Prerequisite Courses" as a separate entity, linked by the "has prerequisites" relationship, addresses the need to capture potentially multiple and attribute-rich prerequisite information for each course without complicating the main "Course" entity. Key assumptions include that every student and faculty member is associated with one department (total participation), and that the curriculum is structured around courses offered by departments and potentially requiring other courses as prerequisites. The Many-to-Many cardinalities for "enrolls in" and "handled by" reflect the reality that students take multiple courses and faculty teach multiple courses.

RESULT
Thus the ER diagram for the university database is successfully developed.
