# Spring Boot + Liquibase + AWS Aurora Postgres Sample

This project demonstrates best practices for managing database schema using Liquibase in a Java Spring Boot application targeting AWS Aurora PostgreSQL.

## 📦 Project Structure

- `pom.xml` - Maven build file with Spring Boot, Liquibase, and Postgres dependencies
- `src/main/resources/application.yml` - Spring Boot config for local and prod (Aurora) profiles
- `src/main/resources/liquibase.properties` - Liquibase CLI properties
- `db/changelog/` - Liquibase changelogs (XML)
- `db/changelog/db.changelog-master.xml` - Master changelog
- `db/changelog/db.changelog-1.0-initial.xml` - Initial schema for Customer entity

## 🚀 Quick Start

### 1. Prerequisites
- Java 17+
- Maven 3.8+
- AWS Aurora PostgreSQL or local Postgres

### 2. Configure Database
Set environment variables for your environment:

#### Local
```
export LOCAL_DB_HOST=localhost
export LOCAL_DB_PORT=5432
export LOCAL_DB_NAME=sampledb
export LOCAL_DB_USER=postgres
export LOCAL_DB_PASSWORD=yourpassword
```

#### Aurora (Production)
```
export AURORA_HOST=aurora-cluster.cluster-xxxxxx.us-east-1.rds.amazonaws.com
export AURORA_PORT=5432
export AURORA_DB=sampledb
export AURORA_USER=aurorauser
export AURORA_PASSWORD=aurorapass
```

### 3. Run Migrations

#### With Spring Boot (auto on startup)
```
mvn spring-boot:run -Dspring-boot.run.profiles=local
```

#### With Liquibase CLI
```
mvn liquibase:update -Dspring.profiles.active=local
```

### 4. Best Practices
- Use a dedicated schema for Liquibase tracking tables (`liquibase_schema`)
- Use separate changelog files for each feature/release
- Test migrations locally before applying to Aurora
- Use `rollback` blocks for safe downgrades
- Avoid unsupported Postgres features in Aurora

### 5. Example Entity
The initial changelog creates a `customer` table:
- `id` (UUID, PK)
- `name` (string)
- `email` (unique string)
- `created_at`, `updated_at` (timestamps)

### 6. Migration Workflow
1. Add new changelog XML in `db/changelog/` (e.g., `db.changelog-1.1-add-orders.xml`)
2. Reference it in `db.changelog-master.xml` with `<include file=... />`
3. Test locally, then apply to Aurora

### 7. Troubleshooting
- Check the `DATABASECHANGELOG` and `DATABASECHANGELOGLOCK` tables in `liquibase_schema`
- Use `mvn liquibase:status` to see pending changes
- Use `mvn liquibase:rollback` for downgrades

### 8. References
- [Liquibase Docs](https://docs.liquibase.com/)
- [Spring Boot + Liquibase](https://docs.spring.io/spring-boot/docs/current/reference/html/howto.html#howto.data-initialization.migration-tool.liquibase)
- [AWS Aurora PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.Reference.html) 