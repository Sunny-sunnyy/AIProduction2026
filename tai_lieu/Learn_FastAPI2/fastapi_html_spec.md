# FastAPI HTML Handbook Specification

## 1. Document Identity

- **Artifact type:** Detailed specification for a long-form educational HTML handbook.
- **Target output:** One polished HTML file that teaches FastAPI from zero to production, with a dedicated AI/LLM/RAG section.
- **Spec filename:** `fastapi_html_spec.md`
- **Primary execution model:** Agent handoff contract for downstream agents such as Gemini 3.5 Flash.
- **Workflow basis:** This spec is intentionally written in the spirit of `using-superpowers`, `brainstorming`, and `writing-plans`: explicit assumptions, strict source priority, no placeholder sections, and strong verification gates.

## 2. Objective

Create a single long, clear, visually polished HTML handbook about FastAPI for absolute beginners who know some Python but have no FastAPI knowledge. The handbook must start with the basics, then gradually move through real backend engineering concerns, and end with production-grade AI/LLM/RAG usage patterns.

The result must feel like a serious study handbook, not a short blog post, marketing page, or shallow cheatsheet.

## 3. Audience

- Primary audience: beginner learners who are new to FastAPI.
- Secondary audience: backend learners who want to understand how FastAPI is used in real production systems.
- Tertiary audience: AI engineers who want to use FastAPI for model serving, LLM wrappers, streaming APIs, embeddings, and RAG systems.

### Audience assumptions

- The reader knows basic Python syntax.
- The reader may not know HTTP, REST, ASGI, dependency injection, JWT, or database migrations.
- The reader needs explanations in simple Vietnamese, while keeping English technical terms where that improves clarity.

## 4. Source Priority and Evidence Policy

### Primary sources

1. Official FastAPI docs:
   - `https://fastapi.tiangolo.com/tutorial/`
   - `https://fastapi.tiangolo.com/advanced/`
   - `https://fastapi.tiangolo.com/deployment/`
2. `G:\Agent2026Win\Tai_lieu_on_tap_pv\TaiLieu_AI_Advanced\Fast_API.pdf`
3. `G:\Agent2026Win\Tai_lieu_on_tap_pv\TaiLieu_AI_Advanced\FAST API gg.pdf`

### Secondary supporting sources

- `https://viblo.asia/p/huong-dan-co-ban-framework-fastapi-tu-a-z-phan-1-V3m5W0oyKO7`
- Additional internet research only when it helps fill obvious gaps or clarify current FastAPI practices.

### Non-negotiable source rules

- If official FastAPI docs conflict with older PDF material, the official docs win.
- PDF content may be older in package names, CLI commands, version assumptions, or security practices. Downstream agents must normalize outdated details before presenting them.
- If a topic is highly version-sensitive, the handbook must include a short `Version note`.
- The final HTML must not present outdated commands as the current best practice when official docs show a newer approach.

## 5. Scope

The HTML must cover:

- FastAPI fundamentals
- HTTP and REST basics needed for understanding FastAPI
- Routing, parameters, request bodies, validation, and response modeling
- Error handling and API contracts
- Dependency injection and application structure
- Database integration and CRUD architecture
- Authentication and authorization
- Testing, debugging, and quality practices
- Middleware, lifespan, background work, streaming, SSE, and WebSockets
- Deployment, Docker, workers, proxies, HTTPS concepts, scaling, and observability
- FastAPI for AI/ML/LLM/RAG
- Practical end-to-end code examples with Vietnamese explanations

The HTML must not drift into:

- Full frontend engineering tutorials
- Deep DevOps platform-specific implementation beyond what is necessary for FastAPI deployment literacy
- Generic machine learning theory unrelated to FastAPI usage

## 6. Output Contract for the HTML

### General requirements

- One long HTML file.
- Prefer a self-contained artifact.
- If separate CSS or JS files are created, they must be justified and kept minimal.
- The HTML must be readable on desktop and mobile.
- The HTML must be appropriate for long-form study and review.

### Design requirements

- Apply the visual direction from `G:\harness_template\DESIGN-claude.md`.
- Preserve the warm editorial feel:
  - cream canvas
  - coral accent
  - dark code panels
  - expressive serif display headings
  - humanist sans body text
- Avoid flat, generic, or template-like educational layouts.
- Maintain strong visual hierarchy because the document will be long.

