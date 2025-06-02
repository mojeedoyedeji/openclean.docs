# Quotes

**Table Name:** `quotes`  
**Description:** Stores service quote requests submitted by clients to providers, including property details, service needs, and pricing options.

## Columns

| Column Name         | Data Type                                                                        | Description                                                   |
| ------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| id                  | `INT AUTO_INCREMENT PRIMARY KEY`                                                 | Unique identifier for each quote request.                     |
| provider            | `INT NOT NULL`                                                                   | Foreign key to the service provider (`service_providers.id`). |
| client              | `INT NOT NULL`                                                                   | Foreign key to the client (`clients.id`).                     |
| client_name         | `VARCHAR(1000)`                                                                  | Full name of the client.                                      |
| client_phone        | `VARCHAR(50)`                                                                    | Contact phone number.                                         |
| client_email        | `VARCHAR(255)`                                                                   | Email address of the client.                                  |
| client_province     | `VARCHAR(100)`                                                                   | Province or region of the service location.                   |
| client_postal       | `VARCHAR(100)`                                                                   | Postal code of the client's address.                          |
| client_address      | `VARCHAR(1000)`                                                                  | Address where the service is needed.                          |
| client_title        | `VARCHAR(10)`                                                                    | Client title (e.g., Mr., Ms., Dr.).                           |
| client_description  | `TEXT`                                                                           | Description of the client's needs.                            |
| client_availability | `TEXT`                                                                           | Client's available times/days for service.                    |
| category            | `VARCHAR(50)`                                                                    | Main service category requested.                              |
| category_options    | `VARCHAR(2000)`                                                                  | Detailed service options selected within the category.        |
| property_type       | `VARCHAR(50)`                                                                    | Type of property (e.g., house, condo, apartment).             |
| square_footage      | `INT`                                                                            | Estimated size of the property in square feet.                |
| number_of_rooms     | `INT`                                                                            | Number of rooms in the property.                              |
| has_pets            | `TINYINT(1)`                                                                     | Whether pets are present (1 = Yes, 0 = No).                   |
| special_requests    | `TEXT`                                                                           | Additional notes or requests from the client.                 |
| booking_date        | `VARCHAR(50)`                                                                    | Preferred date for service delivery.                          |
| pricing             | `VARCHAR(25)`                                                                    | Pricing model (e.g., flat, hourly).                           |
| price               | `VARCHAR(25)`                                                                    | Estimated or quoted price for the service.                    |
| images              | `VARCHAR(1000)`                                                                  | Comma-separated list of uploaded image URLs or paths.         |
| status              | `ENUM('pending', 'sent', 'accepted', 'declined', 'cancelled') DEFAULT 'pending'` | Current status of the quote.                                  |
| status_code         | `VARCHAR(20) DEFAULT '101'`                                                      | Internal status tracking code.                                |
| created             | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                             | Timestamp when the quote was created.                         |
| modified            | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`                 | Timestamp of last update.                                     |
| reference           | `VARCHAR(25)`                                                                    | Unique reference code for the quote.                          |
| cancel_reason       | `VARCHAR(1000)`                                                                  | Reason provided by the client for cancellation.               |
| decline_reason      | `VARCHAR(1000)`                                                                  | Reason provided by the provider for declining the quote.      |
| payment_method      | `VARCHAR(100)`                                                                   | Preferred or proposed method of payment.                      |
| payment_due         | `VARCHAR(25)`                                                                    | Suggested due date for the payment.                           |
| payment_ref         | `VARCHAR(100)`                                                                   | Reference to the related payment, if applicable.              |

## Relationships

- **Clients (`quotes.client` → `clients.id`)**: Links each quote to the requesting client.
- **Providers (`quotes.provider` → `service_providers.id`)**: Links each quote to the responding provider.
- **Payments (`quotes.payment_ref` → `payments.payment_intent`)** _(optional)_: Maps accepted quotes to actual payments.

## Notes

- Consider using `DECIMAL(10,2)` for the `price` column for financial precision.
- For multiple images, consider creating a separate `quote_images` table.
- Adding an index on `status`, `provider`, and `client` could improve query performance for dashboards.
