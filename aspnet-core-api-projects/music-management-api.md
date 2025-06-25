# 🎵 MusicManagement API

A REST API built with **ASP.NET Core 8**, following a **three-layer architecture** (Presentation / Application / Infrastructure), for **music management** (Songs, Artists, Albums).

---

## Table of Contents

- [🎵 MusicManagement API](#-musicmanagement-api)
  - [Table of Contents](#table-of-contents)
  - [🧱 Architecture](#-architecture)
    - [🔄 Layer Coupling](#-layer-coupling)
  - [🎯 Features Overview](#-features-overview)
    - [🔹 1. Song Management](#-1-song-management)
      - [Available operations:](#available-operations)
    - [🔹 2. Artist Management](#-2-artist-management)
      - [Available operations:](#available-operations-1)
    - [🔹 3. Album Management](#-3-album-management)
      - [Available operations :](#available-operations-)
    - [🔹 4. Search and Navigation](#-4-search-and-navigation)
      - [Example usage :](#example-usage-)
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
└── AppManagement.sln     # Main
```

### 🔄 Layer Coupling

* `Presentation (API)` depends on `Application` and `Infrastructure`
* `Infrastructure` depends on `Application`
* `Application` is independent (entities + business logic)

---

## 🎯 Features Overview

### 🔹 1. Song Management

The API allows you to manage a catalog of songs.  
Each song has a **title**, a **duration**, one or more **artists**, and an associated **album** if applicable.

#### Available operations:
- **Create** a new song by specifying its title, duration, artist, and album.
- **List** all registered songs.
- **Search** for a song by title or artist.
- **Update** the information of an existing song.
- **Delete** a song from the catalog.


### 🔹 2. Artist Management

Artists represent the creators of the songs.  
Each artist has a **name**, a **country of origin**, and optionally a **biography**.

#### Available operations:
- **Add** a new artist.
- **List** all available artists.
- **List songs linked to a given artist**.
- **Update** artist information.
- **Delete** an artist if they are not associated with any song.

### 🔹 3. Album Management

Albums group together a set of songs.  
Each album has a **title**, a **release year**, and can contain multiple songs.

#### Available operations :

- **Create** an album with a title and year.
- **List** all available albums.
- **View** the songs of a given album.
- **Update** album information.
- **Delete** an album (if not associated with any songs).

### 🔹 4. Search and Navigation

The API allows searching for songs, albums, or artists by various criteria:  
A **public search endpoint** is available to everyone, even unauthenticated users. This feature allows anyone to explore the music content without needing to log in.

A user can perform a keyword search (e.g., "beatles") and get a list of results including:

- **Songs** whose title contains the keyword,
- **Albums** that match,
- **Artists** whose name matches the search.

#### Example usage :

> The user enters a keyword in a search bar (like "queen"). The API returns a list containing Queen's songs, albums, and the artist name.

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

| Method | Route             | Description      |
| ------ | ----------------- | ---------------- |
| GET    | `/api/songs`      | List all songs   |
| POST   | `/api/songs`      | Create a song    |
| PUT    | `/api/songs/{id}` | Update a song    |
| DELETE | `/api/songs/{id}` | Delete a song    |
| GET    | `/api/albums`     | List all albums  |
| GET    | `/api/artists`    | List all artists |
