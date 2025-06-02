# Overview

The OpenClean API enables seamless integration with the OpenClean platform, allowing developers to interact with core resources such as clients, service providers, services, quotes, bookings, transactions, and administrative tools.

Whether you're building a frontend interface, automating service provider workflows, or managing platform analytics, the API provides RESTful endpoints for secure and flexible data access.

---

## Base URL

```
https://api.openclean.ca/
```

> All endpoints follow REST conventions and return JSON-formatted responses.

---

## Authentication

The OpenClean API uses **JWT (JSON Web Tokens)** for authenticating requests. Tokens must be included in the `Authorization` header for all protected routes.

**Header Example:**

```
Authorization: Bearer <your_token>
```

See the [Authentication & Authorization](auth.md) section for full details.

---

## API User Roles

The API supports different user roles, each with specific access scopes:

| Role             | Description                                     |
| ---------------- | ----------------------------------------------- |
| Client           | End-users who search, book, and review services |
| Service Provider | Vendors who list services and handle bookings   |
| Admin            | Internal platform staff who manage the system   |

---

## Common Features

- **Service Listing & Discovery**: Search, filter, and view services available for booking.
- **Quote Management**: Request, send, and accept quotes between clients and providers.
- **Booking System**: Schedule and manage service appointments with built-in payment handling.
- **Review & Rating**: Post-service feedback system to enhance quality assurance.
- **Admin Tools**: Control user accounts, monitor activities, and oversee system-level configurations.

---

## Versioning

All API endpoints are versioned using the path prefix:

```
https://api.openclean.ca/v1/
```

Future versions will maintain backward compatibility where possible. Breaking changes will be documented in the [Changelog](../reference/changelog.md).
