# Day 2 Summary: Building Full-Stack AI Applications (Next.js & FastAPI)

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

---

# 9. Day 2 - Building Full-Stack AI Apps - Frontend-Backend Architecture for LLMs

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 9).
- Slide: Đã dùng (Trang 1, 3, 4, 5).
- Code: Không có (Bài học này thuần lý thuyết nền tảng).
- Summary lịch sử: Đã dùng (Đọc [day1_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day1_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin hoàn toàn đồng nhất. Slide tóm lược cấu trúc bài học và transcript giải thích chi tiết các thuật ngữ cốt lõi.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học mở đầu ngày học thứ 2 bằng việc đặt viên gạch nền móng lý thuyết cho kiến trúc full-stack (toàn diện cả frontend và backend) thay vì chỉ chạy backend API đơn lẻ như ngày 1.
- Frontend được định nghĩa là mã nguồn chạy trực tiếp trên browser (trình duyệt) của người dùng, sử dụng HTML cho structure (cấu trúc), CSS cho appearance (giao diện) và JavaScript/TypeScript cho interactivity (tính tương tác).
- Backend được định nghĩa là logic nghiệp vụ chạy trên server (máy chủ), chịu trách nhiệm quản lý database (cơ sở dữ liệu), thực hiện gọi LLM, tích hợp các API bên ngoài và bảo mật secrets (thông tin nhạy cảm).
- Giao tiếp giữa frontend và backend dựa trên mô hình request-response (yêu cầu - phản hồi) qua HTTP bằng định dạng dữ liệu JSON phổ biến, hoặc backend có thể render (dựng hình) toàn bộ trang web để trả về cho trình duyệt.
- Giảng viên phân tích cơ chế hoạt động của Gradio (framework Python tự động sinh frontend phía sau hậu trường) và nêu lý do khóa học này không sử dụng Gradio để hướng học viên tới việc xây dựng các ứng dụng web thực tế, chuyên nghiệp ("for reals").
- Tiến trình phát triển công nghệ frontend được phác thảo qua 3 cột mốc: Vanilla HTML/CSS/JS (sử dụng jQuery, tương tác DOM trực tiếp) -> Frontend Frameworks (React, Vue, Angular với mô hình SPA - Single Page Application) -> Application Frameworks (Next.js tích hợp sẵn routing, data fetching và SSR).

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Phân biệt rõ vai trò và trách nhiệm của frontend (chạy trên client browser) và backend (chạy trên server).
  - Hiểu cách thức giao tiếp client-server qua giao thức HTTP (gửi request và nhận về JSON hoặc HTML).
  - Nắm được cơ chế hoạt động của Gradio (python backend tự động sinh HTML/JS tĩnh) và nhược điểm của nó trong môi trường sản xuất.
  - Hiểu lộ trình phát triển của công nghệ frontend qua các giai đoạn từ vanilla HTML đến các framework Next.js hiện đại.
- Practical goals - mục tiêu thực hành:
  - Có khả năng tư duy thiết kế hệ thống phân tách rõ ràng luồng dữ liệu giữa giao diện người dùng và máy chủ logic.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích được cấu trúc cơ bản của một ứng dụng web full-stack thông thường.
  - Trình bày được khái niệm DOM (Document Object Model) và Single Page Application (SPA).
  - Giải thích tại sao backend lại là nơi an toàn duy nhất để gọi LLM và lưu trữ API keys.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Day 1 ([day1_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day1_summary.md)): Sau khi học viên đã làm quen với việc triển khai nhanh ứng dụng backend FastAPI đơn giản lên Vercel, bài học này nâng cấp tư duy của học viên lên cấp độ thiết kế hệ thống full-stack bằng cách giới thiệu cấu trúc frontend chuyên nghiệp sẽ kết hợp với backend FastAPI.

## 5. Core Theory - Lý thuyết cốt lõi
- Frontend - giao diện người dùng:
  - Meaning - nghĩa: Phần mã nguồn thực thi trực tiếp trên thiết bị của người dùng thông qua trình duyệt web, bao gồm HTML, CSS và JavaScript/TypeScript.
  - Why it matters - vì sao quan trọng: Là nơi trực tiếp tương tác với người dùng cuối, quyết định trải nghiệm người dùng (UX) và tính trực quan của ứng dụng.
- Backend - máy chủ dịch vụ:
  - Meaning - nghĩa: Phần mã nguồn chạy trên máy chủ vật lý hoặc máy chủ đám mây, xử lý các tính toán nặng, lưu trữ dữ liệu và giao tiếp với các API bên thứ ba.
  - Why it matters - vì sao quan trọng: Đảm bảo tính bảo mật của hệ thống bằng cách che giấu mã nguồn logic, các khóa bí mật (API keys) và quản trị tính toàn vẹn của dữ liệu.
- API contract - hợp đồng API:
  - Meaning - nghĩa: Sự thống nhất về cấu trúc dữ liệu truyền nhận giữa frontend và backend (ví dụ: frontend gửi JSON dạng nào và backend trả về JSON định dạng nào).
  - Why it matters - vì sao quan trọng: Giúp hai nhóm lập trình viên frontend và backend làm việc độc lập mà không lo ngại xung đột tích hợp hệ thống.
- Document Object Model (DOM) - mô hình đối tượng tài liệu:
  - Meaning - nghĩa: Cấu trúc dữ liệu dạng cây do trình duyệt tạo ra để biểu diễn giao diện HTML của trang web, cho phép JavaScript có thể đọc và thay đổi giao diện động.
  - Why it matters - vì sao quan trọng: Là đối tượng trung gian giúp các mã script tương tác trực tiếp với giao diện người dùng.
- Single Page Application (SPA) - ứng dụng đơn trang:
  - Meaning - nghĩa: Kiến trúc ứng dụng web trong đó trình duyệt chỉ tải mã nguồn HTML/JS một lần duy nhất, các thao tác chuyển trang tiếp theo chỉ là việc vẽ lại DOM qua dữ liệu lấy từ API.
  - Why it matters - vì sao quan trọng: Giúp chuyển đổi giao diện cực kỳ mượt mà, giảm latency (độ trễ) tải trang và tạo cảm giác như ứng dụng máy tính cục bộ.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
`Không có pipeline rõ ràng trong tài liệu nguồn`
Thay vào đó là luồng trao đổi dữ liệu (data flow) chuẩn trong kiến trúc Full-stack AI:
1. Input: Người dùng click vào một button trên trình duyệt (ví dụ: "Generate Idea").
2. Processing steps:
   - Frontend bắt sự kiện click, đóng gói yêu cầu và gửi một HTTP request tới endpoint `/api` của Backend.
   - Backend tiếp nhận request, gọi API của LLM (OpenAI) để xử lý logic, nhận kết quả và đóng gói thành JSON object.
   - Backend phản hồi HTTP response chứa JSON về cho Frontend.
   - Frontend nhận JSON, dùng JavaScript phân tích dữ liệu và cập nhật DOM để hiển thị kết quả cho người dùng.
3. Output: Giao diện web được vẽ lại động với ý tưởng kinh doanh mới mà không cần reload (tải lại) toàn bộ trang.

## 7. Techniques - Kỹ thuật sử dụng
- Separation of Concerns (SoC) - phân tách mối quan tâm:
  - Purpose - mục đích: Tách biệt rõ ràng phần hiển thị (Frontend) và phần xử lý logic/dữ liệu (Backend).
  - When to use - dùng khi nào: Áp dụng cho mọi dự án phần mềm thương mại từ nhỏ đến lớn để dễ bảo trì và nâng cấp.
  - Trade-off - đánh đổi: Phải thiết lập thêm tầng API giao tiếp và quản lý hai môi trường runtime khác nhau (browser vs server).
  - Common mistake - lỗi dễ gặp: Viết các logic xử lý nghiệp vụ quan trọng hoặc lưu API key trực tiếp ở frontend.

## 8. Code Walkthrough - Phân tích code nếu có
`Code được cung cấp trong session nhưng chưa thấy code liên quan trực tiếp tới lesson này.`
(Bài học này tập trung vào định nghĩa kiến trúc và các khái niệm lý thuyết frontend sơ khởi).

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Sử dụng Gradio làm giao diện người dùng.
  - Pros: Phát triển siêu nhanh hoàn toàn bằng Python, không cần viết HTML/CSS/JS, rất phù hợp làm prototype.
  - Cons: Không thể tùy biến sâu giao diện, hiệu năng chịu tải kém, không phù hợp cho sản phẩm SaaS thương mại thực tế.
  - When to choose: Khi cần làm bản demo nhanh (PoC) trong vài giờ để kiểm tra tính khả thi của model AI.
- Option 2: Thiết kế Frontend (Next.js/React) và Backend (FastAPI) tách biệt.
  - Pros: Tự do tùy biến giao diện, tối ưu hóa hiệu năng cực tốt, chuẩn cấu trúc công nghiệp SaaS chuyên nghiệp.
  - Cons: Phức tạp hơn, yêu cầu kiến thức ở cả hai phía (JavaScript/TypeScript và Python).
  - When to choose: Khi xây dựng dự án SaaS thương mại thực tế để đưa ra thị trường cho người dùng trả phí.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lộ OpenAI API key hoặc các private keys.
  - Root cause - nguyên nhân gốc rễ: Gọi trực tiếp API OpenAI từ mã nguồn frontend (browser). Người dùng chỉ cần F12 mở tab Network là có thể lấy cắp key.
  - Symptom - dấu hiệu: Tài khoản OpenAI bị trừ tiền vô tội vạ hoặc bị khóa do quá hạn mức.
  - Fix / prevention - sửa đổi / phòng ngừa: Luôn gọi LLM thông qua server backend. Server backend sẽ giữ API key trong biến môi trường an toàn và không bao giờ trả key về phía frontend.

## 11. Knowledge Extension - Kiến thức mở rộng
- Edge Network - mạng lưới biên: Khi triển khai Next.js lên Vercel, các file tĩnh (HTML, CSS, JS) được lưu trữ tại các CDN (mạng phân phối nội dung) sát với vị trí địa lý của người dùng nhất để giảm tối đa thời gian tải trang ban đầu. Đây là lý do Vercel giúp frontend chạy cực kỳ nhanh trên toàn thế giới.

## 12. Study Pack - Gói ôn tập
### Must remember
- Frontend thực thi trên browser; Backend thực thi trên server.
- Giao tiếp client-server chủ yếu qua HTTP requests sử dụng định dạng JSON.
- Single Page Application (SPA) giúp trang web không cần reload toàn bộ khi chuyển hướng.
- Không bao giờ đặt API keys hoặc gọi LLM trực tiếp từ phía client frontend.
- Gradio chỉ dùng cho demo, Next.js + FastAPI là cặp bài trùng tiêu chuẩn cho full-stack AI SaaS.

### Self-check questions
- Hãy giải thích vai trò của HTML, CSS và JavaScript trong một tệp frontend?
- Tại sao cơ chế SPA lại cải thiện đáng kể trải nghiệm người dùng so với mô hình web truyền thống?
- Điểm khác biệt lớn nhất giữa Gradio và Next.js trong cách tạo ra mã nguồn frontend là gì?

### Flashcards
- Q: DOM là viết tắt của từ gì?
  A: Document Object Model - Mô hình đối tượng tài liệu biểu diễn HTML dưới dạng cây.
- Q: Giao thức truyền tải chính được dùng để frontend gửi dữ liệu đến backend là gì?
  A: HTTP (Hypertext Protocol).

### Interview Q&A nếu phù hợp
- Q: Tại sao bạn lại chọn kiến trúc chia tách Frontend và Backend cho một ứng dụng AI thay vì xây dựng một monolith application (ứng dụng nguyên khối) bằng Django?
  A: Chia tách Frontend (Next.js) và Backend (FastAPI) giúp tối ưu hóa hiệu năng cho từng thành phần. FastAPI cực kỳ nhẹ và nhanh, tối ưu hóa cho các tác vụ bất đồng bộ (async) như streaming dữ liệu từ LLM. Next.js giúp tối ưu hóa SEO và phân phối tĩnh nhanh qua CDN biên. Ngoài ra, việc tách biệt giúp hai đội phát triển hoạt động độc lập và dễ dàng scale up riêng lẻ từng phần khi lượng user tăng.

## 13. Missing Inputs - Còn thiếu gì
Không có tài nguyên bị thiếu cho bài học này.

---

# 10. Day 2 - Building Full-Stack AI Apps with React, FastAPI, and NextJS

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 10).
- Slide: Đã dùng (Trang 2, 6, 7, 8, 9).
- Code: Không có (Bài học này tập trung giải thích lý thuyết chi tiết về React, Next.js và FastAPI).
- Summary lịch sử: Đã dùng (Day 1 summary).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Mọi thông tin đều đồng nhất. Sơ đồ lộ trình học và phân tích ưu nhược điểm các backend framework trong slide khớp hoàn toàn với bài giảng.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học đi sâu vào chi tiết của React - một JavaScript library phổ biến nhất thế giới để xây dựng giao diện dựa trên component (thành phần tái sử dụng).
- React mang tính declarative (khai báo): lập trình viên chỉ cần mô tả giao diện sẽ trông thế nào ứng với từng trạng thái dữ liệu (state), React sẽ tự động cập nhật DOM một cách hiệu quả nhất thay vì phải thao tác DOM thủ công.
- Hai khái niệm cốt lõi của React được định nghĩa: `Props` (các thuộc tính truyền dữ liệu từ component cha xuống component con) và `State` (trạng thái dữ liệu nội bộ của component, khi state thay đổi, component sẽ re-render).
- JSX và TSX được giới thiệu dưới dạng cú pháp lai trực quan giữa HTML và JS/TS, giúp mã nguồn trở nên gọn gàng, tăng năng suất coding.
- Next.js (phát triển bởi Vercel) được giới thiệu như một framework mạnh mẽ xây dựng trên React, tích hợp sẵn routing và hỗ trợ hai loại router: Pages Router (thư mục `/pages` - cổ điển, ổn định) và App Router (thư mục `/app` - hiện đại, mạnh mẽ).
- Khóa học quyết định sử dụng Pages Router cho tuần đầu tiên vì framework xác thực người dùng (authentication) tích hợp ở các bài sau chỉ tương thích tốt nhất với Pages Router.
- So sánh các backend framework Python: Django (battery-included, nặng, có sẵn ORM và admin UI), Flask (micro-framework, cực nhẹ và linh hoạt nhưng phải tự cấu hình mọi thứ), FastAPI (nằm giữa, hiện đại, hỗ trợ async và tích hợp sẵn Pydantic để định nghĩa schema). FastAPI được chọn xuyên suốt khóa học.
- Ed Donner giới thiệu cấu trúc phân chia repository (kho mã nguồn): mỗi tuần học sẽ có một repo riêng (tuần 1 là repo `production`) để học viên quen với quy trình thiết lập dự án SaaS thực tế từ đầu.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cách thức hoạt động của React (declarative UI, Virtual DOM cập nhật các phần thay đổi thay vì vẽ lại toàn bộ).
  - Nắm vững sự khác biệt và vai trò của `Props` và `State` trong quản lý vòng đời component.
  - Phân biệt được Pages Router và App Router trong cấu trúc dự án Next.js.
  - Hiểu quy trình transpiling (biên dịch) TypeScript thành vanilla JavaScript để trình duyệt hiểu được.
  - Nắm được đặc tính của các python backend framework (Django vs Flask vs FastAPI).
- Practical goals - mục tiêu thực hành:
  - Định hình cấu trúc thư mục của một dự án SaaS full-stack sử dụng Next.js làm frontend và FastAPI làm backend.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích sự khác nhau giữa Props và State.
  - Giải thích lý do lựa chọn Pages Router thay vì App Router trong tuần này của khóa học.
  - Trình bày được ưu điểm của việc sử dụng FastAPI kết hợp với Pydantic.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Lesson 9: Sau khi nắm vững bức tranh tổng quan frontend-backend, bài học này đi sâu vào chi tiết kỹ thuật của React, Next.js và FastAPI - bộ ba công nghệ sẽ trực tiếp cấu thành ứng dụng Business Idea Generator trong phần thực hành tiếp theo.

## 5. Core Theory - Lý thuyết cốt lõi
- Props - thuộc tính component:
  - Meaning - nghĩa: Dữ liệu cấu hình được truyền từ một component cha xuống một component con, có tính chất read-only (chỉ đọc) đối với component nhận.
  - Why it matters - vì sao quan trọng: Giúp tái sử dụng các component với các hiển thị dữ liệu khác nhau (ví dụ: một button component nhận props màu sắc khác nhau).
- State - trạng thái dữ liệu:
  - Meaning - nghĩa: Đối tượng dữ liệu nội bộ được quản lý bên trong một component, có thể thay đổi theo thời gian thông qua các tương tác của người dùng.
  - Why it matters - vì sao quan trọng: Khi state thay đổi, React sẽ tự động kích hoạt quá trình render lại component để giao diện luôn đồng bộ với dữ liệu.
- JSX/TSX - cú pháp lai:
  - Meaning - nghĩa: Tiêu chuẩn mở rộng cú pháp cho JavaScript/TypeScript cho phép viết các thẻ HTML trực tiếp bên trong file logic code.
  - Why it matters - vì sao quan trọng: Giúp code trực quan, dễ đọc, dễ viết và tránh việc phải ghép chuỗi HTML thủ công bằng JavaScript.
- Transpiling - biên dịch mã:
  - Meaning - nghĩa: Quá trình chuyển đổi mã nguồn viết bằng một ngôn ngữ lập trình bậc cao (như TypeScript hiện đại) sang một ngôn ngữ bậc cao khác (như vanilla JavaScript cổ điển) để môi trường đích (trình duyệt) có thể thực thi.
  - Why it matters - vì sao quan trọng: Giúp lập trình viên sử dụng các tính năng mới nhất của ngôn ngữ mà không lo ngại tính tương thích của trình duyệt cũ.
- Pydantic - thư viện kiểm chuẩn dữ liệu:
  - Meaning - nghĩa: Thư viện Python dùng để phân tích và kiểm tra tính hợp lệ của dữ liệu đầu vào/đầu ra dựa trên type hints (gợi ý kiểu dữ liệu).
  - Why it matters - vì sao quan trọng: Là hạt nhân giúp FastAPI tự động kiểm tra dữ liệu request và sinh tài liệu API (Swagger UI) tự động.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
`Không có pipeline rõ ràng trong tài liệu nguồn`
Thay vào đó là luồng xử lý biên dịch mã nguồn của Next.js (Transpilation & Bundling Pipeline):
1. Input: Mã nguồn TypeScript (.ts, .tsx) do lập trình viên viết.
2. Processing steps:
   - Next.js Compiler tiếp nhận mã nguồn.
   - Quá trình **Transpiling** diễn ra: Chuyển đổi mã TypeScript hiện đại sang vanilla JavaScript tương thích mọi trình duyệt.
   - Quá trình **Bundling** diễn ra: Gom tất cả các file code nhỏ lẻ, các thư viện phụ thuộc thành các tệp chunk (gói mã nguồn) nhỏ gọn và tối ưu hóa dung lượng.
3. Output: Các file JavaScript thuần túy đã được nén và tối ưu hóa để sẵn sàng gửi tới trình duyệt của người dùng.

## 7. Techniques - Kỹ thuật sử dụng
- Component-based Architecture - kiến trúc dựa trên thành phần:
  - Purpose - mục đích: Chia nhỏ toàn bộ giao diện người dùng thành các phần độc lập, tự quản lý giao diện và logic riêng.
  - When to use - dùng khi nào: Xây dựng mọi giao diện người dùng hiện đại để tăng tính tái sử dụng và khả năng mở rộng của code.
  - Trade-off - đánh đổi: Đòi hỏi tư duy thiết kế cấu trúc tốt để tránh việc phân chia quá nhỏ hoặc truyền dữ liệu lòng vòng qua quá nhiều cấp component (prop drilling).

## 8. Code Walkthrough - Phân tích code nếu có
`Code được cung cấp trong session nhưng chưa thấy code liên quan trực tiếp tới lesson này.`
(Bài học này tập trung giải thích lý thuyết chi tiết về các framework React, Next.js và FastAPI trước khi bước vào thực hành).

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Sử dụng Pages Router (Next.js).
  - Pros: Cổ điển, cực kỳ ổn định, tương thích với hầu hết các thư viện và framework bên thứ ba lâu đời (như Clerk auth sử dụng trong tuần này).
  - Cons: Không tối ưu tốt các tính năng server component hiện đại của React 18+.
  - When to choose: Phù hợp nhất cho các dự án cần tính ổn định cao và tích hợp các thư viện truyền thống.
- Option 2: Sử dụng App Router (Next.js).
  - Pros: Hiện đại, mạnh mẽ, tối ưu hóa SEO tốt hơn nhờ React Server Components mặc định.
  - Cons: Cú pháp phức tạp hơn, một số thư viện cũ chưa hỗ trợ đầy đủ.
  - When to choose: Thích hợp cho các dự án mới hoàn toàn, không phụ thuộc vào các thư viện auth/billing cũ.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lỗi biên dịch TypeScript do sai kiểu dữ liệu khi truyền Props.
  - Root cause - nguyên nhân gốc rễ: Không định nghĩa kiểu dữ liệu (interface/type) cho props hoặc truyền dữ liệu không đúng kiểu mà component con quy định.
  - Symptom - dấu hiệu: Next.js báo lỗi build đỏ lòm trong terminal và không thể chạy ứng dụng.
  - Fix / prevention - sửa đổi / phòng ngừa: Luôn khai báo rõ ràng kiểu dữ liệu của props ở component con và sử dụng TypeScript linter để bắt lỗi ngay trong lúc viết code.

## 11. Knowledge Extension - Kiến thức mở rộng
- Virtual DOM - DOM ảo: React không tác động trực tiếp vào DOM thật của trình duyệt vì việc này rất tốn tài nguyên. Thay vào đó, React duy trì một bản sao DOM ảo bằng bộ nhớ RAM. Khi state thay đổi, React tính toán sự khác biệt giữa hai trạng thái DOM ảo (thuật toán diffing) rồi mới ghi nhận phần thay đổi duy nhất lên DOM thật.

## 12. Study Pack - Gói ôn tập
### Must remember
- React hoạt động theo cơ chế Component-based và Declarative (khai báo trạng thái).
- Props truyền từ cha xuống con (read-only); State là dữ liệu nội bộ tự quản lý (mutable).
- TSX/JSX là sự kết hợp cú pháp giữa HTML và JS/TS.
- Next.js hỗ trợ cả Pages Router (`/pages`) và App Router (`/app`).
- FastAPI sử dụng Pydantic để thực hiện validation (kiểm chuẩn) kiểu dữ liệu cho API.

### Self-check questions
- Giải thích sự khác biệt lớn nhất giữa Props và State trong React?
- Tại sao Next.js lại cần thực hiện bunding mã nguồn trước khi deploy?
- FastAPI tận dụng Starlette và Pydantic như thế nào để xây dựng các endpoint?

### Flashcards
- Q: Props có thể bị thay đổi trực tiếp bởi component nhận nó không?
  A: Không, props là read-only (chỉ đọc). Muốn thay đổi phải thông qua hàm callback được truyền từ component cha.
- Q: Tên thư mục chứa các page trong Next.js Pages Router là gì?
  A: `/pages`.

### Interview Q&A nếu phù hợp
- Q: Khi nào bạn chọn Django và khi nào chọn FastAPI cho một dự án backend?
  A: Tôi chọn Django khi dự án yêu cầu một hệ thống quản lý dữ liệu lớn, cần một trang quản trị (Admin UI) có sẵn, hệ thống xác thực người dùng phức tạp và ORM mạnh mẽ để làm việc với DB SQL truyền thống (tư duy "batteries included"). Tôi chọn FastAPI khi xây dựng các microservices hoặc API endpoints hiệu năng cao, yêu cầu độ trễ thấp, hỗ trợ xử lý bất đồng bộ (async/await) tốt, đặc biệt là khi xây dựng các ứng dụng AI cần streaming dữ liệu thời gian thực và tích hợp nhanh gọn với các thư viện Python hiện đại.

## 13. Missing Inputs - Còn thiếu gì
Không có tài nguyên bị thiếu cho bài học này.

---

# 11. Day 2 - Building Your First Full-Stack AI SaaS with NextJS and FastAPI

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 11).
- Slide: Đã dùng (Trang 9, 10).
- Code: Đã dùng (Đọc tài liệu hướng dẫn tạo dự án Next.js trong [day2.md](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L22-L40)).
- Summary lịch sử: Đã dùng (Day 1 summary).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Mọi thông tin thống nhất. Các bước clone repo và chạy lệnh khởi tạo Next.js khớp hoàn toàn giữa hướng dẫn của giảng viên và tài liệu code.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học đánh dấu điểm bắt đầu của phần thực hành ngày 2. Ed Donner hướng dẫn học viên cách clone (sao chép) repository chính của khóa học (`production`) từ GitHub về máy local.
- Giảng viên lưu ý học viên không nên đặt thư mục dự án bên trong các thư mục đồng bộ đám mây như OneDrive (Windows) hay iCloud (Mac) để tránh xung đột đồng bộ file cục bộ và làm chậm quá trình biên dịch của IDE.
- Lệnh khởi tạo dự án Next.js được sử dụng là: `npx create-next-app saas --ts --eslint --tailwind --no-src-dir --no-app`.
- Giải thích các tham số (flags) của lệnh khởi tạo: `--ts` (sử dụng TypeScript), `--eslint` (cài đặt công cụ bắt lỗi code), `--tailwind` (sử dụng Tailwind CSS), `--no-src-dir` (không dùng thư mục `/src`), và quan trọng nhất là `--no-app` (sử dụng Pages Router).
- Cấu trúc thư mục mặc định của dự án Next.js Pages Router được phân tích chi tiết, giúp học viên làm quen với các tệp tin quan trọng như `pages/_app.tsx`, `pages/_document.tsx`, `pages/index.tsx` và `styles/globals.css`.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cách thức hoạt động của lệnh `npx create-next-app` và vai trò của các flag cấu hình dự án Next.js.
  - Hiểu vai trò của file `tsconfig.json` and `package.json` trong việc quản lý cấu hình TypeScript và các dependencies (thư viện phụ thuộc) của dự án Node.js.
  - Hiểu cấu trúc phân bổ file trong mô hình Next.js Pages Router.
