# Reviews Table

**Table Name:** `reviews`  
**Description:** Stores user-submitted reviews and ratings for entities such as service providers or bookings, including metadata like likes, dislikes, and status.

## Columns

| Column Name    | Data Type                                                        | Description                                                         |
| -------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------- |
| id             | `INT AUTO_INCREMENT PRIMARY KEY`                                 | Unique identifier for the review.                                   |
| reviewer_name  | `VARCHAR(255) NOT NULL`                                          | Name of the reviewer.                                               |
| reviewer_email | `VARCHAR(255)`                                                   | Email address of the reviewer (optional for moderation or contact). |
| entity         | `VARCHAR(255) NOT NULL`                                          | ID or reference to the entity being reviewed (e.g., provider ID).   |
| rating         | `TINYINT UNSIGNED`                                               | Rating score (e.g., from 1 to 5).                                   |
| review         | `VARCHAR(1000)`                                                  | Textual feedback or comment.                                        |
| created        | `DATETIME DEFAULT CURRENT_TIMESTAMP`                             | When the review was created.                                        |
| modified       | `DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | When the review was last updated.                                   |
| likes          | `INT DEFAULT 0`                                                  | Number of likes or upvotes on the review.                           |
| dislikes       | `INT DEFAULT 0`                                                  | Number of dislikes or downvotes.                                    |
| status         | `ENUM('pending', 'approved', 'rejected') DEFAULT 'pending'`      | Moderation status of the review.                                    |

## Relationships

- **Entities (`reviews.entity` → `service_providers.id` or `bookings.id`)**: The entity being reviewed.
- **Users (`reviews.reviewer_email` → `clients.email`)** _(optional)_: Link to user if authentication is used.

## Notes

- Use `TINYINT` for the `rating` column and validate between 1–5 or 1–10 depending on your UI.
- Consider indexing `entity` and `status` for efficient filtering in dashboards or public pages.
- Optionally add `reviewer_id` if you want to enforce registered-only reviews.
