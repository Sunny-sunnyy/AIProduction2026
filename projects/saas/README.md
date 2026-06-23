# MediNotes Pro

link: https://github.com/Sunny-sunnyy/SaaS

Ứng dụng chuyển ghi chú khám bệnh thô của bác sĩ thành:

- tóm tắt hồ sơ chuyên môn
- next steps cho bác sĩ
- email nháp thân thiện để gửi bệnh nhân

Project hiện kết hợp:

- `Next.js` Pages Router cho frontend
- `Clerk` cho authentication và subscription gating
- `FastAPI` cho backend streaming
- `OpenAI` để sinh nội dung AI
- `Docker` + `AWS Lambda Web Adapter` cho hướng deploy AWS hiện tại

## Trạng thái hiện tại

Repo này đã hoàn thành đến Day 5 của course, bao gồm:

- `pages/index.tsx`: landing page của sản phẩm
- `pages/product.tsx`: form consultation được bảo vệ bằng Clerk plan
- `api/server.py`: backend FastAPI phục vụ API và static export
- `Dockerfile`: build frontend tĩnh và chạy toàn bộ app trong một container
- flow đóng gói container để chuẩn bị deploy AWS Lambda

Ngoài ra repo còn giữ một số file tham chiếu từ các giai đoạn học trước:

- `api/index.py`: backend cũ cho flow kiểu Vercel
- `product.tsx`: bản tham chiếu fix SSE token 60s, không phải route đang chạy
- `week1/`: ghi chú bài học và summary theo ngày

## App Flow

1. User đăng nhập bằng Clerk.
2. User mở `/product`.
3. `Protect plan="premium_subscription"` kiểm tra quyền truy cập.
4. Form gửi `patient_name`, `date_of_visit`, `notes` tới `POST /api/consultation`.
5. FastAPI xác thực JWT bằng `CLERK_JWKS_URL`.
6. Backend gọi OpenAI với structured prompt và stream kết quả về UI qua SSE.

## Cấu trúc thư mục

```text
saas/
├── api/
│   ├── index.py          # legacy backend flow
│   └── server.py         # backend hiện tại cho container/AWS
├── pages/
│   ├── _app.tsx
│   ├── _document.tsx
│   ├── index.tsx
│   └── product.tsx
├── public/
├── styles/
│   └── globals.css
├── week1/                # learning notes
├── Dockerfile
├── next.config.ts
├── package.json
└── requirements.txt
```

## Yêu cầu môi trường

- `Node.js 22+` khuyến nghị
- `npm`
- `Python 3.12+`
- `Docker` để chạy full app đúng kiến trúc hiện tại

## Cài Docker

### Ubuntu / WSL

Nếu máy chưa có Docker, cài Docker Engine:

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
```

Sau đó đăng nhập lại shell rồi kiểm tra:

```bash
docker --version
docker run hello-world
```

### Windows / macOS

Cài `Docker Desktop` từ trang chính thức:

```text
https://www.docker.com/products/docker-desktop/
```

Sau khi cài xong, kiểm tra:

```bash
docker --version
docker run hello-world
```

## Biến môi trường

Frontend build cần:

```bash
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
```

Backend runtime cần:

```bash
OPENAI_API_KEY=
CLERK_JWKS_URL=
```

Ghi chú:

- `OPENAI_API_KEY` được `openai.OpenAI()` tự đọc từ environment.
- `CLERK_JWKS_URL` dùng để verify JWT từ Clerk ở backend.
- Repo đang ignore `.env*`, không commit secrets.

## Cài dependencies

Frontend:

```bash
npm install
```

Backend:

```bash
python -m pip install -r requirements.txt
```

## Cách chạy

### 1. Chạy frontend preview

```bash
npm run dev
```

Mở `http://localhost:3000`.

Lưu ý: cách này chỉ phù hợp để xem UI/frontend. Route `pages/product.tsx` hiện gọi `/api/consultation`, nên muốn chạy end-to-end đúng như code hiện tại thì nên dùng Docker/container flow bên dưới.

### 2. Chạy full app bằng Docker

Từ root của project, build image:

```bash
docker build \
  --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key \
  -t medinotes-pro .
```

Chạy container:

```bash
docker run --rm -p 8000:8000 \
  -e OPENAI_API_KEY=your_openai_api_key \
  -e CLERK_JWKS_URL=your_clerk_jwks_url \
  medinotes-pro
```

Sau đó mở `http://localhost:8000`.

Container này sẽ:

- build static export của Next.js
- copy output vào `static/`
- chạy `FastAPI + Uvicorn`
- phục vụ UI tĩnh và API trên cùng một origin

### 3. Chạy lại nhanh sau lần build đầu

Nếu image đã build sẵn, chỉ cần chạy lại container:

```bash
docker run --rm -p 8000:8000 \
  -e OPENAI_API_KEY=your_openai_api_key \
  -e CLERK_JWKS_URL=your_clerk_jwks_url \
  medinotes-pro
```

### 4. Kiểm tra container đang chạy

Kiểm tra log:

```bash
docker ps
docker logs <container_id>
```

Health endpoint:

```bash
curl http://localhost:8000/health
```

Kỳ vọng:

```json
{"status":"healthy"}
```

## AWS Deployment Direction

Project đã hoàn thành phần Day 5 theo hướng deploy:

- build Docker image
- push image lên Amazon ECR
- deploy image lên AWS Lambda
- dùng `AWS Lambda Web Adapter` để chạy FastAPI như web server thông thường
- dùng Lambda Function URL để public HTTPS endpoint

Các ghi chú triển khai học tập nằm trong:

- `week1/day5.md`
- `week1/day5_summary.md`

## Tech Notes

- `next.config.ts` đang dùng `output: 'export'` để frontend có thể được phục vụ như static files.
- `pages/product.tsx` đang dùng `fetchEventSource` để nhận streaming response.
- `api/server.py` có endpoint `/health` cho local Docker healthcheck.
- SSE token refresh 60s đã có tài liệu tham chiếu trong `jwt_token_60s_fix.md`, nhưng logic đó chưa được tích hợp vào `pages/product.tsx` hiện tại.

## Tài liệu học kèm theo

Nếu muốn hiểu tiến trình xây dựng dự án theo từng ngày, đọc:

- `week1/day3_summary.md`
- `week1/day4_summary.md`
- `week1/day5_summary.md`
- `week1/day4.md`
- `week1/day5.md`

## Hạn chế hiện tại

- README này phản ánh trạng thái code hiện có, không phải mọi phần trong tài liệu course đều đã được đồng bộ hoàn toàn vào source.
- `pages/product.tsx` chưa áp dụng reconnection flow cho JWT 60 giây như file tham chiếu `product.tsx` ở root.
- Local dev không có một script duy nhất để chạy frontend và backend cùng lúc ngoài container path.