- Practical goals - mục tiêu thực hành:
  - Thực hiện clone repo GitHub thông qua terminal của Cursor/VS Code.
  - Chạy lệnh khởi tạo và cấu hình thành công dự án Next.js có hỗ trợ TypeScript và Tailwind CSS từ dòng lệnh.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích ý nghĩa của từng flag trong lệnh `npx create-next-app` được sử dụng.
  - Giải thích tại sao không nên để thư mục code dự án trong các thư mục đồng bộ như OneDrive/iCloud.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Lesson 10: Sau khi đã nắm vững lý thuyết về Next.js và cấu trúc Pages Router, bài học này chuyển sang phần thực hành thực tế để tự tay người học khởi tạo cấu trúc dự án này trên máy local của mình.

## 5. Core Theory - Lý thuyết cốt lõi
- package.json - file quản lý gói:
  - Meaning - nghĩa: File cấu hình định dạng JSON nằm ở root của dự án Node.js, chứa thông tin metadata của dự án, các script chạy lệnh và danh sách các thư viện phụ thuộc (dependencies).
  - Why it matters - vì sao quan trọng: Là xương sống để trình quản lý gói (npm hoặc yarn) hiểu và cài đặt chính xác các thư viện cần thiết để ứng dụng hoạt động.
- tsconfig.json - cấu hình TypeScript:
  - Meaning - nghĩa: File cấu hình chỉ định các tùy chọn biên dịch của trình biên dịch TypeScript (tsc) dành riêng cho dự án.
  - Why it matters - vì sao quan trọng: Giúp quy định mức độ khắt khe của việc kiểm tra kiểu dữ liệu và định dạng đầu ra của JavaScript sau khi compile.
