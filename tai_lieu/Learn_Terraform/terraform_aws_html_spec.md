# Terraform AWS HTML Handbook Specification

## 1. Mục tiêu tài liệu

Tạo ra **một file HTML duy nhất**, rất dài, rất chi tiết, có thể đọc độc lập, giúp một người **chưa biết gì về Terraform** học từ số 0 đến mức có thể hiểu, đọc, chỉnh sửa, và tự triển khai các dự án Terraform trên AWS theo tư duy production.

Tài liệu này không phải là một bài blog ngắn, cũng không phải cheat sheet rời rạc. Đây phải là một **guided handbook** có nhịp dạy học rõ ràng:

1. Giải thích nền tảng thật dễ hiểu.
2. Minh họa bằng code `.tf` thật.
3. Ghi chú giải thích từng khối quan trọng.
4. Đi từ core Terraform sang AWS practical patterns.
5. Đi tiếp đến production practices.
6. Kết thúc bằng các capstone project liên quan AI trên AWS.

Tài liệu phải đủ tốt để:

- người mới đọc một mạch từ đầu đến cuối;
- dùng lại như tài liệu ôn tập;
- tra cứu lại khi triển khai project thực tế;
- làm nền để học các phần nâng cao như CI/CD, module design, backend, drift handling, zero-downtime, và AI deployment patterns.

## 2. Required Superpowers Workflow

Agent được giao dựng HTML **bắt buộc** phải áp dụng workflow Superpowers, không được nhảy thẳng vào viết HTML kiểu generic:

1. `using-superpowers`
2. `brainstorming`
3. review lại spec này và khóa requirements
4. `writing-plans`
5. triển khai HTML
6. tự review completeness + source coverage + design-guide compliance
7. bàn giao để review tiếp

Các quy định bắt buộc:

- Không được bỏ qua `using-superpowers`.
- `brainstorming` là cổng vào chính, nhưng không được mắc kẹt ở brainstorming.
- Nếu đã có spec này thì không được hỏi lan man lại các yêu cầu đã khóa trong file.
- Chỉ hỏi thêm nếu phát hiện mâu thuẫn thật sự ảnh hưởng trực tiếp đến implementation.
- HTML cuối cùng phải phản ánh đúng tinh thần của spec này thay vì viết một bài tổng hợp nông.

## 3. Output Contract

Artifact cuối cùng mà agent khác phải tạo là:

- `terraform_aws_beginner_handbook.html`

Artifact đó phải:

- tự chứa toàn bộ HTML/CSS/JS cần thiết;
- không phụ thuộc framework frontend;
- mở trực tiếp trong browser được;
- có trải nghiệm đọc tốt trên desktop và mobile;
- có sticky table of contents;
- có progress indicator;
- có code blocks rõ ràng, dễ copy;
- có các box ghi chú như `Note`, `Warning`, `Common mistake`, `Why this matters`;
- có khả năng thu gọn/mở rộng một số phần dài bằng `details/summary` hoặc cơ chế tương đương;
- có visual direction bám theo `G:\harness_template\DESIGN-claude.md`.

## 4. Design Guide Compliance

HTML phải áp dụng tinh thần của `G:\harness_template\DESIGN-claude.md`:

- nền `cream canvas`;
- nhịp editorial, không phải giao diện “AI slop” màu tím hoặc dashboard rẻ tiền;
- headline mang cảm giác học thuật, rõ ràng, dễ đọc;
- section spacing rộng, có nhịp nghỉ;
- code blocks tối màu, dễ nhìn;
- accent coral ấm để nhấn CTA, callout, badges;
- table of contents và content cards phải đồng nhất;
- ưu tiên layout đọc dài hạn, không flashy.

Không được:

- dùng giao diện mặc định trắng trơn + sans-serif đơn điệu;
- dùng màu tím neon, gradient công nghiệp, hoặc dark mode toàn trang mặc định;
- biến tài liệu thành landing page marketing;
- lạm dụng animation.

## 5. Audience và Writing Contract

Đối tượng mục tiêu:

