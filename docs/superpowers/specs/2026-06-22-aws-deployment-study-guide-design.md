# Design Spec - Week 2 Day 2 Study Guide

## 1. Goal Description
Create a comprehensive, self-contained HTML study guide for Week 2 Day 2. The guide covers Context Engineering (personal facts, style, summary, and PDF resume processing), AWS Serverless Migration (boto3 S3 client, Mangum ASGI adapter, and IAM policies), Docker-based packaging for OS compatibility, API Gateway setup, and HTTPS CDN distribution using CloudFront. It matches the warm-cream editorial style of the Claude design guide and integrates interactive review components.

---

## 2. Target File
* **Path:** [day2_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day2_study_guide.html)
* **Status:** NEW

---

## 3. Detailed Architecture & Design

### A. Layout and Styling (Claude Aesthetic)
* Tinted cream canvas floor (`#faf9f5`), surface cards (`#efe9de`), primary coral accents (`#cc785c`), and dark navy product containers (`#181715`).
* Serif display typography for headings, humanist sans-serif for content, and monospaced font for code blocks.
* Interactive sidebar navigation, scroll-linked progress indicator,details toggler, click-to-reveal flashcards, and a quick quiz.

### B. Technical Content Coverage
* **Context Engineering:** Purpose and implementation of facts JSON, personal summary, communication style, and PDF profile scanning. System Prompt structure with temporal anchors (`datetime.now()`) and 3 critical security/safety boundaries (jailbreak prevention, hallucination control, and professionalism).
* **AWS Serverless Migration:** 
  * SDK `boto3` configuration for object storage (S3) instead of local files. Handling `ClientError` and the S3-specific `NoSuchKey` error for initial conversations.
  * ASGI Mangum adapter proxying Lambda JSON events into FastAPI ASGI requests and translating responses.
  * AWS IAM Policy configuration (User Group permissions, execution role S3 full access).
* **Docker Packaging & OS Compatibility:**
  * ELF binary architecture mismatch issue (running Windows/Mac local packages on Lambda's Amazon Linux runtime).
  * Automated Docker build process using `public.ecr.aws/lambda/python:3.12` base image in `deploy.py`.
  * Upload options (direct zip console upload vs S3 bucket sync).
* **Networking & CDN Distribution:**
  * API Gateway routes (ANY, GET, POST, OPTIONS) and CORS header setup.
  * CloudFront configuration using S3 Static Website Hosting origin domain (with HTTP Only origin protocol policy) and Viewer HTTPS redirection.
  * Restricting Lambda `CORS_ORIGINS` to the CloudFront distribution domain (validating prefix and suffix rules).
* **System Diagrams (Mermaid.js):**
  * Sơ đồ 1: AWS Production Deployment and Data Flow (CloudFront CDN -> S3 Frontend; API Gateway -> Lambda -> OpenAI/S3 Memory).
  * Sơ đồ 2: Mangum ASGI Event Translation Sequence (Browser -> API Gateway -> Lambda -> Mangum -> FastAPI -> Mangum -> Lambda -> API Gateway -> Browser).
* **End-to-End Workflow Walkthrough:** In-depth textual trace of request propagation through API Gateway, Mangum event parsing, S3 boto3 CRUD operations, LLM inference, and response serialization.
* **Code Walkthrough:** Visual code panels with detailed Vietnamese inline comments for:
  * `backend/resources.py` (PDF reader and static file loader).
  * `backend/context.py` (Dynamic System Prompt and security rules).
  * `backend/server.py` (S3 memory persistence, NoSuchKey handler).
  * `backend/deploy.py` (Docker subprocess executor and packaging script).
  * `backend/lambda_handler.py` (Mangum ASGI wrapper).
  * `frontend/next.config.ts` (Next.js 15.5 static export configuration).
* **Pitfalls and Trade-offs:** Troubleshooting S3 AccessDenied errors, CloudFront 504 gateway timeouts (Origin policy mismatch), CORS issues, and package size limits.

---

## 4. Verification Plan

### Automated Verification
* Run grep validation to confirm no empty `[[...]]` placeholders remain in the HTML output.
* Verify CSS styles load correctly.
* Inspect script handlers to ensure sticky TOC, progress bar, flashcards, and quiz components respond properly.
* Check Chrome DevTools console for JavaScript errors.
