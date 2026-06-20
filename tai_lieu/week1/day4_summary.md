# Day 4 Summary: Healthcare Consultation Assistant (FastAPI & Next.js)

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

---

# 19. Day 4 - Building Your First Commercial AI App - From Prototype to Business

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 19).
- Slide: Đã dùng (Trang giới thiệu tổng quan Day 4 và màu sắc định hướng của slide).
- Code: Đã dùng (Tham chiếu file [day4.md](file:///G:/AIProduction_t6_2026/production/week1/day4.md) để hiểu sự thay đổi về mục tiêu nghiệp vụ).
- Summary lịch sử: Đã dùng (Đọc [day3_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day3_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn nhất quán hoàn toàn. Transcript giải thích rõ ý tưởng thương mại hoá sản phẩm và cấu hình thực tế.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học mở đầu ngày học thứ 4 (tuần 1) bằng việc chuyển dịch ứng dụng từ một bản demo sinh ý tưởng sang một ứng dụng thương mại thực tế (Commercial Application) phục vụ lĩnh vực Y tế (Healthcare).
- Giảng viên nhắc lại cam kết kiên nhẫn: Platform Engineering và DevOps là công việc chứa đầy sự cấu hình và gỡ lỗi (bashing head against a wall). Các lỗi liên quan đến biến môi trường, tường lửa hay VPN công ty là một phần tất yếu của quá trình xây dựng năng lực triển khai thực tế.
- Khẳng định tính cập nhật của tài liệu: Tài liệu học tập sẽ liên tục được tinh chỉnh và bổ sung các ghi chú sửa lỗi dựa trên trải nghiệm thực tế của học viên từ các khoá học trước để đảm bảo tính thực tiễn.
- Ý tưởng cốt lõi của ứng dụng y tế: Trợ lý hành chính y khoa giúp giảm thiểu gánh nặng giấy tờ (administrative overhead) cho bác sĩ bằng cách chuyển đổi các ghi chú thô của bác sĩ thành bệnh án chuyên nghiệp và email hướng dẫn dễ hiểu gửi cho bệnh nhân.
- Định hướng phát triển tương lai: Ứng dụng này đóng vai trò như một bệ phóng (springboard). Giảng viên khuyến khích học viên tích hợp thêm đa phương thức (multimodal audio - nghe ghi âm cuộc khám) và các dịch vụ email tự động (SendGrid, Resend) để tạo nên tính năng độc quyền cho các gói thuê bao trả phí.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cách thức một ứng dụng AI giải quyết một bài toán ngách cụ thể (thủ tục hành chính y tế) để tạo ra giá trị thương mại.
  - Nhận thức rõ vai trò của Platform Engineering trong việc thiết lập và gỡ lỗi hạ tầng ứng dụng.
  - Hiểu cách thiết kế các tính năng nâng cao (đa phương thức, email tự động) làm cơ sở phân tầng thuê bao (billing tiers).
- Practical goals - mục tiêu thực hành:
  - Chuẩn bị tinh thần và phương pháp tự gỡ lỗi (debugging) khi gặp sự cố cấu hình môi trường.
  - Định hình cấu trúc tính năng mới của ứng dụng hỗ trợ bác sĩ.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích được tầm quan trọng của việc tự xoay xở và kiên nhẫn khi đối mặt với lỗi cấu hình môi trường trong DevOps.
  - Giải thích được quy trình chuyển đổi từ một bản mẫu (prototype) sang một mô hình kinh doanh SaaS có thu phí.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Day 3 ([day3_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day3_summary.md)): Sau khi học viên đã xây dựng thành công hạ tầng bảo mật (Clerk Authentication) và thanh toán định kỳ (Clerk Billing/Stripe), bài học này cung cấp logic nghiệp vụ thương mại thực tế đầu tiên (Healthcare Consultation Assistant) để lấp đầy khung hạ tầng đã dựng sẵn.

## 5. Core Theory - Lý thuyết cốt lõi
- Commercial AI Application - ứng dụng AI thương mại:
  - Meaning - nghĩa: Ứng dụng sử dụng trí tuệ nhân tạo để giải quyết một điểm đau (pain point) cụ thể của khách hàng mục tiêu, tạo ra giá trị thiết thực và có khả năng tạo ra doanh thu.
  - Why it matters - vì sao quan trọng: Giúp chuyển đổi năng lực kỹ thuật thuần túy thành các sản phẩm thương mại có khả năng tự vận hành tài chính.
- Administrative overhead - chi phí hành chính:
  - Meaning - nghĩa: Lượng thời gian, công sức và nguồn lực phi chuyên môn mà một chuyên gia (bác sĩ) phải tiêu tốn để xử lý thủ tục giấy tờ, biên bản và giao tiếp hỗ trợ.
  - Why it matters - vì sao quan trọng: Đây là một điểm đau rất lớn trong ngành y tế, việc giảm tải hành chính giúp bác sĩ tập trung nhiều thời gian hơn vào chuyên môn khám chữa bệnh.
- Platform Engineering - kỹ nghệ nền tảng:
  - Meaning - nghĩa: Kỷ nghệ chuyên môn tập trung vào việc thiết kế, xây dựng và quản trị hạ tầng, chuỗi công cụ triển khai tự động hóa để lập trình viên bàn giao ứng dụng nhanh và an toàn.
  - Why it matters - vì sao quan trọng: Giúp tối ưu hóa năng suất và giảm thiểu các rủi ro vận hành khi đưa ứng dụng lên các môi trường cloud khác nhau.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
`Không có pipeline rõ ràng trong tài liệu nguồn`
Bài học này tập trung vào định hướng tư duy thương mại hoá sản phẩm và chuẩn bị tâm thế lập trình hệ thống nên không chứa quy trình xử lý dữ liệu cụ thể.

## 7. Techniques - Kỹ thuật sử dụng
- Environment Debugging Protocol - giao thức gỡ lỗi môi trường:
  - Purpose - mục đích: Rèn luyện kỹ năng phân tích lỗi hệ thống một cách có hệ thống, không tin tưởng mù quáng vào các đề xuất sửa chữa ngắn hạn của LLM.
  - When to use - dùng khi nào: Sử dụng khi gặp các lỗi về kết nối API, biến môi trường không nhận dạng hoặc lỗi phân quyền deploy.
  - Trade-off - đánh đổi: Tốn thời gian nghiên cứu tài liệu và bản ghi log thay vì viết code tính năng mới.
  - Common mistake - lỗi dễ gặp: Áp dụng vội vã các bản sửa lỗi chắp vá của LLM mà không hiểu rõ nguyên nhân gốc rễ, dẫn đến hệ thống bị lỗi dây chuyền.

## 8. Code Walkthrough - Phân tích code nếu có
`Code được cung cấp trong session nhưng chưa thấy code liên quan trực tiếp tới lesson này.`
(Bài học này thuần lý thuyết giới thiệu định hướng và chuẩn bị tư duy).

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có bản đồ lựa chọn công nghệ cụ thể được phân tích trong bài lý thuyết giới thiệu này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
Không có lỗi kỹ thuật đặc thù nào được ghi nhận trong bài lý thuyết này.

## 11. Knowledge Extension - Kiến thức mở rộng
- HIPAA Compliance (Đạo luật về trách nhiệm giải trình và cung cấp thông tin bảo hiểm y tế): Tiêu chuẩn liên bang Hoa Kỳ nhằm bảo vệ dữ liệu sức khỏe nhạy cảm của bệnh nhân (PHI - Protected Health Information) không bị tiết lộ nếu không có sự đồng ý của bệnh nhân. Đây là quy định bắt buộc khi thương mại hóa phần mềm y tế.

## 12. Study Pack - Gói ôn tập
### Must remember
- Day 4 chuyển hướng dự án sang xây dựng một ứng dụng thương mại thực tế trong ngành y tế.
- Việc gỡ lỗi cấu hình môi trường và nền tảng (Platform Engineering) là kỹ năng quan trọng ngang hàng với viết code logic.
- Ứng dụng y khoa giải quyết trực tiếp điểm đau hành chính của bác sĩ (administrative overhead).
- Luôn kiểm chứng kỹ lưỡng các phản hồi của LLM khi xử lý lỗi môi trường để tránh lỗi dây chuyền.

### Self-check questions
1. Điểm đau lớn nhất trong các phòng khám bác sĩ mà ứng dụng MediNotes Pro giải quyết là gì?
2. Tại sao Platform Engineering lại thường gặp nhiều lỗi môi trường cấu hình hơn lập trình phần mềm thông thường?
3. Tại sao không nên tin tưởng hoàn toàn vào các bản sửa lỗi nhanh của LLM khi gỡ lỗi hạ tầng?

### Flashcards
- Q: Lợi ích chính của ứng dụng Healthcare Consultation Assistant là gì?
  A: Giảm thiểu thủ tục giấy tờ hành chính (administrative overhead) cho bác sĩ bằng cách sinh tự động hồ sơ bệnh án và email gửi bệnh nhân.
- Q: Platform Engineering tập trung vào nhiệm vụ gì?
  A: Thiết lập hạ tầng, cấu hình môi trường, và tự động hóa quy trình triển khai ứng dụng an toàn.

### Interview Q&A nếu phù hợp
- Q: Khi thiết kế một ứng dụng y tế để đưa vào thương mại hóa thực tế, rào cản lớn nhất về mặt pháp lý là gì?
  A: Đó là việc tuân thủ các quy định bảo mật thông tin y tế như đạo luật HIPAA tại Mỹ. Hệ thống cần có cơ chế mã hóa dữ liệu đầu-cuối (end-to-end encryption), lưu vết lịch sử truy cập (audit logging) và cơ chế quản lý sự chấp thuận của bệnh nhân.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 20. Day 4 - Building Healthcare AI Apps with FastAPI and Structured Prompts

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 20).
- Slide: Đã dùng (Trang sơ đồ API Route và cấu trúc dữ liệu y tế).
- Code: Đã dùng (Tham chiếu các file [day4.md](file:///G:/AIProduction_t6_2026/production/week1/day4.md) từ bước 1 đến bước 4).
- Summary lịch sử: Đã dùng (Đọc [day3_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day3_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin đồng nhất. Mã nguồn và transcript khớp nhau về các bước cài đặt thư viện date picker và sửa đổi route.

## 2. Executive Summary - Tóm tắt cốt lõi
- Cài đặt các thư viện frontend bổ sung: `react-datepicker` để hiển thị giao diện lịch chọn ngày và `@types/react-datepicker` phục vụ cho khai báo kiểu TypeScript.
- Thay đổi phương thức API: Chuyển đổi endpoint `/api` của FastAPI backend từ GET sang POST để tiếp nhận JSON payload phức tạp gửi từ client.
- Tích hợp mô hình Pydantic: Khai báo lớp `Visit(BaseModel)` của Pydantic để thực hiện validate (kiểm chứng tính đúng đắn) cấu trúc dữ liệu gửi lên gồm `patient_name`, `date_of_visit`, `notes`. FastAPI tự động chuyển hoá JSON thô thành đối tượng Python có kiểu an toàn.
- Thiết kế Prompt cấu trúc (Structured Prompts): Sử dụng `system_prompt` và `user_prompt_for` để hướng dẫn LLM trả về kết quả đúng cấu trúc gồm 3 phần (Summary, Next steps, Draft email).
- Cập nhật cấu hình ứng dụng: Nhúng stylesheet CSS của DatePicker (`react-datepicker/dist/react-datepicker.css`) vào `pages/_app.tsx` để hiển thị lịch đúng thiết kế. Cập nhật tiêu đề trang và mô tả y tế tại `pages/_document.tsx`.
- Cập nhật giao diện trang sản phẩm `pages/product.tsx`: Xây dựng form nhập liệu (Patient Name, Date picker, Consultation Notes) có ràng buộc validation phía client và tích hợp SSE streaming qua `fetchEventSource`.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cơ chế hoạt động của FastAPI Dependency Injection kết hợp Pydantic model validation.
  - Hiểu vai trò của Structured Prompts trong việc định hướng định dạng phản hồi của LLM.
  - Nắm rõ cơ chế import CSS toàn cục trong Next.js Pages Router.
- Practical goals - mục tiêu thực hành:
  - Cài đặt và sử dụng React component ngoài (`react-datepicker`).
  - Sửa đổi REST API từ GET sang POST.
  - Khai báo Pydantic validation ở backend.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích cơ chế tự động chuyển JSON sang đối tượng Python của FastAPI.
  - Phân tích ưu điểm của việc thiết lập prompt phân rõ vai trò hệ thống (system/user prompts).

## 4. Previous Context - Liên hệ với bài trước
Bài học này nối tiếp trực tiếp sau Bài 19, hiện thực hóa mã nguồn Next.js frontend và FastAPI backend để chạy ứng dụng Consultation Assistant trên môi trường localhost.

## 5. Core Theory - Lý thuyết cốt lõi
- Pydantic BaseModel - mô hình cơ sở Pydantic:
  - Meaning - nghĩa: Một class cơ sở của thư viện Pydantic trong Python, dùng để định hình lược đồ (schema) dữ liệu và tự động kiểm chứng kiểu dữ liệu đầu vào.
  - Why it matters - vì sao quan trọng: Giúp code backend an toàn, ngăn chặn các cuộc gọi API chứa dữ liệu sai lệch hoặc thiếu trường thông tin bắt buộc.
- Structured Prompt - gợi ý có cấu trúc:
  - Meaning - nghĩa: Kỹ thuật phân tách rõ ràng hướng dẫn hệ thống (System Prompt) và dữ liệu cụ thể (User Prompt) để định hướng mô hình AI trả về kết quả khớp với cấu trúc mong muốn.
  - Why it matters - vì sao quan trọng: Đảm bảo đầu ra của AI luôn ổn định, giúp frontend dễ dàng phân tích và hiển thị giao diện phân vùng chuyên nghiệp.
- Datepicker component - linh kiện chọn ngày:
  - Meaning - nghĩa: Linh kiện giao diện người dùng (UI component) cho phép chọn ngày tháng trực quan qua bảng lịch.
  - Why it matters - vì sao quan trọng: Nâng cao trải nghiệm người dùng, đảm bảo dữ liệu ngày tháng luôn đồng bộ theo chuẩn định dạng ISO thay vì để người dùng tự nhập tay.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình xử lý dữ liệu và tạo báo cáo y khoa (Consultation Pipeline):
1. Input: Bác sĩ nhập tên bệnh nhân, chọn ngày khám qua date picker, và nhập ghi chú khám thô -> Click Submit.
2. Processing steps:
   - Frontend Next.js đóng gói dữ liệu thành JSON và gửi POST request đến `/api` kèm theo JWT Bearer token trong tiêu đề `Authorization`.
   - FastAPI backend tiếp nhận request, giải mã token qua `clerk_guard` và tự động chuyển đổi JSON payload thành đối tượng Pydantic `Visit`.
   - Backend kết hợp dữ liệu từ `Visit` vào prompt và gửi yêu cầu tới OpenAI completions API với chế độ `stream=True`.
   - Backend đọc luồng dữ liệu trả về từ OpenAI và phản hồi dưới dạng `StreamingResponse`.
3. Output: Frontend nhận streaming qua sự kiện `onmessage` của `fetchEventSource`, ghép chuỗi liên tục và cập nhật Markdown hiển thị cho bác sĩ.

## 7. Techniques - Kỹ thuật sử dụng
- Pydantic Data Validation - xác thực dữ liệu Pydantic:
  - Purpose - mục đích: Tự động hoá việc kiểm tra định dạng và kiểu dữ liệu gửi lên API backend.
  - When to use - dùng khi nào: Sử dụng cho tất cả các endpoint nhận dữ liệu từ các form nhập liệu phức tạp.
  - Trade-off - đánh đổi: Lập trình viên phải khai báo class định kiểu rõ ràng, không thể linh hoạt nhận dữ liệu tuỳ biến tự do như dạng dictionary thô.
  - Common mistake - lỗi dễ gặp: Khai báo thiếu hoặc sai kiểu dữ liệu của các trường khiến FastAPI tự động trả về lỗi 422 (Unprocessable Entity).
- Form State Binding - liên kết trạng thái biểu mẫu:
  - Purpose - mục đích: Sử dụng React state (`useState`) để liên tục theo dõi và đồng bộ hóa các ký tự bác sĩ gõ trên form vào biến bộ nhớ.
  - When to use - dùng khi nào: Phát triển mọi form nhập liệu tương tác trong React/Next.js.
  - Trade-off - đánh đổi: Tăng lượng code quản lý trạng thái trong component.
  - Common mistake - lỗi dễ gặp: Quên gán thuộc tính `value` hoặc hàm `onChange` cho thẻ input khiến giao diện bị đóng băng không gõ chữ được.

## 8. Code Walkthrough - Phân tích code nếu có
### File `api/index.py` - FastAPI POST Endpoint
- Purpose - mục đích: Định nghĩa cấu trúc Pydantic `Visit` và chuyển route sang POST để tiếp nhận JSON payload.
- Key logic - logic chính: Định nghĩa `class Visit(BaseModel)` và thay đổi decorator thành `@app.post("/api")`.
- Vietnamese inline notes - ghi chú giải thích:
  ```python
  from pydantic import BaseModel

  # Định nghĩa cấu trúc dữ liệu đầu vào của một cuộc khám bệnh
  class Visit(BaseModel):
      patient_name: str
      date_of_visit: str
      notes: str

  @app.post("/api") # Chuyển sang phương thức POST để nhận JSON payload
  def consultation_summary(
      visit: Visit, # FastAPI tự động gán và xác thực JSON gửi lên khớp với model Visit
      creds: HTTPAuthorizationCredentials = Depends(clerk_guard),
  ):
      user_id = creds.decoded["sub"]
      # ... logic dựng user prompt và gọi OpenAI completions API
  ```

### File `pages/product.tsx` - Consultation Form UI
- Purpose - mục đích: Xây dựng form nhập liệu y khoa và streaming kết quả qua POST request.
- Key logic - logic chính: Sử dụng `<DatePicker>` để chọn ngày khám và gửi yêu cầu POST bằng `fetchEventSource` với body JSON.
- Vietnamese inline notes - ghi chú giải thích:
  ```typescript
  import DatePicker from 'react-datepicker';

  // Trong component ConsultationForm
  await fetchEventSource('/api', {
      signal: controller.signal,
      method: 'POST', // Đổi phương thức gửi thành POST
      headers: {
          'Content-Type': 'application/json',
          Authorization: `Bearer ${jwt}`,
      },
      body: JSON.stringify({
          patient_name: patientName,
          // Định dạng ngày khám thành chuỗi yyyy-mm-dd gửi lên server
          date_of_visit: visitDate?.toISOString().slice(0, 10),
          notes,
      }),
      // ... onmessage, onerror
  });
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Trả kết quả AI dưới dạng Markdown thô (chọn trong bài học).
  - Pros - ưu điểm: Phát triển cực kỳ nhanh, giao diện frontend dễ dàng hiển thị streaming trực quan cho bác sĩ bằng thư viện `react-markdown`.
  - Cons - nhược điểm: Khó bóc tách thông tin để lưu trữ riêng lẻ vào database y tế, phụ thuộc hoàn toàn vào khả năng định dạng chính xác của LLM.
  - When to choose - khi nào chọn: Giai đoạn thử nghiệm MVP để kiểm chứng độ hữu ích của ứng dụng với người dùng.
- Option 2: Sử dụng tính năng Structured Outputs (JSON Schema của OpenAI).
  - Pros - ưu điểm: Đảm bảo kết quả trả về đúng định dạng cấu trúc JSON 100%, dễ dàng bóc tách để lưu trữ Summary, Next Steps và Email vào các cột database riêng biệt.
  - Cons - nhược điểm: Tăng độ phức tạp xử lý luồng streaming ở cả frontend và backend.
  - When to choose - khi nào chọn: Khi xây dựng phiên bản chính thức (Production-grade) cần tích hợp sâu vào hệ thống hồ sơ bệnh án điện tử (EHR) của bệnh viện.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lỗi **Method Not Allowed (HTTP 405)** khi gọi API.
  - Root cause - nguyên nhân gốc rễ: Frontend gọi request bằng phương thức GET trong khi backend FastAPI đã chuyển endpoint thành `@app.post("/api")` (hoặc ngược lại).
  - Symptom - dấu hiệu: Console trình duyệt báo lỗi đỏ 405 Method Not Allowed, kết nối API thất bại ngay lập tức.
  - Fix / prevention - sửa đổi / phòng ngừa: Đảm bảo cấu hình `method: 'POST'` trong `fetchEventSource` ở frontend và backend FastAPI sử dụng decorator `@app.post("/api")`.
- Failure mode: Lỗi **Date picker bị vỡ giao diện (lỗi vỡ layout CSS)**.
  - Root cause - nguyên nhân gốc rễ: Quên import stylesheet CSS của thư viện date picker bên thứ ba vào Next.js.
  - Symptom - dấu hiệu: Giao diện lịch chọn ngày hiển thị dạng danh sách chữ thô kéo dài, chồng chéo lên các thành phần khác.
  - Fix / prevention - sửa đổi / phòng ngừa: Đảm bảo đã thêm dòng `import 'react-datepicker/dist/react-datepicker.css';` trong file `pages/_app.tsx`.

## 11. Knowledge Extension - Kiến thức mở rộng
- Pydantic Validation Errors: Khi dữ liệu gửi lên API backend không khớp với định nghĩa của Pydantic (ví dụ: thiếu trường `patient_name` hoặc sai kiểu dữ liệu), FastAPI sẽ tự động trả về phản hồi lỗi HTTP 422 (Unprocessable Entity) kèm theo chi tiết các trường bị lỗi mà không cần chạy vào code nghiệp vụ chính. Điều này giúp ngăn chặn hoàn toàn việc gọi LLM bị lỗi do thiếu tham số.

## 12. Study Pack - Gói ôn tập
### Must remember
- Sử dụng Pydantic `BaseModel` để tự động hóa kiểm chứng và định kiểu dữ liệu JSON đầu vào trên backend FastAPI.
- Chuyển API sang phương thức POST khi cần truyền tải các biểu mẫu dữ liệu lớn hoặc phức tạp.
- stylesheet CSS của thư viện ngoài trong Next.js Pages Router phải được import tại `pages/_app.tsx`.
- Ghi nhận ID người dùng `creds.decoded["sub"]` ở API backend để phục vụ mục đích kiểm toán (auditing) và theo dõi lịch sử.

### Self-check questions
1. Pydantic giúp giải quyết bài toán gì khi xây dựng API RESTful bằng FastAPI?
2. Tại sao ta phải chuyển endpoint từ GET sang POST khi nâng cấp ứng dụng y khoa?
3. File `pages/_document.tsx` trong Next.js đóng vai trò gì?

### Flashcards
- Q: Lớp cơ sở dùng để định nghĩa lược đồ dữ liệu trong Pydantic là gì?
  A: `BaseModel`
- Q: Lỗi HTTP nào trả về khi dữ liệu đầu vào không hợp lệ so với mô hình Pydantic?
  A: `HTTP 422 Unprocessable Entity`
- Q: Phương thức HTTP nào được dùng để thay thế GET khi gửi form khám bệnh?
  A: `POST`

### Interview Q&A nếu phù hợp
- Q: Làm thế nào để xử lý các yêu cầu thay đổi prompt động theo chuyên khoa của bác sĩ (ví dụ: Khoa tim mạch cần prompt khác Khoa nhi)?
  A: Ta có thể thêm trường `specialty` vào Pydantic model `Visit`. Ở backend, xây dựng một hàm ánh xạ (mapping function) nhận vào `specialty` và trả về `system_prompt` tương ứng để truyền vào OpenAI API. Điều này giúp ứng dụng linh hoạt phục vụ nhiều nhóm bác sĩ khác nhau.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 21. Day 4 - Deploying Your Complete AI Healthcare App to Production on Vercel

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 21).
- Slide: Đã dùng (Trang sơ đồ kết nối Vercel Deployment và API key).
- Code: Đã dùng (Tham chiếu các file [day4.md](file:///G:/AIProduction_t6_2026/production/week1/day4.md) từ bước 5 đến bước 8).
- Summary lịch sử: Đã dùng (Đọc [day3_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day3_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin hoàn toàn đồng nhất. Quy trình deploy và chạy thử nghiệm dữ liệu thực tế khớp nhau giữa mã nguồn và transcript.

## 2. Executive Summary - Tóm tắt cốt lõi
- Cấu hình Landing Page mới: Cập nhật `pages/index.tsx` thành giao diện sản phẩm **MediNotes Pro** dành riêng cho bác sĩ, tối ưu hoá các linh kiện hiển thị theo trạng thái đăng nhập.
- Cập nhật thư viện backend: Bổ sung thư viện `pydantic` vào `requirements.txt` để đảm bảo Vercel serverless functions cài đặt và phân tích cú pháp dữ liệu chính xác khi deploy.
- Triển khai ứng dụng y tế: Thực hiện deploy mã nguồn sạch của ứng dụng từ repo `sass` lên môi trường production Vercel bằng lệnh CLI `vercel --prod`.
- Thực nghiệm luồng khám bệnh đầu-cuối: Test thử nghiệm nhập thông tin bệnh nhân (Ed Donna, ghi chú triệu chứng headache, khuyên dùng Tylenol/acetaminophen) và nhận về kết quả tóm tắt y khoa cực kỳ chính xác và lịch sự.
- Ý tưởng nâng cao ứng dụng (giáo viên gợi ý): Tích hợp thu âm đa phương thức (audio dictation), tự động gửi email báo cáo cho bệnh nhân qua Resend/SendGrid. Các tính năng này có thể phân bổ thành quyền hạn nâng cao cho các tier thanh toán khác nhau trong Clerk Billing.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu sự cần thiết của việc đồng bộ các file cấu hình thư viện (`requirements.txt`, `package.json`) trước khi chạy deploy trên cloud.
  - Nắm vững cơ chế phân loại giao diện Next.js động dựa trên các component điều kiện của Clerk.
  - Hiểu quy trình xử lý dữ liệu và định dạng phản hồi chuẩn y khoa của các mô hình LLM lớn.
- Practical goals - mục tiêu thực hành:
  - Viết lại Landing Page theo định hướng thương mại y tế.
  - Đồng bộ hoá các gói thư viện Python trên Vercel.
  - Deploy dự án bằng lệnh CLI và thực hiện kiểm thử dữ liệu bệnh nhân thực tế.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích lý do tại sao thiếu thư viện trong `requirements.txt` lại khiến Vercel deploy lỗi hoặc crash serverless function.
  - Giải thích các hướng mở rộng (SendGrid, Resend, Multimodal audio) giúp nâng cao giá trị thương mại cho sản phẩm SaaS.

## 4. Previous Context - Liên hệ với bài trước
Bài học này nối tiếp trực tiếp sau Bài 20. Sau khi đã viết xong code form nhập liệu và backend POST endpoint, bài học này đưa toàn bộ ứng dụng y tế lên chạy trực tiếp trên Internet.

## 5. Core Theory - Lý thuyết cốt lõi
- Deployment synchronization - đồng bộ hóa triển khai:
  - Meaning - nghĩa: Quy trình đảm bảo tất cả các file cấu hình thư viện ở cả frontend (`package.json`) và backend (`requirements.txt`) được cập nhật đầy đủ trước khi thực hiện đóng gói và deploy.
  - Why it matters - vì sao quan trọng: Tránh tình trạng ứng dụng chạy bình thường trên localhost nhưng bị crash khi chạy trên môi trường serverless thực tế do thiếu thư viện.
- EHR (Electronic Health Record) - hồ sơ bệnh án điện tử:
  - Meaning - nghĩa: Hệ thống lưu trữ thông tin sức khỏe của bệnh nhân dưới dạng số hóa, được chia sẻ giữa các cơ sở y tế.
  - Why it matters - vì sao quan trọng: Đây là đích đến cuối cùng của dữ liệu tóm tắt y khoa được tạo ra bởi bác sĩ.
- Multimodal input - đầu vào đa phương thức:
  - Meaning - nghĩa: Khả năng hệ thống tiếp nhận và xử lý đồng thời nhiều định dạng dữ liệu đầu vào khác nhau (văn bản, âm thanh ghi âm, hình ảnh).
  - Why it matters - vì sao quan trọng: Giúp bác sĩ rảnh tay hơn bằng cách ghi âm trực tiếp cuộc hội thoại khám bệnh và để AI tự động chuyển thành văn bản thô.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình Deploy & Kiểm thử Production (Production Deployment & Testing Workflow):
1. Input: Code và form nhập liệu của y khoa đã chạy ổn định cục bộ.
2. Processing steps:
   - Cập nhật Landing Page `pages/index.tsx` và thêm `pydantic` vào `requirements.txt`.
   - Chạy lệnh `vercel --prod` trên Terminal để Vercel đóng gói và tải ứng dụng lên server.
   - Truy cập URL production, nhấn Sign In để đăng nhập hệ thống.
   - Nhấp vào "Open Consultation Assistant" để vào protected route `/product`.
   - Nhập tên bệnh nhân "Ed Donna", chọn ngày khám hôm nay, và gõ ghi chú thô: "Ed complained of headache. Told him to take two Tylenol and come back in two days".
   - Nhấp Generate Summary và chờ luồng dữ liệu stream về.
3. Output: Xem kết quả phân thành 3 mục chuyên nghiệp và kiểm tra tính chính xác của các thuật ngữ y khoa (ví dụ: AI tự đổi Tylenol thành acetaminophen).

## 7. Techniques - Kỹ thuật sử dụng
- Local validation before deploy - xác minh cục bộ trước khi deploy:
  - Purpose - mục đích: Chạy thử và lưu toàn bộ file trước khi chạy lệnh deploy của Vercel để tránh lỗi thiếu file cấu hình hoặc lỗi cú pháp.
  - When to use - dùng khi nào: Trước mỗi lần chạy lệnh build/deploy production.
  - Trade-off - đánh đổi: Tốn thêm thời gian rà soát thủ công các tệp tin cấu hình.
  - Common mistake - lỗi dễ gặp: Quên lưu file `requirements.txt` khiến bản build trên cloud chạy phiên bản cũ.
- Demo sandbox labeling - gắn nhãn thử nghiệm sandbox:
  - Purpose - mục đích: Đưa ra thông báo "For demonstration purposes only" rõ ràng trên giao diện ứng dụng.
  - When to use - dùng khi nào: Khi xây dựng các ứng dụng y tế, tài chính ở dạng thử nghiệm để tránh các trách nhiệm pháp lý ngoài ý muốn.
  - Trade-off - đánh đổi: Làm giảm đi một chút tính chân thực của sản phẩm đối với khách hàng trải nghiệm thử.
  - Common mistake - lỗi dễ gặp: Khẳng định ứng dụng đã đạt các chuẩn bảo mật (như HIPAA) khi chưa qua các đợt đánh giá kiểm toán thực tế.

## 8. Code Walkthrough - Phân tích code nếu có
### File `pages/index.tsx` - Phân phối giao diện theo trạng thái đăng nhập
- Purpose - mục đích: Hiển thị giao diện Landing page y tế và điều hướng bác sĩ.
- Key logic - logic chính: Sử dụng component `<SignedIn>` và `<SignedOut>` để ẩn hiện nút bấm truy cập trang `/product`.
- Vietnamese inline notes - ghi chú giải thích:
  ```typescript
  import Link from 'next/link';
  import { SignInButton, SignedIn, SignedOut, UserButton } from '@clerk/nextjs';

  export default function Home() {
    return (
      <main className="min-h-screen bg-gradient-to-br from-gray-50 to-gray-100">
        {/* Navigation */}
        <nav className="flex justify-between items-center mb-12">
          <h1 className="text-2xl font-bold">MediNotes Pro</h1>
          <div>
            {/* Nếu bác sĩ chưa đăng nhập, hiển thị nút Sign In modal */}
            <SignedOut>
              <SignInButton mode="modal">
                <button className="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-6 rounded-lg">
                  Sign In
                </button>
              </SignInButton>
            </SignedOut>
            {/* Nếu bác sĩ đã đăng nhập, hiển thị nút Go to App và nút User profile */}
            <SignedIn>
              <div className="flex items-center gap-4">
                <Link 
                  href="/product" 
                  className="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-6 rounded-lg"
                >
                  Go to App
                </Link>
                <UserButton showName={true} />
              </div>
            </SignedIn>
          </div>
        </nav>
        {/* ... các section giới thiệu tính năng */}
      </main>
    );
  }
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có so sánh công nghệ cụ thể trong bài thực hành này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lỗi **Server Error (HTTP 500)** khi gọi API sau khi deploy lên Vercel.
  - Root cause - nguyên nhân gốc rễ: Quên thêm thư viện `pydantic` vào file cấu hình `requirements.txt`. Backend chạy bình thường ở localhost vì thư viện đã được cài sẵn trong môi trường ảo cục bộ, nhưng Vercel không thể build function do thiếu dependencies.
  - Symptom - dấu hiệu: Frontend báo lỗi kết nối, tab Network của trình duyệt hiển thị mã lỗi 500 khi gửi POST request.
  - Fix / prevention - sửa đổi / phòng ngừa: Thêm dòng `pydantic` vào file `requirements.txt`, lưu lại tệp tin và chạy lại lệnh deploy `vercel --prod`.

## 11. Knowledge Extension - Kiến thức mở rộng
- EHR Integration standards (Các tiêu chuẩn tích hợp EHR): Trong thực tế, để ứng dụng y tế AI có thể thương mại hóa sâu rộng, nó phải hỗ trợ các tiêu chuẩn giao tiếp dữ liệu y tế quốc tế như HL7 (Health Level Seven) hoặc FHIR (Fast Healthcare Interoperability Resources). Điều này giúp dữ liệu thô từ AI được phân tách thành các trường tiêu chuẩn và lưu trữ trực tiếp vào các phần mềm quản lý bệnh viện lớn.

## 12. Study Pack - Gói ôn tập
### Must remember
- Đồng bộ dependencies (`requirements.txt`) là bắt buộc để Vercel build serverless function thành công.
- Sử dụng các nút bấm động của Clerk để tối ưu hóa luồng chuyển hướng của bác sĩ từ Landing page.
- Đặt cảnh báo giới hạn trách nhiệm y khoa khi triển khai các ứng dụng demo y tế công cộng.
- AI có khả năng tự động chuẩn hóa các thuật ngữ thô của bác sĩ sang thuật ngữ y khoa chuẩn (như Tylenol thành acetaminophen).

### Self-check questions
1. Tại sao ứng dụng lại chạy thành công trên máy tính cá nhân nhưng lại báo lỗi HTTP 500 khi lên Vercel?
2. FHIR hay HL7 đóng vai trò gì trong việc tích hợp trợ lý AI vào bệnh viện?
3. Làm cách nào để phân biệt giao diện Next.js cho người dùng đã đăng nhập và chưa đăng nhập trên Landing Page?

### Flashcards
- Q: Lệnh deploy production của Vercel CLI là gì?
  A: `vercel --prod`
- Q: Thư viện python nào cần thêm vào requirements.txt để validate dữ liệu y tế đầu vào?
  A: `pydantic`
- Q: Thuật ngữ y khoa chuẩn của Tylenol do AI tự động nhận dạng là gì?
  A: `acetaminophen`

### Interview Q&A nếu phù hợp
- Q: Làm thế nào để tự động gửi bản báo cáo y khoa này trực tiếp về email của bệnh nhân một cách an toàn?
  A: Ta có thể tích hợp thư viện email như Resend hoặc SendGrid ở backend FastAPI. Sau khi nhận kết quả từ OpenAI, backend sẽ gửi một email chứa nội dung Draft Email (đã được định dạng HTML sạch sẽ) tới địa chỉ email của bệnh nhân (có thể lưu trữ trong database hoặc nhập từ form).

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 22. Day 4 - Building a Production Healthcare AI SaaS with Streaming LLMs

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 22).
- Slide: Đã dùng (Trang tóm tắt kiến trúc 4 ngày đầu khóa học).
- Code: Đã dùng (Tham chiếu các file cấu hình và source code của toàn bộ tuần 1).
- Summary lịch sử: Đã dùng (Đọc [day3_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day3_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin hoàn toàn đồng nhất. Báo cáo tổng kết tuần 1 và cảnh báo về mức độ phức tạp của ngày tiếp theo được mô tả đồng điệu giữa slide và transcript.

## 2. Executive Summary - Tóm tắt cốt lõi
- Tổng kết tiến trình 4 ngày đầu khóa học: Xây dựng Next.js frontend (Pages Router, TypeScript, Tailwind CSS, client-side rendering) và FastAPI backend (truyền nhận JSON tự động đóng gói bằng Pydantic model).
- Tóm tắt hạ tầng Vercel: Cơ chế triển khai nhanh gọn qua Vercel CLI với các môi trường dev (`vercel dev`), preview (`vercel`), và production (`vercel --prod`).
- Định hình bảo mật và thương mại: Sử dụng Clerk để xác thực người dùng, tích hợp Clerk Billing (hoặc Stripe) quản lý gói thuê bao trả phí.
- Phân tích bản chất AI trong SaaS: Bài học chỉ ra cuộc gọi LLM chỉ là một thành phần phụ (side note) trong toàn bộ bức tranh kiến trúc sản phẩm. Học phần thực sự quan trọng là Platform Engineering và DevOps (cấu hình, triển khai, mạng bảo mật, môi trường).
- Báo hiệu chặng đường tiếp theo (Day 5): Chuyển đổi từ mô hình PaaS (Vercel) sang IaaS (AWS). Day 5 sẽ là một ngày học cực kỳ nặng nhọc ("lot of sweat" và "gritting of teeth") yêu cầu cài đặt AWS IAM, Docker containerization, AWS ECR và AWS App Runner.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Nhận thức sự khác biệt bản chất giữa các nền tảng PaaS (Vercel) và IaaS (AWS).
  - Nắm vững cấu trúc tổng quan của một sản phẩm Full-stack AI SaaS chuyên nghiệp.
  - Hiểu vai trò của việc đóng gói container trong chu kỳ bàn giao phần mềm.
- Practical goals - mục tiêu thực hành:
  - Rà soát lại toàn bộ kiến thức full-stack đã học trong 4 ngày đầu.
  - Chuẩn bị tâm lý và công cụ cho giai đoạn di chuyển hạ tầng lên AWS ở Day 5.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích tại sao AI chỉ là một phần nhỏ trong ứng dụng SaaS thực tế.
  - Phân tích ưu và nhược điểm về khả năng tự động hóa của Vercel so với tính linh hoạt của AWS.

## 4. Previous Context - Liên hệ với bài trước
Bài học này đóng vai trò là một mốc chốt chặn lý thuyết (recap checkpoint), khép lại toàn bộ chặng đường phát triển và triển khai nhanh trên Vercel từ Day 1 đến Day 4, chuẩn bị chuyển giao hoàn toàn sang hạ tầng công nghiệp AWS ở Day 5.

## 5. Core Theory - Lý thuyết cốt lõi
- Platform as a Service (PaaS) - nền tảng như một dịch vụ:
  - Meaning - nghĩa: Mô hình điện toán đám mây cung cấp sẵn hệ điều hành, runtime và công cụ build giúp lập trình viên chỉ cần tập trung vào viết code và deploy nhanh (ví dụ: Vercel).
  - Why it matters - vì sao quan trọng: Giúp đưa sản phẩm ra thị trường cực nhanh trong giai đoạn đầu của startup mà không tốn chi phí vận hành hệ thống.
- Infrastructure as a Service (IaaS) - hạ tầng như một dịch vụ:
  - Meaning - nghĩa: Mô hình điện toán cung cấp tài nguyên phần cứng thô (mạng, máy chủ ảo, ổ cứng) yêu cầu lập trình viên phải tự cài đặt cấu hình hệ điều hành và phần mềm (ví dụ: AWS).
  - Why it matters - vì sao quan trọng: Mang lại sự tự do tối đa về kiến trúc, kiểm soát bảo mật tuyệt đối và chi phí cực rẻ khi chạy ở quy mô lớn.
- Industrial-grade deployment - triển khai cấp công nghiệp:
  - Meaning - nghĩa: Quy trình đưa ứng dụng lên các hạ tầng đám mây lớn được quản trị nghiêm ngặt về phân quyền (IAM), tối ưu hóa cấu hình tự động co giãn (auto-scaling) và giám sát chi tiết tài chính.
  - Why it matters - vì sao quan trọng: Đảm bảo phần mềm hoạt động bền bỉ, an toàn và sẵn sàng phục vụ hàng triệu người dùng thương mại.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
`Không có pipeline rõ ràng trong tài liệu nguồn`
Bài học này mang tính chất tổng kết chặng đường phát triển Next.js/FastAPI trên PaaS và phác thảo tư duy chuyển đổi hạ tầng đám mây nên không chứa quy trình xử lý dữ liệu kỹ thuật cụ thể.

## 7. Techniques - Kỹ thuật sử dụng
- PaaS to IaaS migration planning - lập kế hoạch di chuyển từ PaaS sang IaaS:
  - Purpose - mục đích: Chuẩn bị quy trình chuyển đổi ứng dụng chạy serverless trên Vercel sang dạng đóng gói Docker chạy trên AWS.
  - When to use - dùng khi nào: Khi sản phẩm SaaS bắt đầu có lượng người dùng lớn và yêu cầu bảo mật/kiểm soát chi phí chặt chẽ hơn.
  - Trade-off - đánh đổi: Tốn rất nhiều công sức cấu hình ban đầu, đòi hỏi kiến thức sâu sắc về hệ thống mạng đám mây.
  - Common mistake - lỗi dễ gặp: Chuyển đổi hạ tầng quá sớm khi sản phẩm chưa có độ khớp thị trường (product-market fit), gây lãng phí nguồn lực kỹ thuật.

## 8. Code Walkthrough - Phân tích code nếu có
`Code được cung cấp trong session nhưng chưa thấy code liên quan trực tiếp tới lesson này.`
(Bài học này tập trung tổng kết lý thuyết chặng đường phát triển Next.js + FastAPI và định hướng cloud).

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Triển khai trên Vercel (PaaS).
  - Pros - ưu điểm: Đơn giản tối đa, deploy trong vài giây, tự động cấu hình SSL và CDN toàn cầu.
  - Cons - nhược điểm: Chi phí tăng rất nhanh khi scale lớn, giới hạn tùy biến hạ tầng mạng và serverless execution timeout.
  - When to choose - khi nào chọn: Các ứng dụng MVP, dự án cá nhân hoặc startup giai đoạn đầu cần kiểm chứng ý tưởng.
- Option 2: Triển khai trên AWS (IaaS).
  - Pros - ưu điểm: Khả năng tùy biến vô hạn, bảo mật cấp doanh nghiệp, chi phí tối ưu khi chạy quy mô cực lớn.
  - Cons - nhược điểm: Độ phức tạp cấu hình cực kỳ cao, tốn nhiều công sức bảo trì và vận hành hệ thống.
  - When to choose - khi nào chọn: Khi sản phẩm đã ổn định thị trường và bắt đầu phục vụ các khách hàng doanh nghiệp (B2B SaaS).

## 10. Pitfalls - Lỗi / bẫy thường gặp
Không có lỗi kỹ thuật trực tiếp nào được ghi nhận ngoài lời cảnh báo về việc dễ nản lòng khi tiếp cận cấu hình AWS phức tạp vào ngày hôm sau.

## 11. Knowledge Extension - Kiến thức mở rộng
- AWS App Runner: Dịch vụ container được quản lý hoàn toàn (fully managed) của AWS, giúp dễ dàng deploy ứng dụng web và API được đóng gói bằng Docker nhanh chóng, tự động co giãn và cân bằng tải. Đây là cầu nối chuyển tiếp mượt mà cho các lập trình viên chuyển từ Vercel sang AWS mà không cần tự cấu hình các tài nguyên mạng (VPC, Subnets) phức tạp.

## 12. Study Pack - Gói ôn tập
### Must remember
- Kiến trúc Full-stack AI SaaS gồm: Next.js (Pages Router, TypeScript, Tailwind) + FastAPI (Pydantic model validation) + Clerk (Auth & Billing).
- Cuộc gọi API LLM chỉ là một thành phần nghiệp vụ phụ; Platform Engineering và DevOps mới là nền móng cốt lõi giúp vận hành sản phẩm SaaS.
- Vercel CLI hỗ trợ ba môi trường phát triển: dev (`vercel dev`), preview (`vercel`), và production (`vercel --prod`).
- Deploy trên các đám mây lớn (AWS, GCP, Azure) cung cấp độ bền bỉ, tính co giãn và bảo mật cấp công nghiệp.

### Self-check questions
1. Sự khác biệt lớn nhất giữa mô hình PaaS (Vercel) và mô hình IaaS (AWS) là gì?
2. Tại sao tác giả nói AI chỉ là một thành phần "side note" trong kiến trúc SaaS?
3. AWS App Runner giúp ích gì cho các lập trình viên khi di chuyển từ Vercel sang AWS?

### Flashcards
- Q: Mô hình dịch vụ điện toán đám mây của Vercel là gì?
  A: PaaS (Platform as a Service).
- Q: Nền tảng IaaS đại diện chính trong bài học tiếp theo là gì?
  A: AWS (Amazon Web Services).
- Q: Lệnh dùng để chạy thử frontend Next.js cục bộ trên máy tính là gì?
  A: `vercel dev`

### Interview Q&A nếu phù hợp
- Q: Khi được yêu cầu di chuyển một ứng dụng web AI từ Vercel sang AWS, bước chuẩn bị quan trọng nhất về mặt đóng gói phần mềm là gì?
  A: Đó là việc container hóa ứng dụng bằng Docker. Ta cần viết các tệp tin `Dockerfile` để đóng gói riêng biệt Next.js frontend và FastAPI backend thành các Docker Images, đảm bảo ứng dụng có thể chạy đồng nhất trên bất kỳ hạ tầng nào của AWS.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.



