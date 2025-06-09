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
| `client_description`  | `string`            | Additional instructions from the client.       |
| `client_availability` | `string`            | Preferred service date/time.                   |
| `service_title`       | `string`            | Name of the service.                           |
| `service_price`       | `string`            | Price of the service.                          |
| `service_description` | `string`            | Detailed service description.                  |
| `service_coverage`    | `string`            | Categories covered (comma-separated).          |
| `service_location`    | `string`            | Service delivery location.                     |
| `service_pricing`     | `string`            | Pricing model (e.g., "hourly").                |
| `booking_date`        | `string`            | Final confirmed date (if set).                 |
| `reference`           | `string`            | Booking reference code.                        |
| `cancel_reason`       | `string`            | Reason for cancellation (if cancelled).        |
| `images`              | `string`            | Comma-separated list of image filenames.       |
| `payment_mode`        | `string`            | Payment method ("offline", "online").          |
| `payment_due`         | `string`            | Payment deadline (if applicable).              |
| `payment_ref`         | `string`            | Payment reference number.                      |
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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch all bookings (client)

###### Endpoint

```http
GET /bookings/client/{client_id} HTTP/1.1
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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch all bookings (provider)

###### Endpoint

```http
GET /bookings/provider/{provider_id} HTTP/1.1
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
const providerId = 123; // Replace with actual client ID
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/provider/${providerId}`, {
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch single booking

###### Endpoint

```http
GET /bookings/booking/{booking_id} HTTP/1.1
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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/${bookingId}`, {
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch booking logs

###### Endpoint

```http
GET /bookings/booking/{booking_id}/logs HTTP/1.1
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
const bookingId = 123; // Replace with actual client ID
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/${bookingId}/logs`, {
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
    console.error("An error occured:", error.message);
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Create booking

###### Endpoint

```http
POST /bookings/booking/create HTTP/1.1
```

###### Request Body

| Field                 | Type     | Required | Description                                                                  |
| --------------------- | -------- | -------- | ---------------------------------------------------------------------------- |
| `client_name`         | `string` | Yes      | Name of the client submitting the service request                            |
| `client_title`        | `string` | No       | Title of the client (e.g., Mr, Ms)                                           |
| `client_address`      | `string` | Yes      | Street address of the client                                                 |
| `client_email`        | `string` | Yes      | Email address of the client                                                  |
| `client_phone`        | `string` | Yes      | Phone number of the client                                                   |
| `client_province`     | `string` | Yes      | Province abbreviation (e.g., ON for Ontario)                                 |
| `client_postal`       | `string` | No       | Postal code of the client                                                    |
| `provider`            | `string` | Yes      | Unique identifier for the service provider                                   |
| `service`             | `string` | Yes      | Unique identifier for the service                                            |
| `service_title`       | `string` | Yes      | Title or label for the service offered                                       |
| `service_description` | `string` | Yes      | Detailed description of the service                                          |
| `service_location`    | `string` | Yes      | City or area where the service is delivered                                  |
| `service_price`       | `number` | Yes      | Price of the service (in CAD)                                                |
| `service_pricing`     | `string` | Yes      | Pricing model (e.g., hourly, flat)                                           |
| `service_coverage`    | `string` | No       | Comma-separated list of service categories (e.g., Deep Cleaning, Industrial) |
| `images`              | `string` | No       | URL(s) or path(s) to uploaded images; empty if none provided                 |

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

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/create`, {
  method: "POST",
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
    console.error("An error occured", error.message);
  });
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "data": {
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
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Update booking

###### Endpoint

```http
POST /bookings/booking/update HTTP/1.1
```

###### Request Body

| Field                 | Type       | Required | Description                                                         |
| --------------------- | ---------- | -------- | ------------------------------------------------------------------- |
| `id`                  | `string`   | Yes      | Unique booking ID                                                   |
| `client`              | `string`   | Yes      | Unique identifier for the client                                    |
| `client_address`      | `string`   | Yes      | Street address of the client                                        |
| `client_availability` | `string`   | Yes      | Preferred time slot(s) for the service                              |
| `client_description`  | `string`   | No       | Notes or description from the client                                |
| `client_email`        | `string`   | Yes      | Email address of the client                                         |
| `client_name`         | `string`   | Yes      | Full name of the client                                             |
| `client_phone`        | `string`   | Yes      | Phone number of the client                                          |
| `client_postal`       | `string`   | Yes      | Postal code of the client's location                                |
| `client_province`     | `string`   | Yes      | Province code (e.g., ON, BC, etc.)                                  |
| `client_title`        | `string`   | No       | Title of the client (Mr, Mrs, etc.)                                 |
| `created`             | `datetime` | Yes      | Timestamp when the booking was created                              |
| `images`              | `string[]` | No       | Comma-separated image file names associated with the booking        |
| `modified`            | `datetime` | Yes      | Timestamp when the booking was last modified                        |
| `payment_due`         | `string`   | No       | Due date or amount pending for payment                              |
| `payment_mode`        | `string`   | Yes      | Mode of payment (e.g., offline, online)                             |
| `payment_ref`         | `string`   | No       | Payment reference number or transaction ID                          |
| `provider`            | `string`   | Yes      | Unique ID of the service provider                                   |
| `reference`           | `string`   | Yes      | Unique alphanumeric booking reference                               |
| `service`             | `string`   | Yes      | Unique ID of the booked service                                     |
| `service_coverage`    | `string`   | Yes      | Comma-separated list of service coverage types                      |
| `service_description` | `string`   | Yes      | Full description of the service                                     |
| `service_location`    | `string`   | Yes      | City or location where the service is to be delivered               |
| `service_price`       | `number`   | Yes      | Total price of the service                                          |
| `service_pricing`     | `string`   | Yes      | Pricing model (e.g., flat, hourly)                                  |
| `service_title`       | `string`   | Yes      | Name/title of the booked service                                    |
| `status`              | `string`   | Yes      | Current status of the booking (e.g., pending, confirmed, cancelled) |
| `status_code`         | `string`   | Yes      | Internal numeric code for the booking status                        |

###### Response

| Parameter | Type   | Description              |
| --------- | ------ | ------------------------ |
| `booking` | Array  | Updated list of bookings |
| `message` | String | API response message     |
| `status`  | String | API response status      |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/update`, {
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
    console.error("An error occured:", error.message);
  });
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Cancel booking

###### Endpoint

```http
POST /bookings/booking/cancel
```

###### Request Body

| Field           | Type     | Required | Description                                           |
| --------------- | -------- | -------- | ----------------------------------------------------- |
| `id`            | `string` | Yes      | Unique booking ID                                     |
| `cancel_reason` | `string` | Yes      | Reason for cancelling the booking                     |
| `cancelled_by`  | `string` | Yes      | The person canceling the booking (provider or client) |

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/cancel`, {
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
    console.error("An error occured:", error.message);
  });
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
  },
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| `401`       | Unauthorized | Missing or invalid JWT token           |
| `403`       | Forbidden    | JWT is valid, but user is not a client |

