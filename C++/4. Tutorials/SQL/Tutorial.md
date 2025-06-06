V
- To use SQLite locally, no server setup is needed. Just open your terminal and run:


```
sqlite3 mydatabase.db
```

- This creates a new database file named `mydatabase.db` (or opens it if it exists).
    
- To quit the SQLite prompt:
    

```
.quit
```

### 1. _Foundations_

1. What is SQL?
    

- SQL = _Structured Query Language_
    
- Language used to communicate with relational databases like SQLite.
    
- You use SQL commands to **create**, **read**, **update**, **delete** data.
    

2. Connect to SQLite
    

- Open terminal and type:
    

```
sqlite3 mydatabase.db
```

- You’ll see the SQLite prompt:
    

```
sqlite>
```

This means you're connected successfully.

3. Check Existing Tables
    

- Run this SQL command:
    

```
.tables
```

It will list all tables in the current database.

4. Create Your First Database
    

- SQLite databases are created automatically as files, so no explicit `CREATE DATABASE` is required.
    

5. Switch Database
    

- Quit SQLite and open another file:
    

```
.quit
sqlite3 another.db
```


### 2. _Data Control & Modification_

1. Creating a Table
    

```
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

- `AUTOINCREMENT` is optional in SQLite :  `INTEGER PRIMARY KEY` auto-increments by default.
    
- To list tables:
    

```
.tables
```

2. Inserting Data
    

```
INSERT INTO users(name, email) VALUES
('Tim', 'tim@example.com'),
('Simon', 'simon@example.com');
```

3. Querying Data
    

```
SELECT * FROM users;
SELECT name FROM users WHERE id = 1;
```

4. Updating Data
    

```
UPDATE users
SET name = 'Robert'
WHERE email = 'simon@example.com';
```

5. Deleting Data
    

```
DELETE FROM users
WHERE name = 'Robert';
```

### 3. _Relational Database Design_

1. What's a relational database?
    

- A database where tables can relate to each other via **foreign keys**.
    

2. Create Related Tables
    

```
PRAGMA foreign_keys = ON;

CREATE TABLE accounts (
    id INTEGER PRIMARY KEY,
    user_id INTEGER,
    balance REAL DEFAULT 0.00,
    type TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

3. Insert Related Data
    

```
INSERT INTO accounts (user_id, balance, type) VALUES
(2, 1000.00, 'savings');
```

4. Join Tables
    

```
SELECT users.name, accounts.type, accounts.balance
FROM users
JOIN accounts ON users.id = accounts.user_id;
```

5. Types of JOINs
    

```
+-------------+------------------------------------+
| JOIN Type   | Description                        |
+-------------+------------------------------------+
| INNER JOIN  | Only matching records              |
| LEFT JOIN   | All from left + matched from right |
+-------------+------------------------------------+
```

- Example:
    

```
SELECT users.name, accounts.type
FROM users
LEFT JOIN accounts ON users.id = accounts.user_id;
```

6. Aliases for Clean Code
    

```
SELECT u.name, a.type
FROM users AS u
JOIN accounts AS a ON u.id = a.user_id;
```

### 4. _Power Tools_

To view results vertically (one column per row):

```
.mode column
.headers on
.width 15 15 15
SELECT * FROM users;
```

### Notes and Tips

- SQLite stores everything in a single `.db` file.
    
- You can open `.db` files directly and copy them as backups.
    
- SQLite doesn't support some MySQL features (e.g. `SHOW DATABASES`, user management, stored procedures, etc.).