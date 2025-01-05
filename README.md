# Galactic Explorers (BED CA1) API Documentation

This API powers the **Galactic Explorers** Gamified Fitness Tracker, where users can explore planets, join guilds, purchase items from the marketplace, and complete fitness challenges.

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
- [Error Handling](#HTTP-Status-Codes-Used (Error Handling))

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

## Key API Endpoints For Galactic Explorers

## 1. **Create a New User**  
**Endpoint:** `POST /users`  
**Request Body:**
```json
{
  "username": "space_traveler"
}
```
**Response (Success - 201 Created):**
```json
{
  "user_id": 1,
  "username": "space_traveler",
  "skillpoints": 0
}
```
*Error*
- 400 Bad Request: Missing username.
- 409 Conflict: Username already exists.


## 2. **Get All Users**  
**Endpoint:** `GET /users`  

**Request body:**  
No request body required.

**Response (Success - 200 OK):**
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

## 3. **Update User by ID**  
**Endpoint:** `PUT /users/{user_id}`  

**Request Body:**  
```json
{
  "username": "new_username",
  "skillpoints": 150
}
```

**Response (Success - 200 OK):**
```json
{
  "user_id": 1,
  "username": "new_username",
  "skillpoints": 150
}
```
*Error*
- If the requested user_id does not exist, returns 404 Not Found.
- If the provided username is already associated with another user, returns 409 Conflict

## 4. **Get Users Leaderboard**

**Endpoint:** `GET /users/leaderboard`  

**Request body:**  
No request body required.

**Response (Success - 200 OK):**
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

## 5. **Get User Profile**

**Endpoint:** `GET /users/{user_id}`  

**Request body:**  
No request body required.

**Response (Success - 200 OK):**
```json
{
  "user_id": 1,
  "username": "space_traveler",
  "skillpoints": 100,
  "user's guild": "Galactic Explorers"
}
```
*Error*
- User not found (Invalid user_id)

## 6. **Create Challenge** 
**Endpoint:** `POST /challenges`  

**Request body:**  
```json
{
  "challenge": "Complete a space race",
  "user_id": 1,
  "skillpoints": 50
}
```

**Response (Success - 201 Created):**
```json
{
  "challenge_id": 1,
  "challenge": "Complete a space race",
  "creator_id": 1,
  "skillpoints": 50
}
```
*Error*
- Missing required fields. (Status 400 Bad Request)

## 7. **Get Marketplace Items**

**Endpoint:** `GET /marketplace`  

**Request body:**  
No request body required.

**Response (Success - 200 OK):**
```json
[
  {
    "item_id": 1,
    "item_name": "Nano-Heal Kit",
    "item_description": "Repairs 50% of total health using nanobots",
    "item_type": "Gear",
    "cost": 150
  },
  {
    "item_id": 2,
    "item_name": "Oxygen Refill Canister",
    "item_description": "Replenishes oxygen levels in zero-gravity environments",
    "item_type": "Gear",
    "cost": 100
  },
  {
    "item_id": 3,
    "item_name": "Jetpack Module",
    "item_description": "Allows short bursts of flight in low-gravity zones",
    "item_type": "Gear",
    "cost": 300
  },
  {
    "item_id": 4,
    "item_name": "Plasma Drill",
    "item_description": "Drills through asteroid cores to extract rare minerals",
    "item_type": "Tool",
    "cost": 600
  },
  {
    "item_id": 5,
    "item_name": "Star Compass",
    "item_description": "A navigation device for tracking nearby planets",
    "item_type": "Tool",
    "cost": 300
  },
  {
    "item_id": 6,
    "item_name": "Hologram Projector",
    "item_description": "Creates a decoy hologram to distract enemies",
    "item_type": "Tool",
    "cost": 350
  },
  {
    "item_id": 7,
    "item_name": "Explorer Suit",
    "item_description": "Standard suit with moderate protection and oxygen supply",
    "item_type": "Armor",
    "cost": 200
  },
  {
    "item_id": 8,
    "item_name": "Radiation Shield Suit",
    "item_description": "Protects against radiation in hostile environments",
    "item_type": "Armor",
    "cost": 500
  },
  {
    "item_id": 9,
    "item_name": "Voidwalker Suit",
    "item_description": "Advanced suit for extreme zero-gravity survival",
    "item_type": "Armor",
    "cost": 800
  },
  {
    "item_id": 10,
    "item_name": "Starlight Crystal",
    "item_description": "A rare crystal that emits unlimited light",
    "item_type": "Artifact",
    "cost": 1200
  },
  {
    "item_id": 11,
    "item_name": "Void Sphere",
    "item_description": "A mysterious orb with unknown gravitational properties",
    "item_type": "Artifact",
    "cost": 2000
  },
  {
    "item_id": 12,
    "item_name": "Chrono Shard",
    "item_description": "Enables brief manipulation of time",
    "item_type": "Artifact",
    "cost": 2500
  }
]

```
  
## HTTP Status Codes Used (Error Handling)

The API uses appropriate HTTP status codes for error handling:

- **400 Bad Request**: Missing required data (e.g., missing user ID or challenge)
- **403 Forbidden**: Unauthorized actions (e.g., user trying to access restricted routes)
- **404 Not Found**: Resource not found (e.g., user or challenge not found)
- **409 Conflict**: Conflicting requests (e.g., trying to buy an item the user already owns)
