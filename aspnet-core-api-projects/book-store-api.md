# 📚 BookStore API

A REST API built with **ASP.NET Core 8**, following a **three-layer architecture** (Presentation (API) / Application / Infrastructure), for **book store management** (Books, Authors, Categories).

---

## Table of Contents

- [📚 BookStore API](#-bookstore-api)
  - [Table of Contents](#table-of-contents)
  - [🧱 Architecture](#-architecture)
    - [🔄 Layer Coupling](#-layer-coupling)
  - [🎯 Features Overview](#-features-overview)
    - [🔹 1. Book Management](#-1-book-management)
      - [Available operations:](#available-operations)
    - [🔹 2. Author Management](#-2-author-management)
      - [Available operations:](#available-operations-1)
    - [🔹 3. Category Management](#-3-category-management)
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

### 🔹 1. Book Management

The API allows you to manage a catalog of books.  
Each book has a **title**, a **summary**, an **author**, a **category**, and a **publication year**.

#### Available operations:
- **Create** a new book by specifying its title, summary, author, category, and year.
- **List** all registered books.
- **Search** for a book by title or author.
- **Update** the information of an existing book.
- **Delete** a book from the catalog.

### 🔹 2. Author Management

Authors represent the creators of the books.  
Each author has a **name**, a **biography**, and optionally a **country of origin**.

#### Available operations:
- **Add** a new author.
- **List** all available authors.
- **List books linked to a given author**.
- **Update** author information.
- **Delete** an author if they are not associated with any book.

### 🔹 3. Category Management

Categories group together a set of books.  
Each category has a **name** and a **description**.

#### Available operations:
- **Create** a category.
- **List** all available categories.
- **View** the books of a given category.
- **Update** category information.
- **Delete** a category (if not associated with any books).

### 🔹 4. Search and Navigation

The API allows searching for books, authors, or categories by various criteria:  
A **public search endpoint** is available to everyone, even unauthenticated users. This feature allows anyone to explore the book content without needing to log in.

A user can perform a keyword search (e.g., "tolkien") and get a list of results including:

- **Books** whose title contains the keyword,
- **Authors** whose name matches the search,
- **Categories** that match.

#### Example usage:

> The user enters a keyword in a search bar (like "fantasy"). The API returns a list containing fantasy books, authors, and the category.

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
| GET    | `/api/books`      | List all books   |
| POST   | `/api/books`      | Create a book    |
| PUT    | `/api/books/{id}` | Update a book    |
| DELETE | `/api/books/{id}` | Delete a book    |
| GET    | `/api/authors`    | List all authors |
| GET    | `/api/categories` | List             |