# Airbnb Clone Backend Requirement Specifications

## Overview
This document outlines the technical and functional requirements for key backend features of the Airbnb Clone project, based on the features identified in Task 1. The specifications include API endpoints, input/output details, validation rules, and performance criteria.

## 1. User Authentication
- **Description**: Allows users to register, log in, and manage their accounts with role-based access.
- **API Endpoints**:
  - `POST /api/auth/register`: Register a new user.
  - `POST /api/auth/login`: Authenticate and log in a user.
  - `PUT /api/auth/profile`: Update user profile.
  - `DELETE /api/auth/profile`: Delete user account.
- **Input/Output Specifications**:
  - **Register**: Input: `{"email": "string", "password": "string", "first_name": "string", "last_name": "string", "phone_number": "string", "role": "guest|host|admin"}`
    - Output (Success): `{"user_id": "uuid", "email": "string", "role": "string", "message": "Registration successful"}` (HTTP 201)
    - Output (Failure): `{"error": "Email already exists"}` (HTTP 400)
  - **Login**: Input: `{"email": "string", "password": "string"}`
    - Output (Success): `{"token": "jwt", "user_id": "uuid", "role": "string"}` (HTTP 200)
    - Output (Failure): `{"error": "Invalid credentials"}` (HTTP 401)
  - **Update Profile**: Input: `{"first_name": "string", "last_name": "string", "phone_number": "string"}` (Requires JWT token)
    - Output (Success): `{"message": "Profile updated"}` (HTTP 200)
    - Output (Failure): `{"error": "Unauthorized"}` (HTTP 403)
  - **Delete Profile**: Input: None (Requires JWT token)
    - Output (Success): `{"message": "Account deleted"}` (HTTP 200)
    - Output (Failure): `{"error": "Unauthorized"}` (HTTP 403)
- **Validation Rules**:
  - Email must be unique, valid format, max 100 characters.
  - Password must be at least 8 characters, including one uppercase, one lowercase, and one number.
  - Role must be one of `guest`, `host`, or `admin`.
  - Phone number (if provided) must be a valid format.
- **Performance Criteria**:
  - Response time: < 500ms for 95% of requests.
  - Concurrent users: Support 1000 simultaneous registrations/logins.
  - Security: Use JWT with expiration, HTTPS enforced.

## 2. Property Management
- **Description**: Enables hosts to manage property listings and admins to approve them.
- **API Endpoints**:
  - `POST /api/properties`: Add a new property.
  - `PUT /api/properties/{property_id}`: Update a property.
  - `DELETE /api/properties/{property_id}`: Delete a property.
  - `GET /api/properties`: Search properties.
  - `POST /api/properties/{property_id}/approve`: Approve a property (Admin only).
- **Input/Output Specifications**:
  - **Add Property**: Input: `{"name": "string", "description": "string", "location": "string", "pricepernight": "decimal", "host_id": "uuid"}`
    - Output (Success): `{"property_id": "uuid", "message": "Property submitted for approval"}` (HTTP 201)
    - Output (Failure): `{"error": "Unauthorized"}` (HTTP 403)
  - **Update Property**: Input: `{"name": "string", "description": "string", "location": "string", "pricepernight": "decimal"}`
    - Output (Success): `{"message": "Property updated"}` (HTTP 200)
    - Output (Failure): `{"error": "Not found"}` (HTTP 404)
  - **Search Properties**: Input: Query params: `?location=string&price=decimal&start_date=date&end_date=date`
    - Output (Success): `[{"property_id": "uuid", "name": "string", "location": "string", "pricepernight": "decimal"}]`
    - Output (Failure): `{"error": "Invalid parameters"}` (HTTP 400)
  - **Approve Property**: Input: None
    - Output (Success): `{"message": "Property approved"}` (HTTP 200)
    - Output (Failure): `{"error": "Unauthorized"}` (HTTP 403)
- **Validation Rules**:
  - Name and description must be non-empty, max 100 and 1000 characters.
  - Location must be valid, max 255 characters.
  - `pricepernight` must be positive.
  - `host_id` must match the authenticated user.
- **Performance Criteria**:
  - Response time: < 700ms for 95% of search requests.
  - Concurrent requests: Support 500 simultaneous updates.
  - Scalability: Cache search results.

## 3. Booking System
- **Description**: Manages the booking process, including availability checks and confirmations.
- **API Endpoints**:
  - `POST /api/bookings`: Create a new booking.
  - `GET /api/bookings/{booking_id}`: Check booking status.
  - `PUT /api/bookings/{booking_id}/confirm`: Confirm a booking.
  - `DELETE /api/bookings/{booking_id}`: Cancel a booking.
- **Input/Output Specifications**:
  - **Create Booking**: Input: `{"property_id": "uuid", "user_id": "uuid", "start_date": "date", "end_date": "date"}`
    - Output (Success): `{"booking_id": "uuid", "total_price": "decimal", "status": "pending"}` (HTTP 201)
    - Output (Failure): `{"error": "Property unavailable"}` (HTTP 400)
  - **Check Status**: Input: None
    - Output (Success): `{"booking_id": "uuid", "status": "pending|confirmed|canceled", "start_date": "date"}` (HTTP 200)
    - Output (Failure): `{"error": "Not found"}` (HTTP 404)
  - **Confirm Booking**: Input: None
    - Output (Success): `{"message": "Booking confirmed"}` (HTTP 200)
    - Output (Failure): `{"error": "Unauthorized"}` (HTTP 403)
  - **Cancel Booking**: Input: None
    - Output (Success): `{"message": "Booking canceled"}` (HTTP 200)
    - Output (Failure): `{"error": "Cannot cancel confirmed booking"}` (HTTP 400)
- **Validation Rules**:
  - `property_id` and `user_id` must exist.
  - `start_date` >= today, `end_date` > `start_date`.
  - No overlapping bookings.
- **Performance Criteria**:
  - Response time: < 600ms for 95% of creations.
  - Concurrent bookings: Support 800 simultaneous requests.
  - Reliability: 99.9% uptime.

