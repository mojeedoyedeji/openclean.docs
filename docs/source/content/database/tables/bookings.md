# Bookings

```{tip}
Helpful tips can be added like this.
```

**Table Name:** `bookings` <br>
**Description:** Stores information about customer clients.

## Columns

| Column Name         | Data Type                                                         | Description                                            |
| ------------------- | ----------------------------------------------------------------- | ------------------------------------------------------ |
| id                  | `INT PRIMARY KEY`                                                 | Unique identifier for the user.                        |
| provider            | `VARCHAR(255)`                                                    | Name of the service provider.                          |
| service             | `VARCHAR(20)`                                                     | Type or category of service provided.                  |
| client              | `VARCHAR(255) UNIQUE`                                             | Username or login identifier for the client.           |
| client_name         | `VARCHAR(255)`                                                    | Full name of the client.                               |
| client_phone        | `TEXT`                                                            | Contact phone number of the client.                    |
| client_email        | `VARCHAR(255)`                                                    | Email address of the client.                           |
| client_province     | `VARCHAR(100)`                                                    | Province where the client resides.                     |
| client_postal       | `TEXT`                                                            | Postal code of the client's address.                   |
| client_address      | `TEXT`                                                            | Full address of the client.                            |
| client_title        | `VARCHAR(50)`                                                     | Title or role of the client (e.g., Mr., Mrs., Dr.).    |
| client_description  | `TEXT`                                                            | Additional profile description for the client.         |
| client_availability | `BOOLEAN`                                                         | Whether the client is available (`TRUE` or `FALSE`).   |
| service_title       | `VARCHAR(255)`                                                    | Title or name of the service offered.                  |
| service_price       | `DECIMAL(10,2)`                                                   | Price of the service.                                  |
| service_description | `TEXT`                                                            | Description of the service.                            |
| service_coverage    | `TEXT`                                                            | Areas or regions where the service is available.       |
| service_location    | `TEXT`                                                            | Location details for the service.                      |
| service_pricing     | `TEXT`                                                            | Detailed pricing breakdown, if applicable.             |
| booking_date        | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP`                             | Date and time the booking was made.                    |
| reference           | `VARCHAR(100)`                                                    | Booking or transaction reference code.                 |
| cancel_reason       | `TEXT`                                                            | Reason for cancellation, if applicable.                |
| images              | `TEXT`                                                            | Image URLs or paths related to the service or booking. |
| payment_mode        | `VARCHAR(50)`                                                     | Mode of payment (e.g., Credit Card, PayPal, Cash).     |
| payment_due         | `DATE`                                                            | Payment due date.                                      |
| payment_ref         | `VARCHAR(100)`                                                    | Reference for the payment transaction.                 |
| status              | `ENUM('pending', 'confirmed', 'cancelled', 'completed')`          | Status of the booking or service request.              |
| status_code         | `VARCHAR(20)`                                                     | Internal status code for tracking.                     |
| created             | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP`                             | Record creation timestamp.                             |
| modified            | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Record last updated timestamp.                         |

## Relationships

- **Orders (`orders.user_id` → `users.id`)**: Each user can place multiple orders.
- **Transactions (`transactions.user_id` → `users.id`)**: Each user can make payments.
