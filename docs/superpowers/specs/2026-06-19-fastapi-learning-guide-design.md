# Design Specification: Interactive FastAPI Learning Guide (Learn_FastAPI_agy.html)

This specification defines the content structure, UI/UX design tokens, interactive components, and system diagrams for the single-file HTML interactive learning guide for FastAPI.

## 1. Meta Information
- **Title**: FastAPI & Project Book Management API: Comprehensive Guide from Scratch
- **Author**: AI Senior Engineer
- **Format**: Single-file self-contained HTML document (`Learn_FastAPI_agy.html`)
- **Design Tokens**: Claude Warm-Editorial Interface (`DESIGN-claude.md`)

## 2. Content Architecture

### Section 1: FastAPI Essentials & Overview
- **Introduction**: Definition, high performance, automatic interactive API documentation, rapid development, type safety.
- **Architectural base**: 
  - FastAPI = Starlette (Web capabilities) + Pydantic (Data validation) + Uvicorn (ASGI Server).
- **Comparison Table**: FastAPI vs Flask vs Django (performance, learning curve, database support, async processing).
- **Mermaid Diagram**: Basic architectural component interactions.

### Section 2: Environment Setup & Tooling
- **Python environments**: Setup using standard virtual environments (`venv`) and fast modern package manager (`uv`).
- **Dependencies**: Installation steps for core libraries:
  ```bash
  uv pip install fastapi uvicorn[standard] sqlalchemy alembic pydantic python-multipart
  ```

### Section 3: Core Concepts (Fundamentals to Advanced)
- **Hello World application**: Breakdown of a minimal file structure and launching command.
- **Routing**: Path parameters (`/books/{book_id}`) and Query parameters (`/books?author_id=1`).
- **Parameter Validation**: Custom validations using `Path`, `Query`, limit constraints (`gt`, `le`).
- **Pydantic Schemas**: Declaring request and response schemas, validation rules, automatic serialization.
- **Request Body & Response Model**: Declaring input validation models and filtering response attributes using `response_model`.
- **Dependency Injection (DI)**: Concept overview, sharing common utilities, managing database sessions via `Depends(get_db)`.

### Section 4: Book Management API Case Study Architecture
- **Directory Structure**: Layout of the sample codebase:
  - `app/core/config.py`: Configuration using Pydantic BaseSettings.
  - `app/db/session.py`: Database engine and SQLAlchemy session creation.
  - `app/db/base.py`: Declaring declarative base class for model collection.
  - `app/models/`: SQLAlchemy database models (`Author`, `Category`, `Book`).
  - `app/schemas/`: Pydantic input/output schemas.
  - `app/api/endpoints/`: Routing controllers for Authors, Categories, Books.
  - `app/api/deps.py`: Shared dependencies (`get_db`).
- **Entity Relationship Model (ERD)**: SQLAlchemy relationship maps:
  - Author (one) -> Book (many).
  - Category (one) -> Book (many).
- **Alembic Migrations**: Detailed workflow showing how SQLAlchemy models are translated into Alembic revision files and migrated to the SQLite database (`app.db`).

