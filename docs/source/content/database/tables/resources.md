# Resources

**Table Name:** `resources`  
**Description:** Stores links or resource entries submitted by users (clients or admins), including metadata like type, owner, and status.

## Columns

| Column Name | Data Type                                                             | Description                                                    |
| ----------- | --------------------------------------------------------------------- | -------------------------------------------------------------- |
| id          | `INT AUTO_INCREMENT PRIMARY KEY`                                      | Unique numeric identifier for the resource.                    |
| owner       | `VARCHAR(255) NOT NULL`                                               | Identifier (e.g., user ID or email) of the resource submitter. |
| title       | `VARCHAR(255) NOT NULL`                                               | Title or name of the resource.                                 |
| description | `TEXT`                                                                | Detailed description of the resource.                          |
| type        | `ENUM('link', 'video', 'file', 'image', 'other') NOT NULL`            | Type/category of the resource.                                 |
| url         | `VARCHAR(2048) NOT NULL`                                              | Full URL to the resource.                                      |
| shorten_url | `VARCHAR(100)`                                                        | Optional shortened URL or alias.                               |
| created     | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                  | Timestamp when the resource was created.                       |
| modified    | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`      | Timestamp of last update.                                      |
| status      | `ENUM('active', 'inactive', 'pending', 'rejected') DEFAULT 'pending'` | Current status of the resource.                                |

## Relationships

- **Clients/Admins (`resources.owner` → `clients.id` or `admins.id`)**: Links each resource to the user who submitted it.
- **Moderation Logs (`logs.resource_id` → `resources.id`)** _(optional)_: Used to track moderation actions on submissions.
