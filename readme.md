# REST API Project

This is a RESTful API built with Node.js, Express, TypeScript, and MongoDB using Mongoose. The project handles basic user authentication and user management functionality, including registration, login, listing users, and deleting users.

## Features

- User registration with salted and hashed password
- Authentication using session tokens
- Middleware for route protection (`isAuthenticated`, `isOwner`)
- CRUD operations on user resource
- MongoDB integration using Mongoose
- Structured with MVC principles
- Built in TypeScript

## Project Structure

```
src/
├── controllers/         # Business logic for handling requests
│   └── authentication.ts
│   └── users.ts
├── db/                  # Mongoose models and database access functions
│   └── users.ts
├── helpers/             # Utility functions like hashing and random generators
│   └── index.ts
├── middlewares/         # Authentication and authorization middlewares
│   └── index.ts
├── router/              # Express routing setup
│   └── authentication.ts
│   └── user.ts
│   └── index.ts
└── index.ts             # Entry point of the application
```

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Set up environment variables:
   Create a `.env` file in the root and add your MongoDB URI:
   ```
   MONGO_URL=mongodb+srv://your-user:your-password@your-cluster.mongodb.net
   ```

4. Start the development server:
   ```
   npm run dev
   ```

## Available Endpoints

### Authentication

- `POST /auth/register`  
  Register a new user. Requires `email`, `username`, `password` in JSON body.

### Users

- `GET /users`  
  Requires authentication. Returns a list of all users.

- `DELETE /users/:id`  
  Requires authentication and ownership. Deletes the user with the given ID.

## Example Requests

### Using curl

```bash
# Register a new user
curl -X POST http://localhost:8080/auth/register \
-H "Content-Type: application/json" \
-d '{"email":"test@example.com", "password":"123456", "username":"testuser"}'

# Get all users (assuming session token is stored in a cookie)
curl -X GET http://localhost:8080/users \
--cookie "SIMON-AUTH=your-session-token-here"

# Delete a user by ID (only if you're the owner)
curl -X DELETE http://localhost:8080/users/USER_ID \
--cookie "SIMON-AUTH=your-session-token-here"
```

### Using Postman

1. **Register**
   - Method: POST
   - URL: `http://localhost:8080/auth/register`
   - Body: raw JSON
     ```json
     {
       "email": "test@example.com",
       "username": "testuser",
       "password": "123456"
     }
     ```

2. **Get users**
   - Method: GET
   - URL: `http://localhost:8080/users`
   - Add cookie `SIMON-AUTH` with session token (from response after register/login)

3. **Delete user**
   - Method: DELETE
   - URL: `http://localhost:8080/users/{userId}`
   - Add same session token in cookie

## Testing Tips

- You can inspect the session token returned after registration by checking the `Set-Cookie` header or enabling cookies in Postman.
- Ensure MongoDB is running and the connection string is valid.
- Use console.log in middleware and controllers for debugging.
- Use tools like Postman or curl to manually test all endpoints.

## Technologies Used

- Node.js
- Express
- TypeScript
- MongoDB with Mongoose
- ts-node, nodemon
- Lodash
- Crypto module for hashing

## Scripts

- `npm run dev` - Start the server in development mode using nodemon and ts-node
- `npm start` - Run the compiled JavaScript code in production mode

## License

This project is licensed under the MIT License.