- Linter - công cụ kiểm chuẩn mã nguồn:
  - Meaning - nghĩa: Công cụ phân tích mã nguồn tĩnh để phát hiện các lỗi cú pháp, lỗi logic tiềm ẩn hoặc các đoạn code không tuân thủ quy chuẩn style guide (ở đây là ESLint).
  - Why it matters - vì sao quan trọng: Giúp giữ chất lượng mã nguồn đồng đều và phát hiện sớm các lỗi nhỏ trước khi chạy ứng dụng.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình khởi tạo dự án Next.js và mở môi trường phát triển:
1. Input: Terminal chạy trong thư mục dự án cha (`projects/`).
2. Processing steps:
   - Bước 1: Chạy lệnh `git clone https://github.com/ed-donner/production.git` để lấy học liệu.
   - Bước 2: Chạy lệnh `npx create-next-app saas --ts --eslint --tailwind --no-src-dir --no-app` để sinh mã nguồn Next.js.
   - Bước 3: Node.js tự động tải các package mặc định và cài đặt vào thư mục `node_modules/`.
   - Bước 4: Mở thư mục `saas` vừa tạo bằng Cursor IDE (`File -> Open Folder`).
3. Output: Một dự án Next.js hoàn chỉnh với cấu trúc Pages Router sẵn sàng để tùy biến.

## 7. Techniques - Kỹ thuật sử dụng
- CLI-driven Scaffolding - dựng khung dự án qua dòng lệnh:
  - Purpose - mục đích: Tự động tạo ra cấu trúc thư mục tiêu chuẩn cùng các file cấu hình mặc định mà không cần tạo thủ công từng file.
  - When to use - dùng khi nào: Khi bắt đầu một dự án web mới sử dụng Next.js.
  - Trade-off - đánh đổi: Phải hiểu rõ ý nghĩa của các flag cấu hình để tránh sinh ra các file thừa thãi hoặc cấu hình sai router mong muốn.

