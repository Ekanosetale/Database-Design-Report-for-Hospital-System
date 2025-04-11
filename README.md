# Database-Design-Report-for-Hospital-System

## Executive Summary
This report outlines the database system design developed for a hospital seeking to manage patient registration, appointments, medical history, doctors, departments, and reviews. The database was designed using SQL Server and developed based on consultation with hospital stakeholders and their functional requirements. The system enforces data integrity, supports patient interactions through a portal, ensures accurate appointment tracking, and allows healthcare staff to manage medical records effectively.

This report outlines the design decisions, processes, and steps involved in creating a database system tailored to the hospital's requirements, including the creation of necessary tables and constraints in SQL Server.

### Requirements Overview

The system needs to address the following core functionalities:

Patient Registration: Storing personal and contact information, insurance details, username, and password.

Appointment Management: Booking, tracking, and updating appointment details, including patient and doctor information.

Medical Record Management: Storing diagnoses, prescribed medicines, past appointments, and allergies.

Doctor Review: Collecting and storing patient reviews of doctors after an appointment.

Data Integrity and Constraints: Enforcing data validation for appointment dates, password lengths, and appointment statuses.

### Entity Relationship Design

The design is based on the following entities and their relationships:

Patient: Stores information about the patient, including their personal and contact details, insurance, and login credentials.

Department: Stores information about the hospital's departments, including department names, department heads, and contact information.

Doctor: Stores doctor-specific information, including the department they belong to, specialization, and contact details.

Appointment: Manages appointment details between patients and doctors, including status and reasons for appointments.

Medical Record: Contains a record of a patient's medical history, including diagnoses, prescribed medicines, allergies, and past appointments.

-- CREATE THE DATABASE

          *CREATE DATABASE HospitalDB;*

-- SWITCH TO THE NEW DATABASE

          *USE HospitalDB;*


### Patient Table
The Patient table stores all the essential information related to the patient. The columns include PatientID (primary key), FullName, Gender, Address, DateOfBirth, InsuranceID, EmailAddress, PhoneNumber, UserName, and Password. The Password column is restricted to 8 characters to ensure proper security.

           *CREATE TABLE Patient*(
                 PatientID INT PRIMARY KEY IDENTITY(1,1),
                 FullName VARCHAR(50),
                 Gender CHAR(1),
                 Address TEXT,
                 DateOfBirth DATE NOT NULL,
                 InsuranceID VARCHAR(50) NOT NULL,
                 EmailAddress VARCHAR(50),
                 PhoneNumber VARCHAR(50),
                 UserName VARCHAR(50) NOT NULL,
                 Password CHAR(8) CHECK(LEN(Password) >= 8) NOT NULL
         );

*Justification:*
The PatientID is auto-incremented to ensure uniqueness.

EmailAddress and PhoneNumber are optional to accommodate diverse patient preferences.

Password length constraint enforces security policies.

**Department Table**
The Department table stores information about different hospital departments.

*CREATE TABLE Department*(
    DepartmentID INT PRIMARY KEY IDENTITY(1,1),
    DepartmentName VARCHAR(50) NOT NULL,
    HeadOfDepartment VARCHAR(50) NOT NULL,
    PhoneNumber VARCHAR(20) NOT NULL
);

*Justification:*

DepartmentID is auto-generated to ensure uniqueness.

HeadOfDepartment is included to assign responsibility for each department.

**Doctor Table**
The Doctor table stores details about the doctors, including their specialty and which department they belong to.

*CREATE TABLE Doctor*(
    DoctorID INT PRIMARY KEY IDENTITY(1,1),
    DepartmentID INT NOT NULL FOREIGN KEY REFERENCES Department(DepartmentID),
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(50),
    PhoneNumber VARCHAR(20),
    Gender CHAR(1),
    Specialization VARCHAR(50)
);

*Justification:*

Doctors are linked to departments via DepartmentID to track which department each doctor belongs to.


**Appointment Table**
The Appointment table records patient appointments, including the date, time, status, and reason for the appointment.

*CREATE TABLE Appointment*(
    AppointmentID INT PRIMARY KEY IDENTITY(1,1),
    PatientID INT NOT NULL FOREIGN KEY REFERENCES Patient(PatientID),
    DoctorID INT NOT NULL FOREIGN KEY REFERENCES Doctor(DoctorID),
    AppointmentDate DATE NOT NULL,
    AppointmentTime TIME NOT NULL,
    Status VARCHAR(50) CHECK (Status IN ('pending', 'cancelled', 'completed')),
    Reason TEXT NOT NULL
);

*Justification:*

AppointmentDate and AppointmentTime ensure that appointments are scheduled correctly.

The Status column tracks whether an appointment is pending, cancelled, or completed.

The Reason column records the reason for the appointment, which helps doctors in their diagnosis.

**Medical Record Table**
The Medical_Record table contains detailed information about a patient’s medical history, including diagnoses and prescribed medicines.

*CREATE TABLE Medical_Record*(
    MRecord INT PRIMARY KEY IDENTITY(1,1),
    PatientID INT NOT NULL FOREIGN KEY REFERENCES Patient(PatientID),
    DoctorID INT NOT NULL FOREIGN KEY REFERENCES Doctor(DoctorID),
    PastAppointment TEXT,
    Diagnosis VARCHAR(50) NOT NULL,
    Medicine VARCHAR(50) NOT NULL,
    Allergies VARCHAR(50)
);

*Justification:*

MRecord ensures each record is unique.

The inclusion of PastAppointment helps doctors to track the patient's medical journey.

**Review Table**
The Review table stores feedback given by patients about their doctors.

*CREATE TABLE Review*(
         ReviewID INT PRIMARY KEY IDENTITY(1,1),
         PatientID INT NOT NULL FOREIGN KEY REFERENCES Patient(PatientID),
         DoctorID INT NOT NULL FOREIGN KEY REFERENCES Doctor(DoctorID),
         Review TEXT NOT NULL, 
         ReviewDate DATE NOT NULL
);

*Justification:*

The Review column captures feedback, and the ReviewDate records when the feedback was provided.

*Appointment Date Validation*
To ensure that appointments are not scheduled in the past, the following constraint is added:

**ALTER TABLE Appointment**
ADD CONSTRAINT chk_AppointmentDate CHECK (AppointmentDate >= GETDATE());

*Justification:*

This constraint ensures that appointments are only scheduled for future dates.


### Conclusion
The hospital database design fulfills all identified business needs including patient management, appointment scheduling, medical history tracking, and doctor reviews. It promotes efficient record-keeping, enhances patient engagement via the portal, and supports decision-making by healthcare professionals. With added features and role-based security, this system can scale to meet broader clinical requirements in the future.
























