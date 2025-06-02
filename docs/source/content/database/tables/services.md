# Services

**Table Name:** `services`  
**Description:** Stores service offerings listed by providers, including descriptions, pricing models, availability, and location metadata.

## Columns

| Column Name  | Data Type                                                          | Description                                                               |
| ------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| id           | `INT AUTO_INCREMENT PRIMARY KEY`                                   | Unique identifier for each service entry.                                 |
| provider     | `INT NOT NULL`                                                     | Foreign key referencing the provider (`service_providers.id`).            |
| title        | `VARCHAR(255) NOT NULL`                                            | Title of the service (e.g., "Move-In Cleaning", "Standard Housekeeping"). |
| description  | `TEXT`                                                             | Full description of the service.                                          |
| services     | `TEXT`                                                             | Sub-services included (e.g., vacuuming, dusting), possibly as JSON/text.  |
| pricing_type | `ENUM('flat', 'hourly', 'custom') DEFAULT 'flat'`                  | Type of pricing model.                                                    |
| price        | `DECIMAL(10,2)`                                                    | Price based on the selected pricing type.                                 |
| province     | `VARCHAR(20)`                                                      | Province where the service is offered.                                    |
| location     | `VARCHAR(50)`                                                      | City or neighborhood of service availability.                             |
| availability | `ENUM('available', 'unavailable') DEFAULT 'available'`             | Whether the service is currently open for booking.                        |
| images       | `TEXT`                                                             | Comma-separated URLs or paths to images related to the service.           |
| rating       | `DECIMAL(2,1)`                                                     | Average rating received for the service (e.g., 4.5).                      |
| status       | `ENUM('active', 'inactive', 'draft', 'archived') DEFAULT 'active'` | Current state of the service entry.                                       |
| created      | `DATETIME DEFAULT CURRENT_TIMESTAMP`                               | When the service record was created.                                      |
| modified     | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP`   | Last update timestamp.                                                    |

## Relationships

- **Providers (`services.provider` → `service_providers.id`)**: Connects each service to the provider who owns it.
- **Bookings (`bookings.service_id` → `services.id`)** _(optional)_: Bookings may reference this service.
- **Reviews (`reviews.entity` → `services.id`)** _(optional)_: Reviews may be attached to services.

## Notes

- You can normalize `services` (the column) into a child table like `service_features` if you need filtering or tagging.
- Consider indexing `provider`, `status`, and `location` for performance.
- The `images` field could be moved to a `service_images` table if you plan to handle multiple uploads dynamically.
