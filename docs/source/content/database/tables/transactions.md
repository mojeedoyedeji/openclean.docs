# Transactions

**Table Name:** `transactions`  
**Description:** Stores records of financial transactions between clients and service providers, including purpose, type, amount, and status.

## Columns

| Column Name | Data Type                                                              | Description                                                       |
| ----------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------- |
| id          | `INT AUTO_INCREMENT PRIMARY KEY`                                       | Unique identifier for the transaction.                            |
| provider    | `INT`                                                                  | Foreign key to the provider (`service_providers.id`).             |
| client      | `INT`                                                                  | Foreign key to the client (`clients.id`).                         |
| amount      | `DECIMAL(10,2)`                                                        | Transaction amount in platform's currency.                        |
| type        | `ENUM('payment', 'payout', 'refund')`                                  | Type of transaction.                                              |
| purpose     | `VARCHAR(255)`                                                         | Description or purpose of the transaction (e.g., quote, booking). |
| reference   | `VARCHAR(255)`                                                         | External payment gateway reference or internal tracking code.     |
| created     | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                   | When the transaction was recorded.                                |
| modified    | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`       | When the transaction was last updated.                            |
| status      | `ENUM('pending', 'completed', 'failed', 'refunded') DEFAULT 'pending'` | Current status of the transaction.                                |

## Relationships

- **Clients (`transactions.client` → `clients.id`)**: Each transaction is associated with a client.
- **Providers (`transactions.provider` → `service_providers.id`)**: Each transaction may credit or debit a provider.
- **Quotes or Bookings (`transactions.purpose` + `reference`)**: Can optionally be linked to a quote or booking via reference.

## Notes

- Consider indexing `client`, `provider`, `status`, and `created` for faster dashboard/reporting queries.
- For recurring payments, additional columns like `billing_cycle`, `subscription_id`, or `invoice_id` may be added.
