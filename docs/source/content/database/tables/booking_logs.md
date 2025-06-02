# Booking Logs

```{tip}
Helpful tips can be added like this.
```

**Table Name:** `booking_logs` <br>
**Description:** Stores information about booking logs

## Columns

| Column Name | Data Type                                                         | Description                                                    |
| ----------- | ----------------------------------------------------------------- | -------------------------------------------------------------- |
| id          | `INT PRIMARY KEY`                                                 | Unique identifier for the log entry.                           |
| booking     | `VARCHAR(255)`                                                    | Reference to the related booking (e.g., booking ID or code).   |
| type        | `VARCHAR(20)`                                                     | Type of log entry (e.g., update, cancellation, creation).      |
| author      | `VARCHAR(255)`                                                    | User who performed the action (e.g., client, provider, admin). |
| created     | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP`                             | Timestamp when the log entry was created.                      |
| modified    | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Timestamp when the log entry was last modified.                |
| status      | `ENUM('pending', 'confirmed', 'cancelled', 'completed')`          | Status of the booking at the time of the log entry.            |

## Relationships

- **Bookings (`orders.user_id` → `users.id`)**: Each user can place multiple orders.
- **Users (`transactions.user_id` → `users.id`)**: Each user can make payments.
