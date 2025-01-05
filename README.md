# Galactic Explorers (BED CA1) API Documentation

This API powers the **Galactic Explorers** game, where users can explore planets, join guilds, purchase items from the marketplace, and complete challenges.

## Table of Contents

- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Installation Instructions](#installation-instructions)
- [API Endpoints](#api-endpoints)
  - [User Endpoints](#user-endpoints)
  - [Challenge Endpoints](#challenge-endpoints)
  - [Marketplace Endpoints](#marketplace-endpoints)
  - [Explore Endpoints](#explore-endpoints)
  - [Guild Endpoints](#guild-endpoints)
- [Error Handling](#error-handling)

## Project Overview

**Galactic Explorers API** enables the creation and management of users, challenges, guilds, marketplace items, and exploration activities. It provides a RESTful interface for interacting with the game data, using Node.js and MySQL.

## Prerequisites

Before running the API, ensure you have the following:

- **Node.js** (version 14.x or later)
- **MySQL** (or compatible relational database)
- **Nodemon** (for auto-reloading during development)

## Installation Instructions

1. **Clone the Repository:**
    ```bash
    git clone https://github.com/ST0503-BED/bed-ca1-BalamuruganSiddhartha.git
    ```

2. **Install Dependencies:**
    ```bash
    npm install
    ```

3. **Set Up Database:**
    - Update `db.js` in the `services` folder with your MySQL credentials.
    - Run the following command to initialize the database tables:
    ```bash
    npm run init_tables
    ```

4. **Start the Application:**
    ```bash
    npm start
    ```
    The server should be running on `http://localhost:3000`.

## API Endpoints

### User Endpoints

- **POST /users**: Create a new user
- **GET /users**: Get a list of all users
- **PUT /users/{user_id}**: Update user details by user ID
- **GET /users/leaderboard**: Get the leaderboard based on skillpoints
- **GET /users/{user_id}**: Get user details with guild information

### Challenge Endpoints

- **POST /challenges**: Create a new challenge
- **GET /challenges**: Get all challenges
- **PUT /challenges/{challenge_id}**: Update challenge by challenge ID
- **DELETE /challenges/{challenge_id}**: Delete challenge by challenge ID
- **POST /challenges/{challenge_id}**: Create a new challenge completion record
- **GET /challenges/{challenge_id}**: Get all users who completed a challenge

### Marketplace Endpoints

- **POST /marketplace**: Add a new item to the marketplace (Admin only)
- **GET /marketplace**: Get all items for sale
- **GET /marketplace/{item_type}**: Get items by type
- **POST /marketplace/buy**: Buy an item from the marketplace
- **POST /marketplace/sell**: Sell an item back to the marketplace

### Explore Endpoints

- **GET /explore**: Get all available planets for exploration
- **POST /explore/{planet_id}**: Explore a planet and earn skillpoints
- **GET /explore/{user_id}**: Get the list of planets explored by a user

### Guild Endpoints

- **POST /guilds**: Create a new guild
- **GET /guilds**: Get a list of all guilds
- **POST /guilds/join**: Join an existing guild
- **POST /guilds/leave**: Leave a guild
- **GET /guilds/{guild_id}**: Get members of a guild
- **DELETE /guilds**: Delete a guild (Creator only)

## Error Handling

The API uses appropriate HTTP status codes for error handling:

- **400 Bad Request**: Missing required data (e.g., missing user ID or challenge)
- **403 Forbidden**: Unauthorized actions (e.g., user trying to access restricted routes)
- **404 Not Found**: Resource not found (e.g., user or challenge not found)
- **409 Conflict**: Conflicting requests (e.g., trying to buy an item the user already owns)
