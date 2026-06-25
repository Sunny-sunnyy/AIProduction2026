# FastAPI Beginner-to-Production HTML Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a detailed, visually polished HTML handbook about FastAPI that teaches a beginner from zero through production backend practices and AI/LLM/RAG use cases, strictly following the specification.

**Architecture:** The work is content-first, source-grounded, and section-driven. Build a source map first, then a chapter map, then a mandatory code inventory, then the HTML skeleton, and only then write the chapters into the final handbook. Verification must check both content completeness and teaching quality.

**Tech Stack:** HTML, CSS, optional lightweight JavaScript, code blocks, internal navigation, Mermaid only if genuinely useful and render-safe, source-grounded content from official FastAPI docs plus the two supplied PDFs.

---

## 1. Execution Contract

- The downstream agent must read `fastapi_html_spec.md` completely before writing the HTML.
- The downstream agent must review `G:\harness_template\DESIGN-claude.md` before making layout or styling decisions.
- The downstream agent must treat official FastAPI docs as the primary source of truth.
- The downstream agent must not start by writing a pretty shell and filling content later.
- The downstream agent must not leave placeholders such as `TODO`, `TBD`, `write more here`, or `insert diagram later`.
- The downstream agent must preserve Vietnamese teaching prose and English technical identifiers.

## 2. Input Files

**Required inputs**

- `G:\AIProduction_t6_2026\production\tai_lieu\Learn_FastAPI2\fastapi_html_spec.md`
- `G:\harness_template\DESIGN-claude.md`
- `G:\Agent2026Win\Tai_lieu_on_tap_pv\TaiLieu_AI_Advanced\Fast_API.pdf`
- `G:\Agent2026Win\Tai_lieu_on_tap_pv\TaiLieu_AI_Advanced\FAST API gg.pdf`
- Official FastAPI docs:
  - `https://fastapi.tiangolo.com/tutorial/`
  - `https://fastapi.tiangolo.com/advanced/`
  - `https://fastapi.tiangolo.com/deployment/`
- Supporting article:
  - `https://viblo.asia/p/huong-dan-co-ban-framework-fastapi-tu-a-z-phan-1-V3m5W0oyKO7`

**Source priority**

1. Official FastAPI docs
2. `Fast_API.pdf`
3. `FAST API gg.pdf`
4. Viblo and lightweight web research

## 3. Output Files

**Required output**

- Main HTML handbook in `G:\AIProduction_t6_2026\production\tai_lieu\Learn_FastAPI2`

**Recommended default filename**

- `fastapi_complete_handbook.html`

**Optional outputs only if justified**

- One CSS file if self-contained HTML becomes unreasonably large
- One JS file if navigation or interactions genuinely need separation

If optional files are created, they must be named clearly and referenced relative to the HTML file.

## 4. File Responsibility Map

- `fastapi_html_spec.md`
  - the source contract for scope, content, teaching rules, and quality gates
- `DESIGN-claude.md`
  - visual direction and design language
- Final HTML
  - the learner-facing artifact
- Optional CSS
  - visual rules only
- Optional JS
  - navigation and interaction only

## 5. Implementation Strategy

The downstream agent must implement in this order:

1. lock the source map
2. lock the chapter map
3. lock the code inventory
4. build the visual skeleton
5. write foundational chapters
6. write feature chapters
7. write production chapters
8. write AI/LLM/RAG chapters
9. polish teaching quality
10. audit completeness

Do not reverse this order.

## 6. Mandatory Coverage Matrix

Before writing the HTML, create and verify a private working checklist that maps:

- each chapter
- its primary source
- required code examples
- required callouts
- required production note
- required AI note when relevant

The downstream agent must not proceed until every chapter from the spec has at least one mapped source and one mapped teaching outcome.

## 7. Mandatory Code Coverage Matrix

Before writing chapter prose, build a private inventory of code artifacts:

