# Simple E-commerce API

A simple e-commerce REST API built with Spring Boot, Java 17, and MySQL.

## Features

- User authentication with JWT
- Role-based authorization (Customer and Admin roles)
- Product management (CRUD operations)
- Shopping cart functionality
- Order processing
- Stock management

## Prerequisites

- Java 17
- MySQL 8.0
- Maven

## Setup

1. Clone the repository
2. Create a MySQL database named `ecommerce`
3. Update the database configuration in `src/main/resources/application.properties` if needed:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce?createDatabaseIfNotExist=true
   spring.datasource.username=root
   spring.datasource.password=root
   ```
4. Build the project:
   ```bash
   mvn clean install
   ```
5. Run the application:
   ```bash
   mvn spring-boot:run
   ```

## API Endpoints

### Authentication

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login and get JWT token

### Products

- `GET /api/products` - Get all products
- `GET /api/products/{id}` - Get product by ID
- `GET /api/products/search?query={query}` - Search products
- `GET /api/products/available` - Get available products
- `POST /api/products` - Create product (Admin only)
- `PUT /api/products/{id}` - Update product (Admin only)
- `DELETE /api/products/{id}` - Delete product (Admin only)

### Cart

- `GET /api/cart` - Get user's cart
- `POST /api/cart/items?productId={id}&quantity={qty}` - Add item to cart
- `PUT /api/cart/items/{productId}?quantity={qty}` - Update cart item
- `DELETE /api/cart/items/{productId}` - Remove item from cart
- `DELETE /api/cart/clear` - Clear cart

### Orders

- `POST /api/orders` - Create order from cart
- `GET /api/orders` - Get user's orders
- `GET /api/orders/{orderId}` - Get order by ID
- `PUT /api/orders/{orderId}/status` - Update order status (Admin only)

## Authentication

The API uses JWT (JSON Web Token) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer <token>
```

## User Roles

1. Customer
   - Can view products
   - Can manage their cart
   - Can place orders
   - Can view their orders

2. Admin
   - All Customer permissions
   - Can manage products (create, update, delete)
   - Can update order status

## Error Handling

The API returns appropriate HTTP status codes and error messages:

- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Internal Server Error

## Security

- Passwords are encrypted using BCrypt
- JWT tokens expire after 24 hours
- Role-based access control using Spring Security
- Input validation using Jakarta Validation 