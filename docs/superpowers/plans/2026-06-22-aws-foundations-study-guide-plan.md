# Implementation Plan - Week 2 Day 1 Study Guide

Create and verify the self-contained HTML study guide for Week 2 Day 1 under `tai_lieu/week2/day1_study_guide.html` and commit/push the final changes.

---

## User Review Required
* **Git Push:** The final code must be committed and pushed to the remote repository. This will be executed immediately after verification passes.
* **Aesthetics:** The layout must adhere strictly to the Claude theme variables defined in the spec. No visual placeholders or generic styles.

---

## Proposed Changes

### [Week 2 Study Guide Component]

#### [NEW] [day1_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day1_study_guide.html)
Create a new HTML file based on the `study_guide_structure_template.html` template. 
* Customize titles and headings to match the Week 2 Day 1 topic: AWS Foundations & Local Digital Twin Setup.
* Insert high-fidelity theories: AWS root/IAM user difference, AWS Billing, IaC (Terraform vs AWS CDK), 5 Cloud deployment archetypes, and 5 AWS components.
* Render two Mermaid.js system design diagrams:
  1. **Local Development (Day 1):** Showing Next.js frontend, FastAPI backend, local file session manager storing session files in `memory/`, and OpenAI API call.
  2. **AWS Production Deployment (Day 2):** Showing static assets hosted on S3 and delivered via CloudFront CDN, routing client messages to API Gateway, triggering Lambda, connecting to Bedrock for inference, and S3 for persistent chat memory.
* Provide an end-to-end detailed textual description of the workflow down to the function level.
* Embed code panels for `backend/server.py` and `frontend/components/twin.tsx` with complete code syntax and inline Vietnamese explanations.
* Fill in comparison tables, pitfalls, flashcards, interactive quiz, and summary sections. Ensure all `[[...]]` placeholders are completely removed.

---

## Verification Plan

### Automated Tests
* Validate HTML markup is valid and self-contained.
* Start Python HTTP Server and verify visual components:
  ```powershell
  python -m http.server 8000 --directory G:\AIProduction_t6_2026\production\tai_lieu\week2\
  ```
  Open Chrome to access `http://localhost:8000/day1_study_guide.html` and verify:
  * Reading progress bar updates on scroll.
  * Sticky TOC updates highlights correctly.
  * Details toggler operates all foldouts.
  * Flashcards reveal correct answers.
  * Quiz option click updates feedback area.
  * No console errors are thrown.

### Manual Verification
* Review Vietnamese translation tone to ensure it follows the "English - nghĩa tiếng Việt" terminology rules.
* Check that knowledge extensions are visibly separated from official slide/transcript contents.
