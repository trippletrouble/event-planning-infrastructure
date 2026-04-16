<div align="center">
  <h1>Event Planning</h1>
  
[![NestJS](https://img.shields.io/badge/NestJS-11.0.1-E0234E?style=flat-square&logo=nestjs)](https://nestjs.com/)
[![Next.js](https://img.shields.io/badge/Next.js-16.2.1-000000?style=flat-square&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19.2.4-61DAFB?style=flat-square&logo=react)](https://react.dev/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-4-06B6D4?style=flat-square&logo=tailwindcss)](https://tailwindcss.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178C6?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13.5-336791?style=flat-square&logo=postgresql)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma-7.6.0-2D3748?style=flat-square&logo=prisma)](https://www.prisma.io/)
[![Redis](https://img.shields.io/badge/Redis-7-D82C20?style=flat-square&logo=redis)](https://redis.io/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker)](https://www.docker.com/)
</div>


## Prerequisites
- Git
- Docker Desktop (with Docker Compose plugin)
- Free local ports: `3000` (frontend) and `3100` (backend)
- Optional for local non-Docker runs: Node.js `22.x` and npm

#Figma
https://www.figma.com/design/j6hPxpGU3xSX1fASU0jWu6/Event-Planing?node-id=0-1&p=f&t=KqyYZG7N5I7vLIkE-0

## Clone the Project
```powershell
git clone --recurse-submodules https://gitlab.hof-university.de/event-planning/infrastructure.git
cd Event-Planning
```

## Start the Project
### Development mode (hot reload)
```powershell
docker compose -f docker-compose.dev.yml up --build
```
- Frontend: `http://localhost:3000`
- Backend: `http://localhost:3100`

### Production mode
```powershell
docker compose up --build
```
- Frontend: `http://localhost:3000`
- Backend: `http://localhost:3100`


## Diagrams
### ER-Diagram
```mermaid
erDiagram
    USER {
        int user_id PK
        string first_name
        string last_name
        string email
        enum Type "Student|Company|Manager|Admin"
        date created_at
    }

    EVENT {
        int event_id PK
        string location
        int total_tickets
        int sold_tickets
        int available_tickets
    }

    EXHIBITOR {
        int exhibitor_id PK
        string name
    }

    EXHIBITOR_IN_EVENT {
        int exhibitor_id FK
        int event_id FK
        string location
        string one_time_password UK
    }

    USER_IN_EVENT {
      int user_id FK
      int event_id FK
      string one_time_password UK
    }

    USER ||--o{ USER_IN_EVENT : ""
    USER_IN_EVENT }o--o{ EVENT : ""
    EXHIBITOR ||--o{ EXHIBITOR_IN_EVENT : ""
    EXHIBITOR_IN_EVENT }o--o{ EVENT : ""
```