- người mới học Terraform hoàn toàn;
- biết rất ít hoặc chưa biết AWS;
- có thể là developer, DevOps beginner, AI engineer, student;
- muốn học cả lý thuyết nền lẫn cách làm thực tế.

Giọng văn bắt buộc:

- tiếng Việt là chính;
- technical terms để bằng English khi rõ nghĩa hơn;
- giải thích chậm, dễ hiểu, không ra vẻ “ai cũng biết rồi”;
- tránh định nghĩa trừu tượng nếu chưa có ví dụ;
- mỗi phần quan trọng nên trả lời được:
  - nó là gì;
  - dùng để làm gì;
  - khi nào dùng;
  - thường đặt ở đâu trong project;
  - dễ sai ở đâu;
  - ví dụ code tối thiểu là gì.

Không được:

- nhảy cóc vào thuật ngữ nâng cao khi chưa build mental model;
- dùng giọng văn quá ngắn, quá khô, kiểu liệt kê từ khóa;
- giả định người đọc đã biết state, backend, IAM, VPC, ALB, module, drift;
- viết “để đó cho đầy đủ” mà không giải thích.

## 6. Source Strategy

### 6.1 Nguồn xương sống bắt buộc

Series của Quân Huỳnh trên Viblo phải được dùng làm **backbone coverage**, gồm tối thiểu các chủ đề:

1. `Bài 1 - Infrastructure as Code và Terraform`
2. `Bài 2 - Life cycle của một resource trong Terraform`
3. `Bài 4 - Terraform functional programming`
4. `Bài 5 - Terraform Module: Create Virtual Private Cloud on AWS`
5. `Bài 6 - Module In Depth: Create Multi-Tier Application`
6. `Bài 7 - Terraform Backend: Understand Backend`
7. `Bài 8 - Terraform Backend: S3 Standard Backend`
8. `Bài 9 - Terraform Backend: Remote Backend with Terraform Cloud`
9. `Bài 10 - CI/CD with Terraform Cloud and Zero-downtime deployments`
10. `Bài 11 - Terraform Blue/Green deployments`
11. `Bài 12 - Terraform A/B Testing Deployment`
12. `Bài 13 - Ansible with Terraform`
13. `Bài 14 - Automating Terraform with Gitlab CI`
14. `Bài 15 - Automating Terraform with Jenkins`
15. `Bài 16 - Multi-cloud environment`
16. `Bài 17 - Security - Securing Logs and Securing State File`
17. `Bài 18 - Security - Managing Secrets with Vault`
18. `Bài 19 - Handle the difference between Terraform State and Real Infrastructure`

Ghi chú:

- Không cần bám cấu trúc bài 1:1.
- Phải **hấp thụ và tái tổ chức** thành một handbook mạch lạc hơn.
- Không được bỏ rơi các chủ đề production như backend, CI/CD, drift, security, rollout.

### 6.2 Nguồn chuẩn hóa bắt buộc

Phải bổ sung từ tài liệu chính thức để chỉnh nội dung cho đúng best practice hiện hành:

- HashiCorp Terraform Intro
- HashiCorp Terraform Language
- HashiCorp AWS Get Started
- HashiCorp State docs
- HashiCorp Import docs
- HashiCorp Tests docs
- HashiCorp Lifecycle docs
- HashiCorp S3 backend docs
- HashiCorp module refactoring / moved block docs
- AWS Prescriptive Guidance: Best practices for using the Terraform AWS Provider

### 6.3 Nguồn mở rộng nên dùng khi cần

Nếu cần lấp chỗ trống cho phần AI/AWS deployment patterns, có thể tham khảo thêm nguồn uy tín, nhưng phải ưu tiên:

- official docs;
- AWS docs;
- HashiCorp docs;
- bài kỹ thuật có chất lượng cao.

Không được để handbook dựa chủ yếu vào nguồn thứ cấp không rõ chất lượng.

## 7. Source Coverage Matrix bắt buộc

HTML cuối phải ngầm hoặc trực tiếp bao phủ các trục sau:

