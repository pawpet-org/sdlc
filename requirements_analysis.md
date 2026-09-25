# 2. Requirements Analysis

This document specifies the functional and non-functional requirements for the **PawPet** pet health record and reminder application.

## 1. Functional Requirements (FR)

### FR-1: User Account & Authentication
- **FR-1.1:** System shall allow users (pet owners) to register, log in, and manage their profiles.
- **FR-1.2:** System shall support secure password hashing and session authentication (e.g., JWT / OAuth).

### FR-2: Pet Profile Management
- **FR-2.1:** Users shall be able to create, view, edit, and soft-delete pet profiles (Name, Species, Breed, Age, Weight, Microchip ID, Photo).
- **FR-2.2:** System shall support multiple pets per user account.

### FR-3: Vaccination & Medical Records
- **FR-3.1:** Users shall be able to add medical entries (Vaccinations, Checkups, Surgeries, Allergies, Medications).
- **FR-3.2:** Each entry shall support recording Date, Provider/Clinic, Batch Number (for vaccines), Notes, and File Attachments (prescriptions/reports).

### FR-4: Reminder & Notification Engine
- **FR-4.1:** Users shall be able to schedule reminders for upcoming vaccinations, recurring medication, and routine checkups.
- **FR-4.2:** System shall trigger automated notifications (Email / In-App / Push) prior to and on the due date.
- **FR-4.3:** System shall highlight overdue health activities in red/alert state.

### FR-5: Records Export & Sharing
- **FR-5.1:** Users shall be able to export pet medical summaries into PDF or printable formats for veterinary visits.

## 2. Non-Functional Requirements (NFR)

### NFR-1: Usability & Mobile Responsiveness
- **NFR-1.1:** The UI shall be intuitive, responsive across desktop and mobile browsers, and accessible following WCAG 2.1 AA standards.

### NFR-2: Performance
- **NFR-2.1:** Page load times shall remain under 2 seconds on standard standard mobile data connection.
- **NFR-2.2:** Notification engine shall process and send alerts within 60 seconds of scheduled trigger times.

### NFR-3: Security & Data Privacy
- **NFR-3.1:** Data in transit shall be encrypted via HTTPS (TLS 1.3).
- **NFR-3.2:** User pet records and personal information shall be isolated using database tenant boundaries and strict authorization policies.

### NFR-4: Reliability & Availability
- **NFR-4.1:** System target uptime shall be 99.5%.
- **NFR-4.2:** Daily automated database backups with a Recovery Point Objective (RPO) under 24 hours.

## 3. User Roles & Key Use Cases

| User Role | Description | Core Capabilities |
| :--- | :--- | :--- |
| **Pet Owner** | End user managing pets | Add pets, log medical records, set reminders, receive notifications, export history |
| **System Administrator** | Platform administrator | Manage system metrics, monitor notification queues, handle user support |