## 8. Code Walkthrough - Phân tích code nếu có
### File: [npx create-next-app command](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L32-L32)
- Purpose - mục đích: Khởi tạo dự án Next.js với các thiết lập tùy biến cấu trúc.
- Key logic - logic chính:
  - `saas`: Tên thư mục dự án sẽ được tạo ra.
  - `--ts`: Sử dụng TypeScript thay vì JavaScript.
  - `--tailwind`: Tích hợp sẵn Tailwind CSS để phục vụ việc style giao diện.
  - `--no-src-dir`: Tạo trực tiếp thư mục `pages/` ở root level thay vì bọc trong thư mục `src/`.
  - `--no-app`: Tắt cấu hình App Router để ép dự án sử dụng Pages Router truyền thống.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích cú pháp:
  ```bash
  # Khởi tạo dự án Next.js sử dụng Pages Router và TypeScript
  npx create-next-app saas --ts --eslint --tailwind --no-src-dir --no-app
  ```

### File: [pages/_app.tsx](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L181-L190)
- Purpose - mục đích: File wrapper (bọc ngoài) toàn bộ các trang của ứng dụng Next.js, dùng để import CSS toàn cục và giữ state giữa các lần chuyển trang.
- Key logic - logic chính: Import file style toàn cục `globals.css` (chứa các cấu hình Tailwind CSS) để áp dụng cho mọi page.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích snippet:
  ```typescript
  import type { AppProps } from 'next/app';
  import '../styles/globals.css';  // Nhập file CSS toàn cục chứa các utility classes của Tailwind

  // Component khởi tạo và bọc ngoài tất cả các trang khác trong ứng dụng
  export default function MyApp({ Component, pageProps }: AppProps) {
    return <Component {...pageProps} />;
  }
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option: Sử dụng `--src-dir` (bọc thư mục code trong `/src`).
  - Pros: Giúp thư mục root của dự án trông gọn gàng hơn vì các file code chính nằm hết trong `/src`.
  - Cons: Phải import với đường dẫn dài hơn hoặc cấu hình alias phức tạp hơn cho người mới bắt đầu.
  - When to choose: Phù hợp cho các dự án lớn, có nhiều file cấu hình CI/CD ở root level. Trong khóa học này, ta chọn `--no-src-dir` để cấu trúc trực quan và đơn giản nhất.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Node.js chưa được cài đặt khiến lệnh `npx` báo lỗi command not found.
  - Root cause - nguyên nhân gốc rễ: Học viên bỏ qua các bước cài đặt phần mềm tiền đề ở Day 1.
  - Symptom - dấu hiệu: Terminal báo lỗi `npx: command not found` khi gõ lệnh.
  - Fix / prevention - sửa đổi / phòng ngừa: Tải và cài đặt Node.js LTS từ trang chủ trước khi tiếp tục thực hành.

## 11. Knowledge Extension - Kiến thức mở rộng
- npx vs npm: `npm` (Node Package Manager) là công cụ dùng để cài đặt và quản lý các package trên máy. `npx` (Node Package Execute) là công cụ đi kèm với npm, cho phép tải về và thực thi trực tiếp các package/script mà không cần cài đặt chúng vĩnh viễn vào hệ thống (ví dụ như chạy trình khởi tạo dự án).

## 12. Study Pack - Gói ôn tập
### Must remember
- Lệnh `npx create-next-app` giúp dựng nhanh khung dự án Next.js.
- Flag `--no-app` bắt buộc dự án sử dụng Pages Router.
- File `_app.tsx` là nơi import CSS toàn cục.
- Tuyệt đối tránh đặt thư mục dự án trong OneDrive hoặc iCloud để tránh lỗi đồng bộ.

### Self-check questions
- Vai trò của file `package.json` trong dự án Node.js là gì?
- Ý nghĩa của tham số `--ts` trong lệnh khởi tạo Next.js?
- Tại sao phải xóa thư mục `pages/api` mặc định trong dự án khi kết hợp với FastAPI?

### Flashcards
- Q: Lệnh khởi tạo Next.js sử dụng Pages Router là gì?
  A: Chú ý flag `--no-app` đi kèm lệnh `npx create-next-app`.
- Q: Thư mục nào chứa các file tĩnh (như hình ảnh, logo) trong Next.js?
  A: Thư mục `/public`.

### Interview Q&A nếu phù hợp
- Q: Tại sao trong cấu trúc dự án Next.js Pages Router, mọi trang con đều phải import style qua `_app.tsx` thay vì import trực tiếp tại các file component lẻ?
  A: Next.js quy định các file CSS toàn cục (global CSS) chỉ được phép import tại file `_app.tsx` để đảm bảo thứ tự load CSS của trình duyệt được nhất quán và tránh việc xung đột ghi đè các lớp style (style sheet collision) giữa các component khác nhau khi ứng dụng được build ra bản production.

## 13. Missing Inputs - Còn thiếu gì
Không có tài nguyên bị thiếu cho bài học này.

---

# 12. Day 2 - Building Your First FastAPI Backend for Production LLM Deployment

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 12).
- Slide: Đã dùng (Trang 8, 10).
- Code: Đã dùng (Đọc tài liệu hướng dẫn tạo backend trong [day2.md](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L92-L127)).
- Summary lịch sử: Đã dùng.
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thống nhất. Mã nguồn backend sử dụng thư viện OpenAI khớp hoàn toàn giữa video bài giảng và file hướng dẫn.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học tập trung vào việc thiết lập môi trường backend Python độc lập ngay bên trong dự án Next.js.
- Học viên xóa thư mục `pages/api` (vốn dùng cho backend JavaScript mặc định của Next.js) và tạo một thư mục `/api` mới nằm ở root level của dự án để chứa logic Python FastAPI.
- File `requirements.txt` được tạo ra ở root level để khai báo các dependencies cần thiết cho backend: `fastapi`, `uvicorn` và `openai`.
- File mã nguồn backend chính được đặt tên chính xác là `api/index.py` (Vercel yêu cầu tên này để tự động nhận diện và build thành serverless function mà không cần file cấu hình `vercel.json` phức tạp như Day 1).
- Trong `api/index.py`, học viên khởi tạo ứng dụng FastAPI và định nghĩa endpoint GET `/api` trả về kiểu dữ liệu PlainTextResponse.
- Logic API thực hiện kết nối tới OpenAI, gửi prompt yêu cầu tạo ý tưởng kinh doanh về AI Agents và trả về nội dung text của phản hồi.
- Ed Donner sử dụng tên model giả định là `gpt-5-nano` trong bài giảng (mang tính chất ví dụ minh họa và pha trò), đồng thời nhắc nhở học viên có thể tùy biến prompt hoặc đổi sang các nhà cung cấp model miễn phí khác nếu không muốn trả phí trước cho OpenAI.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cách cấu trúc thư mục để tích hợp mã nguồn Python FastAPI song song với Next.js trên hạ tầng Vercel.
  - Hiểu cơ chế Vercel tự động phát hiện thư mục `/api` và tệp `index.py` để map thành các serverless functions.
  - Nắm được cách gọi API chat completions cơ bản của OpenAI trong Python.
- Practical goals - mục tiêu thực hành:
  - Tạo thư mục `/api` ở root level và file `requirements.txt` chứa dependencies.
  - Viết hoàn chỉnh code FastAPI khởi tạo server và xử lý API route trả về PlainTextResponse.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích tại sao file backend Python lại phải đặt tên chính xác là `api/index.py`.
  - Trình bày được ý nghĩa của tham số `response_class=PlainTextResponse` trong FastAPI route decorator.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Lesson 11: Sau khi đã có bộ khung dự án Next.js và dọn dẹp các API route mặc định của JavaScript, bài học này tiến hành xây dựng phần xương sống backend chạy bằng Python cho dự án.

## 5. Core Theory - Lý thuyết cốt lõi
- PlainTextResponse - phản hồi văn bản thuần:
  - Meaning - nghĩa: Lớp phản hồi của FastAPI thiết lập Header `Content-Type` là `text/plain`, trả về chuỗi văn bản thô trực tiếp cho client thay vì đóng gói dạng JSON.
  - Why it matters - vì sao quan trọng: Thích hợp cho các trường hợp chỉ cần truyền tải chuỗi chữ đơn giản, giúp giảm overhead (chi phí xử lý dữ liệu) ở cả hai phía client và server.
- Serverless function mapping - ánh xạ hàm không máy chủ:
  - Meaning - nghĩa: Cơ chế của các nhà cung cấp cloud (như Vercel) tự động biên dịch các file code nằm trong các thư mục đặc biệt thành các hàm serverless độc lập chịu trách nhiệm xử lý các đường dẫn HTTP tương ứng.
  - Why it matters - vì sao quan trọng: Loại bỏ hoàn toàn việc phải viết cấu hình máy chủ Web (như Nginx hay Apache) thủ công.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Luồng thực thi của Backend API khi nhận request:
1. Input: HTTP GET request gửi tới URL `/api`.
2. Processing steps:
   - FastAPI Router bắt request và gọi hàm `idea()`.
   - Hàm `idea()` khởi tạo đối tượng `client = OpenAI()` (tự động lấy API key từ biến môi trường hệ thống).
   - Backend gửi payload chứa prompt tới server của OpenAI:
     `[{"role": "user", "content": "Come up with a new business idea for AI Agents"}]`
   - OpenAI xử lý và trả về kết quả generation.
   - Backend trích xuất text từ phản hồi: `response.choices[0].message.content`.
3. Output: Trả về chuỗi text ý tưởng kinh doanh dưới dạng PlainTextResponse cho frontend.

## 7. Techniques - Kỹ thuật sử dụng
- Route Decorator - bộ trang trí tuyến đường:
  - Purpose - mục đích: Đăng ký một hàm Python để xử lý các request HTTP cụ thể (GET, POST...) gửi tới một đường dẫn URL xác định.
  - When to use - dùng khi nào: Sử dụng khi định nghĩa bất kỳ API endpoint nào trong FastAPI.
  - Trade-off - đánh đổi: Phải khai báo chính xác phương thức HTTP để tránh lỗi Method Not Allowed (405).

## 8. Code Walkthrough - Phân tích code nếu có
### File: [requirements.txt](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L101-L107)
- Purpose - mục đích: Khai báo các thư viện Python cần cài đặt cho server backend.
- Key logic - logic chính: Liệt kê fastapi, uvicorn (phục vụ local run) và thư viện chính thức của openai.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích:
  ```text
  fastapi   # Framework chính để xây dựng API
  uvicorn   # ASGI server để chạy thử nghiệm local
  openai    # Thư viện để kết nối và gọi model của OpenAI
  ```

### File: [api/index.py](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L111-L126)
- Purpose - mục đích: Khởi tạo FastAPI app và định nghĩa endpoint xử lý logic gọi LLM sinh ý tưởng kinh doanh.
- Key logic - logic chính:
  - Sử dụng `@app.get("/api")` để lắng nghe request GET.
  - Thiết lập `response_class=PlainTextResponse` để trả về string thuần.
  - Sử dụng model `gpt-5-nano` (model giả định trong bài học) để tạo phản hồi qua API OpenAI.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích logic:
  ```python
  from fastapi import FastAPI  # type: ignore
  from fastapi.responses import PlainTextResponse  # type: ignore
  from openai import OpenAI  # type: ignore

  app = FastAPI()  # Khởi tạo ứng dụng FastAPI

  # Đăng ký endpoint GET tại đường dẫn "/api", trả về phản hồi dạng văn bản thuần thô
  @app.get("/api", response_class=PlainTextResponse)
  def idea():
      client = OpenAI()  # Khởi tạo client OpenAI (tự lấy OPENAI_API_KEY từ môi trường)
      prompt = [{"role": "user", "content": "Come up with a new business idea for AI Agents"}]
      
      # Gọi API OpenAI tạo completion với model gpt-5-nano (model giả định trong bài học)
      response = client.chat.completions.create(model="gpt-5-nano", messages=prompt)
      
      # Trích xuất nội dung text của câu trả lời và trả về cho client
      return response.choices[0].message.content
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option: Sử dụng các nhà cung cấp mô hình miễn phí hoặc thay thế (như OpenRouter, Gemini).
  - Pros: Tránh được việc phải nạp tiền trước (upfront payment) của OpenAI, phù hợp cho học viên muốn tiết kiệm chi phí.
  - Cons: Phải thay đổi thư viện và cấu hình endpoint tương ứng trong code, đôi khi độ trễ hoặc độ ổn định của các model miễn phí không cao bằng.
  - When to choose: Tham khảo các tài liệu hướng dẫn thay thế trong phần guides của repo nếu không có tài khoản OpenAI trả phí.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lỗi không tìm thấy thư viện `openai` hoặc `fastapi` khi chạy ứng dụng trên local.
  - Root cause - nguyên nhân gốc rễ: Quên chưa cài đặt các package trong file `requirements.txt` vào môi trường Python local.
  - Symptom - dấu hiệu: Python báo lỗi `ModuleNotFoundError: No module named 'fastapi'` hoặc `openai`.
  - Fix / prevention - sửa đổi / phòng ngừa: Chạy lệnh cài đặt thư viện tương ứng trong terminal (ví dụ sử dụng `pip install -r requirements.txt` hoặc tạo virtual environment trước khi chạy).

