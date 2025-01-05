# Galactic Explorers (BED CA1) API Documentation

This API powers the **Galactic Explorers** Gamified Fitness Tracker, where users can explore planets, join guilds, purchase items from the marketplace, and complete fitness challenges.

I developed the Galactic Explorers API to power a gamified fitness tracker aimed at engaging users in both physical and virtual activities. In this project, I enabled users to explore planets, join guilds, view their inventory and purchase items from the marketplace, while completing fitness challenges to earn skillpoints (**in-game currency**).

I implemented a space theme to enhance the immersive experience, drawing inspiration from space exploration to provide a motivational backdrop for physical activity. By blending fitness with gamification, I aimed to encourage users to stay active, track their progress, and compete within a community.

This project serves as my ***CA1 assignment***, where I focused on creating an **engaging** and **interactive** platform that integrates gamification with physical activity tracking.

## Table of Contents

- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Installation Instructions](#installation-instructions)
- [API Endpoints](#api-endpoints)
  - [User Endpoints](#user-endpoints)
  - [Challenge Endpoints](#challenge-endpoints)
  - [Marketplace Endpoints](#Marketplace-Endpoints)
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

# Key API Endpoints For Galactic Explorers

## User & FitnessChallenge Endpoints

## **Create a New User**  
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


## **Get All Users**  
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

## **Update User by ID**  
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

## **Get Users Leaderboard**

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

## **Get User Profile**

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

## **Create Challenge** 
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

## Marketplace Endpoints

## **Get Marketplace Items**

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

## **Filter Marketplace by Item Type**

**Endpoint:** `GET /marketplace/{item_type}`  

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
  }
]
```
*Error*
- If the requested item_type does not exist, returns 404 Item type not found.

## **Buy Item from Marketplace**

**Endpoint:** `POST /marketplace/buy`

**Request Body:**
```json
{
  "user_id": 1,
  "item_id": 1
}
```
**Response (Success - 200 OK):**
```json
{
  "message": "Purchase successful!",
  "item_bought" : "Nano-Heal Kit"
  "remaining_skillpoints": 850
}

```

*Error*
- 400 (Missing fields)
- 404 (User or item not found)
- 409 (Insufficient skillpoints or item already owned)
- 500 (Internal server error)


## **Sell Item to Marketplace**

**Endpoint:** `POST /marketplace/sell`

**Request Body:**
```json
{
  "user_id": 1,
  "item_id": 1
}
```
**Response (Success - 200 OK):**
```json
{
    "message": "Item sold successfully!",
    "item_sold": "Nano-Heal Kit",
    "remaining_skillpoints": 200
}

```

*Error*
- 400 (Missing fields)
- 404 (User or item not found)
- 409 (Insufficient skillpoints or item not owned and tries to sell!)
- 500 (Internal server error)


## Inventory Endpoints

### View User's Inventory  
**GET /inventory/{user_id}**  
- **Request**: `user_id` (Path parameter)  
- **Success (200 OK)**:  
    ```json
  [
    {
      "item_id": 0,
      "item_name": "Essential Survival Pack",
      "item_description": "A basic survival pack containing essential items for space exploration.",
      "item_type": "Gear",
      "acquisition_date": "2025-01-05 15:04:06"
    }
  ]
  

---

### View User's Inventory by Item Type  
**GET /inventory/{user_id}/{item_type}**  
- **Request**: `user_id` (Path parameter), `item_type` (Path parameter)  
- **Success (200 OK)**:  
    ```json
    [
      {
        "item_id": 1,
        "item_name": "Nano-Heal Kit",
        "item_description": "Repairs 50% of total health using nanobots",
        "item_type": "Gear",
        "acquisition_date": "2025-01-04T12:30:00"
      },
    ]
  

---

## A cool thing to note about `GET /inventory/{user_id}`
### Adds Essential Survival Pack (When First Accessed)  
**GET /inventory/{user_id}**  
- **Request**: `user_id` (Path parameter)  
- **Success (201 Created)**:  
    ```json
  [
    {
      "item_id": 0,
      "item_name": "Essential Survival Pack",
      "item_description": "A basic survival pack containing essential items for space exploration.",
      "item_type": "Gear",
      "acquisition_date": "2025-01-05 15:04:06"
    }
  ]
    ```

---

### Error Handling  
- 400 (Bad Request): Missing required data  
- 404 (Not Found): User or item not found  
- 409 (Conflict): Item already in inventory  
- 500 (Internal Server Error): Error while accessing or updating inventory


## Explore Endpoints

## Explore Endpoints

### Get All Available Planets  
**GET /explore**  
- **Description**: Retrieves a list of all planets available for exploration.  
- **Request**: None  
- **Success (200 OK)**:  
    ```json
    [
      {
        "planet_id": 1,
        "planet_name": "Nebula-5",
        "planet_description": "A mysterious nebula filled with cosmic debris and unknown resources.",
        "reward_skillpoints": 100
      },
      {
        "planet_id": 2,
        "planet_name": "Asteroid Belt",
        "planet_description": "A dense field of asteroids rich with minerals and rare resources.",
        "reward_skillpoints": 50
      }
    ]
    ```

---

### Explore a Planet  
**POST /explore/{planet_id}**  
- **Description**: Allows a user to explore a planet and receive skill points upon successful exploration.  
- **Request**:  
    ```json
    {
      "user_id": 1
    }
    ```  
- **Success (200 OK)**:  
    ```json
    {
      "message": "Exploration completed successfully!",
      "reward_skillpoints": 100
    }
    ```

---

### View Explored Planets for a User  
**GET /explore/{user_id}**  
- **Description**: Retrieves a list of planets that a user has already explored.  
- **Request**: None  
- **Success (200 OK)**:  
    ```json
    [
      {
        "planet_name": "Nebula-5",
        "exploration_date": "2025-01-04T12:30:00",
        "reward_skillpoints": 100
      },
      {
        "planet_name": "Asteroid Belt",
        "exploration_date": "2025-01-03T14:30:00",
        "reward_skillpoints": 50
      }
    ]
    ```

---

### Error Handling
- 400 (Bad Request): Missing `user_id`  
- 404 (Not Found): Planet or User not found  
- 409 (Conflict): Planet already explored  
- 500 (Internal Server Error): Server issues

## Guilds Endpoints

### 1. Create a Guild  
**POST /guilds**  
- **Description**: Allows users to create a new guild in GalacticExplorers.  
- **Request**:  
    ```json
    {
      "user_id": 1,
      "guild_name": "Galactic Warriors",
      "guild_description": "A guild of elite space explorers."
    }
    ```  
- **Success (201 Created)**:  
    ```json
    {
      "message": "Guild created successfully!",
      "guild_id": 1,
      "guild_name": "Galactic Warriors"
    }
    ```

---

### 2. Get All Guilds  
**GET /guilds**  
- **Description**: Allows users to view all available guilds in GalacticExplorers.  
- **Request**: None  
- **Success (200 OK)**:  
    ```json
    [
      {
        "guild_id": 1,
        "guild_name": "Galactic Warriors",
        "guild_description": "A guild of elite space explorers.",
        "member_count": 50,
        "total_skillpoints": 5000
      },
      {
        "guild_id": 2,
        "guild_name": "Space Rangers",
        "guild_description": "A guild for fearless adventurers.",
        "member_count": 30,
        "total_skillpoints": 3000
      }
    ]
    ```

---

### 3. Join a Guild  
**POST /guilds/join**  
- **Description**: Allows a user to join an existing guild by providing their `user_id` and `guild_id`.  
- **Request**:  
    ```json
    {
      "user_id": 1,
      "guild_id": 2
    }
    ```  
- **Success (200 OK)**:  
    ```json
    {
      "message": "Successfully joined the guild!"
    }
    ```

---

### 4. Leave a Guild  
**POST /guilds/leave**  
- **Description**: Allows a user to leave a guild they have joined by providing their `user_id` and the corresponding `guild_id`.  
- **Request**:  
    ```json
    {
      "user_id": 1,
      "guild_id": 2
    }
    ```  
- **Success (200 OK)**:  
    ```json
    {
      "message": "Successfully left the guild!"
    }
    ```

---

### 5. Get Members of a Guild  
**GET /guilds/{guild_id}**  
- **Description**: Fetches members of the guild identified by `guild_id`.  
- **Request**: None  
- **Success (200 OK)**:  
    ```json
    {
      "guild_id": 2,
      "guild_name": "Space Rangers",
      "members": [
        {
          "user_id": 1,
          "username": "space_hero",
          "skillpoints": 150
        },
        {
          "user_id": 2,
          "username": "galactic_warrior",
          "skillpoints": 200
        }
      ]
    }
    ```

---

### 6. Delete a Guild  
**DELETE /guilds**  
- **Description**: Allows the creator of a guild to delete their guild.  
- **Request**:  
    ```json
    {
      "user_id": 1,
      "guild_id": 1
    }
    ```  
- **Success (200 OK)**:  
    ```json
    {
      "message": "Guild deleted successfully!"
    }
    ```

---

### Error Handling  
- 400 (Bad Request): Missing `user_id`, `guild_id`, `guild_name`, or `guild_description`.  
- 404 (Not Found): Guild or User not found.  
- 409 (Conflict): User already belongs to a guild.  
- 403 (Forbidden): Only the guild creator can delete the guild.  
- 500 (Internal Server Error): Server issues.


## HTTP Status Codes Used (Error Handling)

The API uses appropriate HTTP status codes for error handling:

- **400 Bad Request**: Missing required data (e.g., missing user ID or challenge)
- **403 Forbidden**: Unauthorized actions (e.g., user trying to access restricted routes)
- **404 Not Found**: Resource not found (e.g., user or challenge not found)
- **409 Conflict**: Conflicting requests (e.g., trying to buy an item the user already owns)
