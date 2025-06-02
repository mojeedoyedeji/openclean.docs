# Subscriptions

**Table Name:** `subscriptions`  
**Description:** Stores subscription plans assigned to clients, including duration, payment method, amount, and expiration date.

## Columns

| Column Name | Data Type                                  | Description                                                           |
| ----------- | ------------------------------------------ | --------------------------------------------------------------------- |
| id          | `INT AUTO_INCREMENT PRIMARY KEY`           | Unique identifier for each subscription record.                       |
| client      | `INT NOT NULL`                             | Foreign key referencing the client (`clients.id`).                    |
| plan        | `VARCHAR(100) NOT NULL`                    | Name or type of the subscription plan (e.g., Basic, Pro, Enterprise). |
| period      | `VARCHAR(20)`                              | Duration of the subscription (e.g., monthly, yearly).                 |
| method      | `ENUM('card', 'paypal', 'bank', 'wallet')` | Payment method used for the subscription.                             |
| amount      | `DECIMAL(10,2) NOT NULL`                   | Cost of the subscription.                                             |
| created     | `DATETIME DEFAULT CURRENT_TIMESTAMP`       | Timestamp when the subscription was created.                          |
| expires     | `DATETIME`                                 | Timestamp when the subscription expires.                              |

## Relationships

- **Clients (`subscriptions.client` → `clients.id`)**: Connects the subscription to a specific client.
- **Payments (`payments.subscription_id` → `subscriptions.id`)** _(optional)_: If tracking subscription-related transactions separately.

## Notes

- Consider enforcing unique active subscriptions per client if needed.
- Expired subscriptions can be used to downgrade or restrict platform access.
- You may want to track `status` (active, expired, cancelled) for better management.
