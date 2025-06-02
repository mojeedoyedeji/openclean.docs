# Notifications

**Table Name:** `notifications`  
**Description:** Stores user-facing system messages or alerts, including delivery channel, recipient, and status.

## Columns

| Column Name | Data Type                                                                 | Description                                       |
| ----------- | ------------------------------------------------------------------------- | ------------------------------------------------- |
| id          | `INT AUTO_INCREMENT PRIMARY KEY`                                          | Unique identifier for each notification message.  |
| type        | `ENUM('info', 'warning', 'error', 'success')`                             | Type or severity of the message.                  |
| recipient   | `VARCHAR(255) NOT NULL`                                                   | Target recipient (user ID, email, or system tag). |
| message     | `TEXT NOT NULL`                                                           | Full message or notification body.                |
| title       | `VARCHAR(255)`                                                            | Optional title or subject of the message.         |
| channel     | `ENUM('email', 'sms', 'push', 'in-app')`                                  | Delivery channel used for this message.           |
| created     | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                      | Time the notification was created.                |
| updated     | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`          | Last updated timestamp.                           |
| status      | `ENUM('sent', 'pending', 'failed', 'read', 'archived') DEFAULT 'pending'` | Current state of the notification.                |

## Notes

- **`recipient`**: Can be used flexibly for user ID, email, or system-wide identifiers.
- **`channel`**: Restricts delivery to supported modes (email, SMS, etc.).
- **`status`**: Helps track the lifecycle of the notification (e.g., delivered or failed).

## Relationships

- **Users (`notifications.recipient` → `clients.id`)**: Messages are typically directed to a client or admin.
- **Delivery Logs (`logs.notification_id` → `notifications.id`)** _(optional)_: Track message retries, delivery events, etc.
