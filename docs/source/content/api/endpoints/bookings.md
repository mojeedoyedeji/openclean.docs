# Booking

Version: `1.0`  
Base URL: `https://api.openclean.ca/api/v1/`

---

### Introduction

The **Booking API** allows **clients**, **service providers**, and **administrators** to manage service appointments on the **OpenClean platform**. It includes endpoints for:

- Retrieving existing bookings
- Creating new bookings
- Updating or cancelling bookings
- Tracking booking history and payment status

Each booking object encapsulates full details of the transaction between a client and a service provider, including service type, schedule, pricing, and contact information. Below is a complete list of fields returned in a booking object:

| Property              | Type                | Description                                    |
| --------------------- | ------------------- | ---------------------------------------------- |
| `id`                  | `string`            | Unique booking ID.                             |
| `provider`            | `string`            | ID of the service provider.                    |
| `service`             | `string`            | ID of the selected service.                    |
| `client`              | `string`            | ID of the client who made the booking.         |
| `client_name`         | `string`            | Full name of the client.                       |
| `client_phone`        | `string`            | Client's phone number.                         |
| `client_email`        | `string`            | Client's email address.                        |
| `client_province`     | `string`            | Province code (e.g., "ON").                    |
| `client_postal`       | `string`            | Client’s postal code.                          |
| `client_address`      | `string`            | Client’s street address.                       |
| `client_title`        | `string`            | Title (e.g., "Mr", "Ms").                      |
| `client_description`  | `string` or `null`  | Additional instructions from the client.       |
| `client_availability` | `string` (ISO 8601) | Preferred service date/time.                   |
| `service_title`       | `string`            | Name of the service.                           |
| `service_price`       | `string` or `float` | Price of the service.                          |
| `service_description` | `string`            | Detailed service description.                  |
| `service_coverage`    | `string`            | Categories covered (comma-separated).          |
| `service_location`    | `string`            | Service delivery location.                     |
| `service_pricing`     | `string`            | Pricing model (e.g., "hourly").                |
| `booking_date`        | `string` or `null`  | Final confirmed date (if set).                 |
| `reference`           | `string`            | Booking reference code.                        |
| `cancel_reason`       | `string` or `null`  | Reason for cancellation (if cancelled).        |
| `images`              | `string`            | Comma-separated list of image filenames.       |
| `payment_mode`        | `string`            | Payment method ("offline", "online").          |
| `payment_due`         | `string` or `null`  | Payment deadline (if applicable).              |
| `payment_ref`         | `string` or `null`  | Payment reference number.                      |
| `status`              | `string`            | Booking status ("pending", "confirmed", etc.). |
| `status_code`         | `string`            | Internal status code.                          |
| `created`             | `string` (ISO 8601) | Creation timestamp.                            |
| `modified`            | `string` (ISO 8601) | Last updated timestamp.                        |

All requests to the OpenClean Booking API must include the appropriate headers to ensure secure and properly formatted communication. The Authorization header is used to authenticate requests using a JWT token, which must be obtained from the login endpoint and included with the Bearer prefix. The Accept header ensures that the server responds with data in JSON format, which is the standard for all API responses.

| Header          | Required | Description                              |
| --------------- | -------- | ---------------------------------------- |
| `Authorization` | Yes      | JWT access token prefixed with `Bearer`. |
| `Accept`        | Yes      | Set to `application/json`.               |

---

### Fetch all bookings (client)

###### Endpoint

```http
GET /bookings/client/{client_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter   | Type     | Description                  |
| ----------- | -------- | ---------------------------- |
| `client_id` | `string` | The unique ID of the client. |

###### Response

| Parameter  | Type   | Description             |
| ---------- | ------ | ----------------------- |
| `bookings` | Array  | List of booking objects |
| `message`  | String | API response message    |
| `status`   | String | API response status     |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
// Sample JavaScript code to interact with Chetaa API

const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const clientId = 123; // Replace with actual client ID
const baseUri = "yourdomain.com/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/client/${clientId}`, {
  method: "GET",
  headers: {
    Authorization: `Bearer ${jwtToken}`,
    "Content-Type": "application/json",
    Accept: "application/json",
  },
})
  .then((response) => {
    if (!response.ok) {
      return response.json().then((err) => {
        throw new Error(
          err.message || `HTTP error! status: ${response.status}`
        );
      });
    }
    return response.json();
  })
  .then((data) => {
    console.log("Bookings:", data);
  })
  .catch((error) => {
    console.error("Error fetching bookings:", error.message);
  });