### UX requirements

- Sticky or easily accessible table of contents.
- Clear chapter segmentation.
- Strong code block readability.
- Distinct callout components for:
  - `Khai niem`
  - `Luu y`
  - `Pitfall`
  - `Best practice`
  - `Production note`
  - `AI note`
- End-of-chapter recap blocks.
- Smooth internal linking for navigation.

## 7. Language and Pedagogy Rules

- Main language: Vietnamese.
- Technical terms: keep English where clearer, for example `request body`, `response model`, `dependency injection`, `lifespan`, `streaming`, `worker`.
- Tone: patient, simple, structured, non-intimidating.
- Every major concept should follow this teaching order:
  1. concept
  2. why it matters
  3. syntax or mechanism
  4. example code
  5. explanation of the code
  6. when to use it
  7. common mistakes
- Difficult topics must use intuitive mental models or analogies.

## 8. Mandatory Code Rules

### Coverage rule

The handbook must include enough code to teach all major FastAPI topics, not just isolated toy snippets.

### Comment rule

- Code identifiers must stay in English.
- Code comments must be in Vietnamese when comments are used.
- Comments should be short and educational, not noisy.
- Under each important code block, include a Vietnamese explanation section.

### Required explanation structure for each important code block

- `Muc tieu doan code`
- `Code`
- `Giai thich`
- `Request/Response mau` when relevant
- `Loi thuong gap`
- `Production note` when relevant

### Mandatory code inventory

The final HTML must include all of the following, either as standalone examples or embedded inside end-to-end mini projects:

1. `main.py` hello world app
2. Basic GET and POST endpoints
3. Path parameters and query parameters
4. Pydantic request body model
5. Nested Pydantic model
6. Response model and field filtering
7. Error handling with `HTTPException`
8. Custom exception handler example
9. Header, cookie, form, and file upload examples
10. Dependency injection with `Depends`
11. `yield` dependency example for resource cleanup
12. `APIRouter` multi-file application example
13. Database session management example
14. CRUD example using SQLAlchemy or SQLModel
15. Alembic migration workflow example
16. Password hashing example
17. OAuth2/JWT authentication example
18. Protected route example
19. Middleware example
20. CORS configuration example
21. Lifespan startup and shutdown example
22. Background tasks example
23. `StreamingResponse` example
24. SSE example
25. WebSocket example
26. `pytest` + `TestClient` example
27. Dependency override test example
28. Async test example
29. Settings and environment variable example
30. Health endpoint example
31. Dockerfile example
32. Worker/deployment command example
33. LLM proxy endpoint example
34. Token streaming AI endpoint example
35. Embeddings endpoint example
36. RAG query endpoint example

## 9. Macro Structure of the HTML

The HTML must use this top-level structure:

1. Hero / opening section
2. Reader promise and how to use the handbook
3. Table of contents
4. Part A: FastAPI foundations
5. Part B: Working with requests, responses, and validation
6. Part C: Structuring a real FastAPI application
7. Part D: Databases and CRUD architecture
8. Part E: Security and authentication
9. Part F: Testing and debugging
10. Part G: Middleware, lifecycle, background work, and realtime features
11. Part H: Production operations, deployment, Docker, and scaling
12. Part I: FastAPI for AI/LLM/RAG
13. Part J: Common mistakes, best practices, and learning roadmap
14. Appendix

## 10. Chapter Contract Template

Every major chapter in the HTML must contain:

- `Muc tieu`
- `Ban se hoc duoc gi`
- `Giai thich khai niem`
- `Code vi du`
- `Giai thich code`
- `Vi du request/response` if relevant
- `Loi thuong gap`
- `Best practice`
- `Recap ngan`

## 11. Detailed Chapter Requirements

### Chapter 1. FastAPI la gi?

- Explain what FastAPI is.
- Explain why it became popular.
- Explain its relationship with Starlette, Pydantic, and OpenAPI.
- Compare FastAPI with Flask and Django in beginner-friendly language.
- Include a simple comparison table.
- Include a section: when FastAPI is a great fit, and when it is not the best choice.

### Chapter 2. HTTP va REST foundation cho nguoi moi

- Explain request, response, JSON, endpoint, route, method, header, body.
- Explain GET, POST, PUT, PATCH, DELETE.
- Explain status codes beginners will see most often.
- Explain idempotency simply.
- Explain path vs query vs body with examples.

