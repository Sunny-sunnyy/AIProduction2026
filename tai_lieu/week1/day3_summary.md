# Day 3 Summary: Adding User Authentication & Subscription Billing (Clerk & Stripe)

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

---

# 15. Day 3 - Adding User Authentication to Your Production AI Application

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 15).
- Slide: Đã dùng (Trang tóm tắt tổng quan Day 3).
- Code: Đã dùng (Tham chiếu file [day3.md](file:///G:/AIProduction_t6_2026/production/week1/day3.md) để hiểu bối cảnh tích hợp).
- Summary lịch sử: Đã dùng (Đọc [day2_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day2_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin hoàn toàn nhất quán. Giảng viên tóm tắt lại kiến trúc full-stack từ Day 2 và giới thiệu lộ trình của Day 3.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học giới thiệu chủ đề trọng tâm của Day 3: Tích hợp hai thành phần cốt lõi của một ứng dụng SaaS thực tế là User authentication (xác thực người dùng) và Subscription billing (thanh toán gói thuê bao).
- Giảng viên cảnh báo về độ khó của việc triển khai cloud: Tuần này sử dụng Vercel nên việc deploy rất đơn giản, nhưng các tuần tiếp theo sẽ chuyển sang AWS, GCP, Azure - một "vũ trụ hoàn toàn khác" đòi hỏi cấu hình phức tạp hơn nhiều.
- Cấu trúc thư mục được phân tách rõ ràng thành hai repository: repo `production` chứa tài liệu hướng dẫn/slides học tập và repo `sass` chứa mã nguồn thực tế của học viên xây dựng từ đầu (from scratch) để rèn luyện thói quen viết code sạch.
- Khuyến khích văn hóa cộng đồng: Học viên được khuyến khích tạo Pull Request (PR) đóng góp ghi chú, mã nguồn hoặc các bản vá lỗi vào thư mục `community_contributions`.
- Giới thiệu giải pháp Clerk: Nền tảng xác thực hiện đại, gọn nhẹ giúp lập trình viên nhanh chóng tích hợp đăng nhập mạng xã hội (social auth) và quản lý người dùng với lượng code tối thiểu, tránh việc mất hàng tuần hoặc hàng tháng để tự xây dựng hệ thống xác thực từ đầu.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu rõ tại sao một ứng dụng AI cần có lớp xác thực người dùng trước khi thương mại hóa hoặc giới hạn truy cập.
  - Phân biệt được vai trò của hai repository: repository tài liệu học tập (`production`) và repository ứng dụng thực hành (`sass`).
  - Nắm được khái niệm cơ bản về cách Clerk hỗ trợ giảm thiểu thời gian phát triển tính năng xác thực và quản lý tài khoản.
- Practical goals - mục tiêu thực hành:
  - Thiết lập cấu trúc thư mục làm việc độc lập cho dự án SaaS.
  - Biết cách định vị các tài liệu hướng dẫn tự học và khu vực đóng góp của cộng đồng.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích được cấu trúc giao tiếp cơ bản giữa Frontend (Next.js) và Backend (FastAPI) trong luồng ứng dụng được bảo mật.
  - Giải thích lý do tại sao nên sử dụng một dịch vụ xác thực bên thứ ba như Clerk thay vì tự xây dựng cơ chế đăng ký/đăng nhập từ đầu cho các sản phẩm MVP (Minimum Viable Product).

## 4. Previous Context - Liên hệ với bài trước
Nối tiếp Day 2 ([day2_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day2_summary.md)): Ở Day 2, học viên đã hoàn thành và triển khai thành công ứng dụng Business Idea Generator full-stack dạng mở (ai cũng có thể truy cập và sử dụng không giới hạn). Bài học này đặt nền móng để bảo mật và thương mại hóa ứng dụng đó bằng cách yêu cầu đăng nhập trước khi sử dụng.

## 5. Core Theory - Lý thuyết cốt lõi
- User authentication - xác thực người dùng:
  - Meaning - nghĩa: Quá trình xác minh danh tính của một thực thể (người dùng) cố gắng truy cập vào hệ thống.
  - Why it matters - vì sao quan trọng: Ngăn chặn người dùng trái phép truy cập tài nguyên, bảo vệ dữ liệu cá nhân và làm cơ sở để đo lường lượng sử dụng (usage tracking).
- Subscription billing - thanh toán gói thuê bao:
  - Meaning - nghĩa: Mô hình kinh doanh trong đó người dùng trả một khoản phí định kỳ (hàng tháng/hàng năm) để duy trì quyền truy cập vào sản phẩm hoặc dịch vụ.
  - Why it matters - vì sao quan trọng: Là mô hình tạo doanh thu cốt lõi của các ứng dụng SaaS (Software as a Service).
- Repository separation - phân tách kho lưu trữ:
  - Meaning - nghĩa: Việc chia tách mã nguồn dự án thực tế của học viên và kho lưu trữ chứa tài liệu/hướng dẫn học tập chung.
  - Why it matters - vì sao quan trọng: Đảm bảo mã nguồn deploy lên production không bị lẫn tài liệu rác, giúp việc quản lý môi trường trên Vercel hoặc các nền tảng cloud sạch sẽ và chuyên nghiệp hơn.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
`Không có pipeline rõ ràng trong tài liệu nguồn`
Bài học này mang tính chất giới thiệu và định hướng tổng quan cho ngày học thứ 3 nên không chứa quy trình xử lý dữ liệu kỹ thuật cụ thể.

## 7. Techniques - Kỹ thuật sử dụng
- Repository Isolation - cô lập kho lưu trữ:
  - Purpose - mục đích: Đảm bảo mã nguồn ứng dụng thực tế chạy độc lập với tài nguyên học tập, tránh các lỗi xung đột biến môi trường hoặc cấu hình khi deploy.
  - When to use - dùng khi nào: Thực hiện ngay từ khi bắt đầu viết dòng code đầu tiên cho dự án SaaS thương mại.
  - Trade-off - đánh đổi: Người phát triển phải chuyển đổi qua lại giữa các cửa sổ thư mục hoặc editor để vừa đọc hướng dẫn vừa viết code.
  - Common mistake - lỗi dễ gặp: Code đè trực tiếp lên kho lưu trữ hướng dẫn chung, dẫn đến khó khăn khi cập nhật bài học mới từ tác giả hoặc lộ thông tin cấu hình cá nhân khi đẩy code lên git.

## 8. Code Walkthrough - Phân tích code nếu có
`Code được cung cấp trong session nhưng chưa thấy code liên quan trực tiếp tới lesson này.`
(Bài học này thuần lý thuyết giới thiệu bối cảnh repo và chuẩn bị môi trường).

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Tự viết hệ thống quản lý người dùng và xác thực (Custom Auth).
  - Pros - ưu điểm: Kiểm soát 100% dữ liệu người dùng, không phụ thuộc vào nhà cung cấp bên thứ ba, không tốn phí dịch vụ xác thực khi lượng người dùng tăng cao.
  - Cons - nhược điểm: Tốn rất nhiều thời gian phát triển (có thể mất từ vài tuần đến hàng tháng), dễ gặp các lỗ hổng bảo mật nghiêm trọng nếu không có chuyên môn sâu về an ninh mạng.
  - When to choose - khi nào chọn: Khi xây dựng các ứng dụng của doanh nghiệp lớn có yêu cầu khắt khe về việc lưu trữ dữ liệu người dùng tại chỗ (on-premise) hoặc có đội ngũ kỹ sư bảo mật chuyên trách.
- Option 2: Sử dụng các dịch vụ Identity Provider (IdP) đám mây như Clerk.
  - Pros - ưu điểm: Tích hợp cực kỳ nhanh chóng (chỉ mất vài phút), có sẵn giao diện đăng nhập đẹp mắt, hỗ trợ tích hợp đăng nhập bằng Google/Github/Apple ngay lập tức, độ bảo mật đạt chuẩn công nghiệp.
  - Cons - nhược điểm: Phụ thuộc vào tính ổn định của bên thứ ba, có thể phát sinh chi phí hàng tháng khi số lượng người dùng hoạt động (MAU - Monthly Active Users) vượt quá hạn mức miễn phí.
  - When to choose - khi nào chọn: Rất phù hợp cho các dự án khởi nghiệp, các sản phẩm MVP cần đưa ra thị trường nhanh nhất có thể để kiểm chứng ý tưởng kinh doanh.

## 10. Pitfalls - Lỗi / bẫy thường gặp
Không có lỗi kỹ thuật hoặc sự cố cụ thể nào được ghi nhận trong bài học lý thuyết giới thiệu này.

## 11. Knowledge Extension - Kiến thức mở rộng
- AWS Cognito: Dịch vụ quản lý định danh và xác thực người dùng của AWS. Mặc dù rất mạnh mẽ và tích hợp sâu vào hệ sinh thái AWS, Cognito nổi tiếng với cấu hình cực kỳ phức tạp và giao diện mặc định thô sơ, thường đòi hỏi lập trình viên phải tự xây dựng lại giao diện đăng nhập từ đầu. Điều này giải thích tại sao Clerk là lựa chọn tối ưu hơn cho các dự án Next.js MVP.

## 12. Study Pack - Gói ôn tập
### Must remember
- Day 3 là bước chuyển dịch từ ứng dụng demo phi thương mại sang một sản phẩm SaaS thực tế tích hợp đăng nhập và trả phí.
- Clerk được sử dụng vì tính đơn giản, tích hợp nhanh giao diện và hỗ trợ xác thực bằng token bảo mật cao.
- Tránh viết code trực tiếp trong repo tài liệu học tập chung để bảo vệ thông tin cấu hình và secrets.
- Giao tiếp bảo mật giữa Next.js và FastAPI dựa trên việc truyền các token mã hóa.

### Self-check questions
1. Tại sao việc tự xây dựng hệ thống đăng nhập mạng xã hội (OAuth) lại tốn nhiều thời gian và công sức?
2. Sự khác biệt chính giữa repository `production` và repository `sass` là gì?
3. Tại sao Clerk được khuyên dùng cho các dự án SaaS mới bắt đầu thay vì các dịch vụ xác thực đám mây phức tạp khác?

### Flashcards
- Q: SaaS repository đóng vai trò gì?
  A: Là kho lưu trữ chứa mã nguồn sạch của ứng dụng do học viên tự xây dựng từ đầu để chuẩn bị deploy lên production.
- Q: Lợi ích lớn nhất của Clerk so với Custom Auth là gì?
  A: Tiết kiệm tối đa thời gian phát triển (vài phút so với vài tuần/tháng) và đảm bảo các tiêu chuẩn bảo mật công nghiệp sẵn có.

### Interview Q&A nếu phù hợp
- Q: Khi chuyển từ môi trường Vercel sang các cloud provider lớn như AWS hay GCP, lập trình viên cần lưu ý điều gì về độ phức tạp?
  A: Độ phức tạp sẽ tăng lên đáng kể do không còn các cơ chế tự động hóa hoàn toàn của Vercel. Lập trình viên phải tự quản lý hạ tầng mạng, cấu hình máy chủ, bảo mật cổng kết nối và phân quyền truy cập IAM chi tiết.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 16. Day 3 - Adding User Authentication to Production AI Apps with Clerk

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 16).
- Slide: Đã dùng (Trang sơ đồ kiến trúc Auth và API Keys).
- Code: Đã dùng (Tham chiếu các file [day3.md](file:///G:/AIProduction_t6_2026/production/week1/day3.md) và file [product.tsx](file:///G:/AIProduction_t6_2026/production/community_contributions/product.tsx)).
- Summary lịch sử: Đã dùng (Đọc [day2_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day2_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin nhất quán. Dữ liệu mã nguồn thực tế và transcript thống nhất về các bước thiết lập và đặt tên biến môi trường.

## 2. Executive Summary - Tóm tắt cốt lõi
- Bài học đi sâu vào thực hành cài đặt và tích hợp SDK Clerk phiên bản v6 (`@clerk/nextjs@6.39.0`) và thư viện streaming `@microsoft/fetch-event-source` vào ứng dụng Next.js Pages Router.
- Wrapper bảo mật: Sử dụng `<ClerkProvider>` bọc quanh toàn bộ ứng dụng tại `pages/_app.tsx` để cung cấp và chia sẻ trạng thái đăng nhập cho tất cả các trang con trong ứng dụng.
- Bảo vệ trang sản phẩm: Chuyển toàn bộ giao diện và logic gọi API generator cũ của trang chủ sang tuyến đường được bảo mật mới tại `pages/product.tsx` sử dụng token JWT xác thực.
- Cấu trúc Landing Page mới: Cập nhật `pages/index.tsx` làm trang tiếp thị tĩnh, sử dụng các component của Clerk như `<SignInButton>`, `<SignedIn>`, `<SignedOut>`, và `<UserButton>` để phân phối giao diện thông minh theo trạng thái đăng nhập.
- Bảo mật API Backend: Cấu hình backend FastAPI xác thực JWT không đồng bộ thông qua thư viện `fastapi-clerk-auth`, sử dụng biến môi trường `CLERK_JWKS_URL` chứa các khóa công khai để giải mã token tự động trên server.
- Khắc phục lỗi 403 khi kết nối SSE dài: Tích hợp giải pháp từ cộng đồng (Artur P) sử dụng `AbortController` và `getToken()` để tự động bắt lỗi hết hạn token sau 60 giây và tái kết nối mượt mà bằng token mới.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cơ chế hoạt động của `<ClerkProvider>` trong việc phân phối trạng thái xác thực trong cây linh kiện React (React component tree).
  - Nắm rõ cách thức hoạt động của JSON Web Token (JWT) và JSON Web Key Set (JWKS) trong việc xác thực người dùng không trạng thái (stateless auth).
  - Hiểu kiến trúc bảo mật API bằng cách gán JWT vào tiêu đề Authorization của HTTP requests.
- Practical goals - mục tiêu thực hành:
  - Cài đặt Clerk SDK bản v6 trên Next.js và tích hợp thành công vào Pages Router.
  - Xây dựng trang sản phẩm được bảo vệ ở Client-side và API endpoint được bảo vệ ở Server-side.
  - Cấu hình các biến môi trường nhạy cảm trên Vercel bằng công cụ CLI.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích được JWKS URL từ Clerk và vai trò của nó; Trình bày được luồng đi của JWT từ frontend sang backend.
  - Giải thích nguyên nhân gây ra lỗi 403 Forbidden khi chạy SSE streaming dài hơn 60 giây và cách thức hoạt động của giải pháp AbortController + Token Rotation.

## 4. Previous Context - Liên hệ với bài trước
Bài học này nối tiếp trực tiếp phần lý thuyết tổng quan của Bài 15. Đây là bài thực hành kỹ thuật đầu tiên để biến Business Idea Generator thành ứng dụng Next.js + FastAPI được bảo mật đầu-cuối.

## 5. Core Theory - Lý thuyết cốt lõi
- JSON Web Token (JWT) - mã thông báo web JSON:
  - Meaning - nghĩa: Một định dạng mã thông báo nhỏ gọn, an toàn trên môi trường web, dùng để truyền tải các xác nhận danh tính được mã hóa và ký số giữa client và server.
  - Why it matters - vì sao quan trọng: Giúp xác thực người dùng một cách phi trạng thái (stateless), máy chủ không cần duy trì session trong RAM hay database.
- JSON Web Key Set (JWKS) - bộ khóa web JSON:
  - Meaning - nghĩa: Tập hợp các khóa mật mã công khai dạng JSON do nhà cung cấp xác thực (Clerk) công bố để các bên xác minh chữ ký của JWT token.
  - Why it matters - vì sao quan trọng: Cho phép backend FastAPI tự giải mã và kiểm chứng tính hợp lệ của JWT độc lập, giảm thiểu độ trễ mạng (network latency) cho mỗi API request.
- Client-side route protection - bảo vệ tuyến đường phía máy khách:
  - Meaning - nghĩa: Việc kiểm tra trạng thái đăng nhập của người dùng ngay trên trình duyệt trước khi hiển thị giao diện của một trang web.
  - Why it matters - vì sao quan trọng: Mang lại trải nghiệm người dùng (UX) mượt mà bằng cách lập tức chuyển hướng hoặc hiển thị giao diện đăng nhập thay vì tải trang bị lỗi từ server.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình trao đổi thông tin xác thực đầu-cuối (End-to-End Auth Pipeline):
1. Input: Người dùng đã đăng nhập click vào nút sinh ý tưởng tại `/product`.
2. Processing steps:
   - Frontend Next.js gọi `getToken()` để lấy mã token JWT mới từ Clerk.
   - Frontend thực hiện yêu cầu kết nối SSE bằng `fetchEventSource` tới endpoint `/api` của Backend, truyền kèm header `Authorization: Bearer <JWT_TOKEN>`.
   - Backend FastAPI tiếp nhận request, truyền token vào dependency `clerk_guard`.
   - `clerk_guard` giải mã token bằng các khóa công khai tải từ `CLERK_JWKS_URL`, kiểm tra chữ ký số và thời hạn sử dụng.
   - Sau khi xác thực hợp lệ, backend lấy ra ID người dùng (`creds.decoded["sub"]`) để xử lý nghiệp vụ tiếp theo (ví dụ: gọi OpenAI API stream ý tưởng).
3. Output: Backend phản hồi dữ liệu `StreamingResponse` chứa nội dung ý tưởng kinh doanh về cho Client.

## 7. Techniques - Kỹ thuật sử dụng
- JWT Authorization Header - tiêu đề ủy quyền JWT:
  - Purpose - mục đích: Truyền tải thông tin xác thực an toàn từ client lên server thông qua chuẩn HTTP Header.
  - When to use - dùng khi nào: Sử dụng cho mọi API request cần bảo mật thông tin hoặc giới hạn quyền truy cập.
  - Trade-off - đánh đổi: Client phải lưu trữ token an toàn trong bộ nhớ ngắn hạn và đính kèm vào mọi request.
  - Common mistake - lỗi dễ gặp: Quên đính kèm từ khóa `Bearer ` trước chuỗi token khiến backend từ chối xác thực.
- Client-side Guard components - linh kiện bảo vệ phía máy khách:
  - Purpose - mục đích: Sử dụng các component điều kiện như `<SignedIn>` và `<SignedOut>` của Clerk để tự động rẽ nhánh giao diện hiển thị.
  - When to use - dùng khi nào: Thiết kế Landing page và khu vực thanh điều hướng (navbar).
  - Trade-off - đánh đổi: Code giao diện frontend phụ thuộc sâu vào cấu trúc component của Clerk SDK.
  - Common mistake - lỗi dễ gặp: Sử dụng các phiên bản SDK mới hơn v7 dẫn đến mất một số component cũ và gây ra lỗi biên dịch (red underline).
- Auto Token Refresh on SSE - tự động làm mới mã thông báo trên luồng SSE:
  - Purpose - mục đích: Bắt lỗi token hết hạn 60s để tự động tái kết nối bằng token mới mà không làm ngắt quãng trải nghiệm của người dùng.
  - When to use - dùng khi nào: Khi tích hợp Clerk Auth với luồng streaming dài như Server-Sent Events.
  - Trade-off - đánh đổi: Code frontend phức tạp hơn vì phải quản lý các trạng thái kết nối (`isConnecting`) và hủy kết nối (`AbortController`).
  - Common mistake - lỗi dễ gặp: Không xử lý huỷ kết nối cũ trước khi kết nối lại, dẫn đến tình trạng rò rỉ bộ nhớ (memory leak) hoặc gọi API trùng lặp.

## 8. Code Walkthrough - Phân tích code nếu có
### File `pages/_app.tsx` - Khởi tạo Clerk Provider
- Purpose - mục đích: Thiết lập môi trường dùng chung của Clerk cho toàn bộ ứng dụng Next.js.
- Key logic - logic chính: Bọc component chính `Component` bên trong thẻ `<ClerkProvider>` và truyền toàn bộ `pageProps`.
- Vietnamese inline notes - ghi chú giải thích:
  ```typescript
  import { ClerkProvider } from '@clerk/nextjs';
  import type { AppProps } from 'next/app';
  import '../styles/globals.css';

  export default function MyApp({ Component, pageProps }: AppProps) {
    return (
      // Cung cấp ngữ cảnh xác thực cho toàn bộ cây component con
      <ClerkProvider {...pageProps}>
        <Component {...pageProps} />
      </ClerkProvider>
    );
  }
  ```

### File `pages/product.tsx` - Trang sản phẩm được bảo vệ
- Purpose - mục đích: Lấy token JWT và gửi request streaming bảo mật đến FastAPI.
- Key logic - logic chính: Sử dụng hook `useAuth()` để truy xuất hàm `getToken()`, đính kèm JWT vào header `Authorization`.
- Vietnamese inline notes - ghi chú giải thích:
  ```typescript
  const { getToken } = useAuth();
  // ... trong useEffect
  const jwt = await getToken(); // Lấy JWT token phi trạng thái từ Clerk client
  if (!jwt) {
      setIdea('Authentication required');
      return;
  }
  await fetchEventSource('/api', {
      headers: { Authorization: `Bearer ${jwt}` }, // Đính kèm JWT vào header yêu cầu
      onmessage(ev) {
          buffer += ev.data;
          setIdea(buffer);
      },
      onerror(err) {
          console.error('SSE error:', err);
      }
  });
  ```

### File `api/index.py` - Xác thực backend FastAPI
- Purpose - mục đích: Nhận, giải mã và phê duyệt request dựa trên mã token JWT.
- Key logic - logic chính: Sử dụng `fastapi-clerk-auth` để cấu hình `ClerkHTTPBearer` dựa trên `CLERK_JWKS_URL` và tích hợp làm dependency.
- Vietnamese inline notes - ghi chú giải thích:
  ```python
  import os
  from fastapi import FastAPI, Depends
  from fastapi_clerk_auth import ClerkConfig, ClerkHTTPBearer, HTTPAuthorizationCredentials

  app = FastAPI()

  # Cấu hình khóa giải mã bằng JWKS URL từ biến môi trường
  clerk_config = ClerkConfig(jwks_url=os.getenv("CLERK_JWKS_URL"))
  clerk_guard = ClerkHTTPBearer(clerk_config)

  @app.get("/api")
  # Yêu cầu dependency clerk_guard, FastAPI tự động kiểm tra token gửi lên
  def idea(creds: HTTPAuthorizationCredentials = Depends(clerk_guard)):
      user_id = creds.decoded["sub"]  # Trích xuất User ID từ payload của JWT
      # ... logic gọi OpenAI và stream kết quả
  ```

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Client-Side Route Protection (Ẩn hiện component bằng code client).
  - Pros - ưu điểm: Tải trang nhanh, phản hồi tức thì trên UI, dễ viết code.
  - Cons - nhược điểm: Chỉ mang tính chất giao diện, dữ liệu thô tải từ API vẫn có nguy cơ bị đọc trộm nếu không bảo mật API endpoint.
  - When to choose - khi nào chọn: Khi xây dựng các chức năng thông thường, không chứa dữ liệu tối mật của doanh nghiệp.
- Option 2: Server-Side Middleware Protection (Chặn truy cập bằng Next.js Middleware).
  - Pros - ưu điểm: Chặn hoàn toàn request tải trang từ phía server Next.js trước khi gửi bất kỳ file HTML/JS nào về trình duyệt, bảo mật tối đa.
  - Cons - nhược điểm: Phức tạp hơn trong việc cấu hình định tuyến và xử lý các tệp tĩnh.
  - When to choose - khi nào chọn: Khi xây dựng ứng dụng chứa thông tin cực kỳ nhạy cảm và muốn bảo vệ cả cấu trúc mã nguồn giao diện.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lỗi **403 Forbidden** sau 60 giây khi stream kết quả.
  - Root cause - nguyên nhân gốc rễ: Token JWT của Clerk chỉ có hiệu lực mặc định là 60 giây. Khi kết nối SSE chạy lâu hơn 60s để LLM stream nốt câu trả lời dài, request backend sẽ từ chối nhận token đã hết hạn này và ngắt kết nối.
  - Symptom - dấu hiệu: Trình duyệt nhận được mã lỗi HTTP 403, giao diện dừng hiển thị chữ mới dù AI chưa viết xong.
  - Fix / prevention - sửa đổi / phòng ngừa: Sử dụng giải pháp đóng góp của Artur P: Bắt lỗi 403 trong callback `onopen` và `onerror` của `fetchEventSource`, dùng `AbortController` hủy kết nối cũ, sau đó gọi lại `connectWithFreshToken()` để lấy token mới bằng `getToken()` và khởi động lại luồng stream.
- Failure mode: Lỗi **Unauthorized** hoặc **401/403** trên mọi request.
  - Root cause - nguyên nhân gốc rễ: Cấu hình sai hoặc thiếu biến môi trường `CLERK_JWKS_URL` ở backend hoặc trên Vercel settings.
  - Symptom - dấu hiệu: Client gửi request đúng định dạng nhưng server luôn từ chối xác thực.
  - Fix / prevention - sửa đổi / phòng ngừa: Đảm bảo sao chép chính xác JWKS URL từ Clerk Dashboard -> Configure -> API Keys và cập nhật đầy đủ các biến môi trường bằng lệnh `vercel env add CLERK_JWKS_URL`.

## 11. Knowledge Extension - Kiến thức mở rộng
- Token Rotation - xoay vòng mã thông báo: Việc Clerk cấu hình hạn dùng token cực ngắn (60 giây) là để hạn chế rủi ro bảo mật nếu token bị chặn thu giữ (man-in-the-middle attack). Cơ chế này đòi hỏi ứng dụng frontend phải liên tục làm mới token dưới chế độ ẩn (silent token refresh) để duy trì phiên làm việc cho người dùng một cách an toàn.

## 12. Study Pack - Gói ôn tập
### Must remember
- JWT được gửi trong tiêu đề `Authorization: Bearer <TOKEN>` để backend FastAPI giải mã và xác thực.
- `CLERK_JWKS_URL` chứa các khóa công khai giúp backend tự verify token mà không cần tạo request phụ gọi tới Clerk server.
- Sử dụng Clerk SDK v6 để tránh lỗi mất linh kiện `SignedIn` và `SignedOut` trên Pages Router.
- Khắc phục lỗi 403 timeout 60s bằng cách chủ động bắt mã lỗi và xoay vòng làm mới token ngay trên frontend client.

### Self-check questions
1. JSON Web Key Set (JWKS) hoạt động như thế nào để giúp backend xác thực chữ ký của JWT?
2. Tại sao Clerk lại thiết lập thời gian hết hạn của JWT token rất ngắn (chỉ 60 giây)?
3. Sự khác biệt giữa xác thực ở frontend (dùng component `<Protect>`) và xác thực ở backend (dùng dependency FastAPI) là gì?

### Flashcards
- Q: Lệnh để cài đặt Clerk SDK v6 cho Next.js là gì?
  A: `npm install @clerk/nextjs@6.39.0`
- Q: Biến môi trường nào chứa khóa công khai của Clerk để backend sử dụng?
  A: `CLERK_JWKS_URL`
- Q: Token mặc định của Clerk hết hạn sau bao lâu và gây ra lỗi HTTP nào trên luồng SSE?
  A: Hết hạn sau 60 giây và gây ra lỗi `403 Forbidden`.

### Interview Q&A nếu phù hợp
- Q: Làm thế nào để đảm bảo an toàn cho các API key và Secrets trong ứng dụng Full-stack AI?
  A: Tuyệt đối không lưu trữ hoặc gọi các API key (như OpenAI API Key, Clerk Secret Key) ở phía frontend. Mọi API key nhạy cảm phải được lưu trữ trong biến môi trường của máy chủ backend và các cuộc gọi API ngoài phải thực hiện hoàn toàn từ server.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 17. Day 3 - Adding Subscription Billing to Your Production AI SaaS Application

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 17).
- Slide: Đã dùng (Trang sơ đồ hoạt động của Clerk Billing).
- Code: Đã dùng (Tham chiếu file [day3.part2.md](file:///G:/AIProduction_t6_2026/production/week1/day3.part2.md) về các bước cấu hình billing).
- Summary lịch sử: Đã dùng (Đọc [day2_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day2_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin đồng nhất. Slide mô tả cấu hình dashboard của Clerk và transcript giải thích chi tiết các bước vô hiệu hóa bảo vệ mặc định của Vercel.

## 2. Executive Summary - Tóm tắt cốt lõi
- Cấu hình Vercel deployment: Tắt chức năng "Deployment Protection" (Vercel Authentication) trong Vercel Project Settings để đảm bảo Clerk Auth có thể hoạt động mà không bị chặn bởi tường lửa của Vercel.
- Triển khai ứng dụng: Thực hiện deploy mã nguồn sạch của ứng dụng từ repo `sass` lên Vercel Production bằng lệnh CLI `vercel --prod`.
- Kích hoạt Clerk Billing: Giới thiệu giải pháp billing tích hợp sẵn của Clerk, cho phép kết nối Stripe để xử lý giao dịch hoặc dùng Clerk Payment Gateway ở chế độ thử nghiệm (zero-config).
- Thiết lập gói dịch vụ: Cấu hình gói "Premium Subscription" trên Clerk Dashboard với khoá định danh `premium_subscription`, giá $100/tháng (hoặc $90/tháng nếu thanh toán năm - Annual billing).
- Phân tích sự quan trọng của việc thống nhất tham số định danh gói dịch vụ (Plan Key/ID) giữa cấu hình cổng thanh toán và mã nguồn Next.js.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cơ chế phân tách và phối hợp giữa Vercel Auth (deployment protection) và Clerk Auth.
  - Nắm vững kiến trúc tích hợp cổng thanh toán Clerk Billing & Stripe.
  - Hiểu cấu trúc của một Subscription Plan gồm Pricing, Billing cycle (chu kỳ thanh toán), và Annual discount (chiết khấu năm).
- Practical goals - mục tiêu thực hành:
  - Vô hiệu hóa Vercel Deployment Protection.
  - Deploy dự án SaaS qua Vercel CLI.
  - Cấu hình Clerk Billing Dashboard và thiết lập gói thuê bao Premium.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích được tại sao cần tắt Vercel Auth để Clerk Auth hoạt động bình thường trên internet công cộng.
  - Phân tích ưu và nhược điểm của Clerk Payment Gateway so với Stripe.

## 4. Previous Context - Liên hệ với bài trước
Bài học này kết nối trực tiếp với Bài 16. Sau khi đã cài đặt thành công Clerk Auth trên code, học viên cần chuẩn bị hạ tầng triển khai trên Vercel và cấu hình các gói thanh toán trên Dashboard của Clerk trước khi viết code kiểm tra trạng thái thanh toán ở Bài 18.

## 5. Core Theory - Lý thuyết cốt lõi
- Deployment Protection - bảo vệ triển khai:
  - Meaning - nghĩa: Tính năng bảo mật của Vercel tự động chặn quyền truy cập vào các bản preview/production bằng cách yêu cầu đăng nhập tài khoản Vercel.
  - Why it matters - vì sao quan trọng: Cần phải tắt tính năng này để người dùng cuối có thể tự do truy cập trang web và để Clerk có thể giao tiếp với ứng dụng mà không bị chặn.
- Zero-config payment gateway - cổng thanh toán không cấu hình:
  - Meaning - nghĩa: Cổng giả lập tích hợp sẵn của Clerk cho phép xử lý và mô phỏng giao dịch thanh toán thử ngay lập tức mà không cần tạo tài khoản Stripe.
  - Why it matters - vì sao quan trọng: Giúp lập trình viên nhanh chóng kiểm thử tính đúng đắn của luồng thanh toán trong quá trình phát triển (development phase) mà không lo ngại về chi phí hoặc thủ tục phức tạp.
- Plan Key - khóa định danh gói:
  - Meaning - nghĩa: Chuỗi ký tự duy nhất dùng để định danh gói cước (ví dụ: `premium_subscription`).
  - Why it matters - vì sao quan trọng: Đây là cầu nối giữa cấu hình sản phẩm trên Dashboard và code frontend. Nếu sai lệch dù chỉ một ký tự, code sẽ không nhận dạng được gói cước.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình thiết lập Billing & Triển khai (Billing & Deployment Workflow):
1. Input: Ứng dụng Next.js đã chạy ổn định cục bộ.
2. Processing steps:
   - Vào Vercel Settings -> Project Settings -> Deployment Protection -> Chuyển sang Off và nhấn Save.
   - Chạy lệnh `vercel --prod` trên Terminal của Cursor để deploy phiên bản mới nhất của dự án lên production.
   - Truy cập Clerk Dashboard -> Configure -> Billing -> Settings -> Nhấp vào Get Started và kích hoạt Clerk Billing.
   - Vào Configure -> Subscription Plans -> Nhấp Create Plan.
   - Thiết lập cấu hình Plan: Tên là Premium Subscription, Key là `premium_subscription`, Monthly Price là $100.
3. Output: Ứng dụng được deploy trực tiếp và gói cước sẵn sàng để tích hợp vào mã nguồn.

## 7. Techniques - Kỹ thuật sử dụng
- Vercel CLI Production Deployment - triển khai production bằng Vercel CLI:
  - Purpose - mục đích: Đẩy trực tiếp các thay đổi mã nguồn lên bản chạy production thay vì môi trường preview.
  - When to use - dùng khi nào: Sử dụng khi hoàn thành một mốc tính năng lớn đã được test kỹ ở máy cục bộ (localhost).
  - Trade-off - đánh đổi: Bản build sẽ lập tức hiển thị ra ngoài internet công cộng, đòi hỏi mã nguồn phải hoàn chỉnh và không chứa lỗi biên dịch.
  - Common mistake - lỗi dễ gặp: Quên thêm flag `--prod` khiến Vercel chỉ build bản Preview.
- Multi-tier billing configuration - cấu hình tính phí nhiều cấp độ:
  - Purpose - mục đích: Cấu hình linh hoạt các chu kỳ thanh toán và chiết khấu năm trên Clerk Dashboard.
  - When to use - dùng khi nào: Khi thiết kế chiến lược định giá sản phẩm (pricing strategy) để khuyến khích khách hàng trả trước dài hạn.
  - Trade-off - đánh đổi: Tăng độ phức tạp khi quản lý trạng thái tài khoản của người dùng.
  - Common mistake - lỗi dễ gặp: Đặt key chứa ký tự đặc biệt không được hỗ trợ (Clerk chỉ hỗ trợ chữ thường và dấu gạch dưới).

## 8. Code Walkthrough - Phân tích code nếu có
`Code được cung cấp trong session nhưng chưa thấy code liên quan trực tiếp tới lesson này.`
(Bài học này tập trung hoàn toàn vào các bước cấu hình đồ họa trên Vercel và Clerk Dashboard).

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Clerk Payment Gateway.
  - Pros - ưu điểm: Zero-config, hoạt động ngay lập tức, hoàn hảo cho giai đoạn test và PoC.
  - Cons - nhược điểm: Không thể dùng để thu tiền thật.
  - When to choose - khi nào chọn: Trong giai đoạn phát triển và chạy thử nghiệm cục bộ/staging.
- Option 2: Stripe Integration.
  - Pros - ưu điểm: Cổng thanh toán tiêu chuẩn công nghiệp, hỗ trợ thu tiền thật toàn cầu, tính năng quản lý doanh thu cực kỳ mạnh mẽ.
  - Cons - nhược điểm: Yêu cầu đăng ký tài khoản Stripe doanh nghiệp/cá nhân, cấu hình webhook phức tạp hơn.
  - When to choose - khi nào chọn: Khi ứng dụng sẵn sàng ra mắt thị trường (Go-to-market).

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Lỗi **xung đột xác thực kép (Double Auth)**.
  - Root cause - nguyên nhân gốc rễ: Quên tắt Vercel Deployment Protection. Khi người dùng truy cập trang web, họ bị Vercel chặn hỏi mật khẩu/login Vercel trước khi Clerk kịp hoạt động.
  - Symptom - dấu hiệu: Màn hình đăng nhập Vercel hiển thị đè lên Landing Page.
  - Fix / prevention - sửa đổi / phòng ngừa: Vào Settings -> Deployment Protection trên Vercel và chuyển trạng thái sang Off, sau đó lưu lại.

## 11. Knowledge Extension - Kiến thức mở rộng
- PCI-DSS Compliance (Chuẩn bảo mật dữ liệu thẻ thanh toán): Một tiêu chuẩn an ninh thông tin bắt buộc dành cho các tổ chức xử lý thẻ tín dụng. Việc sử dụng Clerk Billing hoặc Stripe giúp SaaS startup đạt chuẩn PCI-DSS ngay lập tức vì toàn bộ thông tin thẻ nhạy cảm được gửi thẳng đến đối tác thanh toán, không bao giờ đi qua máy chủ của startup.

## 12. Study Pack - Gói ôn tập
### Must remember
- Cần tắt Vercel Deployment Protection để Clerk Auth hoạt động bình thường trên internet công cộng.
- Triển khai production bằng lệnh `vercel --prod`.
- Clerk Billing hỗ trợ cả Clerk Payment Gateway (cho test) và Stripe (cho production).
- Plan Key (`premium_subscription`) được đặt trên Clerk Dashboard phải khớp 100% với key được dùng trong mã nguồn.

### Self-check questions
1. Tại sao phải tắt Vercel Deployment Protection khi triển khai Clerk Authentication?
2. Sự khác biệt giữa Clerk Payment Gateway và Stripe là gì?
3. Nếu nhập sai Plan Key trên Clerk Dashboard so với trong code Next.js, điều gì sẽ xảy ra?

### Flashcards
- Q: Lệnh deploy lên production của Vercel là gì?
  A: `vercel --prod`
- Q: Nơi cấu hình gói dịch vụ trên Clerk Dashboard nằm ở đâu?
  A: Configure -> Subscription Plans.
- Q: Chu kỳ thanh toán hàng năm đem lại lợi ích gì cho SaaS?
  A: Tăng dòng tiền trả trước (cash flow) và tăng cam kết gắn bó của người dùng (user retention).

### Interview Q&A nếu phù hợp
- Q: Tại sao việc sử dụng Stripe/Clerk Billing lại giúp dự án tránh được gánh nặng pháp lý PCI-DSS?
  A: Do dữ liệu thẻ của khách hàng được xử lý trực tiếp qua iframe/widget của Stripe/Clerk. Hệ thống backend của ứng dụng không bao giờ nhìn thấy hoặc lưu trữ số thẻ, do đó được miễn trừ các quy định kiểm toán PCI-DSS phức tạp.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.

---

# 18. Day 3 - Adding Authentication and Billing to Production AI Applications

Course domain: AI Engineer Production Track: Deploy LLMs & Agents at Scale
Course name: AI Engineer Production Track: Deploy LLMs & Agents at Scale

## 1. Source Map - Bản đồ nguồn
- Transcript: Đã dùng (Đọc chi tiết transcript bài 18).
- Slide: Đã dùng (Trang sơ đồ checkout và pricing table).
- Code: Đã dùng (Tham chiếu các file [day3.part2.md](file:///G:/AIProduction_t6_2026/production/week1/day3.part2.md) về Next.js billing và landing page).
- Summary lịch sử: Đã dùng (Đọc [day2_summary.md](file:///G:/AIProduction_t6_2026/production/tai_lieu/week1/day2_summary.md) làm bối cảnh tiếp nối).
- Ghi chú về độ tin cậy hoặc mâu thuẫn giữa nguồn: Các nguồn thông tin hoàn toàn đồng nhất. Mã nguồn và transcript khớp nhau về tên component của Clerk (`Protect`, `PricingTable`, `UserButton`) và luồng thanh toán mô phỏng.

## 2. Executive Summary - Tóm tắt cốt lõi
- Kiểm tra quyền truy cập ở frontend: Tích hợp linh kiện `<Protect>` từ `@clerk/nextjs` để bọc lấy component chính `IdeaGenerator` trên tuyến protected route `/product`.
- Trải nghiệm đăng ký động: Nếu người dùng đã đăng nhập nhưng chưa đăng ký gói cước Premium, `<Protect>` sẽ tự động chặn hiển thị generator và render bảng giá `<PricingTable />` làm fallback.
- Landing Page tích hợp thanh toán: Cập nhật `pages/index.tsx` để hiển thị bản xem trước giá dịch vụ ($10/tháng, có thể cập nhật để khớp với Clerk Dashboard) và điều phối các nút hành động dựa trên trạng thái thuê bao của người dùng.
- Thử nghiệm luồng thanh toán đầu-cuối: Thực hiện mô phỏng quy trình đăng ký tài khoản Apple mới (sử dụng tính năng Hide My Email để tránh Clerk gộp email trùng với Google), tiến hành thanh toán thành công bằng thẻ kiểm thử và truy cập thẳng vào chức năng sinh ý tưởng AI.
- Tự phục vụ quản lý thuê bao: Hướng dẫn người dùng cách tự kiểm tra, thay đổi thông tin thanh toán hoặc huỷ gói cước thông qua menu tích hợp sẵn trong component `<UserButton>` -> Manage Account -> Subscriptions.

## 3. Lesson Goals - Mục tiêu bài học
- Concept goals - mục tiêu kiến thức:
  - Hiểu cơ chế hoạt động của thẻ bảo vệ quyền truy cập `<Protect>` của Clerk bằng cách sử dụng fallback.
  - Nắm vững cách các component Clerk UI phối hợp với nhau để tạo ra trải nghiệm thanh toán khép kín và tự động.
  - Hiểu cách thức hệ thống thanh toán tự động làm mới session token sau khi giao dịch thành công.
- Practical goals - mục tiêu thực hành:
  - Viết code bảo vệ trang sản phẩm dựa trên quyền sở hữu gói dịch vụ Premium.
  - Cấu hình Landing Page phân phối nút điều hướng theo trạng thái đăng ký thuê bao.
  - Chạy thử luồng thanh toán thực tế và huỷ gói thử nghiệm trên môi trường production.
- What learner should be able to explain - người học cần giải thích được:
  - Giải thích cơ chế rẽ nhánh hiển thị của `<Protect>` bằng fallback.
  - Trình bày được cách người dùng tự quản lý gói cước mà không cần hệ thống admin can thiệp thủ công.
  - Giải thích sự cần thiết của tính năng ẩn email (Hide My Email) khi kiểm thử đăng ký nhiều tài khoản trên cùng một hệ thống xác thực Clerk.

## 4. Previous Context - Liên hệ với bài trước
Bài học này là bước hoàn thiện kỹ thuật cuối cùng của Day 3, nối tiếp trực tiếp sau khi các cấu hình gói cước và billing được xuất bản ở Bài 17.

## 5. Core Theory - Lý thuyết cốt lõi
- Billing Fallback - giao diện phản hồi thanh toán:
  - Meaning - nghĩa: Giao diện (thường là bảng giá cước) được hiển thị thay thế khi người dùng cố truy cập một tính năng cao cấp mà chưa thực hiện thanh toán.
  - Why it matters - vì sao quan trọng: Giúp hướng dẫn người dùng mua gói cước một cách tự nhiên ngay tại giao diện sử dụng, tối ưu hóa doanh thu cho SaaS.
- Test Card - thẻ kiểm thử:
  - Meaning - nghĩa: Các số thẻ tín dụng giả định được đối tác thanh toán cung cấp để kiểm thử hoạt động của hệ thống thanh toán mà không phát sinh giao dịch tài chính thật.
  - Why it matters - vì sao quan trọng: Giúp kiểm tra an toàn luồng thanh toán đầu-cuối trước khi cấu hình nhận tiền thật.
- Identity consolidation - hợp nhất danh tính:
  - Meaning - nghĩa: Cơ chế của Clerk tự động liên kết các phương thức đăng nhập khác nhau (ví dụ: Google Auth và Apple Auth) vào cùng một hồ sơ người dùng nếu chúng sử dụng chung địa chỉ email.
  - Why it matters - vì sao quan trọng: Tránh việc tạo tài khoản trùng lặp cho cùng một khách hàng, nâng cao trải nghiệm quản trị tài khoản tập trung.

## 6. Workflow / Pipeline - Quy trình / luồng hoạt động
Quy trình kiểm tra quyền thuê bao và thanh toán (Subscription Verification & Checkout Pipeline):
1. Input: Người dùng truy cập tuyến `/product`.
2. Processing steps:
   - Clerk SDK kiểm tra session token xem có chứa quyền truy cập của gói cước `premium_subscription` hay không.
   - Nếu có -> Hiển thị trực tiếp component `IdeaGenerator`.
   - Nếu không có -> Hiển thị component `<PricingTable />`.
   - Người dùng nhấn nút Subscribe trên bảng giá -> Clerk mở hộp checkout -> Nhập số Test Card -> Nhấn Pay.
   - Clerk Gateway xử lý thanh toán -> Phản hồi thành công -> Làm mới session token -> Cấp quyền truy cập.
3. Output: Hệ thống chuyển hướng người dùng trở lại trang sản phẩm và hiển thị giao diện Generator.

## 7. Techniques - Kỹ thuật sử dụng
- Declarative subscription protection - bảo vệ thuê bao dạng khai báo:
  - Purpose - mục đích: Sử dụng linh kiện `<Protect>` để tự động hoá việc chặn quyền truy cập thay vì viết các đoạn mã kiểm tra logic rườm rà.
  - When to use - dùng khi nào: Sử dụng khi cần giới hạn tính năng của ứng dụng theo các cấp bậc tài khoản khác nhau (Basic, Premium, Enterprise).
  - Trade-off - đánh đổi: Giao diện ứng dụng phụ thuộc chặt chẽ vào Clerk UI SDK.
  - Common mistake - lỗi dễ gặp: Viết sai chính tả của plan key trong code so với cấu hình trên dashboard.
- Billing self-service integration - tích hợp quản trị thanh toán tự phục vụ:
  - Purpose - mục đích: Sử dụng component `<UserButton>` của Clerk để cung cấp trang cá nhân tự phục vụ cho người dùng (hủy gói, đổi thẻ, xem hóa đơn).
  - When to use - dùng khi nào: Cần triển khai nhanh SaaS mà không muốn tốn công sức xây dựng trang quản trị tài khoản riêng biệt.
  - Trade-off - đánh đổi: Giao diện trang quản lý sẽ mở ra trong một widget của Clerk, có thể không đồng bộ hoàn toàn với giao diện chính của ứng dụng.
  - Common mistake - lỗi dễ gặp: Quên bật tính năng Billing trong cấu hình hiển thị của UserButton.

## 8. Code Walkthrough - Phân tích code nếu có
### File `pages/product.tsx` - Bảo vệ trang sản phẩm bằng gói Premium
- Purpose - mục đích: Kiểm tra và chặn truy cập Generator nếu người dùng chưa mua gói Premium.
- Key logic - logic chính: Bọc component `IdeaGenerator` bên trong thẻ `<Protect plan="premium_subscription" fallback={<PricingTable />}>`.
- Vietnamese inline notes - ghi chú giải thích:
  ```typescript
  import { Protect, PricingTable, UserButton } from '@clerk/nextjs';

  // Tách biệt phần giao diện chính của sản phẩm ra một component con
  function IdeaGenerator() {
      // ... Logic useEffect chứa fetchEventSource gửi JWT auth token lên backend FastAPI
  }

  export default function Product() {
      return (
          <main className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100">
              {/* Nút hiển thị thông tin và menu quản lý tài khoản của người dùng */}
              <div className="absolute top-4 right-4">
                  <UserButton showName={true} />
              </div>

              {/* Lớp bảo vệ subscription: Chỉ cho phép người sở hữu gói premium_subscription đi qua */}
              <Protect
                  plan="premium_subscription"
                  // Fallback: Nếu không thỏa mãn quyền sở hữu gói Premium, tự động hiển thị bảng giá cước
                  fallback={
                      <div className="container mx-auto px-4 py-12">
                          <header className="text-center mb-12">
                              <h1 className="text-5xl font-bold bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent mb-4">
                                  Choose Your Plan
                              </h1>
                              <p className="text-gray-600 dark:text-gray-400 text-lg mb-8">
                                  Unlock unlimited AI-powered business ideas
                              </p>
                          </header>
                          {/* Bảng giá cước tự sinh từ Clerk Dashboard */}
                          <div className="max-w-4xl mx-auto">
                              <PricingTable />
                          </div>
                      </div>
                  }
              >
                  {/* Nếu người dùng đã mua gói Premium, render component generator */}
                  <IdeaGenerator />
              </Protect>
          </main>
      );
  }
  ```

### File `pages/index.tsx` - Cập nhật Landing Page
- Purpose - mục đích: Bổ sung thông tin bảng giá và cấu hình các nút đăng ký phù hợp với mô hình SaaS trả phí.
- Key logic - logic chính: Sử dụng `<SignedIn>` và `<SignedOut>` để chuyển đổi nút bấm giữa "Start Your Free Trial" và "Access Premium Features".

## 9. Options / Trade-offs - Bản đồ lựa chọn
- Option 1: Sử dụng bảng giá mặc định `<PricingTable />` của Clerk.
  - Pros - ưu điểm: Tích hợp nhanh chỉ với 1 dòng code, tự động đồng bộ hóa thông tin và tính năng từ Dashboard của Clerk.
  - Cons - nhược điểm: Không thể tùy biến sâu giao diện, bố cục thiết kế bị cố định.
  - When to choose - khi nào chọn: Trong giai đoạn thử nghiệm MVP cần tối ưu hóa tốc độ đưa sản phẩm ra thị trường.
- Option 2: Xây dựng bảng giá tự thiết kế (Custom Pricing Table).
  - Pros - ưu điểm: Tự do thiết kế giao diện phù hợp 100% với giao diện chung của ứng dụng, tăng khả năng tối ưu trải nghiệm người dùng (UX).
  - Cons - nhược điểm: Đòi hỏi phải viết thêm mã nguồn để xử lý sự kiện nhấn nút mua và gọi API checkout của Clerk thủ công.
  - When to choose - khi nào chọn: Khi sản phẩm đã đi vào hoạt động ổn định và cần tối ưu hóa tỷ lệ chuyển đổi khách hàng mua gói.

## 10. Pitfalls - Lỗi / bẫy thường gặp
- Failure mode: Người dùng đã thanh toán thành công nhưng hệ thống vẫn tiếp tục hiển thị Bảng giá.
  - Root cause - nguyên nhân gốc rễ: Token session hiện tại đang lưu ở client chưa được tự động làm mới để cập nhật metadata gói cước mới mua.
  - Symptom - dấu hiệu: Sau khi thanh toán thành công và quay lại trang ứng dụng, người dùng vẫn bị chặn ở màn hình Pricing Table.
  - Fix / prevention - sửa đổi / phòng ngừa: Hướng dẫn người dùng thực hiện thao tác Đăng xuất (Sign Out) và Đăng nhập (Sign In) lại để làm mới hoàn toàn session token hoặc cấu hình cơ chế lắng nghe sự kiện cập nhật token tự động của Clerk SDK.

## 11. Knowledge Extension - Kiến thức mở rộng
- Webhooks in Billing - sự kiện Webhook trong thanh toán: Trong các ứng dụng SaaS chuyên nghiệp, khi người dùng thực hiện huỷ gói cước hoặc thanh toán thất bại, cổng thanh toán (Clerk/Stripe) sẽ gửi một HTTP POST request (Webhook) về endpoint backend được cấu hình sẵn. Backend API sẽ dựa vào đó để cập nhật cơ sở dữ liệu (database), đảm bảo quyền hạn của người dùng luôn được đồng bộ chính xác bất kể họ có đang mở trình duyệt web hay không.

## 12. Study Pack - Gói ôn tập
### Must remember
- Sử dụng `<Protect>` bọc lấy tính năng cao cấp để kiểm soát quyền truy cập theo gói cước.
- Fallback của `<Protect>` giúp hiển thị bảng giá cước `<PricingTable />` một cách mượt mà cho người dùng chưa đăng ký.
- Menu quản lý tài khoản được tích hợp sẵn trong `<UserButton>` giúp người dùng tự phục vụ việc quản lý và huỷ gói.
- Đăng xuất và đăng nhập lại là phương pháp đơn giản nhất để làm mới session token sau khi nâng cấp gói.

### Self-check questions
1. Thẻ `<Protect>` của Clerk hoạt động như thế nào để chặn người dùng chưa mua gói?
2. Bảng giá `<PricingTable />` của Clerk đồng bộ dữ liệu từ đâu?
3. Tại sao người dùng cần đăng xuất và đăng nhập lại nếu giao diện không tự cập nhật sau khi nâng cấp gói?

### Flashcards
- Q: Component nào của Clerk dùng để hiển thị danh sách các gói thanh toán?
  A: `<PricingTable />`
- Q: Component nào dùng để giới hạn hiển thị tính năng theo gói cước?
  A: `<Protect>`
- Q: Người dùng có thể huỷ gói cước ở đâu trong giao diện mặc định của Clerk?
  A: Trong menu quản lý tài khoản của `<UserButton>` -> mục Subscriptions.

### Interview Q&A nếu phù hợp
- Q: Trong Next.js Pages Router, làm thế nào để đảm bảo người dùng chưa đăng nhập không thể truy cập mã nguồn của trang `/product` ngay từ trình duyệt?
  A: Có thể sử dụng Next.js Middleware hoặc Server-side props (`getServerSideProps`) để kiểm tra session token của Clerk. Nếu không hợp lệ, thực hiện chuyển hướng (redirect) người dùng về trang chủ ngay từ phía server trước khi trình duyệt tải mã nguồn của trang `/product`.

## 13. Missing Inputs - Còn thiếu gì
- Không có tài liệu hoặc ngữ cảnh nào bị thiếu cho bài học này.
