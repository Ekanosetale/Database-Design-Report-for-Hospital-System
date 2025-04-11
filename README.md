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