- `IaC foundation`
- `Terraform mental model`
- `resource lifecycle`
- `HCL and functional patterns`
- `module design`
- `multi-tier AWS app`
- `backend and remote state`
- `Terraform Cloud overview`
- `CI/CD automation`
- `zero-downtime patterns`
- `blue/green`
- `A/B testing`
- `Terraform + Ansible`
- `GitLab CI`
- `Jenkins`
- `multi-cloud awareness`
- `security logs/state`
- `Vault for secrets`
- `drift between state and real infra`
- `modern import/test/refactor guidance`
- `AWS provider best practices`
- `AI deployment use cases on AWS`

## 8. Handbook Structure bắt buộc

HTML phải có tối thiểu các phần lớn sau, theo thứ tự logic gần tương đương.

### Part 1. Orientation

- Terraform là gì
- IaC là gì
- vì sao cần IaC trên AWS
- pain của click tay trên Console
- Terraform phù hợp với bài toán nào
- khi nào Terraform không phải lựa chọn duy nhất
- Terraform vs CloudFormation vs Ansible vs shell script
- mental picture: viết config -> init -> plan -> apply -> state -> update -> destroy

### Part 2. Setup for beginners

- cài Terraform trên Windows
- cài AWS CLI
- tạo AWS account / IAM user / IAM role ở mức khái niệm
- cấu hình AWS credentials bằng profile
- cách verify với `aws sts get-caller-identity`
- cách kiểm tra Terraform version
- warning về secret handling
- cấu trúc thư mục làm bài học đầu tiên

### Part 3. Terraform Core Concepts

- block là gì
- argument là gì
- expression là gì
- provider là gì
- resource là gì
- data source là gì
- variable là gì
- local là gì
- output là gì
- module là gì
- state là gì
- backend là gì
- workspace là gì
- dependency graph là gì
- declarative model là gì

### Part 4. Terraform File Structure

Phải giải thích rõ các file:

- `versions.tf`
- `provider.tf`
- `main.tf`
- `variables.tf`
- `terraform.tfvars`
- `outputs.tf`
- `locals.tf`
- `backend.tf`
- `README.md` trong project Terraform
- `modules/`
- `envs/` hoặc environment split

Phải có ví dụ project tree rõ ràng.

### Part 5. HCL từ cơ bản đến đủ dùng

- string, number, bool
- list, map, object, tuple
- comments
- references
- interpolation mindset
- conditional expressions
- `for_each`
- `count`
- `for` expressions
- `dynamic` blocks
- built-in functions cơ bản

Phải có ví dụ minh họa ngắn trước, rồi mới đến ví dụ project.

### Part 6. First Terraform Project on AWS

Phải có một tutorial mở đầu thật chậm với:

- provider AWS
- một EC2 đơn giản
- tags
- output
- `terraform init`
- `terraform fmt`
- `terraform validate`
- `terraform plan`
- `terraform apply`
- `terraform destroy`

Mỗi command phải được giải thích.
Mỗi file phải được giải thích.
Phải có box “lỗi beginner thường gặp”.

### Part 7. Resource Lifecycle và tư duy thay đổi hạ tầng

Phải dạy rõ:

- create
- update in-place
- destroy and recreate
- immutable infra mindset
- vì sao plan quan trọng
- khi nào đổi một field gây replacement
- `lifecycle` meta-argument
- `create_before_destroy`
- caveat của zero-downtime

### Part 8. Variables, Locals, Outputs, Naming, Tagging

Phải có:

- input variable best practices
- default vs required
- type constraints
- validations nếu phù hợp
- local values để giảm lặp
- output để chia sẻ thông tin
- naming convention
- tagging strategy cho AWS

### Part 9. AWS Building Blocks with Terraform

Phải có các section riêng, đầy đủ code và giải thích:

- EC2
- Security Group
- Elastic IP
- S3 bucket
- IAM role/policy/profile
- VPC
- subnet public/private
- internet gateway
- route table
- NAT gateway
- ALB
- Auto Scaling Group
- CloudWatch logs ở mức áp dụng phù hợp

Không bắt buộc mọi ví dụ đều production-complete, nhưng phải có đủ số lượng và độ sâu để người đọc hiểu cấu trúc AWS thực tế.

