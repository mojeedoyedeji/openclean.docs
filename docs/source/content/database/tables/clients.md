# Clients

**Table Name:** `clients`  
**Description:** Stores client account details, service preferences, and related metadata.

## Columns

| Column Name        | Data Type                                                        | Description                                                          |
| ------------------ | ---------------------------------------------------------------- | -------------------------------------------------------------------- |
| id                 | `INT AUTO_INCREMENT PRIMARY KEY`                                 | Unique numeric identifier for each client.                           |
| title              | `ENUM('Mr.', 'Mrs.', 'Ms.', 'Dr.', 'Prof.')`                     | Client’s preferred title.                                            |
| name               | `VARCHAR(255)`                                                   | Full name of the client.                                             |
| phone              | `VARCHAR(20)`                                                    | Client’s contact phone number.                                       |
| email              | `VARCHAR(255) UNIQUE`                                            | Email address of the client.                                         |
| avatar             | `VARCHAR(2083)`                                                  | URL or path to the client’s profile image.                           |
| password           | `VARCHAR(255)`                                                   | Encrypted password.                                                  |
| address            | `TEXT`                                                           | Full residential address.                                            |
| province           | `VARCHAR(50)`                                                    | Province where the client resides.                                   |
| city               | `VARCHAR(100)`                                                   | City of residence.                                                   |
| postal             | `VARCHAR(20)`                                                    | Postal or ZIP code.                                                  |
| subscription       | `INT`                                                            | Foreign key reference to `subscriptions.id`.                         |
| description        | `TEXT`                                                           | Additional profile information.                                      |
| services           | `TEXT`                                                           | Services requested by the client.                                    |
| cleaning_frequency | `ENUM('daily', 'weekly', 'biweekly', 'monthly', 'custom')`       | Desired cleaning schedule.                                           |
| time_slots         | `TEXT`                                                           | Preferred time slots for service.                                    |
| flexible_on_timing | `BOOLEAN`                                                        | Whether the client allows flexible service times.                    |
| repeat_cleaner     | `BOOLEAN`                                                        | Whether the client prefers the same cleaner.                         |
| cleaning_supplies  | `BOOLEAN`                                                        | Whether the client provides cleaning supplies.                       |
| ecofriendly        | `BOOLEAN`                                                        | Whether eco-friendly products are preferred.                         |
| property_type      | `ENUM('apartment', 'house', 'condo', 'townhouse', 'other')`      | Type of property.                                                    |
| bedrooms           | `TINYINT`                                                        | Number of bedrooms.                                                  |
| bathrooms          | `TINYINT`                                                        | Number of bathrooms.                                                 |
| pets               | `BOOLEAN`                                                        | Whether pets are present.                                            |
| elevator           | `BOOLEAN`                                                        | Whether the building has an elevator.                                |
| parking            | `BOOLEAN`                                                        | Whether parking is available.                                        |
| preferred_days     | `TEXT`                                                           | Preferred days of the week for service.                              |
| auth               | `VARCHAR(255)`                                                   | Authentication method or token.                                      |
| referral           | `INT`                                                            | Foreign key reference to another client (`clients.id`) for referral. |
| created            | `DATETIME DEFAULT CURRENT_TIMESTAMP`                             | Timestamp when the account was created.                              |
| status             | `ENUM('active', 'inactive', 'banned')`                           | Current account status.                                              |
| modified           | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Last update time.                                                    |
| reset_token        | `VARCHAR(255)`                                                   | Token for password reset.                                            |
| token_expiry       | `DATETIME`                                                       | Expiration datetime for the reset token.                             |
| login_count        | `INT DEFAULT 0`                                                  | Number of successful logins.                                         |
| login_status       | `ENUM('online', 'offline', 'suspended')`                         | Last known login state.                                              |

## Relationships

- **Bookings (`bookings.client_id` → `clients.id`)**: Each client may have multiple bookings.
- **Payments (`payments.client_id` → `clients.id`)**: Each client may initiate multiple payments.
- **Subscriptions (`clients.subscription` → `subscriptions.id`)**: Indicates the subscription plan linked to the client.
- **Booking Logs (`booking_logs.author` → `clients.id`)**: Tracks booking-related actions made by the client.
- **Referrals (`clients.referral` → `clients.id`)**: Tracks which client referred another.
