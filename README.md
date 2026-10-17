# Smart Procurement and Vendor Management System

A web-based procurement management application built with **Java, Spring Boot, Spring Security, Thymeleaf, and MySQL**. It helps organizations manage vendors, create purchase requisitions, generate purchase orders, review approvals, and monitor procurement activity from a centralized dashboard.

## Features

- **Vendor management** — maintain supplier details and vendor status.
- **Requisition management** — create and track purchase requests and their item details.
- **Purchase order management** — create purchase orders linked to vendors, with order line items and totals.
- **Approval workflow** — review requisitions and purchase orders, record decisions, and manage approval comments.
- **Dashboard** — view procurement activity and pending work in one place.
- **Authentication and role-based access** — control access for administrators, procurement managers, and employees.
- **Reporting** — generate vendor reports and export report data to PDF/Excel using the reporting libraries included in the project.
- **REST API documentation** — explore API endpoints through Swagger UI.
- **Validation and error handling** — validate requests and handle application errors centrally.

## Technology Stack

| Area | Technology |
|---|---|
| Language | Java 17 |
| Backend | Spring Boot 3.2.5, Spring MVC |
| Persistence | Spring Data JPA, Hibernate |
| Security | Spring Security, JWT libraries |
| Frontend | Thymeleaf, HTML, CSS |
| Database | MySQL 8.x |
| API documentation | Springdoc OpenAPI / Swagger UI |
| Reporting | JasperReports, OpenPDF, Apache POI |
| Build tool | Maven |

## Prerequisites

Install the following before running the application:

- JDK 17 or later
- MySQL 8.x
- Maven (or use the included Maven Wrapper)
- Git (optional, for cloning the repository)

## Setup and Installation

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd Smart-Procurement-and-Vendor-Management-System
```

If you downloaded the source ZIP, extract it and open a terminal in the project root—the directory containing `pom.xml`.

### 2. Create the database

Start MySQL and run:

```sql
CREATE DATABASE procurement_db;
```

### 3. Configure database credentials

Open `src/main/resources/application.properties` and configure the MySQL connection for your local environment. The default database URL and username are configured for a local MySQL instance; set the password to your own MySQL password.

**Security note:** Do not commit real database passwords or signing secrets to Git. Prefer environment variables, and rotate any credential that has already been committed or shared. For example, you can configure Spring properties using environment-variable placeholders:

```properties
spring.datasource.url=${DB_URL:jdbc:mysql://localhost:3306/procurement_db?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true}
spring.datasource.username=${DB_USERNAME:root}
spring.datasource.password=${DB_PASSWORD}
```

Set `DB_PASSWORD` in your environment before starting the application. Update other security-related secrets similarly if applicable.

### 4. Run the application

Using Maven:

```bash
mvn clean spring-boot:run
```

On Windows, you can use the included wrapper:

```powershell
.\mvnw.cmd clean spring-boot:run
```

On macOS/Linux, use:

```bash
./mvnw clean spring-boot:run
```

The application is configured to use port **8083** by default.

### 5. Open the application

- **Web application:** http://localhost:8083/login
- **Swagger UI:** http://localhost:8083/swagger-ui.html
- **OpenAPI JSON:** http://localhost:8083/v3/api-docs

## Main Modules

- **Authentication** — login and access control.
- **Vendors** — vendor records and vendor-related information.
- **Requisitions** — purchase requests and request items.
- **Purchase orders** — purchase orders and order items.
- **Approvals** — approval decisions for procurement workflows.
- **Reports** — procurement/vendor reporting.
- **Audit logging** — records relevant application actions for traceability.

## Project Structure

```text
src/main/java/com/procurement/procurement/
├── config/          # Security, CORS, JPA, and Swagger configuration
├── controller/      # REST and web controllers
├── dto/             # Request and response DTOs
├── entity/          # JPA entities and domain models
├── exception/       # Application exceptions and global error handling
├── mapper/          # DTO/entity mapping
├── repository/      # Spring Data repositories
├── service/         # Business logic
└── ProcurementApplication.java

src/main/resources/
├── templates/       # Thymeleaf pages
├── static/css/      # Stylesheets
├── jasper/          # JasperReports templates
└── application.properties
```

## User Roles

The application is designed around these roles:

- **ADMIN** — administrative access across the application.
- **PROCUREMENT_MANAGER** — vendor, purchase-order, and approval-related tasks.
- **EMPLOYEE** — create and track procurement requisitions.

Use only demo credentials that are explicitly configured in your local setup. If credentials are not seeded automatically, create or seed users using the project's supported initialization process. Do not deploy with default or demo passwords.

## API Overview

The REST API includes controller groups for:

- Authentication
- Vendor management
- Requisitions
- Purchase orders
- Approvals
- Reports

For exact paths, request parameters, and request/response schemas, run the application and open Swagger UI at `http://localhost:8083/swagger-ui.html`.

## Troubleshooting

- **Database connection fails:** confirm MySQL is running, the database exists, and `DB_URL`, `DB_USERNAME`, and `DB_PASSWORD` (or the corresponding properties) are correct.
- **Port 8083 is busy:** stop the other process using the port or change `server.port` in `application.properties`.
- **Build fails:** verify that JDK 17+ is installed and that Maven can download dependencies; then retry `mvn clean package`.
- **Login does not work:** check how users and roles are initialized in the project and use valid local credentials. Do not assume demo accounts exist unless they have been configured.

## Contributing

1. Create a branch for your change.
2. Keep business logic in the service layer and persistence operations in repositories.
3. Validate API inputs and avoid returning sensitive entity fields.
4. Test the affected workflow before opening a pull request.