### Section 5: End-to-End Detailed Workflow Walkthrough (Down to function level)
- **Interactive Mermaid Pipeline**: Client request -> Uvicorn -> FastAPI App -> Middleware -> Router -> Dependency Injection (`get_db`) -> API Endpoint Handler -> SQLAlchemy Query -> Database -> Pydantic Schema Validation -> JSON response to Client.
- **Step-by-Step Breakdown**:
  - **Phase 1: Bootstrap**: Uvicorn server loads `app.main:app`, reads database URI, mounts static directories, registers APIRouters.
  - **Phase 2: Routing & Parsing**: Client request lands on a router. FastAPI automatically parses JSON inputs, URL queries, and parameters.
  - **Phase 3: Dependency Resolution**: Router invokes `get_db()`. A new database session `db: Session` is yielded to the route handler.
  - **Phase 4: Business Logic & CRUD Operations**: Detailed execution walkthrough of the following route functions:
    - `list_books`: Applying filters (author, category, publication year, keywords) using SQLAlchemy queries.
    - `create_book`: Validating foreign keys (Author/Category existence check) before creating database records.
    - `update_book`: Selectively updating fields while preserving existing data, validating new relationships.
    - `delete_book`: Standard deletion with proper response codes.
    - `upload_book_cover`: Multipart form upload handling. Focus on:
      - Validating MIME type (`image/jpeg`, `image/png`) and file suffix.
      - Enforcing a 2MB maximum file size.
      - Generating a secure unique filename with UUID4.
      - Storing the binary payload to `app/static/covers/` on disk.
      - Saving the static URL `/static/covers/<filename>` to the database Book record.
  - **Phase 5: Response Serialization & Resource Cleanup**: Pydantic serializes database models to JSON using `response_model`, Uvicorn returns the HTTP payload, and the `finally` block in `get_db()` runs `db.close()` to release the connection.

### Section 6: Advanced & Interview Topics
- CORS, Middleware, custom exception handlers, WebSockets, and production deployments (multiple workers, Nginx reverse proxy).

---

## 3. UI/UX Design Token Specifications (Claude-inspired Design)

### Colors
- **Canvas (Background)**: `#faf9f5` (Tinted warm cream)
- **Ink (Primary Text)**: `#141413` (Dark charcoal-black)
- **Primary / Accent (CTAs, links)**: `#cc785c` (Warm coral)
- **Primary Active**: `#a9583e`
- **Surface Card**: `#efe9de` (Slightly darker cream for panels)
- **Surface Dark**: `#181715` (Deep charcoal-navy for code blocks and code window mockups)
- **Surface Dark Soft**: `#1f1e1b` (Inner code block background)
- **Success State**: `#5db872` (Green indicators)
- **Error State**: `#c64545` (Red alerts)
- **Hairline Borders**: `#e6dfd8` (Soft cream-border)

### Typography (Google Fonts CDN)
- **Display Serif Font (h1, h2, h3)**: Cormorant Garamond (substitute for Copernicus)
  - Letter-spacing: `-0.02em`
  - Font-weight: `500` or `400` (Never bolded display titles)
- **Sans Serif Body Font (paragraphs, labels, UI)**: Inter (substitute for StyreneB)
- **Monospace Code Font (code elements)**: JetBrains Mono

### Shapes & Border Radii
- **Buttons / Inputs**: `8px` (`rounded.md`)
- **Content Cards / Code Windows**: `12px` (`rounded.lg`)
- **Pills / Badges**: `9999px` (`rounded.pill`)

---

## 4. Technical Specifications & Interactions

### Single Page Application Sidebar
- A multi-level table of contents is placed in a fixed-width left sidebar (`280px`).
- **Scrollspy**: Vanilla JavaScript monitors heading locations via `IntersectionObserver` and applies an `.active` class (bold coral text) to the corresponding link.
- **Search Bar**: A dynamic input field searches all section titles and paragraphs, hiding non-matching sections and highlighting search results.

### Code Block Interactive Features
- **Prism.js / Highlight.js**: Syntax highlighting with a customized dark navy theme (`surface-dark`).
- **Copy Button**: A button at the top-right of each block triggers `navigator.clipboard.writeText()` and displays a transient "Copied!" notification.
- **Line Explanation Tooltips**: Users can hover over specific lines or comments inside the code windows to trigger a clean HTML tooltip explaining that specific instruction (e.g., explaining `Depends(get_db)` dynamic injection).

### Diagram rendering
- **Mermaid.js CDN**: Loaded asynchronously.
- **Custom Styling**: Customized themes map Mermaid entities to CSS variables matching the main palette:
  - Actor/Node backgrounds: `#efe9de` (Surface Card)
  - Border stroke: `#cc785c` (Coral)
  - Database nodes: `#181715` with `#faf9f5` text
  - Active workflows: Highlighted in solid coral.
