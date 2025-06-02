# Admins Table

**Table Name:** `admins`  
**Description:** Stores administrator credentials, role-based access information, and login metadata for backend users.

## Columns

| Column Name  | Data Type                                                           | Description                                                |
| ------------ | ------------------------------------------------------------------- | ---------------------------------------------------------- |
| id           | `INT AUTO_INCREMENT PRIMARY KEY`                                    | Unique numeric identifier for each admin.                  |
| name         | `VARCHAR(255) NOT NULL`                                             | Full name of the admin.                                    |
| email        | `VARCHAR(255) NOT NULL UNIQUE`                                      | Admin email address (used for login).                      |
| password     | `VARCHAR(255) NOT NULL`                                             | Encrypted password for authentication.                     |
| auth         | `VARCHAR(255)`                                                      | Optional external auth method or token (e.g., OAuth, SSO). |
| access       | `ENUM('superadmin', 'admin', 'editor') NOT NULL DEFAULT 'admin'`    | Role-based access control.                                 |
| created      | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                | Timestamp when the admin account was created.              |
| modified     | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`    | Timestamp of last update.                                  |
| status       | `ENUM('active', 'inactive', 'suspended') NOT NULL DEFAULT 'active'` | Current account status.                                    |
| login_status | `ENUM('online', 'offline', 'locked') DEFAULT 'offline'`             | Current session state of the admin.                        |
| login_count  | `INT DEFAULT 0`                                                     | Number of successful login attempts.                       |

## Relationships

- **Audit Logs (`logs.admin_id` → `admins.id`)**: Each admin's actions can be tracked in a logging table.
- **Roles (`admins.access` → `roles.slug`)** _(if roles table exists)_: Useful for permissions abstraction.
