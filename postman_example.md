# Example: Creating a Customer using Postman

This guide provides a step-by-step example of how to create a new customer using Postman.

## Request Details

### Endpoint
```
POST http://localhost:8080/api/customers
```

### Headers
```
Content-Type: application/json
Accept: application/json
```

### Request Body
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phone": "123-456-7890",
  "status": "ACTIVE"
}
```

#### Field Descriptions:
- `firstName` (String, required): The customer's first name
- `lastName` (String, required): The customer's last name
- `email` (String, required, unique): The customer's email address
- `phone` (String, optional): The customer's phone number
- `status` (Enum, optional, default: ACTIVE): The customer's status. Possible values:
  - ACTIVE
  - INACTIVE
  - SUSPENDED

## Example Response

### Success Response (201 Created)
```json
{
  "id": 1,
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phone": "123-456-7890",
  "createdAt": "2023-07-25T14:30:45.123456+00:00",
  "updatedAt": "2023-07-25T14:30:45.123456+00:00",
  "status": "ACTIVE"
}
```

### Error Response - Email Already Exists (409 Conflict)
If a customer with the same email already exists, you'll receive a 409 Conflict response.

## Additional Examples

### Creating a Customer with Minimal Required Fields
```json
{
  "firstName": "Jane",
  "lastName": "Smith",
  "email": "jane.smith@example.com"
}
```

### Creating a Customer with INACTIVE Status
```json
{
  "firstName": "Alice",
  "lastName": "Johnson",
  "email": "alice.johnson@example.com",
  "phone": "987-654-3210",
  "status": "INACTIVE"
}
```

## Notes
- The `id`, `createdAt`, and `updatedAt` fields are automatically generated and should not be included in the request.
- The `email` field must be unique. If you try to create a customer with an email that already exists, you'll receive a 409 Conflict response.
- If the `status` field is omitted, it defaults to `ACTIVE`.