// Call the function
```

###### Example Response

```json
{
  "bookings": [{}],
  "message": "ok",
  "status": "success"
}
```

###### Possible Errors

- 401 Unauthorized – Missing or invalid JWT token

- 403 Forbidden – JWT is valid, but user is not a client

---

### Fetch all bookings (provider)

###### Endpoint

```http
GET /bookings/provider/{provider_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter     | Type     | Description                            |
| ------------- | -------- | -------------------------------------- |
| `provider_id` | `string` | The unique ID of the service provider. |

###### Response

| Parameter  | Type   | Description             |
| ---------- | ------ | ----------------------- |
| `bookings` | Array  | List of booking objects |
| `message`  | String | API response message    |
| `status`   | String | API response status     |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
// Sample JavaScript code to interact with Chetaa API

const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const clientId = 123; // Replace with actual client ID
const baseUri = "yourdomain.com/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/client/${clientId}`, {
  method: "GET",
  headers: {
    Authorization: `Bearer ${jwtToken}`,
    "Content-Type": "application/json",
    Accept: "application/json",
  },
})
  .then((response) => {
    if (!response.ok) {
      return response.json().then((err) => {
        throw new Error(
          err.message || `HTTP error! status: ${response.status}`
        );
      });
    }
    return response.json();
  })
  .then((data) => {
    console.log("Bookings:", data);
  })
  .catch((error) => {
    console.error("Error fetching bookings:", error.message);
  });

// Call the function
```

###### Example Response

```json
{
  "bookings": [{}],
  "message": "ok",
  "status": "success"
}
```

###### Possible Errors

- 401 Unauthorized – Missing or invalid JWT token

- 403 Forbidden – JWT is valid, but user is not a client

---

### Fetch a single booking

###### Endpoint

```http
GET /app/booking/get/{booking_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter    | Type     | Description                   |
| ------------ | -------- | ----------------------------- |
| `booking_id` | `string` | The unique ID of the booking. |

###### Response

| Parameter | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| `booking` | Object | The requested booking object |
| `message` | String | API response message         |
| `status`  | String | API response status          |

###### Status Codes

###### Example Request

###### Example Response

###### Possible Errors

---

### Fetch booking logs

###### Endpoint

```http
GET /app/booking/logs/{booking_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter    | Type     | Description                   |
| ------------ | -------- | ----------------------------- |
| `booking_id` | `string` | The unique ID of the booking. |

###### Response

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
| `logs`    | Array  | Array of booking logs |
| `message` | String | API response message  |
| `status`  | String | API response status   |

###### Status Codes

###### Example Request

###### Example Response

###### Possible Errors

---

### Create booking

###### Endpoint

```http
POST /booking/create HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

| Parameter | Type   | Description          |
| --------- | ------ | -------------------- |
| `...`     | Object | Booking form payload |

###### Response

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
| `booking` | Object | Newly created booking |
| `message` | String | API response message  |
| `status`  | String | API response status   |

###### Request Parameters

| Parameter    | Type     | Description                   |
| ------------ | -------- | ----------------------------- |
| `booking_id` | `string` | The unique ID of the booking. |

###### Response

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
| `logs`    | Array  | Array of booking logs |
| `message` | String | API response message  |
| `status`  | String | API response status   |

###### Status Codes

###### Example Request

###### Example Response

###### Possible Errors

---

### Update booking

###### Endpoint

```http
POST /app/booking/update HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

###### Response

| Parameter  | Type   | Description              |
| ---------- | ------ | ------------------------ |
| `bookings` | Array  | Updated list of bookings |
| `message`  | String | API response message     |
| `status`   | String | API response status      |

###### Status Codes

###### Example Request

###### Example Response

###### Possible Errors

---

### Cancel booking

###### Endpoint

```http
POST /app/booking/cancel HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

###### Status Codes

###### Example Request

###### Example Response

###### Possible Errors

---

### Booking Payment (Client)

###### Endpoint

```http
POST /booking/client/pay HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

###### Status Codes

###### Example Request

###### Example Response

###### Possible Errors

---

### Confirm Booking

---

### Start Booking

---

### Complete Booking