### Part 10. Modules

Phải dạy:

- module là gì
- khi nào nên tạo module
- khi nào không cần module
- input/output của module
- root module vs child module
- folder structure cho module
- module VPC example
- module app example
- common module mistakes

Phải dùng tinh thần từ Viblo `Bài 5` và `Bài 6`, nhưng mở rộng giải thích cho beginner.

### Part 11. Backend, State, Remote State

Phải là một section rất mạnh:

- state là gì
- state dùng để làm gì
- local state vs remote state
- vì sao team không nên chỉ dùng local state
- backend là gì
- S3 backend
- `use_lockfile`
- bucket versioning
- key layout
- workspace key prefix
- remote state consumption
- drift là gì
- state corruption risk
- cách backup state

Phải nhắc rằng DynamoDB locking cũ có bối cảnh lịch sử, nhưng nội dung phải ưu tiên hiểu đúng hiện trạng docs.

### Part 12. Import, Refactor, Moved Blocks, Drift

Phải có:

- import existing resource
- vì sao import cần cả `import` block và `resource` block
- `moved` block là gì
- rename resource/module mà không phá state
- drift giữa state và real infra
- ví dụ console change gây lệch
- cách đọc lại plan để phát hiện drift
- workflow xử lý drift

Phần này phải liên hệ mạnh với tinh thần từ `Bài 19`.

### Part 13. Terraform Testing, Validation, Quality Gates

Phải có:

- `terraform fmt`
- `terraform validate`
- tư duy review `plan`
- giới thiệu Terraform test framework ở mức beginner-friendly
- khi nào dùng static checks
- quality gate tối thiểu trước khi apply production

Không được viết phần testing mơ hồ.

### Part 14. CI/CD and Automation

Phải bao phủ:

- Terraform Cloud ở mức giải thích
- CI/CD pipeline cho Terraform
- GitLab CI
- Jenkins
- shell script automation
- separation giữa plan và apply
- approval gate
- artifact lưu plan

Phải gắn với production safety, không chỉ liệt kê tên tool.

### Part 15. Deployment Strategies

Phải có:

- zero-downtime mindset
- blue/green
- A/B testing
- rollback thinking
- trade-off giữa đơn giản và an toàn

Phải nói rõ:

- khi nào beginner chỉ nên hiểu concept;
- khi nào production team mới thật sự nên áp dụng.

### Part 16. Terraform + Ansible + Multi-tool Thinking

Phải giải thích rõ:

- Terraform không thay thế mọi tool
- Terraform mạnh ở provisioning
- Ansible mạnh ở configuration management
- shell scripts dùng khi nào
- phối hợp nhiều tool ra sao

### Part 17. Security

Phải có section riêng, không được làm qua loa:

- không hard-code secrets
- state file có thể chứa dữ liệu nhạy cảm
- bảo vệ logs
- bảo vệ backend bucket
- IAM least privilege
- provider/version pinning
- community module caution
- Vault ở mức conceptual + applied workflow
- secret rotation mindset

### Part 18. AI on AWS with Terraform

Đây là phần mở rộng applied, nhưng phải viết thật mạch lạc và có chiều sâu.

Phải có các chapter hoặc subsections rõ ràng cho các chủ đề sau:

1. `Infrastructure as Code for AI: Deploying LLM Apps with Terraform`
2. `Infrastructure as Code: Automating AI Deployments with Terraform`
3. `Automating AI Deployments with Terraform and Shell Scripts`
4. `Automating Full-Stack AI Deployment with Terraform and AWS`
5. `Testing Production AI Deployments and Terraform Cleanup Workflows`
6. `Setting Up Secure AI Ingestion Pipelines with Terraform and AWS`
7. `Deploying AI-Generated APIs to Production with AWS Lambda & Terraform`

Yêu cầu:

- phải nối từ core Terraform sang applied AI, không được chuyển chủ đề đột ngột;
- phải giải thích vì sao AI workloads cần IaC;
- phải làm rõ hạ tầng nào Terraform quản lý, phần app/model nào Terraform không thay thế;
- phải có examples thực tế, ít nhất ở mức AWS services architecture + `.tf` skeleton đủ thật.

