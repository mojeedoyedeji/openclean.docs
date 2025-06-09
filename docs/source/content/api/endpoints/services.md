# Services

Version: `1.0`  
Base URL: `https://api.openclean.ca/api/v1/`

---

### Introduction

The Services API enables clients, service providers, and administrators to manage the creation, listing, and status updates of services offered on the OpenClean platform. This API supports the following operations:

- Listing all available services

- Creating and updating service listings

- Fetching details of a specific service

- Managing service visibility and availability

Each service object contains essential details describing the offering by a provider, including pricing model, service categories, location coverage, and media assets. Below is the complete list of fields returned in a service object:

| Field          | Type     | Description                                                   |
| -------------- | -------- | ------------------------------------------------------------- |
| `id`           | `string` | Unique identifier for the service.                            |
| `provider`     | `string` | ID of the service provider.                                   |
| `title`        | `string` | Title or short name of the service.                           |
| `description`  | `string` | Detailed description of the service.                          |
| `services`     | `string` | Comma-separated list of service categories offered.           |
| `pricing_type` | `string` | Pricing model used (e.g., `flat`, `hourly`).                  |
| `price`        | `string` | Price of the service in smallest currency unit (e.g., cents). |
| `province`     | `string` | Province where the service is offered (e.g., `ON`).           |
| `location`     | `string` | City or specific area where the service is offered.           |
| `availability` | `string` | Availability information or schedule for the service.         |
| `images`       | `string` | Comma-separated list of image URLs or filenames.              |
| `rating`       | `string` | Average rating or review score for the service.               |
| `status`       | `string` | Status of the service (e.g., `active`, `inactive`).           |
| `created`      | `string` | ISO timestamp of when the service was created.                |
| `modified`     | `string` | ISO timestamp of last modification.                           |

All requests to the OpenClean Services API must include appropriate HTTP headers:

| Header          | Required | Description                              |
| --------------- | -------- | ---------------------------------------- |
| `Authorization` | Yes      | JWT access token prefixed with `Bearer`. |
| `Accept`        | Yes      | Set to `application/json`.               |

These headers ensure secure, authenticated, and standardized communication between clients and the OpenClean API.

---

### Fetch all services

###### Endpoint

```http
GET /services/ HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Response

| Parameter  | Type   | Description             |
| ---------- | ------ | ----------------------- |
| `services` | Array  | List of service objects |
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

fetch(`https://${baseUri}/services/`, {
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
    console.error("An error occurred:", error.message);
  });

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "services": []
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch all services (provider)

###### Endpoint

```http
GET /services/provider/:{provider_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter     | Type     | Description                    |
| ------------- | -------- | ------------------------------ |
| `provider_id` | `string` | The unique ID of the provider. |

###### Response

| Parameter  | Type   | Description             |
| ---------- | ------ | ----------------------- |
| `services` | Array  | List of service objects |
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
const baseUri = "yourdomain.com/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/services/provider/${providerId}`, {
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
  "services": []
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch single service

###### Endpoint

```http
GET /services/service/:{service_id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter    | Type     | Description                   |
| ------------ | -------- | ----------------------------- |
| `service_id` | `string` | The unique ID of the service. |

###### Response

| Parameter | Type   | Description                   |
| --------- | ------ | ----------------------------- |
| `service` | Object | The requested booking service |
| `message` | String | API response message          |
| `status`  | String | API response status           |

###### Status Codes

| Code  | Description |
| ----- | ----------- |
| `200` |             |
| `400` |             |

###### Example Request

```javascript
// Sample JavaScript code to interact with Chetaa API

const jwtToken = "YOUR_JWT_TOKEN_HERE"; // Replace with actual token
const serviceId = 123; // Replace with actual client ID
const baseUri = "api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/services/service/${serviceId}`, {
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
    console.error("An error occured", error.message);
  });

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "service": {}
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Create service

###### Endpoint

```http
POST /services/service/create HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |

###### Response

| Parameter | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| `service` | Object | Newly created service object |
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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/services/service/create`, {
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

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "service": {}
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Update service

###### Endpoint

```http
PUT /services/service/update HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

| Field | Type     | Required | Description                 |
| ----- | -------- | -------- | --------------------------- |
| `id`  | `string` | Yes      | The unique ID of the quote. |

###### Response

| Parameter | Type   | Description               |
| --------- | ------ | ------------------------- |
| `service` | Object | An updated service object |
| `message` | String | API response message      |
| `status`  | String | API response status       |

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

fetch(`https://${baseUri}/services/service/update`, {
  method: "PUT",
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

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "service": {}
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Remove service

###### Endpoint

```http
POST /services/service/remove HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

| Field | Type   | Required | Description                  |
| ----- | ------ | -------- | ---------------------------- |
| `id`  | string | Yes      | The unique ID of the service |

###### Response

| Parameter | Type   | Description          |
| --------- | ------ | -------------------- |
| `message` | String | API response message |
| `status`  | String | API response status  |

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

fetch(`https://${baseUri}/services/service/remove`, {
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

// Call the function
```

###### Example Response

```json
{
  "status": "success",
  "message": "The request was successful",
  "service": {}
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---
