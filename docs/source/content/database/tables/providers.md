# Service Providers Table

**Table Name:** `service_providers`  
**Description:** Stores profiles of vendors or cleaning service providers, including location, pricing, verification, and contact details.

## Columns

| Column Name         | Data Type                                                           | Description                                       |
| ------------------- | ------------------------------------------------------------------- | ------------------------------------------------- |
| id                  | `INT AUTO_INCREMENT PRIMARY KEY`                                    | Unique identifier for each service provider.      |
| name                | `VARCHAR(255) NOT NULL`                                             | Full name of the provider.                        |
| phone               | `VARCHAR(20) NOT NULL`                                              | Contact phone number.                             |
| email               | `VARCHAR(255) UNIQUE`                                               | Email address of the provider.                    |
| username            | `VARCHAR(255) UNIQUE`                                               | Optional username or handle.                      |
| password            | `VARCHAR(255) NOT NULL`                                             | Encrypted password.                               |
| address             | `TEXT`                                                              | Street address or general location.               |
| province            | `VARCHAR(100)`                                                      | Province of operation.                            |
| city                | `VARCHAR(100)`                                                      | City of operation.                                |
| latitude            | `DECIMAL(10,7)`                                                     | Latitude coordinate for mapping.                  |
| postal_code         | `VARCHAR(20)`                                                       | Postal or ZIP code.                               |
| longitude           | `DECIMAL(10,7)`                                                     | Longitude coordinate for mapping.                 |
| business_reg        | `VARCHAR(100)`                                                      | Business registration number.                     |
| business_name       | `VARCHAR(1000)`                                                     | Registered or operating business name.            |
| base_price_hourly   | `DECIMAL(10,2)`                                                     | Hourly base rate for services.                    |
| base_price_flat     | `DECIMAL(10,2)`                                                     | Flat rate for standard service package.           |
| about               | `TEXT`                                                              | Provider description or profile bio.              |
| subscription        | `VARCHAR(255)`                                                      | Subscription ID or tier.                          |
| referral            | `VARCHAR(255)`                                                      | Referral code used by the provider.               |
| whatsapp            | `VARCHAR(25)`                                                       | WhatsApp contact number.                          |
| facebook            | `VARCHAR(255)`                                                      | Facebook profile or page URL.                     |
| instagram           | `VARCHAR(255)`                                                      | Instagram handle or URL.                          |
| twitter             | `VARCHAR(255)`                                                      | Twitter handle or URL.                            |
| available           | `BOOLEAN DEFAULT FALSE`                                             | Availability to accept bookings.                  |
| verified            | `BOOLEAN DEFAULT FALSE`                                             | Verification status (manual or automatic).        |
| featured            | `BOOLEAN DEFAULT FALSE`                                             | Whether the provider is featured on the platform. |
| services            | `TEXT`                                                              | Services offered by the provider.                 |
| auth_token          | `VARCHAR(255)`                                                      | Token for session/authentication.                 |
| reset_token         | `VARCHAR(255)`                                                      | Token for password reset.                         |
| token_expiry        | `DATETIME`                                                          | Expiration timestamp for reset token.             |
| avatar              | `VARCHAR(255)`                                                      | URL or path to provider's profile image.          |
| login_count         | `INT DEFAULT 0`                                                     | Number of times the provider has logged in.       |
| login_status        | `ENUM('online', 'offline', 'locked')`                               | Current login status.                             |
| subscription_plan   | `VARCHAR(50) DEFAULT 'basic'`                                       | Name or type of subscription plan.                |
| subscription_expiry | `DATETIME`                                                          | Subscription expiration timestamp.                |
| created             | `DATETIME DEFAULT CURRENT_TIMESTAMP`                                | When the profile was created.                     |
| modified            | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`    | Last updated timestamp.                           |
| status              | `ENUM('active', 'inactive', 'suspended') NOT NULL DEFAULT 'active'` | Account status.                                   |

## Relationships

- **Bookings (`bookings.provider_id` → `service_providers.id`)**: Providers can receive many bookings.
- **Payments (`payments.provider_id` → `service_providers.id`)**: Providers may receive payments via completed services.
- **Subscriptions (`service_providers.subscription` → `subscriptions.id`)**: Linked to a specific subscription plan.

## Notes

- **Location coordinates** (`latitude`, `longitude`) are stored with high precision for mapping.
- Consider indexing frequently queried fields like `city`, `available`, `verified`, and `status` for performance.
