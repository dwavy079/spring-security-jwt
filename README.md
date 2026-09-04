### 🐝 HiveMind — File Sharing App
A full-stack file-sharing platform with folder organization, automatic file versioning, and shareable download links.
- **Backend:** Spring Boot 3 (Java 17), Spring Security + JWT (access/refresh token rotation), JPA/Hibernate (PostgreSQL/H2)
- **Frontend:** React 18 + Vite
- **Storage:** AWS S3 (SDK v2) — files never touch local disk
- **Features:** nested folders, per-file version history, expiring public share links with download tracking

## Stack

- Java 25, Spring Boot 4.1
- Spring Security 7, JJWT 0.11.5
- Spring Data JPA / Hibernate 7
- PostgreSQL
- Maven, Lombok

## Features

- User registration and login returning access + refresh tokens
- Stateless JWT authentication via a request filter
- Tokens persisted to the database, with previous tokens revoked on each login
- BCrypt password hashing
- Role-based user model

## Endpoints

| Method | Path | Auth | Description |
|---|---|---|---|
| POST | `/api/v1/auth/register` | No | Create an account, returns tokens |
| POST | `/api/v1/auth/authenticate` | No | Log in, returns tokens |
| GET | `/api/v1/demo-controller` | Bearer token | Example protected endpoint |

## Running locally

Requires PostgreSQL running with a `securitydb` database.

```bash
mvn spring-boot:run
```

The app starts on port 8080.

## Notes

Built against Spring Boot 4, which differs from the Spring Boot 3 tutorial in
several places: Lombok requires explicit `annotationProcessorPaths` on JDK 23+,
`DaoAuthenticationProvider` takes its `UserDetailsService` via constructor,
`AuthenticationManager` is built directly as a `ProviderManager`, and Jackson
moved to the `tools.jackson` package.
