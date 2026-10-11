# Grocery E-Commerce – Full-Stack Web Application

Full-stack web application for a local grocery store that sells producers' goods. Producers submit batches of products, managers validate and track them, customers reserve products online, and volunteers handle reservations and in-store sales.

> **Context:** team project (group 03) built during the CAE course at University College Vinci, Brussels (2025).
> It was originally developed on the school's GitLab instance and migrated to GitHub to preserve it after I changed universities, which is why the history shows a couple of import commit.

## Features

- **Authentication & roles:** registration, login and password change secured with JWT; role-based access for customers, producers, volunteers and managers.
- **Batch management:** producers create product batches with photos (stored on Azure Blob Storage); managers accept or reject them with a reason and adjust quantities.
- **Shopping basket & reservations:** customers add products to a basket and reserve them for a pick-up date; volunteers process reservations.
- **Free sale:** in-store sales recorded by volunteers and managers.
- **Dashboard & statistics:** monthly and yearly sales charts per batch, product type management.
- **Notifications:** producers are notified when their batches are accepted or rejected.

## Tech stack

| Layer | Technologies |
|---|---|
| Front end | React 18, TypeScript, Vite, Material UI, React Router |
| Back end | Java 21, Spring Boot 3 (Web, Security, Data JPA), Hibernate, JWT, Swagger / OpenAPI |
| Database | PostgreSQL |
| Storage | Azure Blob Storage (product pictures) |
| Testing | JUnit 5 and Mockito (API), Vitest and React Testing Library (front end), Playwright (end-to-end) |
| DevOps | Docker, Docker Compose, Nginx reverse proxy, GitLab CI/CD (test → build → staging → production on Azure) |

## My contributions

- Back end in Java with Spring and Hibernate, including data management on PostgreSQL.
- Authentication and API security with JWT.
- Front-end pages in React and TypeScript: **password change**, **shopping basket** and **product management**.
- Unit tests for the back-end business logic with JUnit.
- UML use case and database diagrams, kept up to date during the project.

## Project structure

```
api/             Spring Boot REST API (controllers, services, repositories, JPA entities)
frontend/        React + TypeScript single-page application
e2e/             Playwright end-to-end tests
reverse-proxy/   Nginx configuration used in deployment
.gitlab-ci.yml   CI/CD pipeline from the original GitLab project
```

## Getting started

### Prerequisites

- Java 21 and Maven (or the included Maven wrapper)
- Node.js 20+ and npm
- Docker

### 1. Start the database

```bash
cd api
docker compose up -d        # PostgreSQL on localhost:5433
```

### 2. Run the API

Create `api/.env` with your own values (this file is ignored by Git):

```
SECRET_JWT=change-me
AZURE_BLOB_SAS_TOKEN=your-sas-token   # only needed for picture uploads
```

Then:

```bash
cd api
./mvnw spring-boot:run      # http://localhost:3000
```

Sample data is loaded from `api/src/main/resources/data.sql`. The API documentation is available at `http://localhost:3000/swagger-ui.html`.

### 3. Run the front end

```bash
cd frontend
npm install
npm run dev                 # http://localhost:5173, /api is proxied to the API
```

## Running the tests

```bash
cd api && ./mvnw test               # API unit tests (JUnit, Mockito)
cd frontend && npm test             # front-end tests (Vitest)
cd e2e && npx playwright test       # end-to-end tests (requires the app running)
```
