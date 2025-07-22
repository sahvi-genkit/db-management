# Spring Boot Project with Liquibase for AWS Aurora Postgres

## Project Overview
A sample Java Spring Boot application demonstrating best practices for database schema management using Liquibase, targeting AWS Aurora PostgreSQL.

## Functional Requirements
- REST API for managing a simple entity (e.g., Customer)
- CRUD operations for the entity

## Database & Migration Requirements
- Use AWS Aurora PostgreSQL as the primary database
- Manage schema changes using Liquibase
- Store changelogs in XML format under `db/changelog/`
- Use a dedicated schema for Liquibase tracking tables (e.g., `liquibase_schema`)
- Support for local development (Postgres) and production (Aurora)
- Example changelog for initial schema and a sample migration
- Secure DB credentials using environment variables

## Technical Requirements
- **Spring Boot 3.x**
- **Java 17**
- **Liquibase** integration via Maven plugin and Spring Boot starter
- **PostgreSQL** driver
- **Aurora**-compatible SQL (avoid unsupported features)
- **application.yml** with profiles for `local` and `prod`
- **README.md** with migration and deployment instructions

## Best Practices
- Use separate changelog files for each feature or release
- Use semantic versioning in changelog file names
- Always test migrations locally before applying to Aurora
- Use `contexts` and `labels` in Liquibase for environment-specific changes
- Avoid using unsupported Postgres features in Aurora
- Use a dedicated schema for Liquibase tables to avoid polluting the main schema
- Use `rollback` blocks in changelogs for safe downgrades

## Example Entity
- **Customer**: id (UUID), name, email, created_at, updated_at

## Success Criteria
- Application starts and runs migrations automatically
- Liquibase changelogs are tracked in the database
- CRUD API for Customer works end-to-end
- Documentation covers migration workflow for Aurora 