### Part 19. Capstones

Phải có đúng 3 capstone lớn.

#### Capstone 1. AWS Foundation Multi-Tier Application

Mục tiêu:

- dùng Terraform tạo hạ tầng AWS nhiều tầng cơ bản;
- minh họa VPC, subnets, security groups, compute, load balancing, outputs;
- dạy cách tổ chức module và biến môi trường.

Phải có:

- project tree
- nhiều file `.tf`
- flow deploy
- flow update
- flow destroy
- notes về cost và cleanup

#### Capstone 2. Serverless AI API on AWS

Mục tiêu:

- deploy một API inference hoặc AI-generated API kiểu serverless;
- dùng AWS Lambda, IAM, logging, API Gateway;
- minh họa shell scripts hỗ trợ package/deploy/cleanup.

Phải có:

- resource map
- Terraform file breakdown
- giải thích IAM permissions
- logging/observability cơ bản
- cleanup workflow

#### Capstone 3. Secure AI Ingestion Pipeline on AWS

Mục tiêu:

- xây một pipeline ingestion an toàn cho dữ liệu AI;
- nhấn mạnh storage, compute trigger, permissions, logging, cleanup;
- có thể dùng S3 + Lambda + IAM + notification/event flow ở mức hợp lý.

Phải có:

- threat-aware explanation
- state and secret handling notes
- destroy safety notes
- shell automation

### Part 20. Troubleshooting and Anti-Patterns

Phải có:

- lỗi credentials
- sai region
- thiếu quyền IAM
- drift
- state lock conflict
- xóa tay trên Console
- sửa module gây phá state
- lạm dụng `depends_on`
- lạm dụng `count` khi `for_each` phù hợp hơn
- hard-code IDs/AMI
- trộn quá nhiều môi trường trong một state

### Part 21. Cheat Sheets and Review

Phải có:

- Terraform command cheat sheet
- lifecycle cheat sheet
- state/backend cheat sheet
- module design checklist
- production apply checklist
- beginner learning path recap

## 9. Required Code Example Inventory

HTML cuối phải có rất nhiều code thật. Không được chỉ có vài snippet nhỏ.

Tối thiểu phải có đầy đủ ví dụ cho các file sau, ở nhiều section khác nhau nếu cần:

- `versions.tf`
- `provider.tf`
- `main.tf`
- `variables.tf`
- `terraform.tfvars`
- `outputs.tf`
- `locals.tf`
- `backend.tf`
- `modules/vpc/main.tf`
- `modules/vpc/variables.tf`
- `modules/vpc/outputs.tf`
- `modules/ec2/main.tf`
- `modules/ec2/variables.tf`
- `modules/ec2/outputs.tf`
- `modules/alb/main.tf`
- `modules/alb/variables.tf`
- `modules/alb/outputs.tf`
- `scripts/init.ps1` hoặc shell equivalent
- `scripts/plan.ps1`
- `scripts/apply.ps1`
- `scripts/destroy.ps1`
- `scripts/package_lambda.ps1` hoặc shell equivalent

Mỗi code block quan trọng phải có:

- tiêu đề file;
- giải thích mục đích file;
- note theo block;
- cảnh báo nếu block có risk production;
- diễn giải “đọc file này từ trên xuống thì đang làm gì”.

## 10. Pedagogical Devices bắt buộc

Trong HTML cuối, phải có các pattern dạy học lặp lại:

- `What this means`
- `Why this matters`
- `Example`
- `Common mistake`
- `Production note`
- `Beginner note`
- `Deep dive`
- `Checklist`

Không được chỉ viết đoạn văn liên tục quá dài mà không có nhịp học.

## 11. HTML UX Requirements

HTML phải có:

- sticky TOC bên trái hoặc trên cùng tùy viewport;
- progress bar;
- callout boxes có màu/kiểu phân biệt;
- code blocks có scroll ngang;
- typography rõ ràng;
- section anchors;
- responsive behavior tốt;
- `details/summary` cho một số deep dive sections;
- không phụ thuộc internet để render cơ bản.

