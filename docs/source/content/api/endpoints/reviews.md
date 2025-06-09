# Reviews

Version: `1.0`  
Base URL: `https://api.openclean.ca/api/v1/`

---

### Introduction

The Reviews API allows clients, service providers, and administrators to create, retrieve, and manage reviews associated with services or providers on the OpenClean platform. It supports the following operations:

- Listing all reviews for a given entity (e.g., service or provider)

- Submitting a new review

- Updating or moderating existing reviews

- Tracking engagement through likes and dislikes

- Managing the approval status of each review

Each review object represents feedback submitted by a user and includes the reviewer's identity, content, rating, and engagement metrics. Below is a complete list of fields returned in a review object:

| Field            | Type      | Description                                                             |
| ---------------- | --------- | ----------------------------------------------------------------------- |
| `id`             | `string`  | Unique identifier for the review.                                       |
| `reviewer_name`  | `string`  | Name of the person who submitted the review.                            |
| `reviewer_email` | `string`  | Email address of the reviewer.                                          |
| `entity`         | `string`  | ID or reference to the item being reviewed (e.g., service or provider). |
| `rating`         | `string`  | Rating value (e.g., 5 stars).                                           |
| `review`         | `string`  | Textual content of the review.                                          |
| `created`        | `string`  | ISO timestamp of when the review was created.                           |
| `modified`       | `string`  | ISO timestamp of the last modification.                                 |
| `likes`          | `integer` | Number of upvotes/likes the review has received.                        |
| `dislikes`       | `integer` | Number of downvotes/dislikes the review has received.                   |
| `status`         | `string`  | Current status of the review (e.g., `approved`, `pending`).             |

All requests to the OpenClean Review API must include appropriate HTTP headers:

| Header          | Required | Description                              |
| --------------- | -------- | ---------------------------------------- |
| `Authorization` | Yes      | JWT access token prefixed with `Bearer`. |
| `Accept`        | Yes      | Set to `application/json`.               |

These headers ensure secure, authenticated, and standardized communication between clients and the OpenClean API.

---

### Fetch all reviews

###### Endpoint

```http
GET /reviews/ HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Response

| Parameter | Type   | Description            |
| --------- | ------ | ---------------------- |
| `reviews` | Array  | List of review objects |
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
const baseUri = "https://api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/reviews/`, {
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
  "reviews": []
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch all reviews (entity)

###### Endpoint

```http
GET /reviews/entity/:{id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter | Type     | Description                    |
| --------- | -------- | ------------------------------ |
| `id`      | `string` | The unique ID of the provider. |

###### Response

| Parameter | Type   | Description             |
| --------- | ------ | ----------------------- |
| `reviews` | Array  | List of service objects |
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
const id = 123; // Replace with actual client ID
const baseUri = "yourdomain.com/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/reviews/entity/${id}`, {
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
  "reviews": []
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch all reviews (reviewer)

###### Endpoint

```http
GET /reviews/reviewer/:{id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter | Type     | Description                    |
| --------- | -------- | ------------------------------ |
| `id`      | `string` | The unique ID of the provider. |

###### Response

| Parameter | Type   | Description             |
| --------- | ------ | ----------------------- |
| `reviews` | Array  | List of service objects |
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
const id = 123; // Replace with actual client ID
const baseUri = "yourdomain.com/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/reviews/entity/${id}`, {
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
  "reviews": []
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---

### Fetch single review

###### Endpoint

```http
GET /reviews/review/:{id} HTTP/1.1
Host: api.openclean.ca
Authorization: Bearer <token>
```

###### Request Parameters

| Parameter | Type     | Description                  |
| --------- | -------- | ---------------------------- |
| `id`      | `string` | The unique ID of the review. |

###### Response

| Parameter | Type   | Description          |
| --------- | ------ | -------------------- |
| `review`  | Object | The review object    |
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
const Id = 123; // Replace with actual client ID
const baseUri = "api.openclean.ca/api/v1"; // Replace with your actual base URI

fetch(`https://${baseUri}/reviews/review/${Id}`, {
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

### Create review

###### Endpoint

```http
POST /reviews/review/create HTTP/1.1
Host: api.openclean.ca
Content-Type: application/json
Authorization: Bearer <token>
```

###### Request Body

| Field          | Type   | Required | Description                                          |
| -------------- | ------ | -------- | ---------------------------------------------------- |
| entity         | string | Yes      | Unique identifier for the entity being reviewed      |
| rating         | string | Yes      | Rating given by the reviewer (e.g., excellent, good) |
| review         | string | Yes      | Content of the review submitted                      |
| reviewer_email | string | Yes      | Email address of the reviewer                        |
| reviewer_name  | string | Yes      | Name of the reviewer                                 |

###### Response

| Parameter | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| `review`  | Object | Newly created service object |
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

fetch(`https://${baseUri}/reviews/review/create`, {
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
  "review": {}
}
```

###### Possible Errors

| Status Code | Error Type   | Description                            |
| ----------- | ------------ | -------------------------------------- |
| 401         | Unauthorized | Missing or invalid JWT token           |
| 403         | Forbidden    | JWT is valid, but user is not a client |

---