---

### Booking payment (client)

###### Endpoint

```http
POST /bookings/booking/payment HTTP/1.1
```

###### Request Body

| Field            | Type     | Required | Description                                    |
| ---------------- | -------- | -------- | ---------------------------------------------- |
| `id`             | `string` | Yes      | Unique booking ID                              |
| `client`         | `string` | No       | Client ID (Registered) or Email (Unregistered) |
| `provider`       | `string` | No       | Service Provider ID                            |
| `method`         | `string` | No       | Online payment method (Card)                   |
| `amount`         | `string` | No       | Payment amount                                 |
| `payment_intent` | `string` | No       | Payment reference number or transaction ID     |
| `payment_mode`   | `string` | Yes      | Mode of payment (e.g., offline, online)        |
| `payment_method` | `string` | Yes      | -                                              |

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

const payload = {
  bookingId: "123456789", // replace with actual data
  amount: 1000,
  paymentMethod: "offline",
  reference: "ze7suyeP",
};

fetch(`https://${baseUri}/bookings/booking/payment`, {
  method: "POST",
  headers: {
    Authorization: `Bearer ${jwtToken}`,
    "Content-Type": "application/json",
    Accept: "application/json",
  },
  body: JSON.stringify(payload),
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
    console.error("An error occurred:", error.message);
  });
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
  },
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| `401`       | Unauthorized | Missing or invalid JWT token           |
| `403`       | Forbidden    | JWT is valid, but user is not a client |

---

### Confirm booking

###### Endpoint

```http
POST /bookings/booking/confirm HTTP/1.1
```

###### Request Body

| Field          | Type     | Required | Description             |
| -------------- | -------- | -------- | ----------------------- |
| `id`           | `string` | Yes      | Unique booking ID       |
| `provider`     | `string` | No       | Service provider ID     |
| `booking_date` | `string` | Yes      | Selected scheduled date |

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

const payload = {
  bookingId: "123456789", // replace with actual data
  amount: 1000,
  paymentMethod: "offline",
  reference: "ze7suyeP",
};

fetch(`https://${baseUri}/bookings/booking/payment`, {
  method: "POST",
  headers: {
    Authorization: `Bearer ${jwtToken}`,
    "Content-Type": "application/json",
    Accept: "application/json",
  },
  body: JSON.stringify(payload),
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
    console.error("An error occurred:", error.message);
  });
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
  },
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Start booking

###### Endpoint

```http
POST /bookings/booking/start/ HTTP/1.1
```

###### Request Body

| Parameter | Type     | Description                   |
| --------- | -------- | ----------------------------- |
| `id`      | `string` | The unique ID of the booking. |

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/${bookingId}/start/`, {
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
  },
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Complete booking

###### Endpoint

```http
GET /bookings/booking/complete/ HTTP/1.1
```

###### Request Body

| Parameter | Type     | Description                   |
| --------- | -------- | ----------------------------- |
| `id`      | `string` | The unique ID of the booking. |

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/${bookingId}/complete/`, {
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
  },
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Confirm payment (provider)

###### Endpoint

```http
POST /bookings/booking/payment/confirm HTTP/1.1
```

###### Request Parameters

| Parameter    | Type     | Description                   |
| ------------ | -------- | ----------------------------- |
| `booking_id` | `string` | The unique ID of the booking. |

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `booking` | Object | Updated booking object |
| `logs`    | Array  | Updated list of logs   |
| `message` | String | API response message   |
| `status`  | String | API response status    |

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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/bookings/booking/${bookingId}/payment/confirm`, {
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
  },
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

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |
