# Quotes

Version: `1.0`  
Base URL: `https://api.openclean.ca/api/v1/`

---

### Introduction

The **Quotes API** allows **clients**, **service providers**, and **administrators** to manage quote requests on the **OpenClean platform**. It includes endpoints for:

- Retrieving existing quotes
- Creating new quotes
- Updating or cancelling quotes
- Tracking booking history and payment status

Each quote object encapsulates full details of the transaction between a client and a service provider, including service type, schedule, pricing, and contact information. Below is a complete list of fields returned in a booking object:

| Field                 | Type      | Description                                               |
| --------------------- | --------- | --------------------------------------------------------- |
| `id`                  | `string`  | Unique identifier for the quote.                          |
| `provider`            | `string`  | ID of the service provider.                               |
| `client`              | `string`  | ID of the client.                                         |
| `client_name`         | `string`  | Full name of the client.                                  |
| `client_phone`        | `string`  | Phone number of the client.                               |
| `client_email`        | `string`  | Email address of the client.                              |
| `client_province`     | `string`  | Province code (e.g., `ON` for Ontario).                   |
| `client_postal`       | `string`  | Postal code of the client.                                |
| `client_address`      | `string`  | Street address of the client.                             |
| `client_title`        | `string`  | Client's title (e.g., Mr, Ms, Dr).                        |
| `client_description`  | `string`  | Additional description from the client.                   |
| `client_availability` | `string`  | Availability window(s) provided by the client.            |
| `category`            | `string`  | Service category (e.g., Residential, Commercial).         |
| `category_options`    | `string`  | Comma-separated options under the selected category.      |
| `property_type`       | `string`  | Type of property (e.g., Apartment, House).                |
| `square_footage`      | `number`  | Size of the property in square feet.                      |
| `number_of_rooms`     | `number`  | Total number of rooms in the property.                    |
| `has_pets`            | `boolean` | Whether pets are present on the property.                 |
| `special_requests`    | `string`  | Any specific instructions or requests.                    |
| `booking_date`        | `string`  | Requested date/time for the booking.                      |
| `pricing`             | `string`  | Pricing model (e.g., `hourly`, `fixed`).                  |
| `price`               | `string`  | Unit price (per hour or fixed).                           |
| `images`              | `string`  | Comma-separated filenames of uploaded quote images.       |
| `status`              | `string`  | Quote status (e.g., `pending`, `paid(online)`).           |
| `status_code`         | `string`  | Internal status code.                                     |
| `created`             | `string`  | ISO timestamp of when the quote was created.              |
| `modified`            | `string`  | ISO timestamp of last modification.                       |
| `reference`           | `string`  | Reference code or number.                                 |
| `cancel_reason`       | `string`  | Reason provided if the quote was cancelled.               |
| `decline_reason`      | `string`  | Reason provided if the quote was declined.                |
| `payment_mode`        | `string`  | Mode of payment used (`online`, `offline`, etc.).         |
| `payment_due`         | `string`  | Total amount due for the quote.                           |
| `payment_ref`         | `string`  | Payment transaction reference ID (e.g., Stripe `pi_...`). |

All requests to the OpenClean Quote API must include the appropriate headers to ensure secure and properly formatted communication. The Authorization header is used to authenticate requests using a JWT token, which must be obtained from the login endpoint and included with the Bearer prefix. The Accept header ensures that the server responds with data in JSON format, which is the standard for all API responses.

| Header          | Required | Description                              |
| --------------- | -------- | ---------------------------------------- |
| `Authorization` | Yes      | JWT access token prefixed with `Bearer`. |
| `Accept`        | Yes      | Set to `application/json`.               |

---

### Fetch all quotes (client)

###### Endpoint