### Chapter 3. ASGI, WSGI, Uvicorn, async

- Explain WSGI vs ASGI.
- Explain why ASGI matters for concurrency and WebSockets.
- Explain the role of Uvicorn.
- Explain `def` vs `async def` in FastAPI in a careful but simple way.
- Include clear guidance about I/O-bound work, external API calls, DB calls, and AI provider calls.

### Chapter 4. Cai dat moi truong va app dau tien

- Show environment setup.
- Show installing FastAPI.
- Prefer current official docs mindset.
- Mention `fastapi dev` and `fastapi run`.
- Show how `/docs`, `/redoc`, and `/openapi.json` help the learner.

### Chapter 5. Tao endpoint co ban

- Basic route decorators.
- Return dict, list, and model-shaped data.
- Explain how path operation functions map to URLs.
- Include at least one GET and one POST example.

### Chapter 6. Path params, query params, body

- Required vs optional query parameters.
- Type conversion.
- Path and body in the same endpoint.
- Multi-parameter examples.
- Numeric and string validation overview.

### Chapter 7. Validation voi Pydantic

- `BaseModel`
- Field constraints
- Nested models
- Collections and common extra data types
- Example data in docs
- Why validation matters in real APIs
- Input schema vs output schema mindset

### Chapter 8. Response models va thiet ke response

- Why response models matter
- Filtering sensitive fields
- Separate read/create/update schemas
- Status codes that communicate intent
- Short note on additional responses

### Chapter 9. Error handling va API contract

- `HTTPException`
- Validation errors
- Custom error shape
- Consistent API error thinking
- Difference between client errors and server errors

### Chapter 10. Headers, cookies, forms, files

- Header parameters
- Cookie parameters
- Form data
- File uploads
- Multipart basics
- Practical use cases and pitfalls

### Chapter 11. Dependency Injection

- Explain `Depends` from zero.
- Show function dependencies.
- Show class-based dependencies.
- Show sub-dependencies.
- Show global dependencies.
- Show `yield` dependencies for DB session or resource management.
- Explain why DI helps testing and architecture.

### Chapter 12. Bigger applications va APIRouter

- Multi-file project layout
- Routers by domain
- Prefixes and tags
- `api/v1` structure
- Suggested folders such as `routers`, `schemas`, `services`, `repositories`, `core`, `db`
- Explain composition over dumping everything into `main.py`

### Chapter 13. Database foundations

- Why APIs usually need persistence
- SQLAlchemy or SQLModel role
- Engine and session
- Development database vs production database
- Unit of work intuition

### Chapter 14. CRUD application

- Create, read, update, delete
- Pagination, filtering, sorting
- Service vs repository boundaries
- `jsonable_encoder` where relevant
- Full code flow from route to DB

### Chapter 15. Alembic migrations

- What migrations are
- Why manual schema edits are risky
- Revision workflow
- Upgrade and downgrade
- Common migration mistakes

### Chapter 16. Security fundamentals

- Authentication vs authorization
- Password hashing
- Bearer tokens
- API keys vs OAuth2
- JWT intuition
- Secret management basics

### Chapter 17. OAuth2 va JWT thuc chien

- Login endpoint flow
- Token creation and validation
- Current user dependency
- Protected endpoints
- Scopes as an advanced production note
- Common JWT mistakes
- Beginner-friendly explanation of BOLA/IDOR-style risks

### Chapter 18. Middleware va CORS

- What middleware is
- Timing/logging example
- Request lifecycle overview
- CORS purpose and common misunderstandings
- When middleware is a better fit than a dependency

### Chapter 19. Lifespan, startup, shutdown

- Lifespan events
- Initializing shared resources
- Closing resources cleanly
- Why lifespan matters for model loading, connection pools, and shared async clients

### Chapter 20. Background work, streaming, SSE, WebSockets

- Background tasks
- When background tasks are enough and when a queue is needed
- `StreamingResponse`
- JSON lines streaming
- SSE
- WebSockets
- Decision guide: which one to use for notifications, live dashboards, and LLM streaming

### Chapter 21. Testing FastAPI applications

- Why testing APIs is different from reading code
- `pytest`
- `TestClient`
- Validation tests
- CRUD tests
- Auth tests
- Dependency overrides
- Async tests
- Testing DB-backed endpoints

### Chapter 22. Debugging va quality mindset

