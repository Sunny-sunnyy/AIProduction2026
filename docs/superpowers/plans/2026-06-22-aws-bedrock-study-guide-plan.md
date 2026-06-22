# Implementation Plan - Week 2 Day 3 Study Guide Creation

Tạo file học liệu ôn tập tự chứa [day3_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day3_study_guide.html) cho bài học **Day 3: Transition to AWS Bedrock**. File sẽ cung cấp đầy đủ lý thuyết, code thực hành, sơ đồ kiến trúc Mermaid, flashcards, và quiz tương tác theo phong cách thiết kế Claude editorial, đảm bảo tính trực quan và học thuật cao.

## Proposed Changes

### Documentation & Study Guides

#### [NEW] [day3_study_guide.html](file:///G:/AIProduction_t6_2026/production/tai_lieu/week2/day3_study_guide.html)
- Tạo tệp HTML tự chứa với đầy đủ CSS/JS tương tác và Mermaid để vẽ sơ đồ.
- **Nội dung lý thuyết:**
  - **AWS Bedrock:** Định nghĩa, vai trò serverless, bảo mật và so sánh với Azure OpenAI.
  - **Amazon Nova family:** Đặc điểm các dòng model Nova Micro, Nova Lite, Nova Pro kèm so sánh chi phí & hiệu năng.
  - **IAM Permissions:** Giải thích việc cấp quyền cho User Group `TwinAccess` (`AmazonBedrockFullAccess`, `CloudWatchFullAccess`, `AmazonDynamoDBFullAccess` cho Day 5).
  - **Converse API:** Cơ chế hoạt động của `bedrock_client.converse()`, so sánh với InvokeModel API truyền thống và cách xử lý System Prompt.
  - **Cross-Region Inference Profiles:** Khái niệm, cơ chế cân bằng tải tự động và cách sử dụng Model ID dạng `global.*` hoặc `us.*` để tối ưu quota.
  - **Keyless Authentication:** Cơ chế Instance Metadata Service (IMDS) giúp Lambda lấy token bảo mật tạm thời mà không cần lưu API key.
- **Sơ đồ Mermaid:**
  - *Sơ đồ 1:* Kiến trúc Serverless AWS Bedrock Integration (Client Browser -> CloudFront -> API Gateway -> Lambda -> AWS Bedrock / S3 Memory).
  - *Sơ đồ 2:* Cơ chế xác thực không khóa (Keyless Auth) với AWS IMDS & SigV4.
- **Code Walkthrough:**
  - `requirements.txt` (loại bỏ `openai`, thêm `boto3`).
  - `backend/server.py` (logic khởi tạo client `bedrock-runtime`, hàm `call_bedrock` xử lý message array và bắt ngoại lệ ValidationException, AccessDeniedException).
  - Deployment Scripts (Kịch bản PowerShell cho Windows và Shell Script cho Linux sử dụng S3 Deployment Bucket tạm thời).
- **Interactive Widgets:**
  - Bộ Flashcards hỏi đáp nhanh về Bedrock & Nova.
  - Interactive Quick Quiz kiểm tra kiến thức về Cross-Region Inference Profiles và Keyless Auth.
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
- `git add G:\AIProduction_t6_2026\production\tai_lieu\week2\day3_study_guide.html`
- `git commit -m "docs: add Week 2 Day 3 study guide on AWS Bedrock transition"`
- `git push origin main`