```http
GET /quotes/client/{client_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter   | Type     | Description                  |
| ----------- | -------- | ---------------------------- |
| `client_id` | `string` | The unique ID of the client. |

###### Response

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
| `quotes`  | Array  | List of quote objects |
| `message` | String | API response message  |
| `status`  | String | API response status   |

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

fetch(`https://${baseUri}/quotes/client/${clientId}`, {
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
    console.error("Error fetching quotes:", error.message);
  });

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "quotes": [
    {
      "id": "021843611261991",
      "provider": "718435596622959",
      "client": "659917167960915",
      "client_name": "Mojeed Oyedeji",
      "client_phone": "+14166197947",
      "client_email": "mojeed.oyedeji@gmail.com",
      "client_province": "ON",
      "client_postal": "M1K 4M1",
      "client_address": "60 Winter Avenue, Scarborough",
      "client_title": "Mr",
      "client_description": null,
      "client_availability": "Mon, 31 Mar 2025 09:30:00 GMT|Mon, 31 Mar 2025 09:55:00 GMT",
      "category": "Residential",
      "category_options": "Regular House,Airbnb & Vacation Rental,Deep Cleaning",
      "property_type": null,
      "square_footage": null,
      "number_of_rooms": null,
      "has_pets": null,
      "special_requests": null,
      "booking_date": "Mon, 31 Mar 2025 09:55:00 GMT",
      "pricing": "hourly",
      "price": "40",
      "images": "quote_531017443760636.jpg,quote_939118979054653.jpg",
      "status": "paid(online)",
      "status_code": "110",
      "created": "2025-03-29T09:59:09+00:00",
      "modified": "2025-05-05T06:56:31+00:00",
      "reference": "123456ab",
      "cancel_reason": null,
      "decline_reason": null,
      "payment_mode": "online",
      "payment_due": "450",
      "payment_ref": "pi_3RLIyLDnXq1SUYsB11lp6tCY"
    }
  ]
}
```

###### Possible Errors

- 401 Unauthorized – Missing or invalid JWT token

- 403 Forbidden – JWT is valid, but user is not a client

---

### Fetch all quotes (provider)

###### Endpoint

```http
GET /quotes/provider/{provider_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter     | Type     | Description                            |
| ------------- | -------- | -------------------------------------- |
| `provider_id` | `string` | The unique ID of the service provider. |

###### Response

| Parameter | Type   | Description             |
| --------- | ------ | ----------------------- |
| `quotes`  | Array  | List of booking objects |
| `message` | String | API response message    |
| `status`  | String | API response status     |

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
const baseUri = "api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/quotes/provider/${providerId}`, {
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

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "quotes": [
    {
      "id": "021843611261991",
      "provider": "718435596622959",
      "client": "659917167960915",
      "client_name": "Mojeed Oyedeji",
      "client_phone": "+14166197947",
      "client_email": "mojeed.oyedeji@gmail.com",
      "client_province": "ON",
      "client_postal": "M1K 4M1",
      "client_address": "60 Winter Avenue, Scarborough",
      "client_title": "Mr",
      "client_description": null,
      "client_availability": "Mon, 31 Mar 2025 09:30:00 GMT|Mon, 31 Mar 2025 09:55:00 GMT",
      "category": "Residential",
      "category_options": "Regular House,Airbnb & Vacation Rental,Deep Cleaning",
      "property_type": null,
      "square_footage": null,
      "number_of_rooms": null,
      "has_pets": null,
      "special_requests": null,
      "booking_date": "Mon, 31 Mar 2025 09:55:00 GMT",
      "pricing": "hourly",
      "price": "40",
      "images": "quote_531017443760636.jpg,quote_939118979054653.jpg",
      "status": "paid(online)",
      "status_code": "110",
      "created": "2025-03-29T09:59:09+00:00",
      "modified": "2025-05-05T06:56:31+00:00",
      "reference": "123456ab",
      "cancel_reason": null,
      "decline_reason": null,
      "payment_mode": "online",
      "payment_due": "450",
      "payment_ref": "pi_3RLIyLDnXq1SUYsB11lp6tCY"
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
GET /bookings/booking/{booking_id} HTTP/1.1
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

### Quote Payment (Client)

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

### Confirm Quote

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

### Start Quote

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

### Complete Quote

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

### Confirm Payment (Provider)

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

### Cancel Quote (Provider)

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