## 11. Knowledge Extension - Kiến thức mở rộng
- Model gpt-5-nano: Trong thực tế phát triển phần mềm, không tồn tại model tên là `gpt-5-nano`. Đây là cách Ed Donner đặt tên giả định để ví dụ hóa việc sử dụng các mô hình ngôn ngữ lớn thế hệ tiếp theo có chi phí siêu rẻ và tốc độ cực nhanh. Khi thực hành, học viên nên sử dụng các mô hình thực tế hiện có như `gpt-4o-mini` hoặc `gpt-3.5-turbo` để API hoạt động bình thường.

## 12. Study Pack - Gói ôn tập
### Must remember
- Tên file backend Python chạy trên Vercel bắt buộc phải là `api/index.py`.
- Thư mục `/api` chứa backend Python phải nằm ở root level của dự án Next.js.
- `PlainTextResponse` giúp tối giản hóa dữ liệu trả về của API chỉ dưới dạng string.
- OpenAI client mặc định sẽ tìm biến môi trường mang tên `OPENAI_API_KEY`.

### Self-check questions
- Tại sao Vercel lại yêu cầu cấu trúc thư mục backend Python phải nằm trong `/api` và file chính là `index.py`?
- Lớp `PlainTextResponse` khác gì so với `JSONResponse` mặc định của FastAPI?
- Làm cách nào OpenAI client tự động xác thực mà không cần lập trình viên truyền key trực tiếp vào hàm dựng `OpenAI(api_key="xxx")`?

### Flashcards
- Q: File requirements.txt dùng để làm gì trong dự án Python?
  A: Khai báo danh sách các thư viện bên ngoài cần cài đặt cho ứng dụng.
- Q: Cú pháp FastAPI để chỉ định một API endpoint lắng nghe phương thức HTTP GET là gì?
  A: `@app.get("/path")`.

### Interview Q&A nếu phù hợp
- Q: Tại sao việc truyền trực tiếp API Key vào hàm khởi tạo client như `client = OpenAI(api_key="your_key")` bị coi là một bad practice cực kỳ nguy hiểm trong môi trường sản xuất?
  A: Việc hard-code API key trực tiếp vào file code sẽ dẫn đến nguy cơ rất cao bị lộ key khi mã nguồn được push lên các hệ thống quản lý phiên bản như GitHub (đặc biệt là public repositories). Các bot quét mã độc trên GitHub có thể tìm ra key của bạn trong vòng vài giây và lạm dụng nó, gây thiệt hại lớn về mặt tài chính. Biện pháp chuẩn hóa công nghiệp luôn là lưu trữ key dưới dạng biến môi trường (environment variables) và để thư viện tự động đọc từ hệ điều hành.

## 13. Missing Inputs - Còn thiếu gì
Không có tài nguyên bị thiếu cho bài học này.

---

# 13. Day 2 - Deploying Full-Stack AI Apps with Next.js Frontend and FastAPI Backend

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 13).
- Slide: Đã dùng (Trang 10, 11).
- Code: Đã dùng (Đọc tài liệu code frontend và các bước deploy trong [day2.md](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L128-L270)).
- Summary lịch sử: Đã dùng.
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Mọi nguồn đều đồng nhất. Các bước cấu hình Vercel CLI khớp hoàn toàn giữa thực tế gõ lệnh và hướng dẫn.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học này hướng dẫn cấu hình frontend để gọi backend FastAPI và thực hiện quy trình deploy ứng dụng lên Vercel.
- Trong Next.js Pages Router, do chúng ta sử dụng Python FastAPI làm backend thay vì Next.js API, các component của frontend cần được đánh dấu bằng `"use client"` ở dòng đầu tiên để đảm bảo:
  1. Component chỉ chạy trên browser.
  2. Trình duyệt thực hiện gọi API trực tiếp tới Python backend `/api`.
  3. Tránh việc Next.js đóng vai trò máy chủ trung gian.
- Mã nguồn `pages/index.tsx` được cập nhật: sử dụng React hooks (`useState` để lưu trữ ý tưởng, `useEffect` để kích hoạt fetch dữ liệu từ `/api` khi trang load lần đầu).
- Cấu hình file `pages/_document.tsx` để định nghĩa cấu trúc HTML cơ bản, thẻ `<head>` và tiêu đề ứng dụng.
- Điểm đặc biệt: Không cần tạo file `vercel.json` vì Vercel sẽ tự động phát hiện cấu trúc Next.js kết hợp FastAPI trong `/api` và tự động điều hướng (routing) các request `/api` sang serverless function Python.
- Quy trình deploy qua Vercel CLI:
  - Chạy `vercel link` để tạo project mới tên là `saas` trên Vercel.
  - Chạy `vercel env add OPENAI_API_KEY` để nạp API key bảo mật lên Cloud (chọn môi trường preview, production và bật thuộc tính sensitive).
  - Chạy `vercel .` để đẩy toàn bộ code cục bộ lên Vercel để build và deploy. Lần đầu tiên chạy, ứng dụng sẽ được deploy trực tiếp ra production link.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu ý nghĩa của chỉ thị `"use client"` trong việc định hướng runtime của React component.
  - Hiểu vai trò của `useEffect` hook trong việc gọi API bất đồng bộ ngay khi component được render lần đầu (mount).
  - Nắm được cách thức Vercel tự động tích hợp và điều hướng (routing) giữa Next.js static files và Python serverless functions.
- Practical goals - mục tiêu thực hành:
  - Viết code React sử dụng hooks `useState` và `useEffect` để fetch dữ liệu từ FastAPI backend.
  - Sử dụng Vercel CLI để link dự án local với tài khoản Vercel đám mây.
  - Thêm biến môi trường bảo mật lên Vercel Dashboard qua CLI.
  - Thực hiện deploy thành công bản preview đầu tiên lên internet.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích tại sao phải dùng chỉ thị `"use client"` ở đầu tệp `pages/index.tsx`.
  - Trình bày được các bước hoạt động của Vercel CLI khi chạy lệnh `vercel link`.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Lesson 12: Sau khi đã viết xong backend FastAPI gọi LLM, bài học này tạo ra giao diện frontend để hiển thị kết quả, đồng thời kết nối và deploy cả 2 thành phần này lên cloud Vercel.

## 5. Core Theory - Lý thuyết cốt lõi
- use client - chỉ thị client component:
  - Meaning - nghĩa: Chỉ thị thông báo cho framework biết component này sẽ được biên dịch và chạy hoàn toàn ở phía client (trình duyệt), hỗ trợ các tính năng của browser như EventSource hay fetch API trực tiếp.
  - Why it matters - vì sao quan trọng: Cần thiết khi xây dựng các trang tương tác động kết nối với backend không phải JavaScript (FastAPI).
