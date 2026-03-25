Quarkus don't follow the classic configuration method `persisntace.xml`,  unless specific advanced needs were required. To configure Hibernate on Quarkus, we need to change config in `applications.properties`.

**Quarkus JDBC Extensions:**

```
quarkus-jdbc-db2 for IBM DB2
quarkus-jdbc-derby for Apache Derby
quarkus-jdbc-h2 for H2
quarkus-jdbc-mariadb for MariaDB
quarkus-jdbc-mssql for Microsoft SQL Server
quarkus-jdbc-mysql for MySQL
quarkus-jdbc-oracle for Oracle Database
quarkus-jdbc-postgresql for PostgreSQL
```

**Config Sample:**

```properties
# Database Configuration
quarkus.datasource.db-kind = postgresql
quarkus.datasource.username = hibernate
quarkus.datasource.password = hibernate
quarkus.datasource.jdbc.url = jdbc:postgresql://localhost:5432/hibernate_db

# Quarkus hibernate configs
quarkus.hibernate-orm.database.generation=drop-and-create
```