- `C01` hello world app
- `C02` GET and POST basics
- `C03` path params
- `C04` query params
- `C05` request body
- `C06` nested Pydantic models
- `C07` response models
- `C08` error handling
- `C09` custom exception handler
- `C10` header and cookie usage
- `C11` form and file upload
- `C12` basic dependency injection
- `C13` `yield` dependency
- `C14` `APIRouter` multi-file structure
- `C15` DB session management
- `C16` CRUD routes
- `C17` Alembic migration flow
- `C18` password hashing
- `C19` JWT auth flow
- `C20` protected route
- `C21` middleware
- `C22` CORS setup
- `C23` lifespan setup
- `C24` background tasks
- `C25` `StreamingResponse`
- `C26` SSE endpoint
- `C27` WebSocket endpoint
- `C28` `TestClient`
- `C29` dependency override tests
- `C30` async test
- `C31` settings/env config
- `C32` health endpoints
- `C33` Dockerfile
- `C34` worker command
- `C35` LLM proxy endpoint
- `C36` token streaming AI endpoint
- `C37` embeddings endpoint
- `C38` RAG query endpoint

Each code artifact must be assigned to at least one chapter and one mini-project or standalone teaching example.

## 8. Phase Plan

### Task 1: Read and normalize requirements

**Files:**
- Read: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_FastAPI2\fastapi_html_spec.md`
- Read: `G:\harness_template\DESIGN-claude.md`
- Read: official docs and source PDFs

- [ ] **Step 1: Read the full specification and extract all hard requirements**

Create a working checklist that includes:

```text
- all required chapters
- all required code artifacts
- all required callout types
- all required production topics
- all required AI/LLM/RAG topics
```

- [ ] **Step 2: Read the design guide and capture the visual language**

Capture these visual anchors:

```text
- cream canvas
- coral accent
- dark code surfaces
- serif display headings
- humanist sans body text
- editorial spacing
```

- [ ] **Step 3: Normalize source priority**

Write a private note similar to:

```text
If official docs and PDFs disagree, trust official docs.
If PDFs are older, preserve their teaching value but modernize commands and practices.
```

- [ ] **Step 4: Verify readiness to continue**

Expected result:

```text
You can point to a requirement source for every major chapter before writing HTML.
```

### Task 2: Build the chapter map

**Files:**
- Create or update: private working notes
- Will drive: final HTML

- [ ] **Step 1: Create the final chapter order**

Use this order:

```text
1. FastAPI overview
2. HTTP and REST basics
3. ASGI/WSGI/Uvicorn/async
4. setup and first app
5. basic endpoints
6. params and bodies
7. Pydantic validation
8. response models
9. error handling
10. headers/cookies/forms/files
11. dependency injection
12. bigger applications
13. database foundations
14. CRUD app
15. Alembic migrations
16. security fundamentals
17. OAuth2/JWT
18. middleware and CORS
19. lifespan
20. background tasks/streaming/SSE/WebSockets
21. testing
22. debugging
23. settings/env
24. observability
25. deployment and Docker
26. scaling
27. AI/LLM/RAG
28. mini projects
29. common mistakes
30. best practices and roadmap
```

- [ ] **Step 2: Map each chapter to source priority**

Expected working output:

```text
Chapter -> official docs section -> PDF support -> optional supporting note
```

- [ ] **Step 3: Verify the learner progression**

Expected result:

```text
No advanced concept appears before its prerequisites are explained.
```

### Task 3: Build the code inventory and teaching placement

**Files:**
- Create or update: private working notes

- [ ] **Step 1: Assign every mandatory code artifact to a chapter**

Expected structure:

```text
Code ID -> Chapter -> Purpose -> Needs VN comments? yes
```

- [ ] **Step 2: Assign every major code artifact to one of the four mini projects**

Use this model:

```text
Project A -> basics
Project B -> CRUD + DB
Project C -> auth + production backend
Project D -> AI/LLM/RAG service
```

- [ ] **Step 3: Verify no major topic is theory-only**

Expected result:

```text
Security, DB, testing, deployment, and AI sections all have real code, not only prose.
```

### Task 4: Build the HTML structure skeleton

**Files:**
- Create: main HTML file
- Optional: CSS/JS files if justified

- [ ] **Step 1: Create the top-level HTML sections**

The skeleton must include:

```html
<header>...</header>
<nav class="toc">...</nav>
<main>
  <section id="hero">...</section>
  <section id="part-a">...</section>
  <section id="part-b">...</section>
  <section id="part-c">...</section>
  <section id="part-d">...</section>
  <section id="part-e">...</section>
  <section id="part-f">...</section>
  <section id="part-g">...</section>
  <section id="part-h">...</section>
  <section id="part-i">...</section>
  <section id="part-j">...</section>
  <section id="appendix">...</section>