- useEffect - hook tác vụ phụ:
  - Meaning - nghĩa: React hook cho phép thực thi các tác vụ phụ (side effects) trong component, ví dụ như fetch dữ liệu, thiết lập subscriptions hoặc tương tác trực tiếp với DOM sau khi giao diện đã hiển thị.
  - Why it matters - vì sao quan trọng: Là nơi tiêu chuẩn để kích hoạt việc gọi API lấy dữ liệu từ server khi người dùng mở trang web.
- Link project - liên kết dự án:
  - Meaning - nghĩa: Quá trình ánh xạ thư mục code cục bộ trên máy tính với một dự án được quản trị trên Vercel dashboard thông qua file cấu hình ẩn `.vercel/project.json`.
  - Why it matters - vì sao quan trọng: Giúp Vercel CLI hiểu được code cần đẩy lên đâu trong các lần chạy lệnh deploy tiếp theo.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình liên kết và triển khai dự án lên Vercel:
1. Input: Thư mục dự án local `saas` đã lưu đầy đủ code frontend và backend.
2. Processing steps:
   - Bước 1: Mở terminal, chạy lệnh `vercel link` -> chọn scope cá nhân -> chọn không link tới dự án có sẵn -> đặt tên dự án là `saas` -> chọn thư mục hiện tại.
   - Bước 2: Chạy lệnh `vercel env add OPENAI_API_KEY` -> paste OpenAI API key -> chọn môi trường preview/production -> chọn Yes để ẩn key bảo mật.
   - Bước 3: Chạy lệnh `vercel .` -> Vercel nén mã nguồn local và tải lên cloud -> Vercel cloud cài đặt packages Node/Python và build ứng dụng.
3. Output: Nhận về URL public dạng `https://saas-xxxxxx.vercel.app` để truy cập ứng dụng trực tiếp từ internet.

## 7. Techniques - Kỹ thuật sử dụng
- Client-side Fetching - lấy dữ liệu từ phía máy khách:
  - Purpose - mục đích: Sử dụng hàm `fetch` tích hợp sẵn của trình duyệt để gọi API và lấy dữ liệu bất đồng bộ mà không cần reload trang.
  - When to use - dùng khi nào: Phưu hợp cho các ứng dụng SaaS cần hiển thị nhanh khung giao diện (skeleton) trước, sau đó mới tải dữ liệu động từ backend sau.
  - Trade-off - đánh đổi: Người dùng sẽ thấy trạng thái loading (chờ đợi) trong vài giây khi dữ liệu đang được tải từ server.

## 8. Code Walkthrough - Phân tích code nếu có
### File: [pages/index.tsx (Bản fetch API ban đầu)](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L141-L169)
- Purpose - mục đích: Giao diện trang chủ ban đầu thực hiện gọi API `/api` và hiển thị kết quả ý tưởng kinh doanh.
- Key logic - logic chính:
  - Khởi tạo state `idea` với giá trị mặc định là `'…loading'`.
  - Dùng `useEffect` chạy một lần khi load trang để fetch dữ liệu từ route `/api`.
  - Sau khi fetch xong, gọi `setIdea` để cập nhật giao diện.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích logic:
  ```typescript
  "use client" // Khai báo component chạy hoàn toàn trên trình duyệt người dùng

  import { useEffect, useState } from 'react';

  export default function Home() {
      // Khởi tạo trạng thái ý tưởng với giá trị ban đầu là đang tải
      const [idea, setIdea] = useState<string>('…loading');

      useEffect(() => {
          // Thực hiện gọi API bất đồng bộ tới backend FastAPI tại URL "/api"
          fetch('/api')
              .then(res => res.text()) // Chuyển đổi phản hồi nhận được sang định dạng text thuần
              .then(setIdea)           // Cập nhật giá trị ý tưởng vào state để React vẽ lại UI
              .catch(err => setIdea('Error: ' + err.message)); // Bắt lỗi nếu API bị sập
      }, []); // Mảng dependency rỗng nghĩa là effect này chỉ chạy duy nhất 1 lần khi trang load xong

      return (
          <main className="p-8 font-sans">
              <h1 className="text-3xl font-bold mb-4">
                  Business Idea Generator
              </h1>
              <div className="w-full max-w-2xl p-6 bg-white dark:bg-gray-800 border border-gray-300 dark:border-gray-600 rounded-lg shadow-sm">
                  {/* Hiển thị nội dung ý tưởng từ state */}
                  <p className="text-gray-900 dark:text-gray-100 whitespace-pre-wrap">
                      {idea}
                  </p>
              </div>
          </main>
      );
  }
  ```

### File: [pages/_document.tsx](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L196-L215)
- Purpose - mục đích: Thiết lập cấu trúc khung HTML của ứng dụng và cấu hình thẻ meta cho SEO.
- Key logic - logic chính: Sử dụng các tag `Html`, `Head`, `Main`, `NextScript` của Next.js để cấu trúc trang, đặt tiêu đề trang là "Business Idea Generator".
- Vietnamese inline notes - ghi chú tiếng Việt giải thích:
  ```typescript
  import { Html, Head, Main, NextScript } from 'next/document';

  // Component cấu trúc toàn bộ document HTML đầu ra
  export default function Document() {
    return (
      <Html lang="en">
        <Head>
          {/* Đặt tiêu đề mặc định hiển thị trên tab trình duyệt */}
          <title>Business Idea Generator</title>
          {/* Cấu hình meta mô tả cho SEO */}
          <meta name="description" content="AI-powered business idea generation" />
        </Head>
        <body>
          <Main /> {/* Nơi Next.js chèn nội dung của các trang con */}
          <NextScript /> {/* Nơi Next.js chèn các mã script JS cần thiết */}
        </body>
      </Html>
    );
  }
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Triển khai preview environment (môi trường xem trước).
  - Pros: Rất an toàn, giúp test thử các tính năng mới mà không làm ảnh hưởng đến đường dẫn production chính thức của người dùng.
  - Cons: Phải quản lý nhiều URL khác nhau, đôi khi cấu hình môi trường có chút khác biệt.
  - When to choose: Là lựa chọn mặc định của Vercel khi chạy lệnh `vercel` từ lần thứ 2 trở đi.
- Option 2: Deploy thẳng ra production bằng `vercel --prod`.
  - Pros: Cập nhật ngay lập tức thay đổi lên URL chính thức của sản phẩm.
  - Cons: Nếu code có lỗi, tất cả người dùng thực tế sẽ gặp lỗi ngay lập tức.
  - When to choose: Khi phiên bản thử nghiệm đã được test kỹ càng trên preview và sẵn sàng ra mắt.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Gọi API bị lỗi CORS hoặc 404 khi chạy ở local.
  - Root cause - nguyên nhân gốc rễ: Next.js frontend chạy ở port 3000 và FastAPI backend chạy ở port 8000 trên local, trình duyệt chặn gọi chéo domain (CORS) hoặc không tìm thấy `/api` do Next.js không có proxy chuyển hướng request.
  - Symptom - dấu hiệu: Màn hình hiển thị chữ `...loading` vĩnh viễn, console trình duyệt báo lỗi đỏ về CORS hoặc 404 Not Found.
  - Fix / prevention - sửa đổi / phòng ngừa: Khi chạy local, cần cấu hình proxy trong `next.config.js` để chuyển hướng `/api` sang `http://localhost:8000/api`, hoặc đơn giản hơn là kiểm thử trực tiếp bằng cách deploy lên Vercel (Vercel tự xử lý định tuyến này ở môi trường cloud nên sẽ không bị lỗi).

## 11. Knowledge Extension - Kiến thức mở rộng
- Server-side Rendering (SSR) vs Client-side Rendering (CSR): CSR (sử dụng `"use client"`) tải một trang HTML trống cùng mã JS về browser, sau đó browser mới fetch data và tự vẽ giao diện. SSR dựng sẵn toàn bộ HTML chứa đầy đủ dữ liệu trên server Next.js rồi mới gửi về trình duyệt. Do backend của chúng ta là Python FastAPI, ta dùng CSR để browser trực tiếp giao tiếp với FastAPI qua HTTP, bỏ qua tầng server Node.js của Next.js.

## 12. Study Pack - Gói ôn tập
### Must remember
- Chỉ thị `"use client"` bắt buộc phải đặt ở dòng đầu tiên của file component CSR.
- React hook `useEffect` dùng mảng dependency rỗng `[]` để chỉ chạy code fetch dữ liệu một lần duy nhất khi load trang.
- Vercel tự động map route `/api` tới backend Python trong thư mục `/api` mà không cần file vercel.json.
- Lệnh `vercel env add` giúp thêm biến môi trường bảo mật từ CLI mà không cần vào web Dashboard.

### Self-check questions
- Giải thích tại sao mảng dependency rỗng `[]` trong `useEffect` lại giúp hạn chế việc gọi API lặp đi lặp lại vô hạn?
- Lệnh `vercel link` tạo ra tệp tin cấu hình nào trong thư mục dự án và vai trò của nó?
- Biến môi trường OpenAI API Key được Vercel bảo mật thế nào khi chọn thuộc tính sensitive?

### Flashcards
- Q: Lệnh deploy bản build preview lên Vercel là gì?
  A: Chạy lệnh `vercel .` (hoặc chỉ gõ `vercel`).
- Q: React Hook nào được dùng để lưu trữ dữ liệu ý tưởng kinh doanh và cập nhật UI khi dữ liệu thay đổi?
  A: `useState`.

### Interview Q&A nếu phù hợp
- Q: Trong Next.js, tại sao bạn lại chọn phương án fetch dữ liệu ở client-side (CSR) thay vì sử dụng hàm `getServerSideProps` (SSR) để gọi FastAPI backend trước khi trả HTML về cho client?
  A: Việc sử dụng CSR kết hợp với FastAPI backend giúp tối ưu hóa tải trọng của máy chủ Next.js và cải thiện trải nghiệm người dùng. Khi dùng CSR, máy chủ Next.js chỉ việc phân phối các file HTML/JS tĩnh (rất nhẹ và nhanh qua CDN), còn browser của người dùng sẽ chịu trách nhiệm gọi trực tiếp FastAPI để lấy dữ liệu. Điều này giúp giảm thiểu đáng kể thời gian phản hồi ban đầu của trang web (Time to First Byte - TTFB) và cho phép hiển thị ngay lập tức trạng thái loading động trên UI, mang lại cảm giác mượt mà hơn cho người dùng so với việc bắt trình duyệt phải chờ server Next.js gọi backend xong xuôi rồi mới render trang.

