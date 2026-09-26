# Video Game REST API

A REST API server built with Python, Flask, and SQLite for managing video game information.

## Technologies Used

* Python 3
* Flask
* SQLite
* curl

## Database

The API uses a SQLite database named `games.db`.

The `games` table contains the following fields:

| Field          | Type    | Description                |
| -------------- | ------- | -------------------------- |
| `id`           | INTEGER | Unique game ID             |
| `title`        | TEXT    | Name of the video game     |
| `genre`        | TEXT    | Game genre                 |
| `platform`     | TEXT    | Platform of the game       |
| `release_year` | INTEGER | Year the game was released |
| `developer`    | TEXT    | Game developer             |

The database is initially populated with 15 manually created video game records.

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/uy-johnryan/UY-APISERVER-VIDEOGAMES.git
cd UY-APISERVER-VIDEOGAMES
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

### 3. Activate the virtual environment

On Windows Command Prompt:

```cmd
venv\Scripts\activate.bat
```

### 4. Install the required packages

```bash
pip install -r requirements.txt
```

### 5. Start the Flask server

```bash
python app.py
```

The API will run at:

```text
http://127.0.0.1:5000
```

---

# API Endpoints

## 1. GET /games

Returns the complete list of video games.

### Request

```bash
curl http://127.0.0.1:5000/games
```

### Successful Response

**Status:** `200 OK`

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

The actual response contains all available games.

---

## 2. GET /games/<id>

Returns a single video game using its ID.

### Request

```bash
curl http://127.0.0.1:5000/games/1
```

### Successful Response

**Status:** `200 OK`

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

### Game Not Found

**Status:** `404 Not Found`

```json
{
  "error": "Game not found"
}
```

---

## 3. POST /games

Creates a new video game.

### Request

```bash
curl -X POST http://127.0.0.1:5000/games -H "Content-Type: application/json" -d "{\"title\":\"Sea of Stars\",\"genre\":\"RPG\",\"platform\":\"PC\",\"release_year\":2023,\"developer\":\"Sabotage Studio\"}"
```

### Successful Response

**Status:** `201 Created`

```json
{
  "id": 18,
  "title": "Sea of Stars",
  "genre": "RPG",
  "platform": "PC",
  "release_year": 2023,
  "developer": "Sabotage Studio"
}
```

The ID may be different depending on the current database contents.

### Missing Required Field

**Status:** `400 Bad Request`

Example:

```json
{
  "error": "Missing required field: platform"
}
```

Required fields:

* `title`
* `genre`
* `platform`
* `release_year`
* `developer`

---

## 4. PUT /games/<id>

Updates an existing video game.

### Request

```bash
curl -X PUT http://127.0.0.1:5000/games/18 -H "Content-Type: application/json" -d "{\"title\":\"Sea of Stars\",\"genre\":\"Turn-Based RPG\",\"platform\":\"PC\",\"release_year\":2023,\"developer\":\"Sabotage Studio\"}"
```

### Successful Response

**Status:** `200 OK`

```json
{
  "id": 18,
  "title": "Sea of Stars",
  "genre": "Turn-Based RPG",
  "platform": "PC",
  "release_year": 2023,
  "developer": "Sabotage Studio"
}
```

### Missing Required Field

**Status:** `400 Bad Request`

```json
{
  "error": "Missing required field: platform"
}
```

### Game Not Found

**Status:** `404 Not Found`

```json
{
  "error": "Game not found"
}
```

---

## 5. DELETE /games/<id>

Deletes an existing video game.

### Request

```bash
curl -X DELETE http://127.0.0.1:5000/games/18
```

### Successful Response

**Status:** `200 OK`

```json
{
  "message": "Game deleted successfully"
}
```

### Game Not Found

**Status:** `404 Not Found`

```json
{
  "error": "Game not found"
}
```

---

# HTTP Status Codes

| Status Code       | Meaning                                              |
| ----------------- | ---------------------------------------------------- |
| `200 OK`          | Successful GET, PUT, or DELETE                       |
| `201 Created`     | Successfully created a new game                      |
| `400 Bad Request` | Required field is missing or request data is invalid |
| `404 Not Found`   | The requested game does not exist                    |

# Project Structure

```text
UY-APISERVER-VIDEOGAMES/
│
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
└── venv/
```

The `venv/` directory and `games.db` are excluded from Git using `.gitignore`.

# Testing

All CRUD operations were tested locally using curl:

* GET
* POST
* PUT
* DELETE

The API was tested using the local Flask server at:

```text
http://127.0.0.1:5000
```