## 12. AI Chapter Content Requirements

Các chương AI không được viết chung chung. Phải dạy rõ:

- Terraform quản lý hạ tầng, không thay thế application logic;
- shell scripts hỗ trợ packaging/deployment/cleanup;
- khi nào serverless phù hợp cho AI API;
- khi nào container/ECS phù hợp hơn;
- khi nào ingestion pipeline cần tách state/permissions;
- security concerns với AI data paths;
- cleanup workflow quan trọng vì AI infra có thể tốn phí.

Phải có ít nhất các AWS services được nhắc tới hợp lý trong phần AI:

- Lambda
- API Gateway
- IAM
- S3
- CloudWatch Logs
- ECR hoặc ECS ở mức giải thích nếu phù hợp

## 13. Non-Negotiable Quality Bar

HTML cuối bị xem là **không đạt** nếu xảy ra một trong các lỗi sau:

- quá ngắn;
- thiếu flow từ zero đến production;
- không đủ code `.tf`;
- không giải thích code;
- bỏ qua backend/state/drift/security;
- phần AI chỉ là vài đoạn mô tả chung chung;
- không bám design guide;
- không có capstone rõ ràng;
- không có notes về cleanup/cost/risk;
- không phản ánh coverage từ Viblo series + official docs.

## 14. Anti-Slop Rules

Không được:

- chèn các câu “Terraform is powerful and flexible” kiểu sáo rỗng mà không giải thích;
- lạm dụng bullet list thay cho dạy học;
- dùng snippet giả, thiếu context;
- viết pseudo-code thay cho `.tf` thật;
- bỏ qua file structure;
- dùng placeholder như `TODO`, `...`, `your_resource_here` trừ khi có giải thích cụ thể;
- đưa ra các lệnh nguy hiểm mà không cảnh báo;
- viết các chương AI như marketing trend summary.

## 15. Recommended Content Density

Tài liệu nên có cảm giác:

- dài;
- đọc được;
- không nông;
- có thể học thành nhiều buổi;
- mỗi phần core đều có code;
- phần production và AI có chiều sâu ứng dụng.

Nếu phải ưu tiên, ưu tiên:

1. tính dễ hiểu;
2. tính đầy đủ;
3. tính source-grounded;
4. tính thực hành;
5. tính đẹp.

## 16. Review Checklist cho agent dựng HTML

Trước khi bàn giao HTML, agent phải tự kiểm tra:

1. Đã áp dụng `using-superpowers` và workflow Superpowers chưa?
2. Đã bám `DESIGN-claude.md` chưa?
3. Có bao phủ backbone Viblo `Bài 1 -> Bài 19` chưa?
4. Có cập nhật bằng official docs ở các phần state/backend/import/tests/lifecycle/AWS best practices chưa?
5. Có đủ 3 capstone chưa?
6. Có đủ nhiều file `.tf` thật chưa?
7. Code block nào cũng đã được giải thích chưa?
8. Có section security, drift, backend, cleanup workflow chưa?
9. Phần AI có thực sự applied và AWS-focused chưa?
10. HTML mở local có đọc tốt trên desktop/mobile chưa?

## 17. Spec Self-Review

Tự kiểm tra spec này:

- Không có `TODO`, `TBD`, hoặc placeholder mơ hồ.
- Scope lớn nhưng vẫn là **một HTML handbook duy nhất**, không tách thành nhiều website con.
- Đã khóa rõ audience, tone, visual direction, source strategy, section requirements, code inventory, capstones, và quality bar.
- Đã làm rõ rằng AI chapters là applied extension trên nền Terraform core, không được lấn át phần nền tảng.
- Đã làm rõ rằng series Viblo là backbone coverage, còn HashiCorp/AWS docs là lớp chuẩn hóa và cập nhật production guidance.

Kết luận self-review:

- Scope hợp lệ cho một handbook lớn.
- Không mâu thuẫn nội bộ đáng kể.
- Đủ chi tiết để chuyển sang implementation planning.