- Reading docs output
- Inspecting OpenAPI
- Common import and startup errors
- Common schema mismatch issues
- Practical debugging checklist

### Chapter 23. Settings va environment variables

- Config separation
- `.env` role
- Secret hygiene
- Per-environment settings
- Why production config should not be hardcoded

### Chapter 24. Observability va production operations

- Structured logs
- Metrics overview
- Tracing concept
- Health checks
- Readiness vs liveness
- Timeouts and retries
- Rate limiting concept
- Caching concept
- p95 and p99 intuition

### Chapter 25. Deployment va Docker

- `fastapi run`
- Uvicorn workers
- Deployment concepts
- Reverse proxy and HTTPS concepts
- Behind a proxy
- Dockerfile explained line by line
- Environment variables in deployment

### Chapter 26. Scaling basics

- Stateless API design
- Horizontal scaling
- Worker count intuition
- DB connection pressure
- CPU-bound vs I/O-bound behavior
- Shared state pitfalls

### Chapter 27. FastAPI cho AI, ML, LLM, va RAG

- Why FastAPI is popular in AI services
- Model loading patterns
- LLM gateway pattern
- Streaming token responses
- Embeddings endpoints
- Retrieval endpoints
- RAG orchestration endpoint shape
- Guardrails for inputs and outputs
- Cost, latency, timeout, retry, and fallback thinking

### Chapter 28. End-to-end mini projects

The handbook must include four progressive mini projects:

1. `Project A`: Hello FastAPI starter
2. `Project B`: CRUD API with DB and routers
3. `Project C`: Authenticated production-minded backend
4. `Project D`: AI/LLM/RAG service skeleton

Each project must contain:

- objective
- folder structure
- code
- explanation
- likely next improvements

### Chapter 29. Common mistakes

- Overusing `async`
- Returning ORM entities directly
- Not separating schemas
- Mishandling DB sessions
- Hardcoding secrets
- Using background tasks for the wrong workloads
- Missing timeout logic for upstream AI calls
- Skipping test overrides

### Chapter 30. Best practices va roadmap hoc tiep

- Best practices summary
- Production-ready checklist
- AI API checklist
- Suggested next FastAPI docs sections
- Suggested next learning path for backend engineers and AI engineers

## 12. Appendix Requirements

The appendix should include concise but useful supporting material such as:

- Glossary of key terms
- FastAPI command quick reference
- HTTP status code quick reference
- Suggested project structure reference
- Optional advanced topics to explore later:
  - callbacks
  - webhooks
  - SDK generation
  - sub-applications
  - WSGI integration

## 13. Visual and Structural Requirements

- Use large editorial headings for parts and chapters.
- Code must sit on dark surfaces with strong contrast.
- Avoid dense walls of text by alternating:
  - prose
  - code
  - tables
  - callouts
  - recaps
- Use subtle section dividers.
- The document should feel crafted, not auto-generated.

## 14. Mandatory Quality Gates

The final HTML is not acceptable if any of the following happen:

- Missing major chapters from this spec
- Code exists without explanation in important sections
- Important topics are explained without code where code is necessary
- Security section is too shallow
- Database section is too shallow
- Testing section is too shallow
- Deployment section ignores Docker/workers/proxy/HTTPS concepts
- AI section is vague and lacks endpoint design examples
- No Vietnamese teaching explanations
- Comments inside code are missing in places where beginner guidance would help
- Obvious placeholders remain
- The design guide is ignored

## 15. Completion Criteria

The HTML will be considered successful only if it:

- Teaches FastAPI clearly to a beginner
- Covers FastAPI broadly and deeply enough for practical backend work
- Includes production-grade thinking, not only syntax
- Includes strong AI/LLM/RAG coverage
- Contains detailed code examples with Vietnamese educational comments and explanations
- Feels visually premium and coherent under the `DESIGN-claude.md` direction
- Can act as a standalone study handbook

## 16. Downstream Agent Instructions

- Read this entire spec before writing any HTML.
- Do not shrink scope without stating exactly what is being cut.
- If time is limited, preserve the backbone chapters first:
  - foundations
  - validation
  - dependency injection
  - routers/application structure
  - database/CRUD
  - auth/security
  - testing
  - deployment/operations
  - AI/LLM/RAG
- Prefer completeness and clarity over decorative extras.
- Never leave placeholders.
