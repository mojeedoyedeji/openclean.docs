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

### Fetch all bookings

###### Endpoint

```http
GET /bookings/ HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

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
const baseUri = "api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/`, {
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
  "status": "success",
  "message": "The request was successful",
  "bookings": [
    {
      "id": "058443672140854",
      "provider": "718435596622959",
      "service": "555766148148896",
      "client": "659917167960915",
      "client_name": "Mojeed Opeyemi Oyedeji",
      "client_phone": "+14166197949",
      "client_email": "mojeed.oyedeji@gmail.com",
      "client_province": "ON",
      "client_postal": "M1K 4M1",
      "client_address": "60 Winter Avenue, Scarborough, M1K 4M1",
      "client_title": "Mr",
      "client_description": null,
      "client_availability": "Sat, 31 May 2025 04:00:00 GMT",
      "service_title": "Mobile Service",
      "service_price": "50",
      "service_description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.",
      "service_coverage": "Regular House,Deep Cleaning,Industrial,Disinfection & Sanitization",
      "service_location": "Toronto",
      "service_pricing": "hourly",
      "booking_date": "Sat, 31 May 2025 04:00:00 GMT",
      "reference": "DyPSBiNB",
      "cancel_reason": null,
      "images": "booking_871350296969383.jpg,booking_047922598621941.jpg",
      "payment_mode": "online",
      "payment_due": "4000",
      "payment_ref": "pi_3ROkddDnXq1SUYsB2RoNCsie",
      "status": "paid(online)",
      "status_code": "110",
      "created": "2025-05-14T12:53:49+00:00",
      "modified": "2025-05-14T19:04:24+00:00"
    }
  ]
}
```

###### Possible Errors

- 401 Unauthorized – Missing or invalid JWT token

- 403 Forbidden – JWT is valid, but user is not a client

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
  "status": "success",
  "message": "The request was successful",
  "bookings": [
    {
      "id": "058443672140854",
      "provider": "718435596622959",
      "service": "555766148148896",
      "client": "659917167960915",
      "client_name": "Mojeed Opeyemi Oyedeji",
      "client_phone": "+14166197949",
      "client_email": "mojeed.oyedeji@gmail.com",
      "client_province": "ON",
      "client_postal": "M1K 4M1",
      "client_address": "60 Winter Avenue, Scarborough, M1K 4M1",
      "client_title": "Mr",
      "client_description": null,
      "client_availability": "Sat, 31 May 2025 04:00:00 GMT",
      "service_title": "Mobile Service",
      "service_price": "50",
      "service_description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.",
      "service_coverage": "Regular House,Deep Cleaning,Industrial,Disinfection & Sanitization",
      "service_location": "Toronto",
      "service_pricing": "hourly",
      "booking_date": "Sat, 31 May 2025 04:00:00 GMT",
      "reference": "DyPSBiNB",
      "cancel_reason": null,
      "images": "booking_871350296969383.jpg,booking_047922598621941.jpg",
      "payment_mode": "online",
      "payment_due": "4000",
      "payment_ref": "pi_3ROkddDnXq1SUYsB2RoNCsie",
      "status": "paid(online)",
      "status_code": "110",
      "created": "2025-05-14T12:53:49+00:00",
      "modified": "2025-05-14T19:04:24+00:00"
    }
  ]
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
  "status": "success",
  "message": "The request was successful",
  "bookings": [
    {
      "id": "058443672140854",
      "provider": "718435596622959",
      "service": "555766148148896",
      "client": "659917167960915",
      "client_name": "Mojeed Opeyemi Oyedeji",
      "client_phone": "+14166197949",
      "client_email": "mojeed.oyedeji@gmail.com",
      "client_province": "ON",
      "client_postal": "M1K 4M1",
      "client_address": "60 Winter Avenue, Scarborough, M1K 4M1",
      "client_title": "Mr",
      "client_description": null,
      "client_availability": "Sat, 31 May 2025 04:00:00 GMT",
      "service_title": "Mobile Service",
      "service_price": "50",
      "service_description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.",
      "service_coverage": "Regular House,Deep Cleaning,Industrial,Disinfection & Sanitization",
      "service_location": "Toronto",
      "service_pricing": "hourly",
      "booking_date": "Sat, 31 May 2025 04:00:00 GMT",
      "reference": "DyPSBiNB",
      "cancel_reason": null,
      "images": "booking_871350296969383.jpg,booking_047922598621941.jpg",
      "payment_mode": "online",
      "payment_due": "4000",
      "payment_ref": "pi_3ROkddDnXq1SUYsB2RoNCsie",
      "status": "paid(online)",
      "status_code": "110",
      "created": "2025-05-14T12:53:49+00:00",
      "modified": "2025-05-14T19:04:24+00:00"
    }
  ]
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

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
// Sample JavaScript code to interact with Chetaa API

const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const bookingId = 123; // Replace with actual client ID
const baseUri = "api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/${bookingId}`, {
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
  "status": "success",
  "message": "The request was successful",
  "booking": {
    "id": "421423249308415",
    "provider": "718435596622959",
    "service": "555766148148896",
    "client": "659917167960915",
    "client_name": "Mojeed Opeyemi Oyedeji",
    "client_phone": "+14166197949",
    "client_email": "mojeed.oyedeji@gmail.com",
    "client_province": "ON",
    "client_postal": "M1K 4M1",
    "client_address": "60 Winter Avenue, Scarborough, M1K 4M1",
    "client_title": "Mr",
    "client_description": null,
    "client_availability": "Sat, 31 May 2025 04:00:00 GMT",
    "service_title": "Mobile Service",
    "service_price": "50",
    "service_description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.",
    "service_coverage": "Regular House,Deep Cleaning,Industrial,Disinfection & Sanitization",
    "service_location": "Toronto",
    "service_pricing": "hourly",
    "booking_date": "Sat, 31 May 2025 04:00:00 GMT",
    "reference": "684NdsaV",
    "cancel_reason": null,
    "images": "booking_707142212881825.jpg,booking_066767924782075.jpg",
    "payment_mode": "offline",
    "payment_due": "10000",
    "payment_ref": "8852280531",
    "status": "paid(confirmed)",
    "status_code": "109",
    "created": "2025-05-14T17:57:13+00:00",
    "modified": "2025-05-14T18:02:59+00:00"
  }
}
```

###### Possible Errors

- 401 Unauthorized – Missing or invalid JWT token

- 403 Forbidden – JWT is valid, but user is not a client

---

### Fetch booking logs

###### Endpoint

```http
GET /booking/{booking_id}/logs HTTP/1.1
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

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const clientId = 123; // Replace with actual client ID
const baseUri = "api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/booking/${clientId}/logs`, {
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
    console.log(data);
  })
  .catch((error) => {
    console.error("Error fetching bookings:", error.message);
  });
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "logs": [
    {
      "id": "004056511826182",
      "booking": "364132910663025",
      "type": "provider",
      "author": "718435596622959",
      "created": "2025-04-27T20:50:43+00:00",
      "modified": "2025-04-27T20:50:43+00:00",
      "status": "Paid (Confirmed)"
    }
  ]
}
```

###### Possible Errors

- 401 Unauthorized – Missing or invalid JWT token

- 403 Forbidden – JWT is valid, but user is not a client

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

### Booking payment (Client)

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

### Confirm booking

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

### Start booking

###### Endpoint

```http
GET /booking/start/:id HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Parameters

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

### Complete booking

###### Endpoint

```http
GET /booking/complete/:id HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Parameters

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

### Confirm payment (Provider)

###### Endpoint

```http
POST /booking/payment/confirm HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Parameters

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

--

### Cancel booking (Provider)

###### Endpoint

```http
GET /booking/cancel/:id HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Parameters

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
