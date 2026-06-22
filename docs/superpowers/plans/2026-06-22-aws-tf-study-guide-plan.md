# Implementation Plan - Week 2 Day 4 Study Guide Creation

Tạo file học liệu ôn tập tự chứa [day4_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day4_study_guide.html) cho bài học **Day 4: Infrastructure as Code with Terraform**. File sẽ cung cấp đầy đủ lý thuyết, code thực hành, sơ đồ kiến trúc Mermaid, flashcards, và quiz tương tác theo phong cách thiết kế Claude editorial, đảm bảo tính trực quan và học thuật cao.

## Proposed Changes

### Documentation & Study Guides

#### [NEW] [day4_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day4_study_guide.html)
- Tạo tệp HTML tự chứa với đầy đủ CSS/JS tương tác và Mermaid để vẽ sơ đồ.
- **Nội dung lý thuyết:**
  - **Infrastructure as Code (IaC):** Triết lý IaC, 3 lợi ích chính (version controlled, reviewed, automated/repeatable).
  - **Terraform vs AWS CDK/CloudFormation:** So sánh tính chất cloud-agnostic, ngôn ngữ khai báo HCL so với code hướng đối tượng.
  - **6 khái niệm cốt lõi của Terraform:** Provider, Variable, Resource, State (`terraform.tfstate`), Output, Workspace.
  - **Quy trình dọn dẹp thủ công (Clean Slate):** Empty & Delete S3 Buckets, Disable & Delete CloudFront.
  - **Next.js API URL sync:** Tầm quan trọng của tiền tố `NEXT_PUBLIC_` và thứ tự triển khai (chạy Terraform Provisioning để lấy API URL trước khi build & sync frontend).
  - **Cơ chế cô lập môi trường qua Workspace:** Quản lý dev/test/prod thông qua cô lập file state.
- **Sơ đồ Mermaid:**
  - *Sơ đồ 1:* Quy trình dọn dẹp tài nguyên cũ trên AWS Console.
  - *Sơ đồ 2:* Đường ống hoạt động tự động của Deploy Script (Build backend -> Provisioning -> Build frontend với .env.production -> Sync S3).
- **Code Walkthrough:**
  - File cấu hình Terraform: `versions.tf` (gồm alias cho us-east-1), `variables.tf` (gồm validation block), `main.tf` (toàn bộ S3, Lambda, API Gateway, CloudFront, Route 53), `outputs.tf`, `terraform.tfvars`.
  - Deployment Scripts: `deploy.sh` & `deploy.ps1` (tự động hóa toàn phần).
  - Teardown Scripts: `destroy.sh` & `destroy.ps1` (empty buckets trước khi destroy).
- **Interactive Widgets:**
  - Bộ Flashcards hỏi đáp nhanh về Terraform & State.
  - Interactive Quick Quiz kiểm tra kiến thức về Workspace và biến môi trường Next.js.
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
- `git add G:\AIProduction_t6_2026\production\tai_lieu\week2\day4_study_guide.html`
- `git commit -m "docs: add Week 2 Day 4 study guide on Infrastructure as Code with Terraform"`
- `git push origin main`
