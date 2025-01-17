---
title: Designing a Set of Tables for User Login in
date: 2025-01-09 15:37:36
tags:
---

Designing a robust and scalable user login system is a critical component of many applications. In this blog, we’ll explore how to design a set of MySQL tables for managing user login functionality and important SQL queries to interact with these tables effectively.

<!-- more -->
---

#### 1. Key Components of the Database Design
The design will include the following tables:

1. **Users Table**: Stores user information.
2. **Login Logs Table**: Tracks login attempts and details.
3. **Roles and Permissions Tables** (Optional): Implements role-based access control (RBAC).

Let’s break these down one by one.

---

### Users Table
The `users` table stores basic user details such as usernames, hashed passwords, and contact information.

```sql
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY, -- Unique user ID
    username VARCHAR(50) NOT NULL UNIQUE,   -- Username
    password_hash VARCHAR(255) NOT NULL,    -- Encrypted password
    email VARCHAR(100) UNIQUE,              -- Email address
    phone VARCHAR(15),                      -- Phone number (optional)
    is_active BOOLEAN DEFAULT TRUE,         -- Account activation status
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Account creation time
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP -- Last updated time
);
```

---

### Login Logs Table
The `login_logs` table records each login attempt, capturing details like IP address, device, and whether the login was successful.

```sql
CREATE TABLE login_logs (
    log_id INT AUTO_INCREMENT PRIMARY KEY,  -- Unique log ID
    user_id INT NOT NULL,                   -- User ID (foreign key)
    login_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Time of login
    ip_address VARCHAR(45),                 -- IP address (supports IPv4 and IPv6)
    device_info VARCHAR(255),               -- Information about the device used
    success BOOLEAN DEFAULT TRUE,           -- Whether the login was successful
    FOREIGN KEY (user_id) REFERENCES users(user_id) ON DELETE CASCADE
);
```

---

### Roles and Permissions Tables (Optional)
If your application requires role-based access control, include the following tables:

#### Roles Table
```sql
CREATE TABLE roles (
    role_id INT AUTO_INCREMENT PRIMARY KEY, -- Unique role ID
    role_name VARCHAR(50) UNIQUE NOT NULL,  -- Role name (e.g., Admin, User)
    description VARCHAR(255)                -- Description of the role
);
```

#### User Roles Table (Mapping Users to Roles)
```sql
CREATE TABLE user_roles (
    user_id INT NOT NULL,       -- User ID
    role_id INT NOT NULL,       -- Role ID
    PRIMARY KEY (user_id, role_id),
    FOREIGN KEY (user_id) REFERENCES users(user_id) ON DELETE CASCADE,
    FOREIGN KEY (role_id) REFERENCES roles(role_id) ON DELETE CASCADE
);
```

#### Permissions Table
```sql
CREATE TABLE permissions (
    permission_id INT AUTO_INCREMENT PRIMARY KEY, -- Unique permission ID
    permission_name VARCHAR(100) UNIQUE NOT NULL, -- Permission name
    description VARCHAR(255)                      -- Description of the permission
);
```

#### Role Permissions Table (Mapping Roles to Permissions)
```sql
CREATE TABLE role_permissions (
    role_id INT NOT NULL,          -- Role ID
    permission_id INT NOT NULL,    -- Permission ID
    PRIMARY KEY (role_id, permission_id),
    FOREIGN KEY (role_id) REFERENCES roles(role_id) ON DELETE CASCADE,
    FOREIGN KEY (permission_id) REFERENCES permissions(permission_id) ON DELETE CASCADE
);
```

---

#### 2. Important SQL Queries

##### 1. Insert a New User
```sql
INSERT INTO users (username, password_hash, email, phone)
VALUES ('john_doe', 'hashed_password_here', 'john@example.com', '1234567890');
```

##### 2. Record a Login Attempt
```sql
INSERT INTO login_logs (user_id, ip_address, device_info, success)
VALUES (1, '192.168.1.1', 'Chrome on Windows 10', TRUE);
```

##### 3. Fetch Login History for a User
```sql
SELECT login_time, ip_address, device_info, success
FROM login_logs
WHERE user_id = 1
ORDER BY login_time DESC;
```

##### 4. Assign a Role to a User
```sql
INSERT INTO user_roles (user_id, role_id)
VALUES (1, 2); -- Assign role_id 2 to user_id 1
```

##### 5. Check User Permissions
```sql
SELECT p.permission_name
FROM permissions p
JOIN role_permissions rp ON p.permission_id = rp.permission_id
JOIN user_roles ur ON rp.role_id = ur.role_id
WHERE ur.user_id = 1;
```

---

#### 3. Best Practices

- **Password Security**: Always store passwords as hashed values using strong algorithms like bcrypt.
- **Indexes**: Add indexes on frequently queried fields like `username` and `user_id`.
- **Foreign Key Constraints**: Use foreign key constraints to ensure data integrity between related tables.
- **Logging**: Regularly monitor and archive login logs to maintain database performance.
- **Scalability**: Consider sharding or partitioning large tables (e.g., `login_logs`) for better performance in high-traffic systems.

---

By following this design and using the provided queries, you can implement a secure and efficient user login system that scales with your application’s needs. Happy coding!


