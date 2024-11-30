# Software Requirements Specification (SRS) for Pulse

## 1. Introduction

### 1.1 Purpose  
Pulse is a modern, lightweight employee scheduling tool designed to streamline workforce management. Pulse enables managers to create, edit, and monitor schedules while empowering employees to view shifts and submit time-off requests, all within a responsive and intuitive interface.

### 1.2 Scope  
Pulse is part of the Honeycomb Business Suite, aiming to provide efficient scheduling and communication between managers and employees. The app supports OAuth authentication, role-based access control (RBAC), and a dynamic calendar interface to manage schedules seamlessly.

### 1.3 Definitions, Acronyms, Abbreviations  
- **OAuth**: Open Authorization, an industry standard for secure user authentication.  
- **RBAC**: Role-Based Access Control.  
- **API**: Application Programming Interface.  

### 1.4 References  
- [Mina Scheduler Library - GitHub](https://github.com/Mina-Massoud/next-ui-full-calendar)  
- [Keycloak OAuth Documentation](https://www.keycloak.org/documentation)

---

## 2. System Overview  
Pulse provides a centralized platform for shift scheduling and time-off management. The system includes a role-based dashboard for employees and managers, a notification system, and a customizable calendar interface.

### 2.1 Target Users  
- **Managers**: To manage shifts and approve requests.  
- **Employees**: To view schedules and submit requests.  

---

## 3. Functional Requirements  

### 3.1 Authentication  
- Use Keycloak for OAuth 2.0-based secure login.  
- Role-based access for employees and managers.

### 3.2 Employee Features  
- View personal schedule in a calendar view.  
- Submit time-off requests with reasons.  
- Receive notifications for shift changes and approvals.  
- Swap shifts with other employees.  
- Offer or pick up shifts from other employees.  

### 3.3 Manager Features  
- Create, update, and delete shifts.  
- Approve or reject time-off requests.  
- Approve or reject shift swaps.  
- Approve or reject shift offers/pickups.  
- Assign employees to shifts and handle conflicts.

### 3.4 Notification System  
- Send email or in-app alerts for:
  - Schedule updates.  
  - Approval/denial of time-off requests.  

### 3.5 Calendar UI  
- **Views**:
  - Day, week, and month views for schedules.  
  - View individual or full schedules.  

---

## 4. Non-Functional Requirements  

### 4.1 Usability  
- Fully responsive for desktop and mobile.
  - Mobile options for Android and iOS.  
- Accessible for users with basic technical proficiency.

### 4.2 Performance  
- Handle up to 100 concurrent users without performance degradation.

### 4.3 Reliability  
- 99.9% uptime SLA for production environments.

### 4.4 Security  
- Secure all endpoints using OAuth tokens.  
- Encrypt sensitive data during transmission and storage.  

---

## 5. System Architecture  

### 5.1 Frontend  
- **Framework**: React with Next.js for SSR.  
- **Features**: Calendar UI, role-based views, notifications.  

### 5.2 Backend  
- **Framework**: Node.js with Express.js.  
- **Features**: API for authentication, schedule management, and notifications.

### 5.3 Database  
- **Database**: PostgreSQL for relational data storage.  
- **Schemas**:  
  - **User**:  
    - `id` (Primary Key)  
    - `role` (Manager, Employee)  
    - `name`  
    - `email` (Unique)  
    - `password` (Hashed)  
    - `created_at` (Timestamp)  

  - **Schedule**:  
    - `id` (Primary Key)  
    - `employee_id` (Foreign Key → User)  
    - `date`  
    - `start_time`  
    - `end_time`  
    - `created_at` (Timestamp)  

  - **Requests**:  
    - `id` (Primary Key)  
    - `employee_id` (Foreign Key → User)  
    - `status` (Pending, Approved, Denied)  
    - `start_date`  
    - `end_date`  
    - `reason` (Text)  
    - `created_at` (Timestamp)  

---

## 6. User Stories  

### 6.1 Employees  
- "As an employee, I want to view my schedule so that I can plan my week."  
- "As an employee, I want to request time off so that I can notify my manager of my availability."

### 6.2 Managers  
- "As a manager, I want to assign shifts to employees so that work schedules are clear."  
- "As a manager, I want to approve or reject time-off requests to maintain coverage."

---

## 7. Constraints  
- Compliance with GDPR for user data.  
- System must scale for small-to-medium-sized businesses.  

---
