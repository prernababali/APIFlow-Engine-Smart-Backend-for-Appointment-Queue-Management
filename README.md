#  APIFlow Engine  
### *Backend System for Smart Appointment & Queue Management*

##  Project Overview

**APIFlow Engine** is a backend-focused web application built using **Spring Boot**, designed to streamline appointment booking and queue handling in clinics or service-based businesses. It features **role-based access control**, automated scheduling, status-based appointment lifecycles, and real-time queue tracking. This system exposes clean and scalable **RESTful APIs**, built with **Spring Boot, MySQL, JPA**, and **Maven**, and thoroughly tested via **Postman**.


## 🛠️ Tech Stack

| Technology      | Purpose                            |
|---------------- |------------------------------------|
| Spring Boot     | Backend framework (REST APIs)      |
| MySQL           | Relational database                |
| JPA / Hibernate | ORM for DB operations              |
| Maven           | Build and dependency management    |
| Postman         | API testing                        |
| Eclipse IDE     | Java development environment       |


##  Features

- Role-based user access: Admin, Doctor, Receptionist, Patient
- Smart appointment scheduling with slot availability
- Dynamic queue management for real-time wait handling
- Appointment status lifecycle (Scheduled → Finished → Confirmed)
- Manual and automated cancellation support
- Email-ready architecture (email logic excluded in this version)
- Structured API endpoints for seamless frontend integration


##  Project Structure

src/

├── controller/       # REST API Controllers

├── service/          # Business logic layer

├── repository/       # Data access layer using JPA

├── model/            # Entity classes

├── dto/              # Data transfer objects

└── config/           # Security, database, etc.


##  Database Schema (Simplified)

- **Users**: `id`, `name`, `email`, `password`, `role`  
- **Doctors**: `id`, `user_id`, `specialization`, `availability`  
- **Appointments**: `id`, `doctor_id`, `patient_id`, `slot`, `status`  
- **Queue**: `id`, `appointment_id`, `position`, `status`


##  Sample API Endpoints

| Endpoint                  | Method | Description                      |
|---------------------------|--------|----------------------------------|
| `/api/register`           | POST   | User registration                |
| `/api/login`              | POST   | User login                       |
| `/api/appointments/book`  | POST   | Book appointment                 |
| `/api/appointments/{id}`  | PUT    | Update or cancel appointment     |
| `/api/queue/next`         | GET    | Get next person in queue         |


##  How to Run (Without Docker)

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/apiflow-engine.git
   ```

2. **Create MySQL database**
   ```sql
   CREATE DATABASE apiflowdb;
   ```

3. **Import schema**
   Run the SQL script from `src/main/resources/appointmentscheduler.sql` to create tables.

4. **Configure `application.properties`**
   Edit `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/apiflowdb
   spring.datasource.username=your_mysql_username
   spring.datasource.password=your_mysql_password
   spring.jpa.hibernate.ddl-auto=update
   ```

5. **Build and run the project**
   ```bash
   mvn spring-boot:run
   ```

6. **Test APIs**
   Use Postman to send requests to:
   ```
   http://localhost:8080/api/...
   ```

##  Appointment Lifecycle

| Status        | Trigger           | Description                  |
|---------------|-------------------|------------------------------|
| `scheduled`   | On booking        | Default status after booking |
| `finished`    | System time check | After appointment end time   |
| `confirmed`   | 24h after finish  | If no rejection requested    |
| `invoiced`    | Manual or system  | When invoice is issued       |
| `canceled`    | Customer/Doctor   | Within allowed rules         |
| `rejected`    | Customer/Doctor   | If appointment did not occur |


## User Roles

- **Admin**: Can create providers, assign services, view all data
- **Doctor**: Manages their availability, appointments, and services
- **Receptionist**: Handles appointment scheduling and patient queues
- **Patient**: Can book, cancel, or reschedule appointments


##  Future Enhancements

- Integrate email/SMS notifications
- JWT-based authentication
- Admin dashboard with analytics (appointments, queue stats)
- Docker support (optional later)



