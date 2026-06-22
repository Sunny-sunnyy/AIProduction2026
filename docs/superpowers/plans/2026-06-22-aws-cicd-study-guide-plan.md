# Implementation Plan - Week 2 Day 5 Study Guide Creation

Tạo file học liệu ôn tập tự chứa [day5_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day5_study_guide.html) cho bài học **Day 5: CI/CD with GitHub Actions**. File sẽ cung cấp đầy đủ lý thuyết, code thực hành, sơ đồ kiến trúc Mermaid, flashcards, và quiz tương tác theo phong cách thiết kế Claude editorial, đảm bảo tính trực quan và học thuật cao.

## Proposed Changes

### Documentation & Study Guides

#### [NEW] [day5_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day5_study_guide.html)
- Tạo tệp HTML tự chứa với đầy đủ CSS/JS tương tác và Mermaid để vẽ sơ đồ.
- **Nội dung lý thuyết:**
  - **CI/CD & GitHub Actions:** Định nghĩa, YAML syntax, cơ chế trigger (push, workflow_dispatch), runner, job, step.
  - **Remote State & State Locking:** Vai trò của Remote State trong CI/CD, cơ chế khóa DynamoDB (`LockID`), giải quyết vấn đề bootstrapping qua `-target` apply.
  - **OIDC Authentication (Passwordless Auth):** Nguyên lý OpenID Connect, lý do OIDC bảo mật hơn Access Keys dài hạn, cách hoạt động của OIDC Federated Identity provider và trust policy.
  - **Nested Git Repositories Fix:** Giải thích và xử lý lỗi repo lồng nhau do create-next-app sinh ra.
  - **Cải tiến UI Focus & Avatar:** Cách sử dụng React `useRef` để refocus ô input chat sau khi gửi tin nhắn.
- **Sơ đồ Mermaid:**
  - *Sơ đồ 1:* Quy trình OIDC Passwordless Authentication Exchange (GitHub Actions Runner -> AWS STS -> IAM Role).
  - *Sơ đồ 2:* Sơ đồ cô lập state file qua workspaces trong S3 Remote Backend.
- **Code Walkthrough:**
  - File bootstrap: `backend-setup.tf` và `github-oidc.tf`.
  - File workflow YAML: `deploy.yml` và `destroy.yml`.
  - Cập nhật deploy & destroy scripts động: `deploy.sh`, `deploy.ps1`, `destroy.sh`, `destroy.ps1` chứa `-backend-config` động.
  - Frontend improvement: `twin.tsx` sửa lỗi focus input.
- **Interactive Widgets:**
  - Bộ Flashcards hỏi đáp nhanh về OIDC, Remote State, và CI/CD.
  - Interactive Quick Quiz kiểm tra kiến thức về OIDC Trust Policy và YAML configuration.
  - Bộ lọc TOC động, progress bar và các nút đóng/mở tất cả các chi tiết (`details`).

## Verification Plan

### Manual Verification
- Dùng công cụ grep tìm kiếm các chuỗi `[[` để đảm bảo không còn bất kỳ placeholder nào trong mã nguồn HTML.
- Mở tệp HTML trực tiếp trong trình duyệt để kiểm tra:
  - Giao diện CSS Claude editorial (kem, san hô, dark code panel).
  - Độ mượt của TOC động và progress bar khi cuộn trang.
  - Trạng thái hiển thị của các sơ đồ Mermaid.
  - Chức năng tương tác của Flashcards (Reveal/Hide) và Quiz (chọn đáp án đúng/sai hiển thị phản hồi chi tiết).

## Git Commit & Push
- `git add G:\AIProduction_t6_2026\production\tai_lieu\week2\day5_study_guide.html`
- `git commit -m "docs: add Week 2 Day 5 study guide on CI/CD with GitHub Actions"`
- `git push origin main`
