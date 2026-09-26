# Video Game REST API

A REST API server for managing video game data using **Python, Flask, and SQLite**. This project was created as part of the "Build Your Own API Server Challenge."

## Live API

The API is deployed on Render and can be accessed here:

**https://uy-apiserver-videogames.onrender.com/**

Example live endpoint:

```text
GET https://uy-apiserver-videogames.onrender.com/games
```

The live API was tested using `curl` and successfully returned the game data with a `200 OK` response.

## Features

* GET all games
* GET a single game by ID
* POST a new game
* PUT/update an existing game
* DELETE a game
* Basic request validation
* SQLite database
* RESTful HTTP status codes
* Deployed API available online through Render

## Technologies Used

* Python
* Flask
* SQLite
* Gunicorn
* Render
* Git/GitHub

## Database

The API uses a SQLite database named `games.db`.

Each game contains:

| Field        | Type    | Description                |
| ------------ | ------- | -------------------------- |
| id           | INTEGER | Unique game ID             |
| title        | TEXT    | Game title                 |
| genre        | TEXT    | Game genre                 |
| platform     | TEXT    | Game platform              |
| release_year | INTEGER | Year the game was released |
| developer    | TEXT    | Game developer             |

The database is automatically created and populated with 15 handcrafted video game records when the application starts.

## API Endpoints

### 1. GET `/games`

Returns the complete list of games.

**Method:**

```text
GET
```

**Local request:**

```text
http://127.0.0.1:5000/games
```

**Live request:**

```text
https://uy-apiserver-videogames.onrender.com/games
```

**Example response:**

```json
[
    {
        "id": 1,
        "title": "Minecraft",
        "genre": "Sandbox",
        "platform": "PC",
        "release_year": 2011,
        "developer": "Mojang Studios"
    }
]
```

**Status code:**

```text
200 OK
```

### 2. GET `/games/<id>`

Returns one game using its ID.

**Method:**

```text
GET
```

**Example request:**

```text
GET /games/1
```

**Example response:**

```json
{
    "id": 1,
    "title": "Minecraft",
    "genre": "Sandbox",
    "platform": "PC",
    "release_year": 2011,
    "developer": "Mojang Studios"
}
```

**Status code:**

```text
200 OK
```

If the game does not exist:

```json
{
    "error": "Game not found"
}
```

**Status code:**

```text
404 Not Found
```

### 3. POST `/games`

Creates a new game.

**Method:**

```text
POST
```

**Request body:**

```json
{
    "title": "Sea of Stars",
    "genre": "RPG",
    "platform": "PC",
    "release_year": 2023,
    "developer": "Sabotage Studio"
}
```

**Example response:**

```json
{
    "id": 16,
    "title": "Sea of Stars",
    "genre": "RPG",
    "platform": "PC",
    "release_year": 2023,
    "developer": "Sabotage Studio"
}
```

**Status code:**

```text
201 Created
```

If a required field is missing:

```json
{
    "error": "Missing required field: title"
}
```

**Status code:**

```text
400 Bad Request
```

### 4. PUT `/games/<id>`

Updates an existing game.

**Method:**

```text
PUT
```

**Example request:**

```text
PUT /games/16
```

**Request body:**

```json
{
    "title": "Sea of Stars",
    "genre": "Turn-Based RPG",
    "platform": "PC",
    "release_year": 2023,
    "developer": "Sabotage Studio"
}
```

**Example response:**

```json
{
    "id": 16,
    "title": "Sea of Stars",
    "genre": "Turn-Based RPG",
    "platform": "PC",
    "release_year": 2023,
    "developer": "Sabotage Studio"
}
```

**Status code:**

```text
200 OK
```

If the game does not exist:

```json
{
    "error": "Game not found"
}
```

**Status code:**

```text
404 Not Found
```

### 5. DELETE `/games/<id>`

Deletes an existing game.

**Method:**

```text
DELETE
```

**Example request:**

```text
DELETE /games/16
```

**Example response:**

```json
{
    "message": "Game deleted successfully"
}
```

**Status code:**

```text
200 OK
```

If the game does not exist:

```json
{
    "error": "Game not found"
}
```

**Status code:**

```text
404 Not Found
```

## HTTP Status Codes

| Status Code | Meaning                               |
| ----------- | ------------------------------------- |
| 200         | Successful request                    |
| 201         | Game successfully created             |
| 400         | Bad request or missing required field |
| 404         | Game not found                        |

## Running the API Locally

### 1. Clone the repository

```bash
git clone https://github.com/uy-johnryan/UY-APISERVER-VIDEOGAMES.git
cd UY-APISERVER-VIDEOGAMES
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
```

On Windows Command Prompt:

```bash
venv\Scripts\activate
```

### 3. Install the dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the Flask server

```bash
python app.py
```

The local API will be available at:

```text
http://127.0.0.1:5000
```

## Testing

The API was tested using `curl`.

Example:

```bash
curl -i http://127.0.0.1:5000/games
```

The deployed API was also tested using:

```bash
curl -i https://uy-apiserver-videogames.onrender.com/games
```

The live endpoint successfully returned a `200 OK` response with the game data.

The four required CRUD operations were tested:

* GET
* POST
* PUT
* DELETE

Validation and not-found responses were also tested.

## Project Structure

```text
UY-APISERVER-VIDEOGAMES/
│
├── app.py
├── README.md
├── requirements.txt
├── .gitignore
└── games.db
```

`games.db` is excluded from Git using `.gitignore` because the database is generated by the application.

## Deployment

The API is deployed using **Render**.

**Live URL:**

```text
https://uy-apiserver-videogames.onrender.com/
```

The application uses Gunicorn as the production server:

```text
gunicorn app:app
```

## GitHub Repository

```text
https://github.com/uy-johnryan/UY-APISERVER-VIDEOGAMES
```