</main>
```

- [ ] **Step 2: Create reusable teaching components**

Include reusable UI patterns for:

```text
- chapter intro
- code block panel
- callout box
- recap block
- request/response example box
- mini project panel
- comparison table
```

- [ ] **Step 3: Verify layout readiness**

Expected result:

```text
The HTML skeleton can accept long-form content without visual collapse.
```

### Task 5: Write foundational chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 1 to 4**

Required outputs:

```text
- beginner-friendly explanation
- at least one simple code block
- VN explanation after code
- recap block
```

- [ ] **Step 2: Verify beginner readability**

Expected result:

```text
A reader with zero FastAPI knowledge can understand what FastAPI is, why it exists, and how to run the first app.
```

### Task 6: Write request/response/validation chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 5 to 10**

Required content:

```text
- route basics
- params
- bodies
- validation
- response models
- errors
- headers/cookies/forms/files
```

- [ ] **Step 2: Embed code with Vietnamese comments**

Example style:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class ItemCreate(BaseModel):
    name: str  # Ten san pham nguoi dung gui len
    price: float  # Gia san pham, FastAPI se tu dong validate kieu du lieu
```

- [ ] **Step 3: Verify teaching completeness**

Expected result:

```text
No important request/response concept is introduced without a code example and explanation.
```

### Task 7: Write architecture and application-structure chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 11, 12, 18, and 19**

Required concepts:

```text
- dependency injection
- multi-file structure
- middleware
- CORS
- lifespan
```

- [ ] **Step 2: Show architecture progression**

The chapter flow must move from:

```text
single-file demo -> routers -> services/repositories -> production-minded structure
```

- [ ] **Step 3: Verify architectural clarity**

Expected result:

```text
The reader understands where route logic should end and service/resource logic should begin.
```

### Task 8: Write database and CRUD chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 13 to 15**

Required outputs:

```text
- DB setup explanation
- session lifecycle
- CRUD routes
- schema separation
- migration flow
```

- [ ] **Step 2: Include end-to-end examples**

Use code that shows the path from:

```text
request -> schema -> service/repository -> DB -> response schema
```

- [ ] **Step 3: Verify production usefulness**

Expected result:

```text
The CRUD and migration content is good enough to serve as a beginner's real backend starting point.
```

### Task 9: Write security chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 16 and 17**

Required outputs:

```text
- auth vs authorization
- hashing
- token flow
- OAuth2/JWT
- protected routes
- common mistakes
```

- [ ] **Step 2: Include clear risk notes**

Must explicitly mention:

```text
- leaking secrets
- weak token handling
- returning too much user data
- object-level authorization mistakes
```

- [ ] **Step 3: Verify depth**

Expected result:

```text
The security section goes beyond "copy this snippet" and explains why the design works.
```

### Task 10: Write testing and debugging chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 21 and 22**

Required outputs:

```text
- TestClient example
- dependency override example
- async test example
- debugging checklist
```

- [ ] **Step 2: Verify test practicality**

Expected result:

```text
The reader can write tests for normal routes, auth routes, and dependency-driven routes.
```

### Task 11: Write production operations chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapters 23 to 26**

Required outputs:

```text
- settings/env
- logs/metrics/tracing overview
- health endpoints
- retries/timeouts
- deployment concepts
- workers
- Docker
- proxy/HTTPS concepts
- scaling basics
```

- [ ] **Step 2: Include line-by-line Dockerfile explanation**

