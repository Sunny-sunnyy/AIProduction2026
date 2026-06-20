# Day 5 Summary: AWS Setup, Docker & Serverless Lambda Deployment

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

---

# 23. Day 5 - AWS Setup and IAM for Production AI - Your First Cloud Deployment

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 23).
- Slide: Đã dùng (Trang slide giới thiệu AWS Setup và IAM).
- Code: Không có code trực tiếp cho lesson này.
- Summary lịch sử: Đã dùng (Đọc [day4_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day4_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn nhất quán hoàn toàn. Transcript giải thích rõ quy trình thiết lập Root User và bối cảnh sử dụng IAM.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học mở đầu ngày học thứ 5 bằng việc chuẩn bị tài khoản đám mây AWS cho việc triển khai thực tế. Triển khai ứng dụng lên các cloud providers (nhà cung cấp dịch vụ đám mây) lớn như AWS đem lại khả năng mở rộng (scalability) ở quy mô công nghiệp, nhưng đòi hỏi sự kiên nhẫn cao do tính phức tạp của việc cấu hình hạ tầng.
- Khái niệm Root User - tài khoản gốc: Tài khoản có toàn quyền tối cao trên AWS, chỉ nên dùng để thiết lập ban đầu (bật MFA, cấu hình ngân sách, tạo IAM User) và tuyệt đối không được dùng cho công việc phát triển hàng ngày.
- Giới thiệu IAM (Identity and Access Management - quản lý danh tính và truy cập): Hệ thống quản trị phân quyền cực kỳ chi tiết và mạnh mẽ của AWS. Đây là một kỹ năng thương mại quan trọng (commercial skill) mà các nhà tuyển dụng tìm kiếm.
- Tạo tài khoản IAM User tên `aiengineer` để làm việc hàng ngày nhằm đảm bảo an toàn, giảm thiểu rủi ro bảo mật cho tài khoản Root.
- Giới thiệu khái niệm ARN (Amazon Resource Name - tên tài nguyên Amazon): Chuỗi ký tự định danh duy nhất cho bất kỳ tài nguyên nào tồn tại trên hệ thống AWS.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Phân biệt sự khác biệt về quyền hạn và mục đích sử dụng giữa Root User và IAM User.
  - Hiểu cơ chế hoạt động của hệ thống phân quyền IAM (Identity and Access Management).
  - Nắm rõ cấu trúc định danh tài nguyên của AWS qua định dạng ARN.
- Practical goals - mục tiêu thực hành:
  - Đăng ký thành công tài khoản AWS cá nhân (Personal).
  - Cấu hình Multi-Factor Authentication (MFA) cho tài khoản Root.
  - Sao chép và lưu trữ mã số AWS Account ID gồm 12 chữ số.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích tại sao việc sử dụng Root account cho công việc lập trình hàng ngày là một lỗ hổng bảo mật nghiêm trọng.
  - Giải thích ý nghĩa của ARN trong việc quản lý và phân quyền tài nguyên.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Day 4, sau khi ứng dụng Healthcare Consultation Assistant đã chạy thử nghiệm thành công trên localhost, Day 5 chuyển đổi hoàn toàn sang môi trường production đám mây chuyên nghiệp trên AWS.

## 5. Core Theory - Lý thuyết cốt lõi
- Root User - tài khoản gốc:
  - Meaning - nghĩa: Tài khoản quản trị tối cao của AWS, được tạo ra bằng email đăng ký đầu tiên, có toàn quyền truy cập và thanh toán.
  - Why it matters - vì sao quan trọng: Cần bảo mật tối đa và hạn chế sử dụng để tránh việc lạm quyền hoặc vô tình xóa/sửa các dịch vụ quan trọng.
- Identity and Access Management - quản lý danh tính và truy cập:
  - Meaning - nghĩa: Dịch vụ bảo mật của AWS giúp quản lý việc truy cập các tài nguyên đám mây một cách an toàn và chi tiết.
  - Why it matters - vì sao quan trọng: Giúp thiết lập nguyên tắc đặc quyền tối thiểu (least privilege), đảm bảo chỉ những thực thể được phép mới có quyền truy cập tài nguyên cụ thể.
- Amazon Resource Name - tên tài nguyên Amazon:
  - Meaning - nghĩa: Định dạng chuỗi ký tự chuẩn hóa duy nhất của AWS để định danh một tài nguyên (ví dụ: `arn:aws:iam::123456789012:user/aiengineer`).
  - Why it matters - vì sao quan trọng: Giúp các chính sách phân quyền (policies) chỉ định chính xác tài nguyên cần tác động trên toàn bộ hệ thống AWS.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình thiết lập tài khoản Root an toàn:
1. Input: Email, mật khẩu mạnh, thông tin thẻ tín dụng/thanh toán quốc tế, số điện thoại xác thực.
2. Processing steps:
   - Truy cập [aws.amazon.com](https://aws.amazon.com) -> Đăng ký tài khoản mới loại "Personal".
   - Nhập thông tin thanh toán (AWS sẽ xác thực thẻ nhưng không trừ phí đăng ký).
   - Chọn gói hỗ trợ "Basic Support - Free".
   - Đăng nhập vào AWS Console với tư cách Root User -> Vào Security Credentials.
   - Chọn "Assign MFA device" -> Chọn "Authenticator app" -> Quét mã QR bằng Google Authenticator/Authy -> Nhập 2 mã liên tiếp để hoàn tất.
3. Output: Tài khoản AWS Root được kích hoạt MFA thành công và có mã Account ID 12 chữ số để sử dụng cho IAM.

## 7. Techniques - Kỹ thuật sử dụng
- Multi-Factor Authentication - xác thực đa yếu tố:
  - Purpose - mục đích: Thêm một lớp bảo mật thứ hai bên cạnh mật khẩu tĩnh để bảo vệ tài khoản chống lại các cuộc tấn công đánh cắp mật khẩu.
  - When to use - dùng khi nào: Bắt buộc áp dụng cho tài khoản Root AWS và các tài khoản IAM có đặc quyền cao.
  - Trade-off - đánh đổi: Người dùng phải thực hiện thêm một bước nhập mã từ thiết bị di động mỗi lần đăng nhập.
  - Common mistake - lỗi dễ gặp: Không lưu trữ mã khôi phục dự phòng dẫn đến việc bị khóa tài khoản nếu làm mất thiết bị cài app Authenticator.

## 8. Code Walkthrough - Phân tích code nếu có
`Buổi học này không có code được cung cấp`

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có tùy chọn kiến trúc mã nguồn trong bài thiết lập tài khoản ban đầu này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Bị hack tài khoản Root dẫn đến bị tin tặc lợi dụng đào tiền ảo hoặc phá hủy tài nguyên, phát sinh hóa đơn khổng lồ.
- Root cause - nguyên nhân: Không bật MFA cho tài khoản Root, sử dụng mật khẩu yếu hoặc tạo Access Key (khóa truy cập) trực tiếp từ tài khoản Root để lập trình.
- Fix / prevention - cách sửa/phòng tránh: Tuyệt đối không tạo Access Key cho Root user; luôn bật MFA; chỉ dùng IAM User cho các tác vụ hàng ngày.

## 11. Knowledge Extension - Kiến thức mở rộng
- AWS Organizations: Dịch vụ cho phép gom nhóm và quản lý tập trung nhiều tài khoản AWS. Trong môi trường doanh nghiệp lớn, việc phân rã môi trường Development, Staging và Production thành các tài khoản AWS riêng biệt thuộc một Organization là tiêu chuẩn bắt buộc để đảm bảo an toàn tối đa.

## 12. Study Pack - Gói ôn tập
### Must remember
- Root User có toàn quyền tối cao và chỉ dùng để tạo IAM User và thiết lập ngân sách.
- Luôn bật MFA (xác thực đa yếu tố) cho Root User.
- ARN (Amazon Resource Name) là định danh duy nhất cho tài nguyên AWS.
- AWS Account ID là chuỗi 12 chữ số nhận diện tài khoản đám mây của bạn.

### Self-check questions
1. Tại sao AWS khuyến nghị không sử dụng tài khoản Root cho công việc lập trình hàng ngày?
2. Ký tự viết tắt ARN trong AWS có nghĩa là gì và cấu trúc cơ bản của nó gồm những phần nào?
3. AWS Account ID gồm bao nhiêu chữ số và tìm thấy nó ở đâu trên console?

### Flashcards
- Q: IAM là viết tắt của từ gì?
  A: Identity and Access Management - quản lý danh tính và truy cập tài nguyên AWS.
- Q: ARN dùng để làm gì?
  A: Định danh duy nhất cho mọi tài nguyên trên đám mây AWS phục vụ phân quyền.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 24. Day 5 - Setting Up AWS Cost Monitoring for Production AI Deployments

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 24).
- Slide: Đã dùng (Trang slide hướng dẫn thiết lập Budgets).
- Code: Không có code trực tiếp cho lesson này.
- Summary lịch sử: Đã dùng (Đọc [day4_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day4_summary.md)).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn đồng nhất. Quy trình thiết lập cảnh báo ngân sách trên giao diện AWS Billing được giải thích cụ thể.

## 2. Executive Summary - Tóm tắt cốt lõi
- Quản lý chi phí API và hạ tầng đám mây là trách nhiệm của nhà phát triển (developer's responsibility). AWS là môi trường chuyên nghiệp cho doanh nghiệp, có khả năng mở rộng cực lớn nên chi phí có thể phát sinh không giới hạn nếu xảy ra sự cố (ví dụ: vòng lặp vô tận gọi API).
- Điểm khác biệt quan trọng: AWS **không hỗ trợ tính năng tự động tắt dịch vụ khi vượt quá ngân sách (no hard cap / no automatic shutdown)**. Lý do là để bảo vệ tính liên tục của các doanh nghiệp lớn (ví dụ: không thể vì lỗi thanh toán hoặc vượt ngân sách nhỏ mà AWS tự động đánh sập dịch vụ của Netflix).
- Thiết lập cảnh báo ngân sách (AWS Budgets) làm lưới an toàn (safety net) là bắt buộc trước khi triển khai bất kỳ tài nguyên nào lên AWS.
- Hướng dẫn thiết lập 2 loại cảnh báo ngân sách cơ bản:
  - Zero Spend Budget: Cảnh báo ngay khi phát sinh chi phí vượt mức $0.01.
  - Monthly Cost Budget: Cảnh báo theo các ngưỡng chi phí thực tế (actual spend) đạt 85%, 100% hoặc chi phí dự báo (forecasted spend) đạt 100% của một hạn mức xác định (ví dụ: $1, $5, $10).

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu triết lý tính phí của AWS và lý do không tồn tại tính năng giới hạn cứng (hard cap) tự động ngắt dịch vụ.
  - Nắm vững cơ chế hoạt động của AWS Budgets (Actual vs Forecasted).
- Practical goals - mục tiêu thực hành:
  - Truy cập dịch vụ Billing and Cost Management trên AWS Console.
  - Thiết lập Zero Spend Budget gửi cảnh báo về email cá nhân khi chi phí > $0.01.
  - Thiết lập các Monthly Cost Budget ở các mức $1, $5, và $10.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích tại sao trách nhiệm giám sát chi phí trên AWS hoàn toàn thuộc về lập trình viên.
  - Giải thích sự khác biệt giữa cảnh báo dựa trên chi phí thực tế (Actual) và chi phí dự kiến (Forecasted).

## 4. Previous Context - Liên hệ với bài trước
Sau khi thiết lập tài khoản Root AWS ở Bài 23, việc đầu tiên cần làm (trước khi tạo bất kỳ dịch vụ hay IAM user nào) là cấu hình giám sát chi phí để tránh các hóa đơn ngoài ý muốn.

## 5. Core Theory - Lý thuyết cốt lõi
- Actual Cost - chi phí thực tế:
  - Meaning - nghĩa: Số tiền thực tế mà tài khoản đã tiêu dùng cho các dịch vụ AWS tính đến thời điểm hiện tại của chu kỳ thanh toán.
  - Why it matters - vì sao quan trọng: Giúp nhận biết chính xác lượng tiền đã tiêu tốn.
- Forecasted Cost - chi phí dự kiến:
  - Meaning - nghĩa: Thuật toán của AWS dự báo tổng chi phí sẽ đạt được vào cuối tháng dựa trên xu hướng tiêu dùng hiện tại của tài khoản.
  - Why it matters - vì sao quan trọng: Đóng vai trò cảnh báo sớm (early warning) giúp lập trình viên phát hiện sớm các tài nguyên quên tắt trước khi chúng thực sự tiêu tốn nhiều tiền.
- Zero Spend Budget - ngân sách bằng không:
  - Meaning - nghĩa: Loại cấu hình ngân sách gửi email thông báo ngay khi hệ thống bắt đầu phát sinh chi phí dù là nhỏ nhất ($0.01).
  - Why it matters - vì sao quan trọng: Lưới an toàn đầu tiên để phát hiện việc rò rỉ chi phí (cost leak) trên tài khoản mới.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình thiết lập Budget Alerts trên AWS:
1. Input: Địa chỉ email nhận thông báo, hạn mức ngân sách mong muốn (ví dụ: $1, $5, $10).
2. Processing steps:
   - Đăng nhập Root User -> Tìm kiếm "Billing" trên Console -> Chọn "Billing and Cost Management".
   - Chọn mục "Budgets" ở cột menu bên trái -> Nhấp "Create budget".
   - Chọn "Use a template (simplified)" -> Chọn "Monthly cost budget".
   - Điền thông tin:
     - Budget Name: `early-warning`, Budgeted Amount: `1` USD, Email recipients: Email của bạn -> Click "Create budget".
     - Lặp lại để tạo các budget `caution-budget` ($5) và `stop-budget` ($10).
3. Output: Hệ thống hiển thị danh sách các Budget đang hoạt động kèm trạng thái theo dõi chi phí thực tế.

## 7. Techniques - Kỹ thuật sử dụng
- Cost Alerting - cảnh báo chi phí:
  - Purpose - mục đích: Tự động hóa giám sát chi phí hạ tầng thông qua email để phản ứng nhanh khi có bất thường.
  - When to use - dùng khi nào: Ngay lập tức khi tạo tài khoản AWS và trước khi triển khai bất cứ dịch vụ nào.
  - Trade-off - đánh đổi: Nhận được nhiều email thông báo nếu thiết lập các ngưỡng quá nhạy cảm.
  - Common mistake - lỗi dễ gặp: Điền sai email nhận thông báo hoặc bỏ qua các email cảnh báo dự báo (Forecasted) từ AWS.

## 8. Code Walkthrough - Phân tích code nếu có
`Buổi học này không có code được cung cấp`

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có tùy chọn kiến trúc mã nguồn trong bài thiết lập chi phí này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Tài khoản phát sinh hóa đơn hàng nghìn USD do rò rỉ Access Key hoặc chạy tài nguyên đắt đỏ mà không biết.
- Root cause - nguyên nhân: Ỷ lại vào "Free Tier" mà không thiết lập Budgets, hoặc nhầm tưởng AWS có cơ chế tự động ngắt dịch vụ khi quá hạn mức.
- Fix / prevention - cách sửa/phòng tránh: Luôn tạo Zero Spend Budget và Monthly Budget ($1, $5, $10) ngay ngày đầu tiên. Thường xuyên kiểm tra bảng quản lý chi phí Billing Dashboard thủ công.

## 11. Knowledge Extension - Kiến thức mở rộng
- AWS Cost Explorer: Công cụ phân tích sâu chi phí của AWS, cho phép lập trình viên lọc chi phí theo từng dịch vụ, vùng (regions), hoặc nhãn gắn trên tài nguyên (resource tags). Đây là công cụ đắc lực khi cần tối ưu hóa chi phí cho dự án lớn.

## 12. Study Pack - Gói ôn tập
### Must remember
- AWS không có giới hạn cứng (hard cap) tự động ngắt dịch vụ để tránh làm sập ứng dụng của khách hàng doanh nghiệp.
- Budgets giúp cảnh báo dựa trên cả chi phí thực tế (Actual) và chi phí dự báo (Forecasted).
- Luôn kiểm tra Billing dashboard hàng ngày khi đang thử nghiệm dịch vụ cloud mới.

### Self-check questions
1. Tại sao AWS lại không cung cấp tính năng tự động tắt toàn bộ dịch vụ khi vượt quá ngân sách đã đặt?
2. Có những ngưỡng cảnh báo nào được gửi tự động khi bạn thiết lập một Monthly Cost Budget?
3. Sự khác biệt giữa Actual và Forecasted Budget alert là gì?

### Flashcards
- Q: Lợi ích lớn nhất của Zero Spend Budget là gì?
  A: Nhận email cảnh báo ngay khi tài khoản phát sinh chi phí vượt mức $0.01 để kịp thời tắt dịch vụ.
- Q: Forecasted alert hoạt động dựa trên nguyên lý nào?
  A: Dự báo chi phí cả tháng dựa trên tốc độ tiêu thụ hiện tại của tài nguyên đang chạy.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 25. Day 5 - Setting Up Secure IAM Users for Production AI Deployments on AWS

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 25).
- Slide: Đã dùng (Trang sơ đồ phân quyền IAM User và Group).
- Code: Đã dùng (Tham chiếu hướng dẫn phân quyền mới trong [day5.md](file:///G:/AIProduction_t6_2026/production/week1/day5.md) và hướng dẫn cũ trong [prior_day5_app_runner.md](file:///G:/AIProduction_t6_2026/production/week1/prior_day5_app_runner.md)).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Do cập nhật tháng 04/2026 về việc ngưng cung cấp AWS App Runner cho khách hàng mới, chính sách phân quyền cho nhóm người dùng có sự thay đổi lớn: thay thế `AWSAppRunnerFullAccess` bằng `AWSLambda_FullAccess`. Ngoài ra, cần bổ sung `IAMFullAccess` để Lambda tự động tạo service-linked execution role khi chạy.

## 2. Executive Summary - Tóm tắt cốt lõi
- Phân quyền theo chuẩn công nghiệp: Tạo User Group `BroadAIEngineerAccess` để quản lý tập trung chính sách phân quyền, sau đó thêm IAM User `aiengineer` vào group này. Đây là phương pháp quản trị an toàn (best practice).
- Cập nhật phân quyền mới (Tháng 04/2026):
  - Thay thế quyền quản lý App Runner bằng quyền quản lý Lambda: Sử dụng **`AWSLambda_FullAccess`** thay vì `AWSAppRunnerFullAccess` như trong video.
  - Các quyền đồng hành bắt buộc:
    - `AmazonEC2ContainerRegistryFullAccess`: Lưu trữ Docker images trên ECR.
    - `CloudWatchLogsFullAccess`: Giám sát và ghi nhận logs hệ thống.
    - `IAMUserChangePassword`: Cho phép user tự quản lý mật khẩu.
    - `IAMFullAccess`: Bắt buộc để Lambda tự tạo service-linked execution role khi khởi chạy container.
- Cơ chế Access Denied: Khi đăng nhập bằng IAM User `aiengineer`, màn hình billing sẽ báo lỗi truy cập do tài khoản này không có quyền xem chi phí tổng thể (quyền này chỉ dành riêng cho Root User).
- Tầm quan trọng của AWS Regions: Giải thích về các phân vùng vật lý độc lập của AWS trên toàn thế giới (ví dụ: `us-east-1`, `eu-west-1`). Cần chọn vùng gần người dùng nhất và duy trì tính nhất quán trên mọi cấu hình (ECR, Lambda, CLI).

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cách thức hoạt động của User Group trong việc đơn giản hóa quản lý chính sách bảo mật.
  - Nắm vững khái niệm AWS Regions và ảnh hưởng của nó đến độ trễ (latency) và tính khả dụng của dịch vụ.
  - Hiểu cơ chế phân quyền tối thiểu khi làm việc với Docker ECR và Lambda.
- Practical goals - mục tiêu thực hành:
  - Tạo IAM User `aiengineer` và User Group `BroadAIEngineerAccess` từ tài khoản Root.
  - Gán 5 chính sách (policies) bảo mật bắt buộc vào User Group (theo cấu hình Lambda mới).
  - Tải xuống và lưu trữ an toàn tệp thông tin đăng nhập `.csv`.
  - Đăng nhập thành công bằng IAM User qua đường dẫn sign-in riêng biệt.
- What learner should be able to explain - người học cần giải thích được:
  - Tại sao việc gán chính sách bảo mật trực tiếp cho từng User bị hạn chế, thay vào đó nên sử dụng User Group?
  - Sự khác biệt về quyền hạn hiển thị trên console giữa Root User và IAM User.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp việc thiết lập ngân sách ở Bài 24, Bài 25 sử dụng tài khoản Root để tạo ra môi trường làm việc an toàn cho nhà phát triển (IAM User), làm nền tảng cho mọi thao tác lập trình hạ tầng sau đó.

## 5. Core Theory - Lý thuyết cốt lõi
- IAM User - người dùng IAM:
  - Meaning - nghĩa: Một thực thể danh tính được tạo ra trong tài khoản AWS với các thông tin đăng nhập và phân quyền cụ thể để đại diện cho một người dùng hoặc ứng dụng thực tế.
  - Why it matters - vì sao quan trọng: Giúp cô lập môi trường làm việc và thu hồi quyền dễ dàng khi cần thiết mà không ảnh hưởng tới tài khoản gốc.
- User Group - nhóm người dùng:
  - Meaning - nghĩa: Tập hợp các IAM User có chung mục đích công việc. Quyền hạn gán cho group sẽ tự động áp dụng cho tất cả các user thuộc group đó.
  - Why it matters - vì sao quan trọng: Giúp quản lý quyền hạn tập trung, tránh việc phân quyền thủ công riêng lẻ dễ gây ra sai sót bảo mật.
- AWS Region - vùng địa lý AWS:
  - Meaning - nghĩa: Một vị trí địa lý thực tế trên thế giới chứa nhiều Trung tâm dữ liệu (Datacenters) được nhóm lại thành các Vùng sẵn sàng (Availability Zones).
  - Why it matters - vì sao quan trọng: Lựa chọn đúng Region gần khách hàng nhất giúp giảm đáng kể độ trễ truyền tải dữ liệu và tuân thủ các quy định pháp lý về lưu trữ dữ liệu tại bản địa.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình tạo IAM User và Group an toàn (Cập nhật 2026):
1. Input: Tên user mong muốn (`aiengineer`), tên group (`BroadAIEngineerAccess`), danh sách các policy cần gán.
2. Processing steps:
   - Đăng nhập Root User -> Tìm kiếm dịch vụ "IAM" -> Chọn "Users" -> "Create user".
   - Đặt Username: `aiengineer`, chọn "Provide user access to the AWS Management Console" -> Chọn "I want to create an IAM user" -> Đặt Custom password và bỏ tích yêu cầu đổi mật khẩu ở lần đăng nhập tới -> Nhấp "Next".
   - Tại trang Permissions, chọn "Add user to group" -> Click "Create group".
   - Đặt Group Name: `BroadAIEngineerAccess`.
   - Tìm kiếm và tích chọn 5 chính sách (policies) sau:
     1. **`AWSLambda_FullAccess`** (thay thế cho `AWSAppRunnerFullAccess` cũ)
     2. `AmazonEC2ContainerRegistryFullAccess`
     3. `CloudWatchLogsFullAccess`
     4. `IAMUserChangePassword`
     5. `IAMFullAccess`
   - Click "Create user group" -> Chọn group vừa tạo -> Nhấp "Next" -> "Create user".
   - Tải tệp `.csv` chứa thông tin tài khoản và đường dẫn sign-in về máy tính bảo mật.
3. Output: IAM User `aiengineer` được khởi tạo thành công với các quyền hạn giới hạn sẵn sàng để phát triển ứng dụng.

## 7. Techniques - Kỹ thuật sử dụng
- Least Privilege Access Control - kiểm soát truy cập đặc quyền tối thiểu:
  - Purpose - mục đích: Chỉ cung cấp đúng các quyền hạn tối thiểu cần thiết để hoàn thành công việc, ngăn chặn việc lạm dụng quyền phá hoại hệ thống.
  - When to use - dùng khi nào: Áp dụng khi phân quyền cho mọi IAM User hoặc Service Role trong dự án.
  - Trade-off - đánh đổi: Lập trình viên có thể gặp lỗi "Access Denied" liên tục khi bắt đầu làm việc với các dịch vụ mới chưa được cấp quyền, đòi hỏi phải quay lại tài khoản Root để bổ sung chính sách.
  - Common mistake - lỗi dễ gặp: Gán quyền `AdministratorAccess` cho tài khoản lập trình hàng ngày vì sự tiện lợi tạm thời.

## 8. Code Walkthrough - Phân tích code nếu có
`Buổi học này không có code được cung cấp`

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có tùy chọn kiến trúc mã nguồn trong bài thiết lập IAM này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Gặp lỗi phân quyền khi Lambda cố gắng tạo service role để kéo image hoặc ghi logs.
- Root cause - nguyên nhân: Thiếu chính sách `IAMFullAccess` trong cấu hình group của IAM User `aiengineer` (lập trình viên thường chỉ gán các quyền chạy dịch vụ mà quên gán quyền quản lý vai trò của IAM).
- Fix / prevention - cách sửa/phòng tránh: Đảm bảo đã gắn đủ chính sách `IAMFullAccess` vào nhóm `BroadAIEngineerAccess`.

## 11. Knowledge Extension - Kiến thức mở rộng
- IAM Policy Structure: Các chính sách IAM thực chất là các tài liệu JSON định nghĩa quyền hạn. Một tài liệu JSON của policy gồm 3 thành phần chính: `Effect` (Allow/Deny), `Action` (danh sách các thao tác API được phép, ví dụ: `lambda:CreateFunction`), và `Resource` (ARN của tài nguyên cụ thể chịu tác động).

## 12. Study Pack - Gói ôn tập
### Must remember
- Không dùng tài khoản Root để phát triển ứng dụng; luôn dùng IAM User.
- Quyền hạn của IAM User được quản lý tốt nhất thông qua User Group.
- Các quyền cần thiết cho triển khai mới là: `AWSLambda_FullAccess`, `AmazonEC2ContainerRegistryFullAccess`, `CloudWatchLogsFullAccess`, `IAMUserChangePassword`, và `IAMFullAccess`.
- AWS Region được viết dưới dạng chuẩn hóa như `us-east-1`.

### Self-check questions
1. Tại sao cấu hình User Group lại giúp việc quản lý bảo mật tốt hơn việc phân quyền trực tiếp cho từng User?
2. Khi đăng nhập bằng IAM User `aiengineer`, tại sao bạn lại thấy thông báo lỗi "Access Denied" khi cố gắng xem mục Billing?
3. Tại sao chính sách `IAMFullAccess` lại bắt buộc phải có khi triển khai AWS Lambda bằng Docker container?

### Flashcards
- Q: AWS Region là gì?
  A: Phân vùng địa lý thực tế chứa các trung tâm dữ liệu độc lập của AWS.
- Q: Service-linked role là gì?
  A: Vai trò IAM mà dịch vụ AWS (như Lambda) tự động sử dụng để tương tác với các dịch vụ AWS khác thay mặt cho bạn.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 26. Day 5 - Containerizing AI Apps with Docker for Cloud Deployment

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 26).
- Slide: Đã dùng (Trang slide giới thiệu các khái niệm Docker).
- Code: Không có code dự án được tạo ở bài học này (bài học thuần lý thuyết và hướng dẫn cài đặt Docker Desktop).
- Summary lịch sử: Đã dùng (`day4_summary.md` làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn đồng nhất. Quy trình giải thích 3 khái niệm cốt lõi của Docker rất rõ ràng.

## 2. Executive Summary - Tóm tắt cốt lõi
- Giới thiệu công nghệ đóng gói container (Containerization) bằng công cụ Docker. Docker giúp đóng gói ứng dụng chạy độc lập, nhất quán ở bất kỳ môi trường nào (build một lần, chạy mọi nơi).
- So sánh công nghệ:
  - Virtual Machines (Máy ảo - nặng, chạy toàn bộ hệ điều hành giả lập, tốn tài nguyên và thời gian khởi động lâu).
  - Docker Containers (Nhẹ, chia sẻ chung nhân hệ điều hành - OS kernel - với máy chủ vật lý, khởi động tức thì và tốn rất ít tài nguyên).
- Nắm vững 3 khái niệm cốt lõi xây dựng trên nhau của Docker:
  1. Dockerfile: Tập tin cấu hình dạng văn bản thô chứa các chỉ thị từng bước để cài đặt và thiết lập môi trường.
  2. Docker Image: Bản chụp tĩnh (blueprint/snapshot) của môi trường được build từ Dockerfile.
  3. Docker Container: Một thực thể đang hoạt động thực tế (active instance) được tạo ra từ Docker Image. Một image có thể tạo ra nhiều container chạy độc lập.
- Giới thiệu 3 dịch vụ AWS phối hợp trong ngày: ECR (nơi lưu trữ images), Lambda/App Runner (nơi chạy containers), và CloudWatch (nơi giám sát logs tập trung).
- Cài đặt và xác thực Docker hoạt động cục bộ bằng lệnh `docker --version` và chạy thử container mẫu `docker run hello-world`.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu sự khác biệt về mặt kiến trúc phần cứng và hiệu năng giữa Virtual Machines và Docker Containers.
  - Hiểu chuỗi liên kết: `Dockerfile -> Docker Image -> Docker Container`.
  - Hiểu vai trò của ECR, Lambda/App Runner và CloudWatch trong hệ sinh thái ứng dụng container trên đám mây.
- Practical goals - mục tiêu thực hành:
  - Cài đặt thành công Docker Desktop trên máy tính cá nhân.
  - Đối với Windows: Cấu hình tích hợp WSL2 (Windows Subsystem for Linux) làm môi trường nền cho Docker.
  - Chạy lệnh kiểm tra phiên bản Docker và chạy thành công container mẫu `hello-world`.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích tại sao Docker container lại nhẹ và khởi động nhanh hơn đáng kể so với một máy ảo truyền thống.
  - Phân biệt sự khác nhau giữa Docker Image và Docker Container.

## 4. Previous Context - Liên hệ với bài trước
Sau khi đã thiết lập tài khoản và bảo mật IAM ở các bài trước, Bài 26 giới thiệu công cụ Docker làm phương tiện đóng gói phần mềm đồng nhất để chuẩn bị đưa ứng dụng lên dịch vụ lưu trữ ECR của AWS.

## 5. Core Theory - Lý thuyết cốt lõi
- Containerization - đóng gói container:
  - Meaning - nghĩa: Phương pháp ảo hóa cấp hệ điều hành (OS-level virtualization) dùng để đóng gói một ứng dụng và toàn bộ thư viện phụ thuộc của nó vào một container đồng nhất.
  - Why it matters - vì sao quan trọng: Giải quyết triệt để lỗi kinh điển "chạy được trên máy tôi nhưng lỗi trên máy chủ" (it works on my machine problem).
- Dockerfile - tệp Dockerfile:
  - Meaning - nghĩa: Tệp văn bản không có phần mở rộng chứa các lệnh tuần tự để cấu hình môi trường bên trong container.
  - Why it matters - vì sao quan trọng: Đóng vai trò là mã nguồn hạ tầng (infrastructure as code), giúp quy trình xây dựng môi trường có khả năng tái lặp chính xác tuyệt đối.
- Docker Image - ảnh Docker:
  - Meaning - nghĩa: Tệp tin snapshot chỉ đọc chứa mã nguồn, thư viện hệ thống và các cấu hình chạy ứng dụng.
  - Why it matters - vì sao quan trọng: Làm bản thiết kế tĩnh (blueprint) để phân phối ứng dụng lên các kho lưu trữ trực tuyến (registries).
- Docker Container - thùng chứa Docker:
  - Meaning - nghĩa: Một tiến trình bị cô lập chạy thực tế trên máy tính chủ, được khởi tạo từ một Docker Image cụ thể.
  - Why it matters - vì sao quan trọng: Môi trường thực thi thực tế của ứng dụng, có thể bật, tắt, hoặc nhân bản nhanh chóng.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình hoạt động của Docker:
1. Input: File cấu hình Dockerfile -> Chạy lệnh `docker build`.
2. Processing steps: Docker đọc từng câu lệnh trong Dockerfile để kéo các lớp image nền từ Docker Hub -> Cài đặt thư viện -> Xuất ra Docker Image -> Chạy lệnh `docker run <image-name>`.
3. Output: Docker engine khởi tạo một container độc lập chạy ứng dụng từ image vừa build. Trong trường hợp chạy `hello-world`, container tải ảnh từ Docker Hub, in ra màn hình dòng chữ chào mừng và tự động dừng.

## 7. Techniques - Kỹ thuật sử dụng
- Base Image Inheritance - kế thừa ảnh nền:
  - Purpose - mục đích: Sử dụng các Docker images đã được tối ưu hóa sẵn từ cộng đồng (như Alpine Linux, Python-slim) để làm điểm xuất phát cho Dockerfile.
  - When to use - dùng khi nào: Luôn luôn khai báo ở câu lệnh đầu tiên (`FROM`) của mọi Dockerfile.
  - Trade-off - đánh đổi: Phụ thuộc vào chất lượng bảo mật và dung lượng của image gốc được chọn.
  - Common mistake - lỗi dễ gặp: Chọn các image nền quá nặng hoặc chứa các lỗ hổng bảo mật chưa được vá.

## 8. Code Walkthrough - Phân tích code nếu có
`Buổi học này không có code được cung cấp` (Mã nguồn Dockerfile chi tiết sẽ được viết và phân tích ở Bài 28).

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có phân tích lựa chọn kiến trúc phần mềm trong bài lý thuyết cơ bản này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Lỗi không thể kết nối tới Docker daemon khi chạy lệnh trong terminal.
- Root cause - nguyên nhân: Docker Desktop chưa được khởi chạy hoặc bị lỗi crash tiến trình ngầm trên máy chủ.
- Fix / prevention - cách sửa/phòng tránh: Đảm bảo ứng dụng Docker Desktop đang chạy (có biểu tượng con cá voi màu xanh lá cây trên thanh tác vụ hệ thống) trước khi gõ lệnh.

## 11. Knowledge Extension - Kiến thức mở rộng
- Docker Layers and Cache: Mỗi dòng lệnh trong Dockerfile (như `RUN`, `COPY`) tạo ra một lớp (layer) dữ liệu mới trong Docker Image. Khi build lại image, Docker sẽ tái sử dụng cache của các layer cũ không thay đổi để tăng tốc quy trình. Do đó, việc sắp xếp các lệnh ít thay đổi (như cài dependencies) lên trước các lệnh hay thay đổi (như copy source code) là kỹ thuật tối ưu hóa build-time cực kỳ quan trọng.

## 12. Study Pack - Gói ôn tập
### Must remember
- Docker giúp ứng dụng chạy nhất quán ở mọi nơi bằng cách chia sẻ nhân hệ điều hành.
- Dockerfile tạo ra Docker Image, Docker Image khởi tạo Docker Container.
- Amazon ECR là kho chứa Docker images riêng tư của bạn trên AWS.
- CloudWatch là công cụ quản lý log tập trung trên hạ tầng AWS.

### Self-check questions
1. Tại sao Docker container lại khởi động nhanh hơn và tốn ít tài nguyên bộ nhớ hơn máy ảo (Virtual Machine)?
2. Sự khác nhau chính giữa Docker Image và Docker Container là gì?
3. Ba dịch vụ AWS nào sẽ phối hợp với nhau để vận hành ứng dụng đóng gói Docker của chúng ta?

### Flashcards
- Q: Lệnh nào dùng để kiểm tra cài đặt Docker hoạt động bình thường?
  A: Lệnh `docker run hello-world`.
- Q: Dockerfile là gì?
  A: Tập tin văn bản chứa các chỉ thị từng bước để build một Docker Image.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 27. Day 5 - Migrating Your AI App from Vercel to AWS for Production Scale

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 27).
- Slide: Đã dùng (Trang slide mô tả kiến trúc Server-Static-FastAPI).
- Code: Đã dùng (Tham chiếu các file [day5.md](file:///G:/AIProduction_t6_2026/production/week1/day5.md) từ Part 3 Step 1 đến Step 5).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn nhất quán hoàn toàn. Mã nguồn và transcript khớp nhau về các bước sửa đổi cấu hình static export và đổi route gọi API ở frontend.

## 2. Executive Summary - Tóm tắt cốt lõi
- Chuẩn bị chuyển dịch ứng dụng Healthcare từ Vercel lên AWS. Kiến trúc trên Vercel phân tách frontend chạy server-side và API backend độc lập. Để đơn giản hóa hạ tầng và tối ưu hóa chi phí trên AWS, chúng ta chuyển đổi sang kiến trúc **Single Container (Gom chung một container)**.
- Thay đổi cấu hình Next.js: Bật chế độ Static Export (`output: 'export'`) trong [next.config.ts](file:///G:/AIProduction_t6_2026/production/week1/day5.md) để xuất toàn bộ ứng dụng React thành các file HTML/JS/CSS tĩnh trong thư mục `out/`.
- Sửa đổi giao tiếp API ở frontend: Cập nhật file [pages/product.tsx](file:///G:/AIProduction_t6_2026/production/week1/day5.md) để gọi API tại endpoint `/api/consultation` (thay vì `/api` trên Vercel). Điều này là do cả API và frontend tĩnh đều chạy chung một domain và chung một container.
- Tạo file backend mới [api/server.py](file:///G:/AIProduction_t6_2026/production/week1/day5.md):
  - Sử dụng FastAPI để xử lý API endpoint `/api/consultation`.
  - Thiết lập CORS middleware để cho phép gọi API chéo từ client.
  - Mount thư mục tĩnh `static/` (chứa các file Next.js static build) lên route gốc `/` để FastAPI đóng vai trò host toàn bộ website.
  - Thêm endpoint `/health` trả về trạng thái lành mạnh phục vụ giám sát.
- Thiết lập tệp cấu hình môi trường đám mây `.env` chứa đầy đủ các khóa bảo mật của Clerk, OpenAI và thêm 2 biến AWS: `DEFAULT_AWS_REGION` và `AWS_ACCOUNT_ID`.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu kiến trúc Single Container (một container chạy cả frontend tĩnh và API backend).
  - Nắm rõ cơ chế hoạt động của Static Export trong Next.js Pages Router.
  - Hiểu cách FastAPI định tuyến và host các tệp tin tĩnh (static files).
- Practical goals - mục tiêu thực hành:
  - Cập nhật file [next.config.ts](file:///G:/AIProduction_t6_2026/production/week1/day5.md) bật static export.
  - Thay đổi endpoint trong [pages/product.tsx](file:///G:/AIProduction_t6_2026/production/week1/day5.md).
  - Tạo và hoàn thiện file backend [api/server.py](file:///G:/AIProduction_t6_2026/production/week1/day5.md).
  - Tạo tệp `.env` cấu hình AWS Account ID và AWS Region.
- What learner should be able to explain - người học cần giải thích được:
  - Tại sao việc đóng gói toàn bộ frontend tĩnh vào FastAPI backend lại giúp triển khai lên đám mây dễ dàng và tiết kiệm chi phí hơn?
  - CORS middleware trong [api/server.py](file:///G:/AIProduction_t6_2026/production/week1/day5.md) giải quyết vấn đề gì?

## 4. Previous Context - Liên hệ với bài trước
Bài học này lấy mã nguồn ứng dụng ở cuối Day 4 và thực hiện tái cấu trúc lớn về mặt kiến trúc hệ thống (từ đa dịch vụ phân tán trên Vercel sang đơn dịch vụ đóng gói) để chuẩn bị cho quy trình viết Dockerfile ở Bài 28.

## 5. Core Theory - Lý thuyết cốt lõi
- Static Export - xuất bản tĩnh:
  - Meaning - nghĩa: Tính năng của Next.js biên dịch toàn bộ cấu trúc trang động thành các tệp tin HTML, JavaScript và CSS tĩnh có thể chạy trực tiếp trên bất kỳ máy chủ HTTP nào mà không cần Node.js runtime ở phía server.
  - Why it matters - vì sao quan trọng: Loại bỏ sự cần thiết của máy chủ frontend chạy Node.js riêng biệt, giảm thiểu dung lượng RAM tiêu thụ và tăng tốc độ tải trang.
- CORS (Cross-Origin Resource Sharing) - chia sẻ tài nguyên giữa các nguồn khác nhau:
  - Meaning - nghĩa: Cơ chế bảo mật của trình duyệt web ngăn chặn các trang web tải từ một tên miền (origin) này gọi API tới một tên miền khác khi chưa được cho phép.
  - Why it matters - vì sao quan trọng: Cần cấu hình CORS Middleware trong FastAPI để đảm bảo frontend (dù chạy localhost hay trên domain cloud) có quyền gửi request đến API backend mà không bị trình duyệt chặn.
- Static Files Mounting - gắn kết tệp tin tĩnh:
  - Meaning - nghĩa: Quy trình cấu hình để FastAPI tự động phục vụ các tệp tin tĩnh (hình ảnh, mã JS, CSS) từ một thư mục cụ thể trên đĩa cứng khi người dùng truy cập vào các đường dẫn tương ứng.
  - Why it matters - vì sao quan trọng: Giúp FastAPI kiêm nhiệm luôn vai trò của một web server tĩnh, không cần bổ sung thêm Nginx hay Apache trong container.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình chuẩn bị và đóng gói ứng dụng:
1. Input: Mã nguồn frontend Next.js và backend FastAPI cũ trên Vercel.
2. Processing steps:
   - Sửa `nextConfig` trong `next.config.ts`: Thêm `output: 'export'` và `images: { unoptimized: true }`.
   - Sửa hàm `fetchEventSource` trong `pages/product.tsx` hướng cuộc gọi về `/api/consultation`.
   - Tạo file `api/server.py`: import `StaticFiles` và `FileResponse`, định nghĩa CORS middleware, viết endpoint `/api/consultation` trả về `StreamingResponse` cho OpenAI stream, viết `/health` check, và cuối cùng dùng `app.mount("/", StaticFiles(directory="static", html=True))` để host thư mục static tĩnh.
3. Output: Ứng dụng sẵn sàng để build tĩnh và host chung trong một container Python duy nhất.

## 7. Techniques - Kỹ thuật sử dụng
- Single Domain Consolidation - hợp nhất tên miền duy nhất:
  - Purpose - mục đích: Gom cả frontend và backend chạy dưới cùng một domain, giúp loại bỏ các cấu hình CORS phức tạp khi deploy lên môi trường thật.
  - When to use - dùng khi nào: Triển khai các ứng dụng SaaS quy mô nhỏ hoặc trung bình muốn tối giản hạ tầng.
  - Trade-off - đánh đổi: Mất đi khả năng scale độc lập giữa tầng frontend và backend; nếu server backend quá tải, cả giao diện frontend cũng bị ảnh hưởng tốc độ tải.
  - Common mistake - lỗi dễ gặp: Đặt hàm mount static file lên trước các định nghĩa API route, dẫn đến việc FastAPI hiểu nhầm các đường dẫn API là đường dẫn file tĩnh và trả về lỗi 404. (Quy tắc bắt buộc: Phải mount static files ở cuối file `api/server.py`).

## 8. Code Walkthrough - Phân tích code nếu có
### File [next.config.ts](file:///G:/AIProduction_t6_2026/production/week1/day5.md) - Next.js Static Export Configuration
- Purpose - mục đích: Cấu hình cho Next.js xuất ra tệp tĩnh thay vì server-rendered build.
- Key logic - logic chính: Thêm thuộc tính `output: 'export'` và bỏ tối ưu ảnh để không phụ thuộc vào Node.js image server.
```typescript
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  output: 'export',  // Biên dịch ứng dụng thành HTML/JS/CSS tĩnh trong thư mục 'out'
  images: {
    unoptimized: true  // Tắt tính năng tối ưu ảnh động (bắt buộc cho static export)
  }
};

export default nextConfig;
```

### File [api/server.py](file:///G:/AIProduction_t6_2026/production/week1/day5.md) - FastAPI Single Container Server
- Purpose - mục đích: API backend và host static files.
- Key logic - logic chính: Định nghĩa route `/api/consultation`, `/health`, `/` và mount thư mục `static`.
```python
import os
from pathlib import Path
from fastapi import FastAPI, Depends
from fastapi.responses import StreamingResponse, FileResponse
from fastapi.staticfiles import StaticFiles
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel
from fastapi_clerk_auth import ClerkConfig, ClerkHTTPBearer, HTTPAuthorizationCredentials
from openai import OpenAI

app = FastAPI()

# Cấu hình CORS cho phép giao tiếp chéo nguồn
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

clerk_config = ClerkConfig(jwks_url=os.getenv("CLERK_JWKS_URL"))
clerk_guard = ClerkHTTPBearer(clerk_config)

class Visit(BaseModel):
    patient_name: str
    date_of_visit: str
    notes: str

# API endpoint nhận thông tin khám bệnh và stream dữ liệu từ OpenAI
@app.post("/api/consultation")
def consultation_summary(
    visit: Visit,
    creds: HTTPAuthorizationCredentials = Depends(clerk_guard),
):
    user_id = creds.decoded["sub"]
    client = OpenAI()
    
    # ... logic dựng prompts ...
    stream = client.chat.completions.create(
        model="gpt-5-nano", # Sử dụng model phù hợp
        messages=[{"role": "user", "content": "..."}],
        stream=True,
    )
    
    def event_stream():
        for chunk in stream:
            text = chunk.choices[0].delta.content
            if text:
                yield f"data: {text}\n\n"
                
    return StreamingResponse(event_stream(), media_type="text/event-stream")

# Health check route
@app.get("/health")
def health_check():
    return {"status": "healthy"}

# Serve static files (Next.js static export) - MUST BE LAST!
static_path = Path("static")
if static_path.exists():
    @app.get("/")
    async def serve_root():
        # Trả về trang index.html khi người dùng truy cập trang chủ
        return FileResponse(static_path / "index.html")

    # Mount toàn bộ các file tĩnh khác (JS, CSS, images) vào đường dẫn gốc
    app.mount("/", StaticFiles(directory="static", html=True), name="static")
```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- **Lựa chọn**: Host frontend/backend chung trong một container Python (FastAPI) vs Tách biệt độc lập (Next.js chạy Node.js container / FastAPI chạy Python container).
  - *Option 1 (Consolidated)*: Dùng FastAPI phục vụ tệp tĩnh Next.js.
    - Pros: Tiết kiệm tài nguyên (chỉ cần chạy 1 container duy nhất trên đám mây); hóa đơn AWS cực kỳ thấp; cấu hình DNS và CORS đơn giản.
    - Cons: Tải trang frontend tĩnh phụ thuộc vào hiệu năng của luồng xử lý FastAPI; khó mở rộng riêng lẻ khi lượng truy cập một trong hai tầng tăng vọt.
    - When to choose: Phù hợp nhất cho các sản phẩm SaaS giai đoạn MVP, khóa học thực hành, hoặc ứng dụng nội bộ có tải trọng thấp.
  - *Option 2 (Decoupled)*: Frontend deploy riêng (ví dụ: Vercel hoặc AWS Amplify), backend chạy trên dịch vụ container/lambda riêng.
    - Pros: Tách biệt hoàn toàn quyền hạn; tối ưu hóa tốc độ tải trang frontend qua mạng lưới CDN của Vercel; dễ dàng scale backend độc lập.
    - Cons: Tốn kém chi phí hơn khi duy trì nhiều dịch vụ chạy song song; phát sinh lỗi CORS phức tạp; khó quản lý nhất quán biến môi trường.
    - When to choose: Dự án lớn, có đội ngũ phát triển frontend và backend riêng biệt, yêu cầu tốc độ tải trang cao toàn cầu.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Lỗi 404 Not Found khi truy cập vào các API route `/api/consultation` sau khi deploy.
- Root cause - nguyên nhân: Trong file `server.py`, lập trình viên mount StaticFiles lên route gốc `/` ở vị trí phía trên định nghĩa của `@app.post("/api/consultation")`. FastAPI sẽ bắt tất cả các request (kể cả API) để tìm kiếm tệp tĩnh tương ứng và trả về lỗi 404 khi không thấy tệp tĩnh đó.
- Fix / prevention - cách sửa/phòng tránh: Luôn đặt lệnh mount StaticFiles (`app.mount("/", ...)`) ở **dòng cuối cùng** của file cấu hình FastAPI.

## 11. Knowledge Extension - Kiến thức mở rộng
- Single Page Application (SPA) Routing: Khi xuất Next.js dạng static export, các trang con (ví dụ: `/product`) thực chất là các file HTML riêng biệt (như `product.html`). Nếu người dùng reload trang `/product` trực tiếp trên trình duyệt, web server tĩnh FastAPI có thể trả về lỗi 404 vì nó tìm thư mục tên `/product` thay vì file `product.html`. Để giải quyết triệt để trong môi trường SPA thực tế, cần cấu hình cơ chế URL Rewrites trên web server để chuyển hướng tất cả các request không phải file vật lý về lại `index.html`.

## 12. Study Pack - Gói ôn tập
### Must remember
- Chế độ Static Export của Next.js biên dịch mã nguồn thành HTML/JS/CSS tĩnh, loại bỏ sự cần thiết của Node.js server.
- File [api/server.py](file:///G:/AIProduction_t6_2026/production/week1/day5.md) chịu trách nhiệm host cả API và các file tĩnh đã export.
- Lệnh mount static files bắt buộc phải khai báo ở cuối cùng trong FastAPI.
- CORS middleware là bắt buộc để trình duyệt không chặn cuộc gọi API từ client.

### Self-check questions
1. Tại sao phải cập nhật đường dẫn gọi API của frontend thành `/api/consultation` thay vì chỉ để `/api` như trước?
2. Thuộc tính `output: 'export'` trong cấu hình Next.js dùng để làm gì?
3. Nếu bạn đặt dòng code mount thư mục `static` lên đầu file FastAPI, hiện tượng gì sẽ xảy ra với các API routes của bạn?

### Flashcards
- Q: Lợi ích của `images: { unoptimized: true }` trong Next.js static export?
  A: Ngăn Next.js cố gắng tối ưu ảnh bằng các tính năng của máy chủ Node.js động, giúp build tĩnh thành công.
- Q: Endpoint `/health` phục vụ cho mục đích gì trên cloud?
  A: Giúp hệ thống giám sát của AWS kiểm tra xem container có đang hoạt động bình thường hay không.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 28. Day 5 - Containerizing Your AI App - Docker Images for Production Deployment

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 28).
- Slide: Đã dùng (Trang sơ đồ Multi-stage Build và cấu trúc Dockerfile).
- Code: Đã dùng (Tham chiếu các file [day5.md](file:///G:/AIProduction_t6_2026/production/week1/day5.md) Part 4 Step 1 & Step 2 và Part 5 Step 1 đến Step 4).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Do cập nhật tháng 04/2026 về việc chuyển dịch hạ tầng sang AWS Lambda, Dockerfile đã được tích hợp thêm **AWS Lambda Web Adapter** thông qua việc sao chép binary `/lambda-adapter` từ ảnh ECR công khai của AWS Labs (`public.ecr.aws/awsguru/aws-lambda-adapter:1.0.0`) vào thư mục `/opt/extensions/`. Hai biến môi trường quan trọng được bổ sung là `PORT=8000` và `AWS_LWA_INVOKE_MODE=response_stream`. Bản nâng cấp này hoàn toàn tương thích khi chạy thử nghiệm Docker cục bộ (local docker run).

## 2. Executive Summary - Tóm tắt cốt lõi
- Xây dựng Dockerfile sử dụng kỹ thuật **Multi-stage Build (Xây dựng đa tầng)** để tối ưu hóa kích thước ảnh đầu ra:
  - Stage 1 (Frontend Builder - dựa trên `node:22-alpine`): Copy toàn bộ mã nguồn frontend, truyền biến môi trường Clerk Publishable Key dưới dạng Build Argument (`ARG`), cài đặt dependencies bằng `npm ci` và chạy `npm run build` tạo ra thư mục static export `out/`.
  - Stage 2 (Final Python Container - dựa trên `python:3.12-slim`): Copy binary **AWS Lambda Web Adapter** để dịch các cuộc gọi serverless sang HTTP, cài đặt Python dependencies từ `requirements.txt`, copy file `api/server.py` và copy thư mục static build `out/` của Stage 1 sang `./static`.
- Cấu hình file `.dockerignore` để loại bỏ các tệp tin rác hoặc chứa thông tin bảo mật (`node_modules`, `.next`, `.env`, `.env.local`) khỏi tiến trình build, giúp giảm thời gian build và dung lượng image.
- Chạy thử nghiệm cục bộ bằng cách nạp biến môi trường từ file `.env` vào terminal, sau đó chạy lệnh build:
  - `docker build --build-arg ... -t consultation-app .`
- Khởi chạy container local bằng lệnh:
  - `docker run -p 8000:8000 -e ... consultation-app`
- Giải thích cảnh báo "secrets in ARG/ENV" của Docker: Bỏ qua vì Clerk Publishable Key (`pk_...`) được thiết kế để công khai ở phía client, không phải secret key.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cơ chế hoạt động và lợi ích của Multi-stage Build trong việc thu nhỏ kích thước Docker Image.
  - Hiểu nguyên lý hoạt động của AWS Lambda Web Adapter: Đóng vai trò proxy dịch chuyển từ Lambda invocations sang HTTP requests ở port 8000 và ngược lại.
  - Nắm vững vai trò của `.dockerignore`.
- Practical goals - mục tiêu thực hành:
  - Viết thành công file [Dockerfile](file:///G:/AIProduction_t6_2026/production/week1/day5.md) đa tầng tích hợp Web Adapter.
  - Tạo tệp [.dockerignore](file:///G:/AIProduction_t6_2026/production/week1/day5.md).
  - Build thành công Docker image cục bộ đặt tên `consultation-app`.
  - Khởi chạy container trên máy cá nhân và kiểm tra ứng dụng chạy bình thường tại `http://localhost:8000`.
- What learner should be able to explain - người học cần giải thích được:
  - Tại sao Multi-stage build lại giúp giảm kích thước Docker Image so với việc cài đặt cả Node.js và Python vào chung một môi trường?
  - Tại sao Lambda Web Adapter lại cần thiết khi muốn chạy FastAPI trên môi trường serverless Lambda?

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp việc chuẩn bị mã nguồn ở Bài 27, bài này trực tiếp viết các file cấu hình Docker (`Dockerfile`, `.dockerignore`) để thực hiện đóng gói ứng dụng thành một image hoàn chỉnh chạy được trên máy cục bộ trước khi đẩy lên AWS.

## 5. Core Theory - Lý thuyết cốt lõi
- Multi-stage Build - xây dựng đa tầng:
  - Meaning - nghĩa: Kỹ thuật viết Dockerfile sử dụng nhiều câu lệnh `FROM`. Mỗi stage có thể sử dụng một image nền khác nhau. Lập trình viên có thể sao chép các tệp tin kết quả (artifacts) từ stage này sang stage khác, loại bỏ các công cụ build thừa thãi ở stage cuối cùng.
  - Why it matters - vì sao quan trọng: Giúp image cuối cùng cực kỳ nhẹ (chỉ chứa runtime Python và static files, không chứa compiler Node.js hay thư mục `node_modules` nặng nề), tối ưu tốc độ tải và giảm diện tích tấn công bảo mật.
- AWS Lambda Web Adapter - bộ điều hợp web AWS Lambda:
  - Meaning - nghĩa: Tiện ích mở rộng nguồn mở (extension) của AWS Labs, hoạt động như một tiến trình trung gian bên trong Lambda container để chuyển đổi các sự kiện Lambda invocation thô thành các HTTP request thông thường và chuyển tiếp đến port của ứng dụng web.
  - Why it matters - vì sao quan trọng: Cho phép chạy nguyên vẹn các web framework tiêu chuẩn (như FastAPI, Express) trên AWS Lambda mà không cần sửa đổi bất kỳ dòng code xử lý HTTP nào.
- Response Streaming (AWS_LWA_INVOKE_MODE=response_stream) - chế độ truyền phản hồi phát trực tiếp:
  - Meaning - nghĩa: Biến cấu hình của Lambda Web Adapter yêu cầu adapter hoạt động ở chế độ truyền dữ liệu liên tục theo từng đoạn (chunk) thay vì lưu đệm (buffer) toàn bộ phản hồi rồi mới gửi một lượt.
  - Why it matters - vì sao quan trọng: Đây là yếu tố quyết định giúp tính năng Server-Sent Events (SSE) phát trực tiếp kết quả của mô hình ngôn ngữ lớn (LLM) hiển thị mượt mà trên giao diện người dùng.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Luồng build và chạy thử ứng dụng qua Docker:
1. Input: File cấu hình Dockerfile, mã nguồn, tệp `.env`.
2. Processing steps:
   - Viết Dockerfile cấu hình build Node.js tĩnh -> copy sang image Python -> cấu hình Web Adapter extension.
   - Nạp các biến môi trường từ file `.env` vào terminal.
   - Chạy lệnh `docker build` truyền tham số `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`.
   - Chạy lệnh `docker run` ánh xạ cổng 8000 từ container ra máy chủ và truyền các khóa bảo mật làm biến môi trường lúc khởi chạy.
3. Output: Ứng dụng chạy thành công trên container cục bộ và có thể truy cập qua trình duyệt.

## 7. Techniques - Kỹ thuật sử dụng
- Build Arguments (`ARG` vs `ENV`) - tham số xây dựng so với biến môi trường:
  - Purpose - mục đích: Sử dụng `ARG` để truyền các giá trị cấu hình vào container tại thời điểm build image (ví dụ: Clerk Publishable Key cần được nhúng vào file JS tĩnh trong lúc build frontend), còn `ENV` dùng để thiết lập cấu hình khi container thực sự chạy (ví dụ: OpenAI API Key).
  - When to use - dùng khi nào: Sử dụng `ARG` cho cấu hình frontend tĩnh, dùng `ENV` cho các cấu hình động ở backend.
  - Trade-off - đánh đổi: Các giá trị truyền qua `ARG` sẽ bị nhúng cứng vào các lớp của Docker image và có thể bị đọc lại bằng các lệnh kiểm tra lịch sử image (`docker history`), do đó tuyệt đối không truyền các private secret keys qua `ARG`.
  - Common mistake - lỗi dễ gặp: Truyền Clerk Secret Key thông qua `ARG` làm lộ khóa bảo mật hệ thống.

## 8. Code Walkthrough - Phân tích code nếu có
### File [Dockerfile](file:///G:/AIProduction_t6_2026/production/week1/day5.md) - Multi-stage Serverless Dockerfile (Cập nhật 2026)
- Purpose - mục đích: Cấu hình đóng gói ứng dụng Next.js + FastAPI và cấu hình Lambda Web Adapter.
- Key logic - logic chính: Sử dụng 2 stage (`frontend-builder` và Python runner), chép binary Web Adapter và khai báo biến môi trường cổng.
```dockerfile
# Stage 1: Build các tệp tin tĩnh Next.js
FROM node:22-alpine AS frontend-builder

WORKDIR /app

# Copy các tệp định nghĩa thư viện trước để tối ưu hóa cache của Docker
COPY package*.json ./
RUN npm ci

# Copy toàn bộ mã nguồn dự án vào container
COPY . .

# Khai báo Build Argument nhận khóa công khai Clerk để nhúng vào tệp tĩnh
ARG NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
ENV NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=$NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY

# Biên dịch ứng dụng (xuất kết quả ra thư mục 'out')
RUN npm run build

# Stage 2: Khởi tạo container chạy chính thức dựa trên Python
FROM python:3.12-slim

WORKDIR /app

# --- Tích hợp AWS Lambda Web Adapter ---
# Sao chép binary của Web Adapter từ ECR công khai vào thư mục extensions của Lambda
COPY --from=public.ecr.aws/awsguru/aws-lambda-adapter:1.0.0 /lambda-adapter /opt/extensions/lambda-adapter

# Cấu hình cổng chạy mặc định cho FastAPI bên trong container
ENV PORT=8000

# Kích hoạt chế độ truyền dữ liệu streaming liên tục cho Lambda
ENV AWS_LWA_INVOKE_MODE=response_stream
# --------------------------------------

# Cài đặt các thư viện Python
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy file server FastAPI
COPY api/server.py .

# Copy toàn bộ file static đã build ở Stage 1 vào thư mục static của Stage 2
COPY --from=frontend-builder /app/out ./static

# Thiết lập cơ chế kiểm tra sức khỏe cục bộ (chỉ hoạt động khi chạy local Docker)
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8000/health')"

EXPOSE 8000

# Lệnh khởi chạy server FastAPI uvicorn
CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "8000"]
```

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có tùy chọn kiến trúc mã nguồn bổ sung trong bài thực hành viết Dockerfile này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Lỗi cảnh báo bảo mật nghiêm trọng hoặc thất bại trong quá trình build do dung lượng image quá lớn.
- Root cause - nguyên nhân: Thiếu file `.dockerignore` khiến Docker cố gắng copy toàn bộ thư mục `node_modules` local hoặc thư mục `.next` tạm từ máy vật lý vào container, làm ô nhiễm môi trường build và phình to dung lượng.
- Fix / prevention - cách sửa/phòng tránh: Luôn tạo file `.dockerignore` loại bỏ `node_modules`, `.next`, `.env` tương tự như `.gitignore`.

## 11. Knowledge Extension - Kiến thức mở rộng
- Alpine vs Slim Images: Trong Docker, việc chọn image nền quyết định hiệu năng và dung lượng. `alpine` là dòng image cực nhẹ dựa trên Alpine Linux, sử dụng thư viện `musl libc`. Trong khi đó, `slim` (như `python:3.12-slim`) dựa trên Debian nhưng loại bỏ các gói không cần thiết và sử dụng `glibc` tiêu chuẩn. Đối với Python, khuyến khích sử dụng bản `slim` thay vì `alpine` vì nhiều thư viện C-extensions của Python (như NumPy, pandas) tương thích tốt hơn với `glibc` và tránh lỗi biên dịch phức tạp.

## 12. Study Pack - Gói ôn tập
### Must remember
- Multi-stage build giúp loại bỏ các thư viện build tạm thời, giữ cho image cuối cùng siêu nhẹ.
- AWS Lambda Web Adapter được copy vào `/opt/extensions/lambda-adapter` để đóng vai trò dịch sự kiện.
- Đặt biến `AWS_LWA_INVOKE_MODE` thành `response_stream` là điều kiện bắt buộc để hỗ trợ LLM SSE streaming trên Lambda.
- `.dockerignore` là bắt buộc để ngăn sao chép các tệp tin tạm và secrets vào image.

### Self-check questions
1. Tại sao việc đặt biến môi trường `PORT=8000` trong Dockerfile lại quan trọng đối với AWS Lambda Web Adapter?
2. Sự khác nhau về vai trò của lệnh `ARG` và `ENV` trong Dockerfile của dự án này là gì?
3. Tại sao Docker Desktop hiển thị cảnh báo khi nhận Clerk Publishable Key trong quá trình build và tại sao ta có thể bỏ qua cảnh báo này?

### Flashcards
- Q: Lệnh build Docker image truyền Clerk Key trên Windows PowerShell viết thế nào?
  A: `docker build --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY="$env:NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY" -t consultation-app .`
- Q: Tại sao lệnh `docker run hello-world` chạy rất nhanh ở lần thứ hai?
  A: Do Docker đã lưu image hello-world trong cache cục bộ và không cần tải lại từ Docker Hub.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 29. Day 5 - Deploying Dockerized AI Apps to AWS with ECR and App Runner

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 29).
- Slide: Đã dùng (Trang sơ đồ kết nối ECR và Cloud Deployment).
- Code: Đã dùng (Tham chiếu các file [day5.md](file:///G:/AIProduction_t6_2026/production/week1/day5.md) Part 6 Step 1 đến Step 3 và Part 7 Step 1 & Step 2).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Bài học này có sự chuyển dịch lớn về mặt thực hành hạ tầng. Video hướng dẫn triển khai lên **AWS App Runner**. Tuy nhiên, do App Runner đã ngừng nhận khách hàng mới, tài liệu mới cập nhật hướng dẫn đẩy Docker image lên **Amazon ECR** tương tự video, nhưng sau đó tạo **AWS Lambda Function** dựa trên ECR image này thay thế hoàn toàn cho App Runner Service. Cần lưu ý đặc biệt về việc biên dịch chéo nền tảng (cross-platform build).

## 2. Executive Summary - Tóm tắt cốt lõi
- Giới thiệu Amazon ECR (Elastic Container Registry): Kho lưu trữ Docker images bảo mật trên AWS. Tạo repository riêng tư (Private Repository) tên `consultation-app` trên ECR để chứa image của dự án.
- Thiết lập thông tin xác thực AWS CLI: Tạo Access Key (Access Key ID và Secret Access Key) cho IAM User `aiengineer` trong Security credentials. Cài đặt AWS CLI và chạy cấu hình `aws configure` để lưu trữ thông tin đăng nhập và chọn Region mặc định (ví dụ: `us-east-1`).
- Quy trình đăng nhập ECR từ Docker: Sử dụng lệnh của AWS CLI để lấy token xác thực tạm thời và truyền trực tiếp vào Docker client qua đường ống (`get-login-password`).
- **Lưu ý kỹ thuật quan trọng cho máy Apple Silicon Macs (M1/M2/M3/M4/M5)**: Khi build image để deploy lên cloud AWS, bắt buộc phải truyền flag **`--platform linux/amd64`**. Nếu không, Lambda/App Runner sẽ crash ngay khi khởi động và báo lỗi định dạng thực thi (`Exec format error`) do CPU không tương thích.
- Thực hiện đẩy image lên ECR bằng các lệnh tag và push của Docker.
- Bước chuyển dịch triển khai (April 2026 Update): Sau khi có image trên ECR, thay vì tạo App Runner Service như video, ta vào Lambda Console -> Chọn "Create function" -> Chọn nguồn "Container image" -> Browse chọn ECR image `consultation-app:latest` vừa đẩy lên.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu vai trò của Amazon ECR trong quy trình CI/CD container.
  - Hiểu cơ chế hoạt động của AWS CLI trong việc xác thực và ra lệnh cho tài nguyên cloud.
  - Nhận thức được sự khác biệt kiến trúc CPU (ARM64 vs AMD64) ảnh hưởng đến triển khai container.
- Practical goals - mục tiêu thực hành:
  - Tạo Private Repository trên Amazon ECR.
  - Cấu hình AWS CLI with Access Keys của IAM User `aiengineer`.
  - Đăng nhập thành công Docker vào ECR registry.
  - Thực hiện build image cho nền tảng `linux/amd64` và push lên ECR thành công.
  - Tạo Lambda Function từ ECR container image vừa tải lên.
- What learner should be able to explain - người học cần giải thích được:
  - Tại sao một image build bình thường trên MacBook M1 lại không thể chạy trực tiếp trên môi trường chạy mặc định của AWS Lambda?
  - Cơ chế hoạt động của lệnh đăng nhập Docker vào ECR thông qua AWS CLI.

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp việc build và chạy thử thành công Docker image cục bộ ở Bài 28, bài này đưa image đó lên kho lưu trữ trực tuyến đám mây Amazon ECR và khởi tạo tài nguyên Lambda chứa image đó.

## 5. Core Theory - Lý thuyết cốt lõi
- Elastic Container Registry (ECR) - kho đăng ký vùng chứa đàn hồi:
  - Meaning - nghĩa: Dịch vụ lưu trữ và quản lý Docker container images riêng tư, bảo mật và có khả năng mở rộng cao của AWS.
  - Why it matters - vì sao quan trọng: Nơi lưu trữ trung gian an toàn để các dịch vụ tính toán (Lambda, ECS) có thể kéo image về chạy mà không bị lộ mã nguồn ra ngoài Internet.
- AWS Command Line Interface (CLI) - giao diện dòng lệnh AWS:
  - Meaning - nghĩa: Công cụ hợp nhất giúp quản trị toàn bộ các dịch vụ AWS từ cửa sổ dòng lệnh terminal trên máy tính cá nhân.
  - Why it matters - vì sao quan trọng: Tự động hóa các thao tác quản trị hạ tầng, giúp tích hợp vào các kịch bản build tự động (scripts) và CI/CD pipelines.
- Execution Platform (linux/amd64) - nền tảng thực thi:
  - Meaning - nghĩa: Cấu trúc tập lệnh CPU tiêu chuẩn của hầu hết máy chủ đám mây (x86_64).
  - Why it matters - vì sao quan trọng: Đảm bảo container chạy ổn định trên các máy chủ ảo của AWS, đặc biệt khi máy tính của lập trình viên sử dụng kiến trúc ARM64 của Apple Silicon.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình đẩy Docker Image lên ECR và khởi tạo Lambda (Cập nhật 2026):
1. Input: Dockerfile, mã nguồn, Access Keys của IAM user, AWS Account ID và Region.
2. Processing steps:
   - Tạo repo `consultation-app` trên ECR console.
   - Chạy `aws configure` trong terminal để cấu hình CLI.
   - Chạy lệnh xác thực Docker với ECR qua token.
   - Build image với flag `--platform linux/amd64` và gắn tag khớp với ECR URI: `<Account-ID>.dkr.ecr.<Region>.amazonaws.com/consultation-app:latest`.
   - Chạy `docker push` để đẩy image lên ECR.
   - Truy cập Lambda Console -> Click "Create function" -> Chọn "Container image" -> Đặt tên `consultation-app` -> Browse chọn ECR image vừa push -> Click "Create function".
3. Output: Lambda function được khởi tạo dựa trên Docker image lưu trữ ở ECR.

## 7. Techniques - Kỹ thuật sử dụng
- Cross-Platform Compilation - biên dịch chéo nền tảng:
  - Purpose - mục đích: Build một container image cho một kiến trúc CPU đích (AMD64) khác với kiến trúc CPU hiện tại của máy build (ARM64 trên M1/M2 Mac).
  - When to use - dùng khi nào: Bắt buộc sử dụng khi phát triển ứng dụng trên máy Mac M-series để deploy lên các dịch vụ đám mây chạy chip Intel/AMD tiêu chuẩn.
  - Trade-off - đánh đổi: Thời gian build image lâu hơn đáng kể do Docker Desktop phải chạy giả lập tập lệnh CPU khác qua QEMU.
  - Common mistake - lỗi dễ gặp: Quên flag `--platform linux/amd64` dẫn đến việc build ra image ARM64, làm sập Lambda khi chạy thực tế.

## 8. Code Walkthrough - Phân tích code nếu có
### CLI Commands - ECR Push & Authentication (Windows PowerShell)
- Purpose - mục đích: Xác thực Docker, build, tag và đẩy image lên AWS ECR.
- Key logic - logic chính: Sử dụng biến môi trường nạp từ tệp `.env` để truyền tham số tự động.
```powershell
# 1. Đăng nhập Docker vào ECR (lấy token tạm thời từ AWS và truyền vào stdin của docker login)
aws ecr get-login-password --region $env:DEFAULT_AWS_REGION | docker login --username AWS --password-stdin "$env:AWS_ACCOUNT_ID.dkr.ecr.$env:DEFAULT_AWS_REGION.amazonaws.com"

# 2. Build image chỉ định rõ platform linux/amd64 cho máy chủ cloud
docker build `
  --platform linux/amd64 `
  --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY="$env:NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY" `
  -t consultation-app .

# 3. Gắn tag định dạng đường dẫn ECR của bạn
docker tag consultation-app:latest "$env:AWS_ACCOUNT_ID.dkr.ecr.$env:DEFAULT_AWS_REGION.amazonaws.com/consultation-app:latest"

# 4. Đẩy image lên kho chứa ECR của AWS
docker push "$env:AWS_ACCOUNT_ID.dkr.ecr.$env:DEFAULT_AWS_REGION.amazonaws.com/consultation-app:latest"
```

## 9. Options / Trade-offs - Bản đồ lựa chọn
Không có tùy chọn kiến trúc mã nguồn bổ sung trong bài thực hành ECR này.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Lỗi đăng nhập thất bại `docker login ... unauthorized` khi chạy lệnh xác thực ECR.
- Root cause - nguyên nhân: AWS CLI cấu hình Access Key của user không đúng, hoặc user `aiengineer` thiếu chính sách quyền `AmazonEC2ContainerRegistryFullAccess` trong IAM.
- Fix / prevention - cách sửa/phòng tránh: Kiểm tra lại file cấu hình AWS CLI, đăng nhập tài khoản Root để kiểm tra và gán đúng chính sách quyền ECR vào group của user.

## 11. Knowledge Extension - Kiến thức mở rộng
- ECR Lifecycle Policies: ECR tính phí lưu trữ dựa trên dung lượng ($0.10/GB/month). Khi đẩy các bản build mới với tag `latest`, các bản build cũ sẽ bị mất tag (trở thành trạng thái *untagged* hoặc *orphan* image) nhưng vẫn tiêu tốn dung lượng lưu trữ trên ECR. Việc cấu hình Lifecycle Policy trên ECR để tự động xóa các image không gắn tag cũ hơn 14 ngày là kỹ thuật tối ưu hóa chi phí đám mây quan trọng cho doanh nghiệp.

## 12. Study Pack - Gói ôn tập
### Must remember
- Amazon ECR là kho chứa Docker images riêng tư và an toàn trên đám mây AWS.
- Cấu hình AWS CLI bằng lệnh `aws configure` với thông tin Access Key của IAM User.
- Flag `--platform linux/amd64` là bắt buộc khi build image trên Apple Silicon Mac để deploy lên cloud.
- AWS Lambda hỗ trợ tạo hàm trực tiếp từ một Docker container image tối đa 10GB.

### Self-check questions
1. Lỗi `Exec format error` trong log của AWS Lambda xảy ra do nguyên nhân gì và cách khắc phục như thế nào?
2. Lệnh `aws ecr get-login-password` thực hiện nhiệm vụ gì trong chuỗi lệnh đẩy Docker image?
3. Tại sao chúng ta nên sử dụng kho lưu trữ Private trên ECR thay vì Public?

### Flashcards
- Q: Lệnh nào dùng để cấu hình thông tin đăng nhập AWS CLI?
  A: Lệnh `aws configure`.
- Q: Kích thước tối đa của một container image được AWS Lambda hỗ trợ là bao nhiêu?
  A: Tối đa 10GB.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 30. Day 5 - Deploying Your AI App Live on AWS App Runner with Auto-Scaling

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 30).
- Slide: Đã dùng (Trang slide cấu hình hạ tầng trực tuyến và kiểm tra ứng dụng).
- Code: Đã dùng (Tham chiếu các file [day5.md](file:///G:/AIProduction_t6_2026/production/week1/day5.md) Part 7 Step 3 đến Step 6, Part 8 và Part 9).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Đây là phần có sự thay đổi triệt để nhất do chính sách bảo trì của AWS đối với App Runner. Video hướng dẫn cấu hình App Runner Service (v CPU, RAM, Auto Scaling Basic, Health Check path `/health`, v.v.). **Tài liệu mới thay thế bằng việc cấu hình Lambda Function**. Chúng ta sẽ trình bày chi tiết cấu hình Lambda mới nhưng vẫn giữ thông tin đối chiếu với App Runner cũ để làm tài liệu học tập toàn diện.

## 2. Executive Summary - Tóm tắt cốt lõi
- Di chuyển hạ tầng sang AWS Lambda Container (Thay thế cho App Runner):
  - Cấu hình tài nguyên: Thiết lập dung lượng bộ nhớ RAM của Lambda ở mức **1024 MB** và thời gian chạy tối đa (Timeout) là **5 phút (300 giây)** để đảm bảo đủ không gian bộ nhớ cho FastAPI + Next.js static handler và thời gian chờ luồng OpenAI streaming phản hồi.
  - Thiết lập cơ chế thắt trần chi phí (Budget Protection): Cấu hình **Reserved Concurrency (Số luồng chạy đồng thời dự phòng) ở mức cố định là 2**. Điều này giới hạn tối đa chỉ có 2 container chạy song song, bảo vệ tài khoản khỏi chi phí khổng lồ khi bị bot tấn công hoặc lặp vô tận.
  - **Cảnh báo cực kỳ quan trọng**: Tuyệt đối không bật Provisioned Concurrency (Số luồng được duy trì sẵn) vì tính năng này tính phí liên tục ngay cả khi không có request nào đến (idle).
  - Cấu hình các biến môi trường cho Lambda: `CLERK_SECRET_KEY`, `CLERK_JWKS_URL`, `OPENAI_API_KEY`.
- Thiết lập **Lambda Function URL (Đường dẫn hàm trực tiếp)** làm endpoint HTTPS công khai:
  - Auth Type: **NONE** (vì chúng ta tự thực hiện xác thực bằng Clerk Bearer JWT ở mã nguồn).
  - Invoke Mode: **RESPONSE_STREAM** (Yếu tố cốt lõi giúp SSE streaming hoạt động, nếu để BUFFERED thì trình duyệt sẽ bị đơ và nhận kết quả một lượt).
- Hướng dẫn giám sát và debug: Sử dụng CloudWatch Logs để kiểm tra log startup của uvicorn và các lỗi traceback Python.
- Cách thức cập nhật ứng dụng: Khi có code mới, chạy build, push lên ECR, sau đó kích hoạt cập nhật Lambda bằng câu lệnh CLI `aws lambda update-function-code`.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cơ chế định cấu hình tài nguyên (RAM, Timeout) ảnh hưởng đến hiệu năng serverless.
  - Nắm vững khái niệm Concurrency (Reserved vs Provisioned) và tác động của nó đến chi phí đám mây.
  - Hiểu cơ chế hoạt động của Function URLs và chế độ truyền dữ liệu RESPONSE_STREAM.
- Practical goals - mục tiêu thực hành:
  - Cấu hình hoàn chỉnh dung lượng RAM và Timeout cho Lambda Function.
  - Thiết lập giới hạn Reserved Concurrency = 2.
  - Tạo Function URL với Auth Type: NONE và Invoke Mode: RESPONSE_STREAM.
  - Truy cập Function URL, đăng nhập ứng dụng qua Clerk và xác minh kết quả summary y tế được stream chữ theo chữ (SSE).
  - Tra cứu log hệ thống trong CloudWatch Logs để xử lý lỗi.
- What learner should be able to explain - người học cần giải thích được:
  - Sự khác nhau giữa Reserved Concurrency và Provisioned Concurrency là gì và tại sao Provisioned Concurrency lại gây tốn chi phí?
  - Tại sao chế độ RESPONSE_STREAM lại bắt buộc đối với các API trả về luồng dữ liệu liên tục như OpenAI stream?

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp việc khởi tạo Lambda Function từ Docker image ở Bài 29, bài này hoàn thiện các cấu hình vận hành (RAM, timeout, concurrency, network endpoint) để đưa ứng dụng chính thức đi vào hoạt động thực tế.

## 5. Core Theory - Lý thuyết cốt lõi
- Reserved Concurrency - số luồng chạy đồng thời được dự phòng (Giới hạn trần):
  - Meaning - nghĩa: Hạn mức tối đa số lượng container instance của một Lambda function được phép chạy đồng thời tại bất kỳ thời điểm nào.
  - Why it matters - vì sao quan trọng: Đóng vai trò là một chốt chặn chi phí (cost ceiling). Khi vượt quá hạn mức, Lambda sẽ tự động trả về lỗi HTTP 429 (Too Many Requests) thay vì tự động mở rộng vô hạn gây phát sinh chi phí lớn.
- Provisioned Concurrency - số luồng chạy đồng thời được cung cấp sẵn (Duy trì ấm):
  - Meaning - nghĩa: Tính năng chuẩn bị sẵn một số lượng container nhất định luôn ở trạng thái "ấm" (chạy sẵn trong bộ nhớ) để triệt tiêu hoàn toàn độ trễ khởi động lạnh (cold start).
  - Why it matters - vì sao quan trọng: Tính năng này tính phí theo thời gian duy trì kể cả khi không có request nào đến, do đó không phù hợp cho các dự án thử nghiệm hoặc học tập cần tối ưu chi phí.
- Response Streaming Function URL - đường dẫn hàm phát trực tiếp phản hồi:
  - Meaning - nghĩa: Tính năng của Lambda Function URL cho phép trả dữ liệu dần về cho client ngay khi ứng dụng tạo ra (chunk-by-chunk), thay vì đợi phản hồi hoàn tất.
  - Why it matters - vì sao quan trọng: Công nghệ nền tảng để hiển thị nội dung tạo sinh của AI theo thời gian thực (real-time generation) trên trình duyệt web.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình triển khai ứng dụng cập nhật (Cập nhật 2026):
1. Input: Lambda Function đã tạo, các khóa cấu hình bảo mật.
2. Processing steps:
   - Tại Lambda Console -> tab Configuration -> General configuration: Sửa RAM thành `1024 MB`, Timeout thành `5 min`.
   - Vào Concurrency and recursion detection -> Chọn "Reserve concurrency" -> Nhập `2` -> Save. (Để trống mục Provisioned concurrency).
   - Vào Environment variables: Nhập `CLERK_SECRET_KEY`, `CLERK_JWKS_URL`, `OPENAI_API_KEY`.
   - Vào Function URL -> "Create function URL" -> Chọn Auth type: NONE -> Chọn Invoke mode: RESPONSE_STREAM -> Click Save.
   - Click vào đường dẫn Function URL sinh ra để mở trình duyệt kiểm tra -> Đăng nhập -> Điền ghi chú khám -> Click Generate.
3. Output: Ứng dụng y tế chạy live ổn định với URL HTTPS công khai, hỗ trợ streaming chữ từng chữ.

## 7. Techniques - Kỹ thuật sử dụng
- Serverless Budget Ceiling - thắt trần chi phí serverless:
  - Purpose - mục đích: Thiết lập giới hạn cứng về mặt tài nguyên chạy đồng thời để tránh rủi ro tài chính do lỗi code lặp vô tận hoặc bị tấn công DDoS.
  - When to use - dùng khi nào: Luôn áp dụng cho mọi dự án serverless thử nghiệm trên môi trường AWS cá nhân.
  - Trade-off - đánh đổi: Ứng dụng sẽ bị nghẽn (throttled) và trả về lỗi 429 cho người dùng nếu lượng truy cập thực tế vượt quá giới hạn 2 cuộc gọi đồng thời.
  - Common mistake - lỗi dễ gặp: Quên cấu hình Reserved Concurrency khiến Lambda tự động scale lên tới 1000 instances mặc định khi bị tấn công, làm phát sinh hóa đơn khổng lồ chỉ trong vài giờ.

## 8. Code Walkthrough - Phân tích code nếu có
### CLI Commands - Redeployment Script (Windows PowerShell)
- Purpose - mục đích: Cập nhật mã nguồn ứng dụng chạy trên Lambda mà không cần mở giao diện console.
- Key logic - logic chính: Đẩy image mới lên ECR sau đó yêu cầu Lambda tải lại mã nguồn từ URI image đó.
```powershell
# 1. Thực hiện build, tag và push image mới lên ECR (tương tự các bước ở Bài 29)
docker build --platform linux/amd64 --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY="$env:NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY" -t consultation-app .
docker tag consultation-app:latest "$env:AWS_ACCOUNT_ID.dkr.ecr.$env:DEFAULT_AWS_REGION.amazonaws.com/consultation-app:latest"
docker push "$env:AWS_ACCOUNT_ID.dkr.ecr.$env:DEFAULT_AWS_REGION.amazonaws.com/consultation-app:latest"

# 2. Ra lệnh cho AWS Lambda cập nhật code từ image ECR mới nhất
aws lambda update-function-code `
  --function-name consultation-app `
  --image-uri "$env:AWS_ACCOUNT_ID.dkr.ecr.$env:DEFAULT_AWS_REGION.amazonaws.com/consultation-app:latest" `
  --region $env:DEFAULT_AWS_REGION
```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- **Lựa chọn**: Invoke Mode của Function URL: RESPONSE_STREAM vs BUFFERED.
  - *Option 1 (RESPONSE_STREAM)*: Truyền dữ liệu dạng stream.
    - Pros: Hỗ trợ Server-Sent Events (SSE); trải nghiệm người dùng tuyệt vời vì thấy chữ chạy ra lập tức; không bị giới hạn dung lượng phản hồi 6MB của Lambda thông thường (hỗ trợ lên tới 20MB).
    - Cons: Tải tính toán trên mạng kết nối cao hơn; đòi hỏi cấu hình Web Adapter phù hợp.
    - When to choose: Bắt buộc cho các ứng dụng tích hợp LLM chat, chatbot, sinh tài liệu dài trực tuyến.
  - *Option 2 (BUFFERED)*: Lưu đệm toàn bộ phản hồi trước khi gửi.
    - Pros: Dễ lập trình; tương thích hoàn toàn với tất cả các API Gateway truyền thống; dễ xử lý lỗi HTTP ở tầng mạng.
    - Cons: Người dùng phải chờ đợi lâu (phải đợi LLM sinh xong toàn bộ tài liệu y khoa trong 10-20 giây mới thấy phản hồi hiển thị một lượt); giới hạn dung lượng phản hồi cứng là 6MB.
    - When to choose: Các ứng dụng REST API truyền thống trả về dữ liệu JSON ngắn, xử lý nghiệp vụ nhanh.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode - lỗi thường gặp: Kết quả summary từ OpenAI không hiển thị mượt mà mà bị đơ khoảng 15 giây rồi xuất hiện toàn bộ một lúc.
- Root cause - nguyên nhân: Cấu hình Invoke Mode của Lambda Function URL bị đặt nhầm thành `BUFFERED` (mặc định của AWS khi tạo URL), khiến toàn bộ các chunk dữ liệu SSE bị AWS lưu đệm lại.
- Fix / prevention - cách sửa/phòng tránh: Vào tab Configuration -> Function URL -> Click Edit -> Chọn **RESPONSE_STREAM** tại mục Invoke mode và lưu lại.

## 11. Knowledge Extension - Kiến thức mở rộng
- Lambda Cold Starts: Khi một hàm Lambda không có lượt truy cập trong khoảng 15 phút, AWS sẽ tự động hủy container instance để tiết kiệm tài nguyên (scale to zero). Request tiếp theo đến sẽ kích hoạt quá trình "khởi động lạnh" (cold start) - AWS phải cấp phát máy ảo, kéo Docker image từ ECR, dựng container và khởi động FastAPI. Quá trình này mất khoảng 10-30 giây. Các request tiếp sau đó khi container đã "ấm" sẽ phản hồi cực nhanh (sub-second). Đây là sự đánh đổi về mặt hiệu năng để đổi lấy chi phí bằng không khi rảnh rỗi.

## 12. Study Pack - Gói ôn tập
### Must remember
- Cấu hình dung lượng RAM 1024MB và Timeout 5 phút cho Lambda Function chạy container.
- Luôn đặt Reserved Concurrency = 2 để khống chế chi phí tối đa.
- Không bật Provisioned Concurrency cho các dự án thử nghiệm để tránh mất phí duy trì container ấm.
- Chọn Invoke Mode là RESPONSE_STREAM để hỗ trợ streaming SSE.
- Cập nhật code Lambda bằng lệnh `aws lambda update-function-code`.

### Self-check questions
1. Tại sao tính năng Reserved Concurrency lại được ví như một "lưới an toàn tài chính" khi triển khai ứng dụng serverless?
2. Sự khác nhau giữa lỗi 502 (Bad Gateway) và lỗi 503 (Service Unavailable) khi truy cập Function URL của Lambda là gì?
3. Tại sao request đầu tiên truy cập vào Function URL sau một thời gian dài không hoạt động lại phản hồi chậm (mất 10-30 giây)?

### Flashcards
- Q: Lệnh CLI nào dùng để cập nhật code cho Lambda từ image mới?
  A: Lệnh `aws lambda update-function-code --function-name <name> --image-uri <uri> --region <region>`.
- Q: CloudWatch Logs lưu trữ log của Lambda dưới đường dẫn log group nào mặc định?
  A: `/aws/lambda/<function-name>`.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 31. Day 5 - From Vercel to AWS - Deploying Production LLM Apps at Scale

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 31).
- Slide: Đã dùng (Trang tổng kết Week 1).
- Code: Không có code dự án được tạo ở bài học này (bài học tổng kết lý thuyết).
- Summary lịch sử: Đã dùng (Đọc toàn bộ [day1_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day1_summary.md), [day2_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/day2_summary.md), [day3_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/day3_summary.md), [day4_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/day4_summary.md)).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn nhất quán. Tổng kết toàn bộ lộ trình Week 1 từ Vercel sang AWS Lambda.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học tổng kết lại chặng đường học tập của Week 1: Xây dựng một ứng dụng SaaS AI hoàn chỉnh (Healthcare Consultation Assistant) và triển khai thành công lên hai môi trường khác nhau: Vercel (nhanh, dễ dàng) và AWS (phức tạp, chuẩn công nghiệp).
- So sánh sự tương phản sâu sắc giữa hai môi trường:
  - Vercel: Trải nghiệm lập trình viên tuyệt vời (Zero-config, tự động deploy từ Git), nhưng bị giới hạn về công nghệ (chủ yếu tối ưu cho Next.js/JavaScript, khó chạy các ngôn ngữ khác).
  - AWS: Đòi hỏi cấu hình hạ tầng phức tạp (IAM, Regions, ECR, Lambda, CLI) nhưng đem lại quyền kiểm soát tuyệt đối, hỗ trợ Docker container tùy biến (bất kỳ ngôn ngữ nào, dung lượng lên tới 10GB).
- Phân tích so sánh chi phí vận hành (Lambda Container vs App Runner vs ECS Express Mode):
  - **AWS Lambda Container**: Tự động scale to zero khi không có tải. Chi phí cực kỳ rẻ (gần như $0/tháng cho quy mô thử nghiệm do Free Tier cho 1 triệu request và 400.000 GB-giây miễn phí hàng tháng). ECR lưu trữ tốn khoảng $0.05 - $0.10/tháng.
  - **AWS App Runner** (Cũ): Đòi hỏi duy trì tối thiểu 1 instance luôn chạy, tốn khoảng $5-6/tháng tối thiểu.
  - **Amazon ECS Express Mode**: Đòi hỏi Application Load Balancer hoạt động liên tục, chi phí tối thiểu ~$16-20/tháng kể cả khi rảnh rỗi.
  - Kết luận: Lambda Container kết hợp Web Adapter là giải pháp tối ưu nhất cho nhà phát triển độc lập (solopreneur) và các dự án MVP.
- Nhắc lại kiến thức tổng quan của Week 1: Frontend Next.js Pages Router + Tailwind CSS, Backend FastAPI, Clerk Auth & Billing (Stripe), OpenAI Streaming API, Docker multi-stage build.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Khái quát hóa kiến trúc toàn cục của ứng dụng SaaS AI từ client đến LLM và hạ tầng đám mây.
  - Đánh giá ưu nhược điểm và chi phí của các phương án triển khai đám mây (Vercel vs AWS Lambda vs ECS).
- Practical goals - mục tiêu thực hành:
  - Tự tin thực hiện quy trình đóng gói và cập nhật ứng dụng container hóa bằng Docker CLI và AWS CLI.
  - Kiểm tra và tối ưu hóa chi phí trên AWS Billing dashboard định kỳ.
- What learner should be able to explain - người học cần giải thích được:
  - Tại sao AWS Lambda lại được đánh giá là giải pháp deploy Docker container tiết kiệm nhất cho các dự án khởi nghiệp giai đoạn đầu?
  - Giải thích bối cảnh khi nào nên chọn Vercel và khi nào nên chuyển dịch sang AWS.

## 4. Previous Context - Liên hệ với bài trước
Bài học này là phần tổng kết toàn diện của toàn bộ Week 1, xâu chuỗi tất cả các kiến thức từ Day 1 đến Day 5 thành một bức tranh kiến trúc hệ thống thống nhất.

## 5. Core Theory - Lý thuyết cốt lõi
- Scale to Zero - tự động thu nhỏ về không:
  - Meaning - nghĩa: Khả năng của hạ tầng đám mây tự động tắt toàn bộ các tài nguyên tính toán (container instances) của ứng dụng khi không phát sinh bất kỳ yêu cầu truy cập nào từ phía người dùng.
  - Why it matters - vì sao quan trọng: Giúp tối ưu hóa chi phí triệt để, đảm bảo bạn chỉ trả tiền cho thời gian CPU thực sự xử lý request của khách hàng.
- Consolidated Docker Architecture - kiến trúc Docker hợp nhất:
  - Meaning - nghĩa: Phương pháp đóng gói cả giao diện người dùng tĩnh và API backend vào trong một Docker image duy nhất chạy trên một web server Python.
  - Why it matters - vì sao quan trọng: Giúp quy trình triển khai lên các dịch vụ serverless container đơn giản hơn gấp nhiều lần so với việc duy trì hạ tầng vi dịch vụ (microservices) phân tán.
- Cold Start Mitigation - giảm thiểu khởi động lạnh:
  - Meaning - nghĩa: Tập hợp các kỹ thuật (như tối giản kích thước Docker image, giảm dung lượng import thư viện Python, sử dụng cơ chế warming) nhằm rút ngắn thời gian khởi động container lần đầu của Lambda.
  - Why it matters - vì sao quan trọng: Giúp cải thiện trải nghiệm người dùng, tránh việc khách hàng đầu tiên phải chờ đợi quá lâu khi truy cập hệ thống.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Kiến trúc luồng xử lý toàn cục của hệ thống SaaS AI (End-to-End Pipeline):
1. Input: Người dùng đăng nhập qua Clerk -> Điền form thông tin trên frontend Next.js -> Gửi request kèm Bearer JWT Token đến AWS Lambda Function URL.
2. Processing steps:
   - AWS Lambda nhận yêu cầu -> kích hoạt container (khởi động lạnh nếu rảnh rỗi) -> Lambda Web Adapter chuyển sự kiện thành HTTP POST gửi cho FastAPI chạy trên cổng 8000.
   - FastAPI giải mã và xác thực token qua Clerk JWKS URL.
   - FastAPI gọi OpenAI API completions với chế độ stream.
   - FastAPI nhận stream từ OpenAI, format thành định dạng SSE và gửi ngược về cho Lambda Web Adapter dưới dạng chunk dữ liệu.
   - Lambda Function URL ở chế độ `RESPONSE_STREAM` lập tức chuyển tiếp dữ liệu về trình duyệt của khách hàng.
3. Output: Frontend nhận SSE và hiển thị văn bản summary y khoa stream chữ từng chữ theo thời gian thực.

## 7. Techniques - Kỹ thuật sử dụng
- Serverless Container Deployment - triển khai container không máy chủ:
  - Purpose - mục đích: Chạy các ứng dụng đóng gói Docker trên hạ tầng đám mây mà không cần quản trị hệ điều hành máy chủ hay cấu hình load balancer thủ công.
  - When to use - dùng khi nào: Sử dụng khi cần đưa ứng dụng Docker lên cloud nhanh, chịu tải tự động tốt và chi phí thấp.
  - Trade-off - đánh đổi: Phải chấp nhận hiện tượng khởi động lạnh (cold start) ở request đầu tiên.
  - Common mistake - lỗi dễ gặp: Thiết lập dung lượng RAM quá thấp (ví dụ: 128MB) dẫn đến việc container bị thiếu bộ nhớ (Out of Memory) và crash liên tục khi khởi động FastAPI.

## 8. Code Walkthrough - Phân tích code nếu có
`Buổi học này không có code được cung cấp` (Bài học tổng kết lý thuyết).

## 9. Options / Trade-offs - Bản đồ lựa chọn
- **Lựa chọn**: Nền tảng triển khai đám mây cho ứng dụng SaaS AI.
  - *Option 1: Vercel Serverless*.
    - Pros: Triển khai cực nhanh; tích hợp Git tốt; CDN phân tán toàn cầu; trải nghiệm UI mượt mà.
    - Cons: Giới hạn thời gian chạy hàm (thường là 10-15 giây ở gói miễn phí, dễ bị lỗi timeout khi OpenAI phản hồi chậm); chỉ hỗ trợ tốt JavaScript/TypeScript; chi phí tăng vọt khi quy mô lớn.
    - When to choose: Phù hợp cho giai đoạn thử nghiệm giao diện, xây dựng sản phẩm mẫu nhanh.
  - *Option 2: AWS Lambda Container + Web Adapter*.
    - Pros: Hỗ trợ mọi ngôn ngữ (Python, Go, Rust); timeout lên tới 15 phút; chi phí Free Tier cực lớn; scale to zero tự động; hỗ trợ streaming response không giới hạn thời gian qua Function URL.
    - Cons: Cấu hình hạ tầng phức tạp; gặp hiện tượng khởi động lạnh (cold start).
    - When to choose: Phù hợp cho ứng dụng AI có xử lý logic backend phức tạp, đòi hỏi thời gian chạy lâu và truyền dữ liệu streaming lớn.
  - *Option 3: Amazon ECS Express Mode / Fargate*.
    - Pros: Không có độ trễ khởi động lạnh; phù hợp cho các tiến trình chạy ngầm liên tục (background workers); hiệu năng CPU/RAM ổn định cao.
    - Cons: Hóa đơn tối thiểu đắt đỏ do Application Load Balancer chạy liên tục; cấu hình mạng (VPC, Security Groups) cực kỳ phức tạp.
    - When to choose: Khi ứng dụng có lượng truy cập liên tục lớn, yêu cầu độ trễ phản hồi cực thấp và ngân sách dồi dào.

## 10. Pitfalls - Lỗi / bẫy thường gặp
Không có lỗi kỹ thuật đặc thù trong bài tổng kết lý thuyết này.

## 11. Knowledge Extension - Kiến thức mở rộng
- CI/CD Automation with GitHub Actions: Trong thực tế sản xuất, việc chạy thủ công các lệnh build và push Docker lên ECR từ máy cá nhân rất dễ xảy ra lỗi cấu hình. Phương pháp chuẩn là thiết lập một luồng tự động hóa bằng GitHub Actions: Khi lập trình viên push code mới lên nhánh `main`, GitHub runner sẽ tự động thực hiện login AWS, build platform amd64, push lên ECR và ra lệnh cho Lambda update code một cách an toàn và tự động.

## 12. Study Pack - Gói ôn tập
### Must remember
- AWS Lambda Container tự động scale về 0 giúp tiết kiệm tối đa chi phí vận hành cho MVP.
- Vercel tối ưu cho frontend Git-integrated, AWS tối ưu cho container backend đa dạng và khả năng tùy biến cao.
- Không dùng ECS Express Mode cho các dự án nhỏ vì chi phí Load Balancer cố định tối thiểu rất đắt đỏ.
- Hiểu toàn bộ luồng dữ liệu từ Client -> Clerk (Auth) -> Lambda (FastAPI) -> OpenAI (LLM) -> Client.

### Self-check questions
1. So sánh sự khác nhau về mặt kinh tế (chi phí) giữa việc chạy ứng dụng trên AWS Lambda, AWS App Runner và Amazon ECS Express Mode?
2. Trong những trường hợp nào thì bạn nên ưu tiên sử dụng Vercel thay vì chuyển dịch sang AWS?
3. Kiến trúc Single Container của chúng ta giải quyết được điểm đau nào trong việc thiết lập hệ thống mạng và DNS trên AWS?

### Flashcards
- Q: Cold start là gì?
  A: Độ trễ khởi động container của Lambda từ trạng thái không hoạt động khi nhận request đầu tiên.
- Q: ECR lưu trữ Docker image tiêu tốn chi phí khoảng bao nhiêu một tháng?
  A: Khoảng $0.05 - $0.10 cho mỗi GB ảnh lưu trữ.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.
