# 🎮 GameStore API

A REST API built with **ASP.NET Core 8**, following a **three-layer architecture** (Presentation (API) / Application / Infrastructure), for **game store management** (Games, Developers, Genres).

---

## Table of Contents

- [🎮 GameStore API](#-gamestore-api)
  - [Table of Contents](#table-of-contents)
  - [🧱 Architecture](#-architecture)
    - [🔄 Layer Coupling](#-layer-coupling)
  - [🎯 Features Overview](#-features-overview)
    - [🔹 1. Game Management](#-1-game-management)
      - [Available operations:](#available-operations)
    - [🔹 2. Developer Management](#-2-developer-management)
      - [Available operations:](#available-operations-1)
    - [🔹 3. Genre Management](#-3-genre-management)
      - [Available operations:](#available-operations-2)
    - [🔹 4. Search and Navigation](#-4-search-and-navigation)
      - [Example usage:](#example-usage)
    - [🔹 5. Authentication (out of scope)](#-5-authentication-out-of-scope)
  - [🧰 Technologies](#-technologies)
  - [⚙️ Installation](#️-installation)
  - [📡 API Endpoints (examples)](#-api-endpoints-examples)

---

## 🧱 Architecture

```
AppManagement/
├── Presentation (API)/   # API Layer: ASP.NET Core, Controllers, Swagger
├── Application/          # Entities, DTOs, Interfaces, Business Logic
├── Infrastructure/       # Data Access: EF Core, Repositories
└── AppManagement.sln         # Main Solution
```

### 🔄 Layer Coupling

* `Presentation (API)` depends on `Application` and `Infrastructure`
* `Infrastructure` depends on `Application`
* `Application` is independent (entities + business logic)

---

## 🎯 Features Overview

### 🔹 1. Game Management

The API allows you to manage a catalog of games.  
Each game has a **title**, a **description**, a **developer**, a **genre**, and a **release year**.

#### Available operations:
- **Create** a new game by specifying its title, description, developer, genre, and year.
- **List** all registered games.
- **Search** for a game by title or developer.
- **Update** the information of an existing game.
- **Delete** a game from the catalog.

### 🔹 2. Developer Management

Developers represent the creators of the games.  
Each developer has a **name**, a **biography**, and optionally a **country of origin**.

#### Available operations:
- **Add** a new developer.
- **List** all available developers.
- **List games linked to a given developer**.
- **Update** developer information.
- **Delete** a developer if they are not associated with any game.

### 🔹 3. Genre Management

Genres group together a set of games.  
Each genre has a **name** and a **description**.

#### Available operations:
- **Create** a genre.
- **List** all available genres.
- **View** the games of a given genre.
- **Update** genre information.
- **Delete** a genre (if not associated with any games).

### 🔹 4. Search and Navigation

The API allows searching for games, developers, or genres by various criteria:  
A **public search endpoint** is available to everyone, even unauthenticated users. This feature allows anyone to explore the game content without needing to log in.

A user can perform a keyword search (e.g., "mario") and get a list of results including:

- **Games** whose title contains the keyword,
- **Developers** whose name matches the search,
- **Genres** that match.

#### Example usage:

> The user enters a keyword in a search bar (like "adventure"). The API returns a list containing adventure games, developers, and the genre.

### 🔹 5. Authentication (out of scope)

The system is secured with **JWT (JSON Web Tokens)** authentication, already integrated upstream.  
Management routes are protected and accessible only to authorized users.

---

## 🧰 Technologies

| Component      | Technology               |
| -------------- | ------------------------ |
| Backend        | ASP.NET Core 8           |
| ORM            | Entity Framework Core 8  |
| Database       | SQL Server (or InMemory) |
| Authentication | JWT (handled upstream)   |

---

## ⚙️ Installation

1. Clone the project:

   - Open Visual Studio.
   - Go to **File > Clone Repository...** and enter:  
     `https://github.com/Build744/AppManagement.git`

2. Restore NuGet packages:

   - Right-click the solution in Solution Explorer and select **Restore NuGet Packages**.

3. Apply migrations (if using SQL Server):

   - Open the **Package Manager Console** (`Tools > NuGet Package Manager > Package Manager Console`).
   - Set Default project to `AppManagement.Infrastructure`
   - Run:
     ```
     Update-Database -Context ApplicationIdentityDbContext
     ```

4. Run the application:

   - Right-click the `AppManagement.Api` project and select **Set as Startup Project**.
   - Press **F5** or click **Start** to run.

5. Access Swagger:

   ```
   https://localhost:7155/swagger
   ```

---

## 📡 API Endpoints (examples)

| Method | Route             | Description        |
| ------ | ----------------- | ------------------|
| GET    | `/api/games`      | List all games    |
| POST   | `/api/games`      | Create a game     |
| PUT    | `/api/games/{id}` | Update a game     |
| DELETE | `/api/games/{id}` | Delete a game     |
| GET    | `/api/developers` | List all developers|
| GET    | `/api/genres`