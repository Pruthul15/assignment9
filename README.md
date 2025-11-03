# Assignment 9: SQL Database Operations with Docker Compose

**Student:** Pruthul Patel  
**Course:** IS 601  
**GitHub Repository:** https://github.com/Pruthul15/assignment9  
**Date:** October 9, 2025

---

## Overview

This assignment demonstrates SQL database operations using Docker Compose with FastAPI, PostgreSQL, and pgAdmin. The project showcases containerization (CLO9) and database integration with relational table design and CRUD operations (CLO11).

---

## Setup

### Start Services
```bash
cd ~/projects/assignment9
docker compose up
```

### Access pgAdmin
- URL: http://localhost:5050
- Login: admin@example.com / admin

### Database Connection
- Host: `db`
- Database: `fastapi_db`
- Username/Password: `postgres` / `postgres`

---

## Database Design

### Tables Created

**Users Table**
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Calculations Table**
```sql
CREATE TABLE calculations (
    id SERIAL PRIMARY KEY,
    operation VARCHAR(20) NOT NULL,
    operand_a FLOAT NOT NULL,
    operand_b FLOAT NOT NULL,
    result FLOAT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

## SQL Operations Completed

### A. Insert Records
```sql
INSERT INTO users (username, email) VALUES ('alice', 'alice@example.com');
INSERT INTO users (username, email) VALUES ('bob', 'bob@example.com');

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES ('add', 2, 3, 5, 1);
INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES ('divide', 10, 2, 5, 1);
INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES ('multiply', 4, 5, 20, 2);
```

### B. Query Data
```sql
SELECT * FROM users;
SELECT * FROM calculations;

SELECT u.username, c.operation, c.operand_a, c.operand_b, c.result
FROM calculations c
JOIN users u ON c.user_id = u.id;
```

### C. Update Record
```sql
UPDATE calculations SET result = 6 WHERE id = 1;
```

### D. Delete Record
```sql
DELETE FROM calculations WHERE id = 2;
```

---

## Key Results

**One-to-Many Relationship Demonstrated:**
- alice: 2 calculations (add, divide)
- bob: 1 calculation (multiply)

**JOIN Query Output:**
| username | operation | operand_a | operand_b | result |
|----------|-----------|-----------|-----------|--------|
| alice | add | 2 | 3 | 5 |
| alice | divide | 10 | 2 | 5 |
| bob | multiply | 4 | 5 | 20 |

---

## Learning Outcomes

- ✅ Set up multi-container applications with Docker Compose
- ✅ Created tables with foreign key relationships
- ✅ Performed CRUD operations (Create, Read, Update, Delete)
- ✅ Used JOIN queries to combine data from multiple tables
- ✅ Understood one-to-many relationships between users and calculations
- ✅ Implemented referential integrity with ON DELETE CASCADE

---

## Challenges & Solutions

**Challenge 1:** Foreign key constraint error when inserting calculations before users  
**Solution:** Ensured users were inserted before calculations to satisfy foreign key constraint

**Challenge 2:** Connected to wrong database initially  
**Solution:** Verified database name in docker-compose.yml and used correct `fastapi_db`

---

## Project Structure

```
assignment9/
├── docker-compose.yml
├── Dockerfile
├── main.py
├── requirements.txt
├── .github/workflows/
├── app/
├── templates/
└── README.md
```

---

## CI/CD Status

✅ All tests passing  
✅ Docker verification passed  
✅ Security scan completed

**Repository:** https://github.com/Pruthul15/assignment9

---

**Author:** Pruthul Patel  
**Course:** IS 601