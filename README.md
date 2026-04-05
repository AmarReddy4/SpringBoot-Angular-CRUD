# SpringBoot-Angular-CRUD

A full-stack Employee Management System with a Spring Boot REST API backend and an Angular frontend. Provides complete CRUD (Create, Read, Update, Delete) operations for managing employee records, backed by a MySQL database.

## Tech Stack

### Backend
- **Framework:** Spring Boot 3.2.0
- **Language:** Java 17
- **ORM:** Spring Data JPA (Hibernate)
- **Database:** MySQL
- **Build Tool:** Maven

### Frontend
- **Framework:** Angular (served on port 4200)

## Features

- View a list of all employees
- Add a new employee with first name, last name, and email
- Update existing employee details
- Delete an employee record
- RESTful API with proper error handling (custom `ResourceNotFoundException`)
- CORS configured for Angular development server (`http://localhost:4200`)
- Auto DDL generation with Hibernate (`ddl-auto = update`)

## Project Structure

```
SpringBoot-Angular-CRUD/
└── springboot-backend/
    ├── pom.xml
    ├── src/main/java/springboot/springbootbackend/
    │   ├── SpringbootBackendApplication.java   # Application entry point
    │   ├── controller/
    │   │   └── EmployeeController.java         # REST controller with CRUD endpoints
    │   ├── exception/
    │   │   └── ResourceNotFoundException.java  # Custom 404 exception
    │   ├── model/
    │   │   └── Employee.java                   # JPA entity (id, firstName, lastName, emailId)
    │   └── repository/
    │       └── EmployeeRepository.java         # JPA repository interface
    └── src/main/resources/
        └── application.properties              # Database and Hibernate configuration
```

## API Endpoints

All endpoints are prefixed with `/api/v1/`.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/employees` | Get all employees |
| GET | `/api/v1/employees/{id}` | Get employee by ID |
| POST | `/api/v1/employees` | Create a new employee |
| PUT | `/api/v1/employees/{id}` | Update an employee |
| DELETE | `/api/v1/employees/{id}` | Delete an employee |

### Request/Response Body

**Employee object:**
```json
{
  "id": 1,
  "firstName": "John",
  "lastName": "Doe",
  "emailId": "john.doe@example.com"
}
```

### Error Handling

Requests for non-existent employee IDs return a `404 Not Found` response via the `ResourceNotFoundException`.

## Getting Started

### Prerequisites
- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+

### Database Setup

1. Create a MySQL database:
   ```sql
   CREATE DATABASE employee_management_system;
   ```

2. Update the database credentials in `springboot-backend/src/main/resources/application.properties` if your MySQL username/password differ from the defaults:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/employee_management_system?useSSL=false
   spring.datasource.username=root
   spring.datasource.password=password
   ```

   Hibernate will automatically create the `employees` table on startup (`ddl-auto = update`).

### Running the Backend

1. Navigate to the backend directory:
   ```bash
   cd springboot-backend
   ```

2. Build and run with Maven:
   ```bash
   ./mvnw spring-boot:run
   ```
   The API will be available at `http://localhost:8080/api/v1/`.

3. Alternatively, build the JAR and run it:
   ```bash
   ./mvnw clean package
   java -jar target/springboot-backend-0.0.1-SNAPSHOT.jar
   ```

### Testing the API

You can test the endpoints using `curl`:

```bash
# Get all employees
curl http://localhost:8080/api/v1/employees

# Create an employee
curl -X POST http://localhost:8080/api/v1/employees \
  -H "Content-Type: application/json" \
  -d '{"firstName":"Jane","lastName":"Smith","emailId":"jane.smith@example.com"}'

# Update an employee
curl -X PUT http://localhost:8080/api/v1/employees/1 \
  -H "Content-Type: application/json" \
  -d '{"firstName":"Jane","lastName":"Doe","emailId":"jane.doe@example.com"}'

# Delete an employee
curl -X DELETE http://localhost:8080/api/v1/employees/1
```
