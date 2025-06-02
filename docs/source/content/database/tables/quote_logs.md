# Quote Logs

**Table Name:** `quote_logs`  
**Description:** Stores historical records or activity logs related to specific quotes, such as status changes, internal actions, or author notes.

## Columns

| Column Name | Data Type                                                        | Description                                                                 |
| ----------- | ---------------------------------------------------------------- | --------------------------------------------------------------------------- |
| id          | `INT AUTO_INCREMENT PRIMARY KEY`                                 | Unique identifier for each log entry.                                       |
| quote       | `INT NOT NULL`                                                   | Foreign key reference to `quotes.id`, identifying the associated quote.     |
| type        | `ENUM('status_change', 'note', 'comment', 'auto_action')`        | Type of log entry.                                                          |
| author      | `INT`                                                            | Foreign key to the user (client, provider, or admin) who triggered the log. |
| created     | `DATETIME DEFAULT CURRENT_TIMESTAMP`                             | Time the log entry was created.                                             |
| modified    | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Time of last modification.                                                  |
| status      | `VARCHAR(255)`                                                   | Optional status label or comment value associated with the log.             |

## Relationships

- **Quotes (`quote_logs.quote` → `quotes.id`)**: Associates the log entry with a specific quote.
- **Users (`quote_logs.author` → `clients.id` or `admins.id`)**: Identifies the actor (could be system, admin, or client).

## Notes

- Consider replacing `author` with a polymorphic reference (e.g., `author_id` + `author_type`) if authors come from different tables.
- You may also rename `status` to `message` or `note` if it's used for freeform text.
- `type` should be validated to control what kind of actions are logged.
