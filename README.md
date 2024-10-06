# Alfredo Backend

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Socket.IO Events](#socketio-events)
- [Testing](#testing)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Introduction

**Alfredo Backend** is the server-side component of the **Alfredo** collaborative note-taking application. It is built with **Node.js** and **Express.js** and handles user authentication, data storage, and real-time collaboration through **Socket.IO**. The backend provides a RESTful API and real-time communication channels for the frontends developed in Vue.js and Angular.

---

## Features

- **User Authentication & Authorization**
  - Secure registration and login using **JWT tokens**.
  - Password hashing with **bcrypt.js**.
- **Real-Time Collaboration**
  - Simultaneous note editing using **Socket.IO**.
  - Real-time updates and synchronization across clients.
- **RESTful API**
  - Endpoints for managing users and notes.
  - Input validation and error handling.
- **Data Persistence**
  - Uses **MongoDB** with **Mongoose** for data storage.
  - Schema definitions for users and notes.
- **Security**
  - Protects routes using authentication middleware.
  - Sanitizes inputs to prevent injection attacks.
- **Scalability**
  - Modular architecture for easy maintenance and scaling.
  - Supports multiple clients and concurrent connections.

---

## Architecture

The backend follows a modular structure with clear separation of concerns:

- **`server.js`**: Entry point of the application.
- **Controllers**: Handle the logic for each route.
- **Models**: Define the data schema for MongoDB.
- **Routes**: Define the API endpoints.
- **Middleware**: Contains authentication and error-handling middleware.
- **Sockets**: Manages real-time communication events.
- **Config**: Holds configuration files and constants.

---

## Technologies Used

- **Node.js**: JavaScript runtime environment.
- **Express.js**: Web application framework.
- **MongoDB**: NoSQL database for storing data.
- **Mongoose**: Object Data Modeling (ODM) library for MongoDB.
- **Socket.IO**: Enables real-time, bidirectional communication.
- **JWT (jsonwebtoken)**: For secure user authentication.
- **bcrypt.js**: Library for hashing passwords.
- **dotenv**: Loads environment variables from a `.env` file.
- **cors**: Middleware for enabling CORS.
- **nodemon**: Utility that monitors for changes and automatically restarts the server.
- **ESLint** and **Prettier**: For code linting and formatting.
- **Jest**: Testing framework.

---

## Prerequisites

- **Node.js** (v14 or higher)
- **npm** (v6 or higher)
- **MongoDB** (local or cloud instance)

---

## Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/JervisAnthony/alfredo-backend.git
   cd alfredo-backend
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

---

## Configuration

1. **Create a `.env` file** in the root directory.

   ```bash
   touch .env
   ```

2. **Add the following environment variables to `.env`**

   ```env
   PORT=5000
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   ```

   - Replace `your_mongodb_connection_string` with your actual MongoDB connection string.
   - Replace `your_jwt_secret` with a secure secret key for JWT.

---

## Running the Application

### Development Mode

Start the server with **nodemon** for automatic restarts on code changes.

```bash
npm run dev
```

### Production Mode

Start the server without monitoring for changes.

```bash
npm start
```

The server will run on `http://localhost:5000` by default.

---

## API Documentation

The backend provides the following RESTful API endpoints:

### User Routes (`/api/users`)

- **POST `/register`**

  - Registers a new user.
  - **Body Parameters**:
    - `username` (string, required)
    - `email` (string, required)
    - `password` (string, required)
  - **Response**: JWT token.

- **POST `/login`**

  - Authenticates a user.
  - **Body Parameters**:
    - `email` (string, required)
    - `password` (string, required)
  - **Response**: JWT token.

### Note Routes (`/api/notes`)

- **GET `/`**

  - Retrieves all notes for the authenticated user.
  - **Headers**: `x-auth-token` (JWT token)
  - **Response**: Array of notes.

- **POST `/`**

  - Creates a new note.
  - **Headers**: `x-auth-token` (JWT token)
  - **Body Parameters**:
    - `title` (string, required)
    - `content` (string)
  - **Response**: Created note object.

- **GET `/:id`**

  - Retrieves a note by ID.
  - **Headers**: `x-auth-token` (JWT token)
  - **Response**: Note object.

- **PUT `/:id`**

  - Updates a note by ID.
  - **Headers**: `x-auth-token` (JWT token)
  - **Body Parameters**:
    - `content` (string)
  - **Response**: Updated note object.

- **DELETE `/:id`**

  - Deletes a note by ID.
  - **Headers**: `x-auth-token` (JWT token)
  - **Response**: Success message.

---

## Socket.IO Events

The backend uses Socket.IO for real-time communication. The following events are handled:

- **Connection Events**
  - `connection`: Triggered when a client connects.
  - `disconnect`: Triggered when a client disconnects.

- **Note Collaboration Events**
  - `join-note`: Client joins a note room.
    - **Data**: `noteId` (string)
  - `leave-note`: Client leaves a note room.
    - **Data**: `noteId` (string)
  - `send-changes`: Client sends changes to the note.
    - **Data**: `noteId` (string), `delta` (object)
  - `receive-changes`: Server broadcasts changes to other clients.
    - **Data**: `delta` (object)

---

## Testing

### Running Tests

- **Unit and Integration Tests**

  ```bash
  npm test
  ```

Tests are written using **Jest** and are located in the `tests` directory.

---

## Deployment

### Docker

A **Dockerfile** is provided for containerizing the application.

- **Build the Docker image**

  ```bash
  docker build -t alfredo-backend .
  ```

- **Run the Docker container**

  ```bash
  docker run -p 5000:5000 --env-file .env alfredo-backend
  ```

### Environment Variables

Ensure that environment variables are properly set in your deployment environment.

### Hosting

You can deploy the backend to platforms like **Heroku**, **AWS Elastic Beanstalk**, or **DigitalOcean**.

---

## Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**.
2. **Create a new branch** for your feature or bug fix.
3. **Commit your changes** with descriptive messages.
4. **Push to your fork** and submit a **pull request**.

Please ensure all pull requests are accompanied by appropriate tests.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## Contact

- **Author**: Jervis Anthony
- **GitHub**: [JervisAnthony](https://github.com/JervisAnthony)
- **Email**: [jervisaldanha.collabs@gmail.com](mailto:jervisaldanha.collabs@gmail.com)

---
