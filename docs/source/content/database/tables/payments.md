# Payments

**Table Name:** `payments`  
**Description:** Stores payment transaction details made by clients, including purpose, method, and status.

## Columns

| Column Name    | Data Type                                                              | Description                                                      |
| -------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------- |
| id             | `INT AUTO_INCREMENT PRIMARY KEY`                                       | Unique identifier for each payment record.                       |
| client         | `INT NOT NULL`                                                         | Foreign key to the `clients.id` who made the payment.            |
| payment_intent | `VARCHAR(100)`                                                         | External payment reference (e.g., Stripe/PayPal transaction ID). |
| payment_method | `VARCHAR(100)`                                                         | Payment method used (e.g., card, transfer, wallet).              |
| purpose        | `VARCHAR(255)`                                                         | Purpose of payment (e.g., service booking, product purchase).    |
| amount         | `DECIMAL(10,2) NOT NULL`                                               | Amount paid in the platform's base currency.                     |
| method         | `ENUM('credit_card', 'bank_transfer', 'wallet', 'cash')`               | Categorized method of payment.                                   |
| status         | `ENUM('pending', 'completed', 'failed', 'refunded') DEFAULT 'pending'` | Current payment status.                                          |
| created        | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                   | Timestamp when the payment was initiated.                        |
| modified       | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`       | Timestamp of last update.                                        |

## Relationships

- **Clients (`payments.client` → `clients.id`)**: Each payment is linked to a client.
- **Booking (`bookings.payment_id` → `payments.id`)** _(optional)_: Bookings may reference a completed payment.

## Notes

- `amount` changed to `DECIMAL(10,2)` for accuracy in financial calculations.
- `method` and `status` converted to `ENUM` for strict control of valid values.
- Consider adding **currency** if supporting multiple currencies.
