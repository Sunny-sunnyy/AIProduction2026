# Design Spec - Week 2 Day 1 Study Guide

## 1. Goal Description
Create a comprehensive, self-contained HTML study guide for Week 2 Day 1. The guide will cover AWS Foundations, Cost Management, Cloud Deployment Archetypes, AWS Core Components, Local Digital Twin Setup, and File-based Stateful Memory. It follows the editorial style of the Claude design guide (cream canvas, coral accents, dark code panels) and provides interactive widgets (sticky TOC, reading progress bar, details toggle, flashcards, and a quick quiz) using vanilla JavaScript.

---

## 2. Target File
* **Path:** [day1_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day1_study_guide.html)
* **Status:** NEW

---

## 3. Detailed Architecture & Design

### A. Layout and Styling (Claude Aesthetic)
* **Base Variables:**
  * Canvas: `#faf9f5` (tinted warm cream)
  * Surface Soft: `#f5f0e8` (soft cream dividers)
  * Surface Card: `#efe9de` (light cream card background)
  * Primary Coral: `#cc785c` (coral accent for primary CTAs and links)
  * Primary Active: `#a9583e` (pressed coral)
  * Surface Dark: `#181715` (navy-dark background for code windows and headers)
  * Surface Dark Soft: `#1f1e1b` (syntax highlight container)
  * Ink: `#141413` (warm dark titles)
  * Body: `#3d3d3a` (running text)
* **Fonts:** Cormorant Garamond / EB Garamond (substitutes for Copernicus serif display) for H1, H2, H3. Inter (substitute for StyreneB sans) for UI controls, body text, and labels. JetBrains Mono for code blocks.
* **Responsive Breakpoints:**
  * Mobile (< 768px): Navigation collapses or stacks, grid layouts become 1-column, code blocks scroll horizontally.
  * Desktop (>= 1024px): 2-column layout (sidebar navigation at 285px, content area taking the rest).

### B. Interactive Widgets (Vanilla JS)
* **Sticky Table of Contents (TOC):** Sticky sidebar with links highlights the currently active section based on the window's scroll position (offset calculation).
* **Reading Progress Bar:** Tracks the scroll position of the document and updates the width of a thin horizontal indicator at the top of the header card.
* **Details Toggler:** Provides "Expand notes" and "Collapse notes" buttons in the sidebar to open/close all `<details>` elements simultaneously.
* **Interactive Flashcards:** Toggle class `.revealed` to show/hide the answer content when clicking "Reveal answer".
* **Interactive Quiz:** Validates selected options instantly and prints explanatory feedback in a container below the question.

### C. Technical Content Coverage
* **AWS Foundations:** Root user vs IAM User (least privilege), Cost Billing Management, and Cost Explorer.
* **Infrastructure as Code (IaC):** Definition and comparative analysis of Terraform (HCL, cloud-agnostic) vs AWS CDK.
* **5 Cloud Deployment Archetypes:** Categorization of EC2 (IaaS), Elastic Beanstalk/Vercel (PaaS), App Runner (CaaS), ECS/EKS (Container Orchestration), and Lambda (Serverless FaaS). Detail the concepts of Scale-to-Zero and Cold Start.
* **5 AWS Components:** Object Storage (S3), FaaS Runtime (Lambda), Content Delivery Network (CloudFront Edge Caching), API Proxy (API Gateway CORS/Rate-limiting), and Model API Gateway (Amazon Bedrock).
* **System Diagrams (Mermaid.js):**
  * Sơ đồ 1: Local Architecture (Day 1) - Local React client communicating with FastAPI backend saving JSON state to the `/memory` folder, calling OpenAI completion.
  * Sơ đồ 2: AWS Production Architecture (Day 2) - Frontend hosted on S3 and distributed via CloudFront CDN, routing API requests through API Gateway to Lambda backend, which queries Bedrock for LLM reasoning and reads/writes conversational history from/to an S3 memory bucket.
* **Detailed Textual Workflow (End-to-End Walkthrough):** In-depth narrative trace of the local stateful memory loop down to the function level (FastAPI endpoint, UUID generation, `load_conversation`, calling OpenAI completions, updating history list, `save_conversation` using `json.dump(ensure_ascii=False)`).
* **Code Walkthrough:** Code blocks with detailed Vietnamese inline comments for:
  * `backend/server.py` (Stateful session parser and listing routes).
  * `frontend/components/twin.tsx` (React state updates and fetch requests).
  * Configurations: `postcss.config.mjs` and `globals.css` (Tailwind v4 features).
* **Pitfalls and Trade-offs:** Detailed troubleshooting guide covering CORS errors, bill shocks, cold starts, and concurrent file locking.

---

## 4. Verification Plan

### Automated Verification
* Open the generated HTML file using python's built-in web server or directly in a web browser to verify:
  * CSS stylesheet loads properly and matches colors.
  * Sticky TOC updates current active menu item on scroll.
  * Progress bar fills up proportionally to scroll depth.
  * Details toggle buttons open/close all nested elements.
  * Flashcards lật thẻ hiển thị đáp án bình thường.
  * Quiz option click triggers correct validation state.
  * HTML structure contains no empty placeholders (`[[...]]`).
  * Check for console errors in Chrome DevTools.

### Manual Verification
* Inspect the Mermaid diagrams to verify correct formatting and readability.
* Read the generated Vietnamese text to ensure high quality editorial style, consistent with the terminology rules.
