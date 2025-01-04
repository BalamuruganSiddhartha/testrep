# Galactic Explorers (BED CA1) API Documentation

## Table of Contents
- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Installation Instructions](#installation-instructions)
- [API Endpoints](#api-endpoints)
  - [User Endpoints](#user-endpoints)
  - [Challenge Endpoints](#challenge-endpoints)
  - [Marketplace Endpoints](#marketplace-endpoints)
  - [Inventory Endpoints](#inventory-endpoints)
  - [Explore Endpoints](#explore-endpoints)
  - [Guild Endpoints](#guild-endpoints)
- [Error Codes](#error-codes)

## Project Overview
**Galactic Explorers** is an interactive space-themed game designed as an API that allows users to engage in various activities such as exploring planets, purchasing items from the marketplace, participating in challenges, managing inventories, and forming or joining guilds. The project integrates features of gamification with a user-friendly interface, allowing players to earn skill points, progress through different levels, and collaborate with other users in guilds.

This project was developed using **Node.js**, **Express**, and **MySQL**. It follows **RESTful API principles** to provide users with a consistent experience across different platforms. The system is modular, utilising the **MVC (Model-View-Controller)** architecture to ensure separation of concerns, maintainability, and scalability. With detailed error handling, middleware validation, and efficient database design, the Galactic Explorers API delivers a dynamic and engaging gameplay experience.

## Prerequisites
Before running the Galactic Explorers API, ensure you have the following installed:
- **Node.js** (version 14.x or higher)
- **MySQL** (or any compatible relational database system)
- **Nodemon** (for automatic reloading during development)

You can check the required version for **Node.js** and **MySQL** in my **package.json** file.

## Installation Instructions
To set up the project locally, follow the steps below:

1. **Clone the repository:**
    ```bash
    git clone https://github.com/ST0503-BED/bed-ca1-BalamuruganSiddhartha.git
    ```

2. **Navigate to the project directory:**
    ```bash
    cd bed-ca1-BalamuruganSiddhartha
    ```

3. **Install dependencies:**
    ```bash
    npm install
    ```

4. **Set up the environment:**
    - Create a `.env` file to store your sensitive data (e.g., database credentials, environment variables).
    - Example:
    ```bash
    DB_HOST=localhost
    DB_USER=root
    DB_PASSWORD=yourpassword
    DB_NAME=galactic_explorers
    ```

5. **Initialize the database:**
    - Run the following command to create the necessary tables:
    ```bash
    npm run init_tables
    ```

6. **Start the server in development mode:**
    ```bash
    npm run dev
    ```
    Your application should now be running at `http://localhost:3000`.

## API Endpoints

### User Endpoints

#### 1. POST /users
- **Description:** Create a new user by providing the username.
- **Request Body:**
    ```json
    {
      "username" : socuser321
    }
    ```
- **Response (201 Created):**
    ```json
    {
      "user_id": 1,
      "username": 1,
      "skillpoints" : 0
    }
    ```
- **Error (409 Conflict)** (This will be triggered when you try to create an user with an existing username in the database!)
  ```json
  {
    "message" : "Username already exists."
  }
  ```
- **Error (400 Bad Request):**
    ```json
    {
      "message": "Missing required data: username."
    }
    ```

#### 2. GET /users
- **Description:** Fetch all users from the system.
- **Response (200 OK):**
    ```json
    [
      {
        "user_id": 1,
        "username": "space_traveler",
        "skillpoints": 100
      },
      {
        "user_id": 2,
        "username": "star_explorer",
        "skillpoints": 50
      }
    ]
    ```

#### 3. PUT /users/{user_id}
- **Description:** Update the details of an existing user by user_id.
- **Request Body:**
    ```json
    {
      "username": "new_username",
      "skillpoints": 120
    }
    ```
- **Response (200 OK):**
    ```json
    {
      "message": "User updated successfully!"
    }
    ```

#### 4. GET /users/leaderboard
- **Description:** Fetch the leaderboard, sorted by skillpoints.
- **Response (200 OK):**
    ```json
    [
      {
        "user_id": 1,
        "username": "space_traveler",
        "skillpoints": 150
      },
      {
        "user_id": 2,
        "username": "star_explorer",
        "skillpoints": 100
      }
    ]
    ```

#### 5. GET /users/{user_id}
- **Description:** Fetch user details along with guild information.
- **Response (200 OK):**
    ```json
    {
      "user_id": 1,
      "username": "space_traveler",
      "skillpoints": 100,
      "user's guild": "Galactic Explorers"
    }
    ```

---
