# Assignment 9: Database Integration with FastAPI, PostgreSQL, and pgAdmin

**Student:** Pruthul Patel  
**GitHub Repository:** https://github.com/Pruthul15/assignment9  
**Date:** October 9, 2025

---

## Overview

This assignment demonstrates SQL database operations using Docker Compose with FastAPI, PostgreSQL, and pgAdmin.

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

### Connect to Database
- Host: `db`
- Database: `fastapi_db`
- Username/Password: `postgres` / `postgres`


---

## SQL Operations Completed

### A. Create Tables
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

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

### B. Insert Records
```sql
INSERT INTO users (username, email) VALUES ('john_doe', 'john@example.com');
INSERT INTO users (username, email) VALUES ('jane_smith', 'jane@example.com');

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES ('add', 2, 3, 5, 1);

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES ('multiply', 4, 5, 20, 2);
```

### C. Query Data
```sql
SELECT * FROM users;
SELECT * FROM calculations;

-- JOIN query
SELECT users.username, calculations.operation, calculations.result
FROM calculations
JOIN users ON calculations.user_id = users.id;
```

### D. Update Record
```sql
UPDATE calculations SET result = 6 WHERE id = 1;
```

### E. Delete Record
```sql
DELETE FROM calculations WHERE id = 2;
```

---

## Screenshots Included

1. Docker Compose running in terminal
2. pgAdmin tables view (users and calculations tables)
3. JOIN query results showing users and their calculations

---

## What I Learned

- Set up multi-container applications with Docker Compose
- Created tables with foreign key relationships
- Performed CRUD operations (Create, Read, Update, Delete)
- Used JOIN queries to combine data from multiple tables
- Understood one-to-many relationships between users and calculations

---

## Challenges & Solutions

**Challenge:** Foreign key constraint error when inserting calculations before users  
**Solution:** Ensured users were inserted before calculations

**Challenge:** Connected to wrong database initially  
**Solution:** Verified database name in docker-compose.yml and used `fastapi_db`

---

**All CI/CD checks passing** | **Repository:** https://github.com/Pruthul15/assignment9