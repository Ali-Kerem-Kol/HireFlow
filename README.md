# Toyota 32Bit Internship Portal

A full-stack applicant tracking system built as a senior capstone project. Manages the entire internship recruitment pipeline — from job postings and applications to task assignments and candidate evaluation.

## Features

**Candidate Portal:**
- Registration with email verification and password reset
- Profile and CV management
- Browse and apply to open positions
- Track assigned tasks with file uploads
- Availability calendar

**Admin Dashboard:**
- Create and manage job postings
- Review applications and update statuses
- Assign tasks, track progress with timeline view
- Bulk email campaigns
- CSV export, admin notes, question pool management

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Java 17, Spring Boot 3.3, Spring Security, JWT |
| Frontend | React 19, TypeScript, Vite, Tailwind CSS |
| Database | PostgreSQL 16, Flyway migrations |
| Infrastructure | Docker, Docker Compose, Nginx |
| Email | Spring Mail + Mailpit (dev) |

## Project Structure

```
├── backend/                  # Spring Boot REST API
│   ├── src/main/java/
│   │   └── com/project/project/
│   │       ├── config/       # App config & exception handlers
│   │       ├── controller/   # REST controllers
│   │       ├── dto/          # Request/Response DTOs
│   │       ├── entity/       # JPA entities
│   │       ├── repository/   # Spring Data repositories
│   │       ├── security/     # JWT auth & filters
│   │       └── service/      # Business logic
│   └── src/main/resources/
│       └── db/migration/     # Flyway SQL migrations
├── frontend/                 # React SPA
│   └── src/
│       ├── api/              # Axios API client
│       ├── auth/             # Auth context & hooks
│       ├── components/       # Reusable UI components
│       ├── pages/            # Page components
│       ├── hooks/            # Custom React hooks
│       └── lib/              # Utility functions
├── scripts/                  # Helper scripts
├── docker-compose.yml
└── .env.example
```

## Getting Started

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) & Docker Compose
- Git

### Quick Start

```bash
git clone https://github.com/Ali-Kerem-Kol/Toyota-32Bit-Basvuru-Portali.git
cd Toyota-32Bit-Basvuru-Portali
cp .env.example .env
docker compose up -d --build
```

| Service | URL |
|---------|-----|
| Frontend | http://localhost:3000 |
| Backend API | http://localhost:8080/api/v1 |
| Mailpit (SMTP UI) | http://localhost:8025 |

### Default Admin Account

An admin account is automatically seeded on first startup:

- **Email:** `admin@32bit.com.tr`
- **Password:** `Admin12345!`

Configurable via `.env` file.

### Local Development (without Docker)

**Backend:**
```bash
cd backend
./mvnw spring-boot:run -Dspring-boot.run.profiles=dev
```

**Frontend:**
```bash
cd frontend
npm install
npm run dev
```

> Requires a running PostgreSQL instance and Mailpit for email.

## Database Reset

```bash
docker compose down -v
docker compose up -d --build
```

Or use the helper scripts:

```bash
# Linux / macOS
bash ./scripts/reset-db.sh

# Windows (PowerShell)
.\scripts\reset-db.ps1
```

## API Overview

- RESTful API under `/api/v1`
- JWT Bearer token authentication
- Role-based access control: `USER`, `ADMIN`
- Automatic database migrations via Flyway
- File uploads (CV, task attachments) — max 50MB

## License

This project is licensed under the [MIT License](LICENSE).