## 13. Missing Inputs - Còn thiếu gì
Không có tài nguyên bị thiếu cho bài học này.

---

# 14. Day 2 - Adding Real-Time Streaming and Professional UI to Your LLM App

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 14).
- Slide: Đã dùng (Trang 11, 12).
- Code: Đã dùng (Đọc chi tiết mã nguồn streaming backend và frontend trong [day2.md](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L272-L634)).
- Summary lịch sử: Đã dùng.
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Mọi thông tin đều đồng nhất. Quá trình cấu hình CSS và kiểm thử tính năng streaming qua Server-Sent Events (SSE) diễn ra mượt mà và khớp hoàn toàn giữa mã nguồn thực tế và mô tả.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học này nâng cấp ứng dụng Business Idea Generator lên chuẩn thương mại chuyên nghiệp bằng cách tích hợp hai tính năng quan trọng: **Real-Time Streaming** (truyền phát dữ liệu thời gian thực từ LLM) và **Markdown Rendering** (hiển thị định dạng văn bản đẹp mắt).
- Frontend cài đặt các thư viện bổ trợ: `react-markdown`, `remark-gfm` (hỗ trợ định dạng bảng, link của GitHub), `remark-breaks` (hỗ trợ xuống dòng tự nhiên) và plugin Tailwind Typography `@tailwindcss/typography`.
- Backend cập nhật logic trong `api/index.py`: bật tham số `stream=True` trong API chat completions của OpenAI. Sử dụng hàm generator Python `event_stream()` và lớp `StreamingResponse` của FastAPI với `media_type="text/event-stream"` để trả dữ liệu dần về cho client theo định dạng SSE (`data: xxx\n`).
- Frontend cập nhật `pages/index.tsx`: sử dụng đối tượng `EventSource` của trình duyệt để lắng nghe sự kiện từ `/api`, liên tục cộng dồn các mảnh text nhận được vào biến buffer và cập nhật state để React render ra màn hình.
- Để khôi phục các style HTML truyền thống (như thẻ `h1`, `h2`, danh sách `ul`, `ol`) vốn bị Tailwind CSS reset (vô hiệu hóa) mặc định, học viên cần khai báo bổ sung lớp CSS `.markdown-content` ở cuối file `styles/globals.css`.
- Prompt gọi LLM ở backend được nâng cấp để ép model phải xuất ra định dạng Markdown rõ ràng có các thẻ tiêu đề và gạch đầu dòng.
- Giao diện người dùng được nâng cấp bằng Tailwind CSS hiện đại: bổ sung gradient background hỗ trợ dark mode, hiệu ứng pulse loading động khi đang chờ AI xử lý và bố cục card thủy tinh (glassmorphism) sang trọng.
- Quy trình deploy production cuối cùng được thực hiện bằng lệnh `vercel --prod`.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu nguyên lý hoạt động của Server-Sent Events (SSE) trong việc truyền phát dữ liệu thời gian thực từ server về client.
  - Hiểu cách thức hoạt động của thư viện React Markdown và các plugin parser (remark-gfm, remark-breaks).
  - Nắm được lý do Tailwind CSS thực hiện reset CSS mặc định (preflight) và cách khắc phục để hiển thị markdown.
  - Hiểu cách thiết kế prompt để định hướng cấu trúc đầu ra (headings, bullet points) của LLM.
- Practical goals - mục tiêu thực hành:
  - Cài đặt các package npm Node.js cho Markdown và Tailwind Typography.
  - Viết backend Python trả về `StreamingResponse` sử dụng cấu trúc yield generator.
  - Viết mã Javascript frontend sử dụng `EventSource` để xử lý luồng stream SSE.
  - Cấu hình custom layer CSS trong file globals.css của Tailwind.
  - Triển khai bản release production hoàn chỉnh lên Vercel.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích cơ chế hoạt động của Server-Sent Events (SSE) so với phương pháp polling (gọi lặp) truyền thống.
  - Giải thích tại sao Tailwind CSS mặc định lại xóa bỏ định dạng của các thẻ tiêu đề (h1-h6) và cách khôi phục chúng cho markdown content.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Lesson 13: Sau khi đã deploy thành công ứng dụng full-stack đầu tiên nhưng với trải nghiệm UI thô sơ (phải đợi LLM sinh xong toàn bộ text mới hiển thị), bài học này giải quyết triệt độ vấn đề trải nghiệm người dùng bằng cách áp dụng kỹ thuật streaming dữ liệu và làm đẹp giao diện.

## 5. Core Theory - Lý thuyết cốt lõi
- Server-Sent Events (SSE) - sự kiện gửi từ máy chủ:
  - Meaning - nghĩa: Công nghệ cho phép server thiết lập kết nối HTTP một chiều duy nhất và duy trì nó để liên tục đẩy dữ liệu (push) về phía client dưới dạng luồng stream thời gian thực.
  - Why it matters - vì sao quan trọng: Giúp tối ưu hóa trải nghiệm người dùng đối với các tác vụ sinh văn bản của LLM (vốn mất nhiều thời gian xử lý), cho phép người dùng đọc chữ ngay khi nó vừa được sinh ra.
- EventSource - đối tượng lắng nghe sự kiện:
  - Meaning - nghĩa: API tiêu chuẩn của trình duyệt web dùng để mở một kết nối HTTP tới server sử dụng giao thức SSE và lắng nghe các sự kiện `onmessage` do server gửi về.
  - Why it matters - vì sao quan trọng: Là hạt nhân phía frontend giúp thu nhận các mảnh text stream từ backend FastAPI.
- CSS Preflight - thiết lập lại CSS:
  - Meaning - nghĩa: Tập hợp các style mặc định được Tailwind CSS áp dụng để reset tất cả các định dạng mặc định của trình duyệt (như margin, font-size của h1, h2, list-style của li) về 0.
  - Why it matters - vì sao quan trọng: Đảm bảo giao diện đồng đều trên mọi trình duyệt, nhưng lại vô tình làm biến mất các định dạng hiển thị của văn bản Markdown thô nếu không được cấu hình khôi phục.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình truyền phát và hiển thị dữ liệu thời gian thực (End-to-End Streaming Workflow):
1. Input: Hành động load trang hoặc click button của người dùng.
2. Processing steps:
   - Frontend khởi tạo đối tượng `new EventSource('/api')`.
   - Backend FastAPI tiếp nhận kết nối SSE, gọi OpenAI API với `stream=True` và nhận về luồng dữ liệu generator.
   - Khi OpenAI trả về từng chunk (mảnh từ):
     - Backend dùng hàm generator trích xuất nội dung text (`chunk.choices[0].delta.content`).
     - Backend đóng gói mảnh text thành format SSE: `data: [nội dung mảnh text]\n\n` và gửi qua kết nối.
   - Frontend nhận sự kiện `onmessage`, trích xuất dữ liệu `e.data`, cộng dồn vào `buffer` và gọi `setIdea(buffer)`.
   - React tự động re-render, truyền chuỗi buffer vào component `ReactMarkdown` để cập nhật hiển thị lên DOM.
3. Output: Người dùng nhìn thấy văn bản ý tưởng kinh doanh xuất hiện dần trên màn hình với các định dạng tiêu đề, bôi đậm, gạch đầu dòng trực quan.

## 7. Techniques - Kỹ thuật sử dụng
- Yield-based Generator - hàm sinh sử dụng yield:
  - Purpose - mục đích: Sử dụng từ khóa `yield` trong Python để trả về từng phần dữ liệu từ một vòng lặp thay vì lưu toàn bộ dữ liệu vào bộ nhớ và trả về một lần bằng `return`.
  - When to use - dùng khi nào: Sử dụng khi cần stream dữ liệu dung lượng lớn hoặc dữ liệu sinh ra theo thời gian thực như token từ LLM.
  - Trade-off - đánh đổi: Phải quản lý việc đóng kết nối (close) đúng cách từ cả hai phía client và server để tránh rò rỉ tài nguyên.
  - Common mistake - lỗi dễ gặp: Quên ký tự xuống dòng `\n` trong dữ liệu yield, khiến giao thức SSE không nhận dạng được ranh giới message.

## 8. Code Walkthrough - Phân tích code nếu có
### File: [api/index.py (Bản hỗ trợ Streaming)](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L354-L379)
- Purpose - mục đích: Cập nhật backend FastAPI để gọi OpenAI ở chế độ streaming và trả dữ liệu về dạng Server-Sent Events.
- Key logic - logic chính:
  - Gọi OpenAI API với tham số `stream=True`.
  - Định nghĩa hàm generator `event_stream()` lặp qua các chunk trả về từ OpenAI, split văn bản theo dòng và yield theo format `data: {line}\n`.
  - Trả về `StreamingResponse` với media type `text/event-stream`.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích:
  ```python
  from fastapi import FastAPI  # type: ignore
  from fastapi.responses import StreamingResponse  # type: ignore
  from openai import OpenAI  # type: ignore

  app = FastAPI()

  @app.get("/api")
  def idea():
      client = OpenAI()
      # Prompt yêu cầu định dạng đầu ra chi tiết
      prompt = [{"role": "user", "content": "Reply with a new business idea for AI Agents, formatted with headings, sub-headings and bullet points"}]
      
      # Kích hoạt chế độ stream=True để nhận kết quả dạng luồng từ OpenAI
      stream = client.chat.completions.create(model="gpt-5-nano", messages=prompt, stream=True)

      # Định nghĩa hàm sinh (generator) để xử lý từng mảnh dữ liệu
      def event_stream():
          for chunk in stream:
              text = chunk.choices[0].delta.content  # Lấy mảnh text mới sinh ra
              if text:
                  lines = text.split("\n")  # Tách text theo dòng để tránh lỗi ngắt dòng của SSE
                  for line in lines:
                      yield f"data: {line}\n"  # Trả về theo định dạng chuẩn của giao thức SSE
                  yield "\n"  # Gửi thêm dòng trống để báo hiệu kết thúc một cụm message

      # Trả về StreamingResponse kết nối trực tiếp với generator của python
      return StreamingResponse(event_stream(), media_type="text/event-stream")
  ```