Minimum expected code artifact:

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["fastapi", "run", "app/main.py"]
```

The handbook must then explain each line in Vietnamese and modernize the exact command if the project layout requires it.

- [ ] **Step 3: Verify production depth**

Expected result:

```text
The deployment section is operationally meaningful, not just "run uvicorn and done".
```

### Task 12: Write AI/LLM/RAG chapters

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapter 27**

Required outputs:

```text
- model serving basics
- LLM proxy endpoint
- streaming tokens
- embeddings endpoint
- retrieval endpoint
- RAG query endpoint
- guardrails
- latency/cost thinking
```

- [ ] **Step 2: Tie AI patterns back to FastAPI primitives**

Map concepts explicitly:

```text
lifespan -> model loading
async -> upstream LLM call handling
StreamingResponse/SSE/WebSocket -> streaming UX choices
dependency injection -> shared clients/services
settings -> API keys and provider config
```

- [ ] **Step 3: Verify AI section substance**

Expected result:

```text
The AI chapter teaches API design patterns, not vague AI product talk.
```

### Task 13: Write mini-projects, common mistakes, and roadmap

**Files:**
- Modify: main HTML handbook

- [ ] **Step 1: Write chapter 28 mini-projects**

Each project must include:

```text
- objective
- folder structure
- key code
- why this project matters
- what to improve next
```

- [ ] **Step 2: Write chapter 29 common mistakes**

Must include:

```text
- async misuse
- schema mistakes
- security mistakes
- DB session mistakes
- testing gaps
- AI upstream timeout mistakes
```

- [ ] **Step 3: Write chapter 30 best practices and roadmap**

Must include:

```text
- production checklist
- AI API checklist
- suggested next docs to read
- next-step path for backend learners
- next-step path for AI learners
```

- [ ] **Step 4: Verify closure quality**

Expected result:

```text
The handbook ends with practical guidance, not abrupt stopping.
```

### Task 14: Apply visual polish and teaching polish

**Files:**
- Modify: main HTML handbook
- Optional: CSS/JS files

- [ ] **Step 1: Ensure the design language matches the guide**

Check for:

```text
- warm editorial aesthetic
- readable long-form spacing
- premium-looking code panels
- strong chapter headings
- mobile-safe layout
```

- [ ] **Step 2: Improve scanability**

Ensure:

```text
- long chapters are broken into sub-sections
- code is interleaved with explanation
- recap blocks exist
- callouts visually stand apart
```

- [ ] **Step 3: Verify the document does not feel auto-generated**

Expected result:

```text
The document has intentional structure, rhythm, and visual hierarchy.
```

### Task 15: Final verification and completeness audit

**Files:**
- Review: final HTML and any optional assets

- [ ] **Step 1: Run a chapter completeness audit**

Checklist:

```text
- all 30 chapters exist
- appendix exists
- all parts A through J exist
```

- [ ] **Step 2: Run a code completeness audit**

Checklist:

```text
- all mandatory code artifacts are present
- code has VN comments where helpful
- code is followed by VN explanation
```

- [ ] **Step 3: Run a source consistency audit**

Checklist:

```text
- no obvious conflict with official docs
- no outdated practice presented as current without a note
```

- [ ] **Step 4: Run a beginner-readability audit**

Checklist:

```text
- jargon is explained
- no chapter assumes hidden prerequisites
- examples progress from easy to advanced
```

- [ ] **Step 5: Run a production-depth audit**

Checklist:

```text
- security is substantial
- DB and migrations are substantial
- testing is substantial
- deployment is substantial
- AI/LLM/RAG is substantial
```

- [ ] **Step 6: Final acceptance decision**

The final HTML is only acceptable if the answer to all of these is yes:

```text
Can a beginner learn from it?
Can an intermediate learner use it to build a real API?
Does it explain production concerns clearly?
Does it explain AI/LLM/RAG usage concretely?
Does it look polished enough to feel like a serious handbook?
```

## 9. Failure Patterns to Avoid

- Starting with styling before content mapping
- Writing a shallow handbook with many headings but little substance
- Treating AI/LLM/RAG as generic prose without FastAPI endpoint examples
- Writing code snippets without Vietnamese explanations
- Using outdated package commands without noting modernization
- Leaving important topics as bullets instead of real teaching sections
- Making the handbook visually pretty but instructionally weak

## 10. Acceptance Criteria

The downstream agent should stop only when:

- the final HTML follows the full spec
- all major chapters are present
- code coverage is broad and deep
- Vietnamese teaching explanations are present throughout
- production backend topics are taught with real substance
- AI/LLM/RAG topics are taught with concrete API patterns
- the visual result respects `DESIGN-claude.md`
