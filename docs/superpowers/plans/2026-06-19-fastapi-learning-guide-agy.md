# FastAPI Interactive Learning Guide Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a comprehensive, highly interactive, and beautiful self-contained HTML learning guide for FastAPI based on the course materials and tutorial documents, adhering strictly to the Claude editorial design system.

**Architecture:** A single-file HTML page containing an editorial-style dashboard. The left column features a navigation sidebar with client-side search and automatic scrollspy tracking, while the right column houses structured markdown-like content, syntax-highlighted code windows with line explanations, and responsive custom-themed Mermaid.js flowcharts representing system pipelines.

**Tech Stack:** HTML5, Vanilla CSS3 (Claude design tokens), Vanilla JavaScript (ES6+), Mermaid.js CDN (v10+), Prism.js CDN (v1.29.0)

---

### Task 1: Setup HTML Skeleton and Layout Shell

**Files:**
- Create: `G:/AIProduction_t6_2026/production/tai_lieu/Learn_FastAPI/Learn_FastAPI_agy.html`

- [ ] **Step 1: Write HTML base structures and asset inclusions**
  Create the core HTML layout, referencing fonts (Cormorant Garamond, Inter, JetBrains Mono) and libraries (Prism.js CSS/JS, Mermaid.js JS) via CDN.
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>FastAPI & Project Book Management API: Comprehensive Guide</title>
      <!-- Google Fonts CDN -->
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
      <!-- Prism.js Code Highlight Theme CDN -->
      <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css" rel="stylesheet" />
      <style>
          /* CSS styling tokens based on DESIGN-claude.md */
          :root {
              --canvas-bg: #faf9f5;
              --ink-primary: #141413;
              --ink-body: #3d3d3a;
              --ink-body-strong: #252523;
              --primary-coral: #cc785c;
              --primary-coral-active: #a9583e;
              --surface-card: #efe9de;
              --surface-dark: #181715;
              --surface-dark-soft: #1f1e1b;
              --border-hairline: #e6dfd8;
              --font-serif: 'Cormorant Garamond', Garamond, 'Times New Roman', serif;
              --font-sans: 'Inter', -apple-system, sans-serif;
              --font-mono: 'JetBrains Mono', monospace;
          }
          * { box-sizing: border-box; margin: 0; padding: 0; }
          body {
              background-color: var(--canvas-bg);
              color: var(--ink-body);
              font-family: var(--font-sans);
              display: flex;
              height: 100vh;
              overflow: hidden;
          }
          /* Shell Grid Layout */
          #app-layout {
              display: flex;
              width: 100%;
              height: 100%;
          }
          #sidebar {
              width: 300px;
              background-color: var(--surface-card);
              border-right: 1px solid var(--border-hairline);
              display: flex;
              flex-direction: column;
              height: 100%;
          }
          #main-content {
              flex: 1;
              overflow-y: auto;
              padding: 48px;
              scroll-behavior: smooth;
          }
      </style>
  </head>
  <body>
      <div id="app-layout">
          <aside id="sidebar">
              <!-- Sidebar content goes here -->
          </aside>
          <main id="main-content">
              <!-- Main content goes here -->
          </main>
      </div>
      <!-- Prism.js CDN -->
      <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/components/prism-core.min.js"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/plugins/autoloader/prism-autoloader.min.js"></script>
      <!-- Mermaid.js CDN -->
      <script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.9.1/mermaid.min.js"></script>
      <script>
          mermaid.initialize({
              startOnLoad: true,
              theme: 'base',
              themeVariables: {
                  primaryColor: '#efe9de',
                  primaryTextColor: '#141413',
                  primaryBorderColor: '#cc785c',
                  lineColor: '#cc785c',
                  secondaryColor: '#181715',
                  tertiaryColor: '#faf9f5'
              }
          });
      </script>
  </body>
  </html>
  ```

- [ ] **Step 2: Commit base setup**
  Verify the basic empty shell page renders properly in a browser.
  ```bash
  git add Learn_FastAPI_agy.html
  git commit -m "docs: setup HTML skeleton with Claude tokens and CDNs"
  ```

---

### Task 2: Create Left Sidebar with Search and Scrollspy

**Files:**
- Modify: `G:/AIProduction_t6_2026/production/tai_lieu/Learn_FastAPI/Learn_FastAPI_agy.html`

- [ ] **Step 1: Write sidebar template**
  Insert search input, logo header with the Anthropic spike symbol (+ "Antigravity Guide"), and navigation menu lists.
  ```html
  <div class="sidebar-header" style="padding: 24px; border-bottom: 1px solid var(--border-hairline);">
      <div style="display: flex; align-items: center; gap: 8px;">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="var(--primary-coral)">
              <!-- Anthropic 4-spoke spike mark representation -->
              <path d="M12 2v20M2 12h20M5 5l14 14M5 19L19 5" stroke="var(--primary-coral)" stroke-width="2.5" stroke-linecap="round"/>
          </svg>
          <span style="font-family: var(--font-serif); font-size: 20px; font-weight: 500; color: var(--ink-primary);">Antigravity FastAPI</span>
      </div>
      <input type="text" id="search-input" placeholder="Search topics..." style="width: 100%; margin-top: 16px; padding: 10px; border-radius: 8px; border: 1px solid var(--border-hairline); background-color: var(--canvas-bg); color: var(--ink-primary); font-family: var(--font-sans); outline: none;">
  </div>
  <nav class="sidebar-nav" style="flex: 1; overflow-y: auto; padding: 24px;">
      <ul style="list-style: none;" id="nav-list">
          <!-- Dynamic navigation items will match main content headings -->
      </ul>
  </nav>
  ```

- [ ] **Step 2: Implement Scrollspy and Search logic**
  Add scripts to dynamically generate menu items from `section[id]`, track section active states, and perform dynamic text search filters.
  ```javascript
  document.addEventListener('DOMContentLoaded', () => {
      const sections = document.querySelectorAll('section[id]');
      const navList = document.getElementById('nav-list');
      
      // Populate nav items
      sections.forEach(sec => {
          const title = sec.querySelector('h2, h3').innerText;
          const li = document.createElement('li');
          li.style.marginBottom = '12px';
          const a = document.createElement('a');
          a.href = `#${sec.id}`;
          a.innerText = title;
          a.style.textDecoration = 'none';
          a.style.color = 'var(--ink-body)';
          a.style.fontSize = '14px';
          a.style.transition = 'color 0.2s';
          a.classList.add('nav-link');
          a.setAttribute('data-sec', sec.id);
          li.appendChild(a);
          navList.appendChild(li);
      });

      // Scrollspy logic
      const observerOptions = {
          root: document.getElementById('main-content'),
          threshold: 0.2,
          rootMargin: "0px 0px -50% 0px"
      };
      const observer = new IntersectionObserver((entries) => {
          entries.forEach(entry => {
              if (entry.isIntersecting) {
                  document.querySelectorAll('.nav-link').forEach(a => {
                      a.style.color = 'var(--ink-body)';
                      a.style.fontWeight = '400';
                  });
                  const activeA = document.querySelector(`.nav-link[data-sec="${entry.target.id}"]`);
                  if (activeA) {
                      activeA.style.color = 'var(--primary-coral)';
                      activeA.style.fontWeight = '600';
                  }
              }
          });
      }, observerOptions);
      sections.forEach(sec => observer.observe(sec));

      // Live search logic
      const searchInput = document.getElementById('search-input');
      searchInput.addEventListener('input', (e) => {
          const query = e.target.value.toLowerCase();
          sections.forEach(sec => {
              const text = sec.innerText.toLowerCase();
              if (text.includes(query)) {
                  sec.style.display = 'block';
              } else {
                  sec.style.display = 'none';
              }
          });
      });
  });
  ```

- [ ] **Step 3: Commit UI controls**
  Ensure scrollspy and search logic functions properly.
  ```bash
  git commit -am "feat: implement dynamic sidebar navigation, scrollspy, and client-side search"
  ```

---

### Task 3: Write Part 1 (Essentials), Part 2 (Setup), and Part 3 (Core Concepts)

**Files:**
- Modify: `G:/AIProduction_t6_2026/production/tai_lieu/Learn_FastAPI/Learn_FastAPI_agy.html`

- [ ] **Step 1: Write HTML contents for introductory chapters**
  Populate the `main-content` area with Section 1 (FastAPI Overview + comparison), Section 2 (Setup using `uv` and `pip`), and Section 3 (Path, Query parameters, validation, and Pydantic schemas). Include custom Code Windows.
  ```html
  <!-- Code window card style -->
  <div class="code-window-card" style="background-color: var(--surface-dark); border-radius: 12px; padding: 24px; color: var(--canvas-bg); font-family: var(--font-mono); margin-bottom: 24px; position: relative;">
      <div style="display: flex; gap: 6px; margin-bottom: 12px;">
          <span style="width: 10px; height: 10px; background-color: #ff5f56; border-radius: 50%;"></span>
          <span style="width: 10px; height: 10px; background-color: #ffbd2e; border-radius: 50%;"></span>
          <span style="width: 10px; height: 10px; background-color: #27c93f; border-radius: 50%;"></span>
      </div>
      <button class="copy-btn" style="position: absolute; right: 24px; top: 20px; background: none; border: 1px solid var(--border-hairline); color: var(--canvas-bg); padding: 4px 8px; border-radius: 4px; cursor: pointer; font-size: 12px;">Copy</button>
      <pre><code class="language-python">
  from fastapi import FastAPI, Path, Query
  
  app = FastAPI()
  
  @app.get("/items/{item_id}")
  def read_item(
      item_id: int = Path(..., description="The ID of the item", gt=0),
      q: str | None = Query(None, max_length=50)
  ):
      return {"item_id": item_id, "q": q}
      </code></pre>
  </div>
  ```

- [ ] **Step 2: Implement Copy Code functionality**
  Inject a dynamic utility handler for copy buttons.
  ```javascript
  document.querySelectorAll('.copy-btn').forEach(btn => {
      btn.addEventListener('click', (e) => {
          const code = btn.nextElementSibling.querySelector('code').innerText;
          navigator.clipboard.writeText(code).then(() => {
              btn.innerText = 'Copied!';
              setTimeout(() => { btn.innerText = 'Copy'; }, 2000);
          });
      });
  });
  ```

- [ ] **Step 3: Commit core chapters**
  Review the structure and typography.
  ```bash
  git commit -am "feat: add FastAPI overview, setup, path/query parameter validation content with code blocks"
  ```

---

### Task 4: Write Part 4 (Project Case Study) and Part 5 (End-to-End Walkthrough)

**Files:**
- Modify: `G:/AIProduction_t6_2026/production/tai_lieu/Learn_FastAPI/Learn_FastAPI_agy.html`

- [ ] **Step 1: Write detailed Case Study structure & Alembic walkthrough**
  Add structural specifications and migration workflow. Define Mermaid charts:
  ```mermaid
  graph TD
      A[SQLAlchemy Model: Book] -->|Defines Schema| B(Base.metadata)
      B -->|Read by| C[Alembic Environment]
      D[SQLite Database: app.db] -->|Current Schema| C
      C -->|Compare & Autogenerate| E[Migration Script: Revision]
      E -->|Upgrade Head| D
  ```

- [ ] **Step 2: Add End-to-End Pipeline diagrams and function-level textual descriptions**
  Write down-to-function explanations of the pipeline. Define a full Mermaid request pipeline representing routing, validation, dependency Injection, database transaction, and serialization.
  ```mermaid
  sequenceDiagram
      autonumber
      actor Client
      participant App as FastAPI Application
      participant Router as APIRouter (books)
      participant Dep as Dependency (get_db)
      participant Handler as Route Handler (upload_book_cover)
      participant DB as SQLite DB (SQLAlchemy)
      
      Client->>App: POST /books/1/cover (Multipart form + File)
      App->>Router: Match URL route & check HTTP method
      Router->>Dep: Resolve Depends(get_db)
      activate Dep
      Note over Dep: Create db = SessionLocal()
      Dep-->>Handler: Inject db session
      deactivate Dep
      activate Handler
      Note over Handler: Check file type (JPEG/PNG) & size (<2MB)<br/>Generate unique UUID filename<br/>Write file to app/static/covers/<br/>Update DB cover_image URL
      Handler->>DB: db.commit() & db.refresh()
      DB-->>Handler: Return updated Book object
      Handler-->>Client: Return serialized JSON (200 OK)
      deactivate Handler
      Note over Dep: finally: db.close() runs
  ```

- [ ] **Step 3: Commit walkthrough**
  Validate execution and pipeline descriptions.
  ```bash
  git commit -am "feat: add case study details, Alembic workflows, and end-to-end request-response pipeline descriptions with diagrams"
  ```

---

### Task 5: Add Line Explanations, Advanced Chapters, and CSS Styling Polish

**Files:**
- Modify: `G:/AIProduction_t6_2026/production/tai_lieu/Learn_FastAPI/Learn_FastAPI_agy.html`

- [ ] **Step 1: Implement Interactive Line Explanations**
  Add JavaScript tooltip functionality for interactive code annotations. Hovering over lines containing `data-tip` will show an editorial overlay.
  ```html
  <span class="code-line" data-tip="Injects database session automatically using FastAPI dependency mechanism.">db: Session = Depends(get_db)</span>
  ```
  Add corresponding styles and mouse event handlers:
  ```javascript
  const tooltip = document.createElement('div');
  tooltip.style.position = 'absolute';
  tooltip.style.background = 'var(--surface-card)';
  tooltip.style.color = 'var(--ink-primary)';
  tooltip.style.padding = '8px 12px';
  tooltip.style.borderRadius = '4px';
  tooltip.style.border = '1px solid var(--primary-coral)';
  tooltip.style.fontSize = '12px';
  tooltip.style.display = 'none';
  tooltip.style.pointerEvents = 'none';
  tooltip.style.zIndex = '1000';
  document.body.appendChild(tooltip);

  document.querySelectorAll('[data-tip]').forEach(el => {
      el.style.borderBottom = '1px dotted var(--primary-coral)';
      el.style.cursor = 'help';
      el.addEventListener('mouseenter', (e) => {
          tooltip.innerText = el.getAttribute('data-tip');
          tooltip.style.display = 'block';
      });
      el.addEventListener('mousemove', (e) => {
          tooltip.style.left = (e.pageX + 10) + 'px';
          tooltip.style.top = (e.pageY + 10) + 'px';
      });
      el.addEventListener('mouseleave', () => {
          tooltip.style.display = 'none';
      });
  });
  ```

- [ ] **Step 2: Add Advanced topics, Deployment setups, and visual polishing**
  Provide Nginx proxy block templates, CORS configuration models, and responsive stylesheet breakpoints to support mobile readability.

- [ ] **Step 3: Final validation and Commit**
  Perform self-review check on formatting.
  ```bash
  git commit -am "feat: finish line explanation tooltips, advanced production configuration, and responsive polish"
  ```