### File: [pages/index.tsx (Bản UI chuyên nghiệp + Streaming)](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L473-L539)
- Purpose - mục đích: Thiết lập giao diện người dùng chuyên nghiệp sử dụng Tailwind, lắng nghe luồng SSE bằng `EventSource` và hiển thị kết quả bằng `ReactMarkdown`.
- Key logic - logic chính:
  - Khởi tạo kết nối SSE bằng `new EventSource('/api')`.
  - Lắng nghe sự kiện `evt.onmessage` để cập nhật dữ liệu. Đóng kết nối bằng `evt.close()` trong hàm cleanup của `useEffect` hoặc khi có lỗi.
  - Sử dụng Tailwind classes: `bg-gradient-to-br` tạo màu nền, `animate-pulse` tạo hiệu ứng loading động nhấp nháy, card bọc ngoài sử dụng `rounded-2xl shadow-xl`.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích:
  ```typescript
  "use client"

  import { useEffect, useState } from 'react';
  import ReactMarkdown from 'react-markdown';
  import remarkGfm from 'remark-gfm';
  import remarkBreaks from 'remark-breaks';

  export default function Home() {
      const [idea, setIdea] = useState<string>('…loading');

      useEffect(() => {
          // Khởi tạo kết nối EventSource tới endpoint backend
          const evt = new EventSource('/api');
          let buffer = ''; // Biến đệm để tích lũy dữ liệu text trả về

          // Lắng nghe dữ liệu truyền về từ server
          evt.onmessage = (e) => {
              buffer += e.data; // Cộng dồn mảnh text mới nhận được vào buffer
              setIdea(buffer);  // Cập nhật state để React hiển thị
          };

          // Lắng nghe lỗi kết nối (ví dụ khi truyền tải kết thúc hoặc đứt mạng)
          evt.onerror = () => {
              console.error('SSE error, closing');
              evt.close(); // Đóng kết nối để giải phóng tài nguyên
          };

          // Hàm dọn dẹp (cleanup) được gọi khi component bị hủy (unmount)
          return () => { evt.close(); };
      }, []);

      return (
          <main className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 dark:from-gray-900 dark:to-gray-800">
              <div className="container mx-auto px-4 py-12">
                  <header className="text-center mb-12">
                      {/* Tiêu đề lớn định dạng chữ gradient sang trọng */}
                      <h1 className="text-5xl font-bold bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent mb-4">
                          Business Idea Generator
                      </h1>
                      <p className="text-gray-600 dark:text-gray-400 text-lg">
                          AI-powered innovation at your fingertips
                      </p>
                  </header>

                  <div className="max-w-3xl mx-auto">
                      <div className="bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-8 backdrop-blur-lg bg-opacity-95">
                          {idea === '…loading' ? (
                              // Hiển thị hiệu ứng loading pulse nhấp nháy trong lúc chờ AI xử lý
                              <div className="flex items-center justify-center py-12">
                                  <div className="animate-pulse text-gray-400">
                                      Generating your business idea...
                                  </div>
                              </div>
                          ) : (
                              // Hiển thị nội dung markdown đã được khôi phục định dạng CSS base
                              <div className="markdown-content text-gray-700 dark:text-gray-300">
                                  <ReactMarkdown
                                      remarkPlugins={[remarkGfm, remarkBreaks]}
                                  >
                                      {idea}
                                  </ReactMarkdown>
                              </div>
                          )}
                      </div>
                  </div>
              </div>
          </main>
      );
  }
  ```

### File: [styles/globals.css (Custom Base Layer)](file:///G:/AIProduction_t6_2026/production/week1/day2.md#L401-L461)
- Purpose - mục đích: Khôi phục các style mặc định cho các thẻ HTML văn bản thô để hiển thị đẹp định dạng Markdown.
- Key logic - logic chính: Sử dụng directive `@layer base` của Tailwind để định nghĩa lại các thuộc tính font-size, font-weight, list-style, margin cho các thẻ tiêu đề, đoạn văn và danh sách nằm trong lớp `.markdown-content`.
- Vietnamese inline notes - ghi chú tiếng Việt giải thích:
  ```css
  @layer base {
    /* Khôi phục kích thước, độ dày và khoảng cách cho thẻ h1 trong markdown */
    .markdown-content h1 {
      font-size: 2em;
      font-weight: bold;
      margin: 0.67em 0;
    }
    /* Khôi phục kích thước, độ dày và khoảng cách cho thẻ h2 trong markdown */
    .markdown-content h2 {
      font-size: 1.5em;
      font-weight: bold;
      margin: 0.83em 0;
    }
    /* Khôi phục danh sách không có thứ tự (ul) có dạng chấm tròn thụt đầu dòng */
    .markdown-content ul {
      list-style-type: disc;
      padding-left: 2em;
      margin: 1em 0;
    }
    /* Khôi phục danh sách có thứ tự (ol) dạng đánh số tăng dần */
    .markdown-content ol {
      list-style-type: decimal;
      padding-left: 2em;
      margin: 1em 0;
    }
  }
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option: Sử dụng thư viện `@tailwindcss/typography` (lớp `prose`) để tự động style markdown.
  - Pros: Nhanh gọn, không cần viết code CSS khôi phục thủ công, giao diện được thiết kế sẵn bởi đội ngũ Tailwind cực kỳ chuyên nghiệp.
  - Cons: Khó tùy biến màu sắc, kích thước cụ thể theo ý muốn cá nhân trừ khi ghi đè cấu hình trong file `tailwind.config.js`.
  - When to choose: Thích hợp cho các blog, tài liệu kỹ thuật dài cần giao diện chuẩn hóa nhanh chóng. Trong lab này, học viên được hướng dẫn kết hợp cả hai để hiểu sâu cơ chế layer của CSS.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Không hiển thị định dạng markdown (chữ hiện ra dạng chữ thô dính liền nhau).
  - Root cause - nguyên nhân gốc rễ: Ghi đè toàn bộ nội dung file `styles/globals.css` cũ khi thêm các lớp base mới, làm mất dòng import lõi của Tailwind `@tailwind base; @tailwind components; @tailwind utilities;`.
  - Symptom - dấu hiệu: Toàn bộ style của giao diện biến mất, các class Tailwind không hoạt động.
  - Fix / prevention - sửa đổi / phòng ngừa: Chỉ append (dán thêm) đoạn code CSS mới vào phía cuối của file globals.css, tuyệt đối không được xóa các dòng import mặc định của Tailwind nằm ở đầu file.

## 11. Knowledge Extension - Kiến thức mở rộng
- Server-Sent Events (SSE) vs WebSockets: SSE là kết nối một chiều (chỉ truyền từ server về client), chạy trên giao thức HTTP tiêu chuẩn nên rất nhẹ, dễ cấu hình và tự động kết nối lại khi đứt mạng. WebSockets là kết nối hai chiều toàn song công (full-duplex), đòi hỏi giao thức chuyên biệt (ws://) và tài nguyên máy chủ lớn hơn. Đối với tác vụ streaming từ LLM (vốn chỉ cần truyền dữ liệu một chiều từ AI về người dùng), SSE là giải pháp tối ưu và phổ biến nhất.

## 12. Study Pack - Gói ôn tập
### Must remember
- SSE truyền phát dữ liệu một chiều thời gian thực từ server về client qua HTTP.
- FastAPI backend sử dụng `StreamingResponse` kết hợp generator Python (`yield`) để chạy SSE.
- Frontend dùng `EventSource` và sự kiện `onmessage` để bắt dòng dữ liệu stream.
- Phải khôi phục style mặc định bị Tailwind CSS reset bằng custom CSS base layers để markdown hiển thị đúng.
- Chạy `npm install react-markdown remark-gfm remark-breaks` để xử lý phân tích cú pháp markdown.

### Self-check questions
- Giải thích nguyên lý hoạt động của Server-Sent Events (SSE)?
- Tại sao phải sử dụng hàm generator dùng từ khóa `yield` thay vì `return` khi làm streaming backend?
- Làm thế nào để giải quyết việc Tailwind CSS xóa sạch định dạng của thẻ `h1`, `ul`, `ol`?

### Flashcards
- Q: Thuộc tính `media_type` bắt buộc khai báo cho StreamingResponse SSE trong FastAPI là gì?
  A: `text/event-stream`.
- Q: Thư viện react-markdown dùng plugin gì để xử lý ngắt dòng tự nhiên của văn bản?
  A: `remark-breaks`.

### Interview Q&A nếu phù hợp
- Q: Khi người dùng đóng tab trình duyệt đột ngột trong lúc LLM đang stream dữ liệu, server FastAPI của bạn sẽ xử lý thế nào để tránh việc tiếp tục gọi OpenAI vô ích và tiêu tốn chi phí?
  A: Khi trình duyệt đóng tab, kết nối TCP giữa client và server sẽ bị ngắt. FastAPI sẽ nhận biết được sự kiện ngắt kết nối này (Connection Closed). Trong hàm generator của tôi, vòng lặp `for chunk in stream` sẽ bị gián đoạn do luồng ghi dữ liệu vào socket bị lỗi. Để đảm bảo tối ưu, tôi có thể lồng logic generator trong một khối `try...finally` hoặc kiểm tra trạng thái kết nối bất đồng bộ. Khi kết nối bị đứt, khối `finally` sẽ chạy và tôi sẽ gọi phương thức hủy kết nối của client OpenAI (ví dụ: `stream.close()`) để ngắt luồng gọi API OpenAI ngay lập tức, giúp tiết kiệm chi phí.

## 13. Missing Inputs - Còn thiếu gì
Không có tài nguyên bị thiếu cho bài học này.
