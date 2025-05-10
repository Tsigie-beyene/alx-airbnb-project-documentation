# 📋 Airbnb Clone – Backend Feature Requirements

This document outlines the **technical and functional specifications** for key backend features in the Airbnb Clone project.

---

## 1. 🧑‍💼 User Authentication

### Objective
Allow users (guests and hosts) to register, log in, and securely access the system using JWT.

### Functional Requirements
- Register as a new user with role (guest or host)
- Login with email and password
- Maintain secure sessions using JWT tokens

### API Endpoints
| Method | Endpoint         | Description            |
|--------|------------------|------------------------|
| POST   | `/api/register`  | Register a new user    |
| POST   | `/api/login`     | Authenticate user      |
| GET    | `/api/me`        | Get authenticated user |

### Input/Output
- **Register:**
  - Input: `name`, `email`, `password`, `role`
  - Output: `JWT token`, `user info`
- **Login:**
  - Input: `email`, `password`
  - Output: `JWT token`, `user info`

### Validation Rules
- Email must be unique and properly formatted.
- Password must be at least 8 characters.
- Role must be either `guest` or `host`.

### Performance
- Token issued in < 200ms
- Login response time < 500ms

---

## 2. 🏠 Property Management

### Objective
Allow hosts to list, update, and delete rental properties.

### Functional Requirements
- Hosts can create, edit, and delete property listings.
- Guests can view available listings.

### API Endpoints
| Method | Endpoint              | Description                  |
|--------|-----------------------|------------------------------|
| POST   | `/api/properties`     | Create new listing (host)    |
| GET    | `/api/properties`     | List all available properties|
| GET    | `/api/properties/:id` | View single property         |
| PUT    | `/api/properties/:id` | Update property (host only)  |
| DELETE | `/api/properties/:id` | Delete property (host only)  |

### Input/Output
- **Create Property:**
  - Input: `title`, `location`, `price`, `amenities`, `photos`, `availability`
  - Output: `property ID`, `property details`

### Validation Rules
- Title and location required
- Price must be a positive number
- At least one photo required

### Performance
- Property retrieval under 1 second
- Pagination required for > 20 listings

---

## 3. 📆 Booking System

### Objective
Enable guests to book available properties and handle availability logic.

### Functional Requirements
- Guests can book a property for specific dates.
- Prevent double booking.
- Allow cancellation and status tracking.

### API Endpoints
| Method | Endpoint               | Description                     |
|--------|------------------------|---------------------------------|
| POST   | `/api/bookings`        | Create a new booking (guest)    |
| GET    | `/api/bookings`        | Get bookings for current user   |
| PUT    | `/api/bookings/:id`    | Cancel or update booking status |

### Input/Output
- **Create Booking:**
  - Input: `property_id`, `start_date`, `end_date`
  - Output: `booking ID`, `confirmation status`

### Validation Rules
- Check property availability for selected dates
- User must be authenticated
- Start date must be before end date

### Performance
- Response within 1 second
- Prevent race conditions on concurrent bookings

---

## 🔐 Security & Standards
- JWT required for all authenticated endpoints
- All input sanitized and validated
- Error responses include HTTP codes and messages
