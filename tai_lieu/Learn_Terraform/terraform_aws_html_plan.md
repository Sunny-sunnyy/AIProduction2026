# Terraform AWS Beginner HTML Handbook Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `superpowers:subagent-driven-development` (recommended) or `superpowers:executing-plans` to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Tạo ra file `terraform_aws_beginner_handbook.html` rất dài, cực kỳ chi tiết, dễ hiểu cho beginner, bao phủ Terraform nền tảng, Terraform trên AWS, production practices, và 3 capstone AWS/AI, đồng thời bám `terraform_aws_html_spec.md` và `G:\harness_template\DESIGN-claude.md`.

**Architecture:** Một file HTML tự chứa toàn bộ nội dung, CSS, và JavaScript. Nội dung được tổ chức như một editorial handbook có sticky TOC, progress bar, callout boxes, code panels tối màu, và các chương đi theo lộ trình `zero -> Terraform core -> AWS practice -> production -> AI capstones -> troubleshooting -> cheat sheets`.

**Tech Stack:** Plain HTML5, embedded CSS variables, embedded vanilla JavaScript, Markdown-to-HTML handcrafting trực tiếp trong file, code examples `.tf`, `.tfvars`, `.ps1` hoặc shell snippets, không dùng framework frontend.

---

## 1. Locked Inputs

Trước khi triển khai, agent phải khóa lại các input sau:

- Spec nguồn: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_html_spec.md`
- Design guide: `G:\harness_template\DESIGN-claude.md`
- Output file: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`
- Collaboration workflow bắt buộc: `using-superpowers -> brainstorming -> spec review -> writing-plans -> execution -> review`
- Backbone coverage: Viblo Terraform Series của Quân Huỳnh từ `Bài 1` đến `Bài 19`
- Official grounding: HashiCorp docs + AWS Prescriptive Guidance

Nếu có mâu thuẫn giữa các nguồn:

- ưu tiên spec đã duyệt;
- ưu tiên design guide cho visual direction;
- ưu tiên official docs cho best practice hiện hành;
- xem Viblo như backbone tư duy và topic coverage, không phải bản copy nguyên xi.

## 2. File Structure Lock

Chỉ tạo một artifact đầu ra bắt buộc:

- Create: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

Không tách CSS/JS ra file riêng.

Nếu cần working draft tạm trong lúc soạn, agent có thể dùng file tạm nội bộ, nhưng trước khi bàn giao chỉ giữ artifact HTML cuối cùng.

## 3. Output Contract for the HTML

HTML cuối cùng phải có:

- `<!DOCTYPE html>` đầy đủ
- `lang="vi"`
- self-contained CSS
- self-contained JS
- semantic structure bằng `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`
- sticky table of contents
- progress indicator
- responsive layout
- editorial hero section
- section anchors
- code blocks dễ copy
- `details/summary` cho deep dives
- nhiều callout patterns

HTML cuối cùng không được:

- trông như landing page marketing;
- thiếu sticky TOC;
- thiếu mobile behavior;
- chỉ toàn text dài không chia nhịp;
- chỉ có code snippets ngắn không context;
- dùng placeholder chưa điền.

## 4. Content Architecture Lock

HTML phải có thứ tự chương gần như sau. Mỗi phần phải có `id` ổn định để TOC bám được.

1. `hero-overview`
2. `how-to-use-this-guide`
3. `what-is-iac`
4. `what-is-terraform`
5. `terraform-vs-other-tools`
6. `setup-windows-and-aws`
7. `terraform-mental-model`
8. `terraform-file-structure`
9. `hcl-basics`
10. `first-terraform-project`
11. `resource-lifecycle`
12. `variables-locals-outputs`
13. `aws-building-blocks`
14. `terraform-modules`
15. `backend-state-remote-state`
16. `import-moved-drift`
17. `testing-validation-quality-gates`
18. `cicd-and-automation`
19. `deployment-strategies`
20. `terraform-and-ansible`
21. `security`
22. `terraform-for-ai-on-aws`
23. `capstone-foundation-app`
24. `capstone-serverless-ai-api`
25. `capstone-secure-ai-ingestion`
26. `troubleshooting-and-anti-patterns`
27. `cheat-sheets`
28. `final-recap`

Nếu agent muốn thêm section phụ, được phép thêm, nhưng không được bỏ section chính.

## 5. Mandatory Component Set

HTML phải có các component tái sử dụng sau:

- hero editorial section
- sticky TOC card
- progress bar
- chapter card opener
- callout `Beginner note`
- callout `Production note`
- callout `Warning`
- callout `Common mistake`
- callout `Deep dive`
- code panel dark theme
- checklist box
- comparison table
- architecture diagram block bằng HTML/CSS hoặc Mermaid nếu render ổn định
- capstone summary panel

## 6. Visual Implementation Lock

Áp dụng tinh thần `DESIGN-claude.md` bằng các token gần tương đương:

- canvas: `#faf9f5`
- ink: `#141413`
- body: `#3d3d3a`
- muted: `#6c6a64`
- hairline: `#e6dfd8`
- surface-card: `#efe9de`
- surface-dark: `#181715`
- surface-dark-elevated: `#252320`
- primary coral: `#cc785c`
- primary active: `#a9583e`
- on-dark: `#faf9f5`
- code font: `JetBrains Mono, ui-monospace, monospace`

Typography direction:

- display serif: `Copernicus, Tiempos Headline, Cormorant Garamond, serif`
- body sans: `StyreneB, Inter, Segoe UI, sans-serif`
- editorial spacing lớn
- code blocks tối màu, bo góc rõ

Không dùng:

- màu tím làm accent chính
- background trắng lạnh
- UI kiểu dashboard enterprise
- card shadow nặng

## 7. Source Coverage Execution Rules

Agent phải có coverage thực thi, không chỉ mention source names.

### Viblo coverage mapping bắt buộc

- `Bài 1` phải đi vào Part 1 và First Project
- `Bài 2` phải đi vào Resource Lifecycle
- `Bài 4` phải đi vào HCL, functional patterns, loops, locals
- `Bài 5` phải đi vào Module + VPC module example
- `Bài 6` phải đi vào Multi-tier capstone patterns
- `Bài 7` và `Bài 8` phải đi vào Backend/State/S3 backend
- `Bài 9` phải đi vào Terraform Cloud overview
- `Bài 10` đến `Bài 12` phải đi vào CI/CD và deployment strategies
- `Bài 13` phải đi vào Terraform + Ansible
- `Bài 14` và `Bài 15` phải đi vào automation pipeline
- `Bài 16` phải đi vào multi-cloud awareness note
- `Bài 17` và `Bài 18` phải đi vào Security
- `Bài 19` phải đi vào Drift/State/Real Infrastructure

### Official docs coverage bắt buộc

- HashiCorp language docs phải xuất hiện trong phần syntax và file structure
- HashiCorp state/import/lifecycle/moved/tests phải xuất hiện ở các chương tương ứng
- AWS Prescriptive Guidance phải ảnh hưởng tới advice về security, backends, code organization, provider versioning, community modules

## 8. Code Inventory Lock

HTML phải chứa đầy đủ hoặc gần đầy đủ code walkthrough cho ít nhất các file sau:

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
- `scripts/init.ps1`
- `scripts/plan.ps1`
- `scripts/apply.ps1`
- `scripts/destroy.ps1`
- `scripts/package_lambda.ps1`

Ngoài ra, được khuyến nghị thêm:

- `scripts/deploy_ai_api.ps1`
- `scripts/cleanup_ai_api.ps1`
- `scripts/package_ingestion_lambda.ps1`

## 9. HTML Skeleton Starter

Trong Task 1, agent phải dựng skeleton gần theo khung sau rồi mới đổ nội dung:

```html
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Terraform for AWS: Beginner Handbook</title>
  <style>
    :root {
      --canvas: #faf9f5;
      --ink: #141413;
      --body: #3d3d3a;
      --muted: #6c6a64;
      --hairline: #e6dfd8;
      --surface-card: #efe9de;
      --surface-dark: #181715;
      --surface-dark-elevated: #252320;
      --primary: #cc785c;
      --primary-active: #a9583e;
      --on-dark: #faf9f5;
      --max-width: 1200px;
      --radius-md: 8px;
      --radius-lg: 12px;
      --radius-xl: 16px;
      --shadow-soft: 0 1px 3px rgba(20, 20, 19, 0.08);
    }
  </style>
</head>
<body>
  <div class="progress-bar" id="progressBar"></div>
  <header class="hero" id="hero-overview"></header>
  <div class="page-shell">
    <aside class="toc-shell">
      <nav class="toc" id="toc"></nav>
    </aside>
    <main class="content" id="content">
      <section id="how-to-use-this-guide"></section>
      <section id="what-is-iac"></section>
      <section id="what-is-terraform"></section>
      <section id="terraform-vs-other-tools"></section>
      <section id="setup-windows-and-aws"></section>
      <section id="terraform-mental-model"></section>
      <section id="terraform-file-structure"></section>
      <section id="hcl-basics"></section>
      <section id="first-terraform-project"></section>
      <section id="resource-lifecycle"></section>
      <section id="variables-locals-outputs"></section>
      <section id="aws-building-blocks"></section>
      <section id="terraform-modules"></section>
      <section id="backend-state-remote-state"></section>
      <section id="import-moved-drift"></section>
      <section id="testing-validation-quality-gates"></section>
      <section id="cicd-and-automation"></section>
      <section id="deployment-strategies"></section>
      <section id="terraform-and-ansible"></section>
      <section id="security"></section>
      <section id="terraform-for-ai-on-aws"></section>
      <section id="capstone-foundation-app"></section>
      <section id="capstone-serverless-ai-api"></section>
      <section id="capstone-secure-ai-ingestion"></section>
      <section id="troubleshooting-and-anti-patterns"></section>
      <section id="cheat-sheets"></section>
      <section id="final-recap"></section>
    </main>
  </div>
  <script>
    // TOC + progress logic here
  </script>
</body>
</html>
```

## 10. Task Plan

### Task 1: Lock Inputs and Build the Base HTML Scaffold

**Files:**
- Read: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_html_spec.md`
- Read: `G:\harness_template\DESIGN-claude.md`
- Create: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Re-read the approved spec and extract hard constraints into a scratch checklist**

Create a small checklist for yourself with these exact headings:

```text
[ ] using-superpowers workflow acknowledged
[ ] DESIGN-claude visual direction locked
[ ] Viblo Bài 1-19 backbone coverage mapped
[ ] HashiCorp/AWS official docs sections mapped
[ ] 3 capstones locked
[ ] required code inventory locked
[ ] sticky TOC required
[ ] progress bar required
[ ] beginner tone required
[ ] AI chapters required
```

- [ ] **Step 2: Create the HTML shell with semantic regions**

Start from this scaffold and expand it:

```html
<body>
  <div class="progress-bar" id="progressBar"></div>
  <header class="hero" id="hero-overview">
    <div class="hero-inner">
      <p class="eyebrow">Terraform for AWS</p>
      <h1>Tài liệu nhập môn Terraform cho AWS từ số 0 đến production</h1>
      <p class="hero-summary">
        Handbook này giúp bạn hiểu Terraform, học cách viết file .tf, quản lý state,
        tổ chức modules, tự động hóa deployments, và triển khai các ví dụ AI trên AWS.
      </p>
    </div>
  </header>
  <div class="page-shell">
    <aside class="toc-shell">
      <nav class="toc" id="toc"></nav>
    </aside>
    <main class="content" id="content"></main>
  </div>
</body>
```

- [ ] **Step 3: Add the global CSS token layer and editorial layout**

Include these minimum CSS sections:

```css
body {
  margin: 0;
  background: var(--canvas);
  color: var(--body);
  font-family: StyreneB, Inter, "Segoe UI", sans-serif;
  line-height: 1.7;
}

.hero,
.chapter,
.capstone,
.summary-band {
  padding: 4rem 1.5rem;
}

.page-shell {
  width: min(100%, var(--max-width));
  margin: 0 auto;
  display: grid;
  grid-template-columns: 280px minmax(0, 1fr);
  gap: 2rem;
  padding: 2rem 1.5rem 5rem;
}

.toc {
  position: sticky;
  top: 1rem;
  background: var(--surface-card);
  border: 1px solid var(--hairline);
  border-radius: var(--radius-lg);
  padding: 1rem;
}

.content section {
  margin-bottom: 4rem;
}
```

- [ ] **Step 4: Create reusable content primitives before writing long content**

Add class families for:

```css
.callout {}
.callout.beginner {}
.callout.production {}
.callout.warning {}
.callout.mistake {}
.callout.deep-dive {}
.code-card {}
.code-card pre {}
.comparison-table {}
.checklist-box {}
.chapter-intro {}
.diagram-card {}
.capstone-card {}
details.deep-dive {}
```

- [ ] **Step 5: Verify the blank scaffold opens cleanly**

Open the HTML in a browser.

Expected:

- no broken layout;
- cream canvas visible;
- hero section readable;
- no horizontal overflow at desktop width;
- TOC card space reserved;
- no console errors caused by unfinished JS.

### Task 2: Implement Navigation, Progress, and Reusable JS Behavior

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Insert all section shells with locked IDs**

Inside `<main id="content">`, add all required sections in the locked order:

```html
<section id="how-to-use-this-guide" class="chapter"></section>
<section id="what-is-iac" class="chapter"></section>
<section id="what-is-terraform" class="chapter"></section>
<section id="terraform-vs-other-tools" class="chapter"></section>
<section id="setup-windows-and-aws" class="chapter"></section>
<section id="terraform-mental-model" class="chapter"></section>
<section id="terraform-file-structure" class="chapter"></section>
<section id="hcl-basics" class="chapter"></section>
<section id="first-terraform-project" class="chapter"></section>
<section id="resource-lifecycle" class="chapter"></section>
<section id="variables-locals-outputs" class="chapter"></section>
<section id="aws-building-blocks" class="chapter"></section>
<section id="terraform-modules" class="chapter"></section>
<section id="backend-state-remote-state" class="chapter"></section>
<section id="import-moved-drift" class="chapter"></section>
<section id="testing-validation-quality-gates" class="chapter"></section>
<section id="cicd-and-automation" class="chapter"></section>
<section id="deployment-strategies" class="chapter"></section>
<section id="terraform-and-ansible" class="chapter"></section>
<section id="security" class="chapter"></section>
<section id="terraform-for-ai-on-aws" class="chapter"></section>
<section id="capstone-foundation-app" class="capstone"></section>
<section id="capstone-serverless-ai-api" class="capstone"></section>
<section id="capstone-secure-ai-ingestion" class="capstone"></section>
<section id="troubleshooting-and-anti-patterns" class="chapter"></section>
<section id="cheat-sheets" class="chapter"></section>
<section id="final-recap" class="summary-band"></section>
```

- [ ] **Step 2: Add TOC generation script**

Use JS close to the following:

```html
<script>
  const toc = document.getElementById("toc");
  const sections = [...document.querySelectorAll("main section[id]")];
  toc.innerHTML = `
    <h2>Mục lục</h2>
    <ul>
      ${sections.map(section => {
        const heading = section.dataset.toc || section.querySelector("h2")?.textContent || section.id;
        return `<li><a href="#${section.id}">${heading}</a></li>`;
      }).join("")}
    </ul>
  `;
</script>
```

- [ ] **Step 3: Add active section highlighting and progress bar behavior**

Use an `IntersectionObserver` and a scroll progress handler:

```html
<script>
  const progressBar = document.getElementById("progressBar");
  const tocLinks = [...document.querySelectorAll(".toc a")];

  const setProgress = () => {
    const scrollTop = window.scrollY;
    const scrollHeight = document.documentElement.scrollHeight - window.innerHeight;
    const progress = scrollHeight > 0 ? (scrollTop / scrollHeight) * 100 : 0;
    progressBar.style.width = `${progress}%`;
  };

  window.addEventListener("scroll", setProgress, { passive: true });
  setProgress();

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (!entry.isIntersecting) return;
      tocLinks.forEach(link => {
        link.classList.toggle("active", link.getAttribute("href") === `#${entry.target.id}`);
      });
    });
  }, { rootMargin: "-30% 0px -55% 0px", threshold: 0 });

  document.querySelectorAll("main section[id]").forEach(section => observer.observe(section));
</script>
```

- [ ] **Step 4: Add mobile TOC fallback**

At widths below tablet, transform the layout:

```css
@media (max-width: 960px) {
  .page-shell {
    grid-template-columns: 1fr;
  }

  .toc {
    position: relative;
    top: auto;
  }
}
```

- [ ] **Step 5: Verify TOC and progress behavior**

Open the page and verify:

- TOC renders every section;
- clicking a TOC item jumps correctly;
- active TOC link changes while scrolling;
- progress bar moves smoothly;
- layout collapses correctly on narrow widths.

### Task 3: Write Orientation and Setup Chapters

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `how-to-use-this-guide`**

This section must explain:

- ai nên đọc tài liệu này;
- nên đọc tuần tự hay tra cứu;
- phần nào là core bắt buộc;
- phần nào là production/applied;
- cách dùng code blocks;
- cách dùng capstones.

Use structure close to:

```html
<section id="how-to-use-this-guide" class="chapter" data-toc="Cách dùng handbook này">
  <div class="chapter-intro">
    <p class="eyebrow">Reading guide</p>
    <h2>Cách dùng handbook này để học nhanh nhưng không hổng nền</h2>
    <p>...</p>
  </div>
  <div class="callout beginner">
    <strong>Beginner note:</strong>
    <p>Nếu bạn chưa biết gì về Terraform, hãy đọc liền mạch từ đầu đến hết phần State và Modules trước khi nhảy sang capstone.</p>
  </div>
</section>
```

- [ ] **Step 2: Write `what-is-iac` and `what-is-terraform` as beginner-first explanations**

These two sections must include:

- click-ops pain;
- versioning and repeatability;
- drift and disaster recovery intuition;
- Terraform as declarative IaC;
- resource graph;
- why Terraform is popular on AWS.

Also include one comparison table:

```html
<table class="comparison-table">
  <thead>
    <tr>
      <th>Approach</th>
      <th>Cách làm</th>
      <th>Điểm mạnh</th>
      <th>Điểm yếu</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Click trên AWS Console</td>
      <td>Thao tác thủ công</td>
      <td>Nhanh cho thử nghiệm nhỏ</td>
      <td>Khó lặp lại, khó audit, dễ drift</td>
    </tr>
    <tr>
      <td>Terraform</td>
      <td>Khai báo desired state bằng code</td>
      <td>Lặp lại được, review được, scale tốt</td>
      <td>Cần học state, modules, workflow</td>
    </tr>
  </tbody>
</table>
```

- [ ] **Step 3: Write `terraform-vs-other-tools`**

Cover:

- Terraform vs CloudFormation
- Terraform vs Ansible
- Terraform vs shell scripts
- khi kết hợp tool
- khi không nên dùng Terraform cho mọi thứ

Must include one recommended “tool selection” checklist box.

- [ ] **Step 4: Write `setup-windows-and-aws` with commands and warnings**

Must include:

- install Terraform on Windows;
- install AWS CLI;
- configure AWS profile;
- verify identity;
- check Terraform version;
- warning about hard-coded keys;
- note about IAM least privilege.

Include command blocks:

```powershell
terraform version
aws configure --profile terraform-learning
aws sts get-caller-identity --profile terraform-learning
```

- [ ] **Step 5: Verify chapter tone and beginner clarity**

Read only these first sections and verify:

- no section assumes prior Terraform knowledge;
- every new term is explained;
- at least one `Beginner note` and one `Warning` box appear;
- setup commands are realistic and copyable.

### Task 4: Write Terraform Core Mental Model, File Structure, and HCL Basics

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `terraform-mental-model` using a visual flow**

Must explain:

- write config
- init providers
- plan changes
- apply changes
- state updates
- future updates
- destroy

Add a simple diagram block, for example:

```html
<div class="diagram-card">
  <p>Code Terraform</p>
  <p>→ terraform init</p>
  <p>→ terraform plan</p>
  <p>→ terraform apply</p>
  <p>→ Terraform state được cập nhật</p>
  <p>→ lần chạy sau so sánh desired state với real infrastructure</p>
</div>
```

- [ ] **Step 2: Write `terraform-file-structure` with a project tree and file-by-file explanation**

Use a project tree like:

```text
terraform-aws-first-project/
├── versions.tf
├── provider.tf
├── main.tf
├── variables.tf
├── terraform.tfvars
├── outputs.tf
├── locals.tf
├── backend.tf
├── modules/
│   ├── vpc/
│   ├── ec2/
│   └── alb/
└── scripts/
    ├── init.ps1
    ├── plan.ps1
    ├── apply.ps1
    └── destroy.ps1
```

For each file, explain:

- file này tồn tại để làm gì;
- nội dung thường có;
- beginner dễ đặt sai gì;
- vì sao tách file giúp project dễ đọc hơn.

- [ ] **Step 3: Write `hcl-basics` with tiny examples first, then practical examples**

Must include:

- string
- number
- bool
- list
- map
- object
- argument
- block
- reference
- expression
- `count`
- `for_each`
- `for`
- conditional
- `dynamic`

Use tiny code samples such as:

```hcl
variable "aws_region" {
  type    = string
  default = "ap-southeast-1"
}

locals {
  common_tags = {
    Project = "terraform-learning"
    Owner   = "student"
  }
}
```

- [ ] **Step 4: Add at least one callout explaining HCL in plain Vietnamese**

Include a callout like:

```html
<div class="callout beginner">
  <strong>What this means:</strong>
  <p>HCL không phải là một ngôn ngữ lập trình tổng quát như Python. Bạn không viết từng bước để Terraform làm theo. Bạn mô tả trạng thái hạ tầng mà bạn muốn có.</p>
</div>
```

- [ ] **Step 5: Verify file structure and HCL sections contain both concept and code**

Check:

- there is at least one tree view;
- there are at least six HCL code blocks in this area;
- each file listed in the project tree is explained in words.

### Task 5: Write the First AWS Project and Resource Lifecycle Chapters

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write a full first project using `versions.tf`, `provider.tf`, `main.tf`, `outputs.tf`**

Use exact example files similar to:

```hcl
terraform {
  required_version = ">= 1.5.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

```hcl
provider "aws" {
  region  = var.aws_region
  profile = var.aws_profile
}
```

```hcl
resource "aws_instance" "hello" {
  ami           = var.ami_id
  instance_type = "t3.micro"

  tags = merge(local.common_tags, {
    Name = "hello-terraform"
  })
}
```

```hcl
output "instance_id" {
  value = aws_instance.hello.id
}
```

- [ ] **Step 2: Add `variables.tf`, `terraform.tfvars`, and `locals.tf` for this first project**

Use:

```hcl
variable "aws_region" {
  description = "AWS region for the first project"
  type        = string
  default     = "ap-southeast-1"
}

variable "aws_profile" {
  description = "Named AWS CLI profile"
  type        = string
  default     = "terraform-learning"
}

variable "ami_id" {
  description = "AMI ID for the EC2 instance"
  type        = string
}
```

```hcl
locals {
  common_tags = {
    Project     = "terraform-beginner-handbook"
    Environment = "learning"
    ManagedBy   = "terraform"
  }
}
```

```hcl
aws_region  = "ap-southeast-1"
aws_profile = "terraform-learning"
ami_id      = "ami-xxxxxxxxxxxxxxxxx"
```

- [ ] **Step 3: Explain CLI workflow in order with command blocks**

Include:

```powershell
terraform fmt
terraform init
terraform validate
terraform plan
terraform apply
terraform output
terraform destroy
```

For each command, explain:

- command làm gì;
- khi nào nên chạy;
- output nhìn thế nào ở mức khái niệm;
- beginner hay hiểu sai gì.

- [ ] **Step 4: Write `resource-lifecycle` with replace-vs-update reasoning**

Must cover:

- create
- update in place
- destroy/recreate
- why some changes trigger replacement
- `lifecycle` block
- `create_before_destroy`

Use a code block:

```hcl
resource "aws_instance" "app" {
  ami           = var.ami_id
  instance_type = var.instance_type

  lifecycle {
    create_before_destroy = true
  }
}
```

Also explain the caveat that dependencies can inherit `create_before_destroy`.

- [ ] **Step 5: Verify the first project chapter is actually end-to-end**

Check:

- all base files are shown;
- commands are in correct order;
- there is a destroy step;
- there are warning boxes about cost and accidental apply.

### Task 6: Write Variables, Naming, Tagging, and AWS Building Blocks

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `variables-locals-outputs` as a practical engineering section**

Must explain:

- required variable vs default;
- type constraints;
- validation idea;
- `locals` to reduce duplication;
- `output` to expose important values;
- naming convention;
- tagging strategy.

Add a realistic validation example:

```hcl
variable "environment" {
  type = string

  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "environment must be dev, staging, or prod."
  }
}
```

- [ ] **Step 2: Write `aws-building-blocks` with subsection structure**

Create subsections for:

- EC2
- Security Group
- Elastic IP
- S3
- IAM
- VPC
- subnet
- route table
- internet gateway
- NAT gateway
- ALB
- Auto Scaling Group

Each subsection must follow this mini-pattern:

```html
<article class="service-block">
  <h3>EC2 instance</h3>
  <p>Đây là gì...</p>
  <div class="callout beginner">...</div>
  <div class="code-card"><pre><code class="language-hcl">...</code></pre></div>
  <div class="callout mistake">...</div>
</article>
```

- [ ] **Step 3: Add enough code to make AWS blocks feel real**

At minimum, include:

```hcl
resource "aws_security_group" "web" {
  name        = "web-sg"
  description = "Allow HTTP and SSH"
  vpc_id      = aws_vpc.main.id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["203.0.113.10/32"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

```hcl
resource "aws_s3_bucket" "artifacts" {
  bucket = "${var.project_name}-${var.environment}-artifacts"

  tags = local.common_tags
}
```

- [ ] **Step 4: Add production notes where beginner defaults are not enough**

Examples:

- public SSH mở toàn cầu là xấu;
- NAT Gateway có cost;
- S3 bucket naming là global;
- IAM policy quá rộng là nguy hiểm.

- [ ] **Step 5: Verify breadth and readability**

Check:

- all listed AWS building blocks appear;
- every subsection contains explanation, code, and warning/mistake note;
- the section still reads like teaching, not raw docs copy.

### Task 7: Write Modules and Multi-Tier Application Patterns

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `terraform-modules` with root-vs-child explanation**

Must cover:

- what a root module is;
- what a child module is;
- when to create a module;
- when a module is overkill;
- module inputs;
- module outputs;
- keeping module responsibilities narrow.

- [ ] **Step 2: Add a realistic module folder tree**

Use:

```text
modules/
├── vpc/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
├── ec2/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
└── alb/
    ├── main.tf
    ├── variables.tf
    └── outputs.tf
```

- [ ] **Step 3: Add full code examples for `modules/vpc/*`**

At minimum include:

```hcl
resource "aws_vpc" "this" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = merge(var.tags, {
    Name = "${var.name_prefix}-vpc"
  })
}
```

```hcl
output "vpc_id" {
  value = aws_vpc.this.id
}
```

- [ ] **Step 4: Add `modules/ec2/*` and `modules/alb/*` examples plus root-module usage**

Use one root-level example:

```hcl
module "network" {
  source      = "./modules/vpc"
  name_prefix = var.project_name
  vpc_cidr    = "10.10.0.0/16"
  tags        = local.common_tags
}

module "web_alb" {
  source            = "./modules/alb"
  name_prefix       = var.project_name
  vpc_id            = module.network.vpc_id
  public_subnet_ids = module.network.public_subnet_ids
  tags              = local.common_tags
}
```

- [ ] **Step 5: Verify module section bridges into the first capstone**

Check:

- the section explains modules conceptually;
- the code examples are not toy-only;
- the transition to a multi-tier application feels natural.

### Task 8: Write Backend, State, Remote State, Import, Moved Blocks, and Drift

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `backend-state-remote-state` as one of the deepest chapters**

Must explain:

- state purpose;
- why Terraform needs state;
- local state;
- remote state;
- why teams avoid local-only state;
- backend concept;
- S3 backend;
- state locking via `use_lockfile`;
- bucket versioning;
- backend permissions;
- remote state outputs;
- environment separation.

- [ ] **Step 2: Include an S3 backend example and explain every field**

Use:

```hcl
terraform {
  backend "s3" {
    bucket       = "terraform-state-prod-example"
    key          = "network/terraform.tfstate"
    region       = "ap-southeast-1"
    use_lockfile = true
  }
}
```

Add a production note about bucket versioning and backend IAM permissions.

- [ ] **Step 3: Add `terraform_remote_state` example**

Use:

```hcl
data "terraform_remote_state" "network" {
  backend = "s3"

  config = {
    bucket = "terraform-state-prod-example"
    key    = "network/terraform.tfstate"
    region = "ap-southeast-1"
  }
}
```

Explain:

- when to use it;
- why overusing cross-state coupling is risky.

- [ ] **Step 4: Write `import-moved-drift` with real workflows**

Must include:

- import an existing resource;
- `import` block;
- matching `resource` block;
- `moved` block;
- drift from manual console changes;
- reading `terraform plan` to detect divergence.

Use:

```hcl
import {
  to = aws_instance.existing
  id = "i-0123456789abcdef0"
}

resource "aws_instance" "existing" {
  ami           = "ami-xxxxxxxxxxxxxxxxx"
  instance_type = "t3.micro"
}
```

And:

```hcl
moved {
  from = aws_instance.old_name
  to   = aws_instance.new_name
}
```

- [ ] **Step 5: Verify this chapter connects Viblo Bài 7, 8, and 19 with official docs**

Check:

- state purpose is clearly explained;
- S3 backend is concrete;
- drift handling is practical;
- `moved` block is explained in refactor context, not randomly.

### Task 9: Write Testing, Validation, CI/CD, Deployment Strategies, and Terraform + Ansible

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `testing-validation-quality-gates`**

Must cover:

- `terraform fmt`
- `terraform validate`
- reading `terraform plan`
- review before apply
- intro to Terraform test framework
- minimal quality gates for production

Use a test snippet:

```hcl
run "bucket_name_format" {
  command = plan

  assert {
    condition     = can(regex("^[a-z0-9-]+$", aws_s3_bucket.artifacts.bucket))
    error_message = "Bucket name must be lowercase and hyphen-safe."
  }
}
```

- [ ] **Step 2: Write `cicd-and-automation`**

Must cover:

- Terraform Cloud overview;
- CI flow;
- plan/apply separation;
- approval gates;
- GitLab CI;
- Jenkins;
- shell automation.

Include one minimal GitLab CI example:

```yaml
stages:
  - validate
  - plan
  - apply

terraform_validate:
  stage: validate
  script:
    - terraform fmt -check
    - terraform init -backend=false
    - terraform validate
```

- [ ] **Step 3: Write `deployment-strategies`**

Must explain:

- zero-downtime mindset;
- blue/green;
- A/B testing;
- rollback thinking;
- when beginners should stop at understanding concept only.

Add one comparison table for rollout strategies.

- [ ] **Step 4: Write `terraform-and-ansible`**

Must explain:

- Terraform for provisioning;
- Ansible for configuration;
- shell scripts for glue automation;
- why one tool should not be forced to do everything.

- [ ] **Step 5: Verify the chapter group feels production-oriented**

Check:

- these sections are not generic DevOps prose;
- they tie directly back to Terraform AWS workflows;
- they include examples or pseudo-pipeline code where relevant.

### Task 10: Write the Security Chapter and the AI-on-AWS Bridge Chapter

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `security` as a first-class chapter**

Must include:

- no hard-coded secrets;
- state file sensitivity;
- backend bucket protection;
- logs may leak values;
- least privilege IAM;
- provider version pinning;
- community module caution;
- secret handling with Vault at concept level and workflow level.

Add one warning box explicitly saying state can contain sensitive values.

- [ ] **Step 2: Write `terraform-for-ai-on-aws` as the bridge into applied AI**

Structure this chapter into subsections:

- `Infrastructure as Code for AI: Deploying LLM Apps with Terraform`
- `Infrastructure as Code: Automating AI Deployments with Terraform`
- `Automating AI Deployments with Terraform and Shell Scripts`
- `Automating Full-Stack AI Deployment with Terraform and AWS`
- `Testing Production AI Deployments and Terraform Cleanup Workflows`
- `Setting Up Secure AI Ingestion Pipelines with Terraform and AWS`
- `Deploying AI-Generated APIs to Production with AWS Lambda & Terraform`

- [ ] **Step 3: Make the AI chapter concrete with service mapping**

At minimum, explain which layer Terraform manages:

- networking;
- IAM;
- buckets;
- Lambda/API Gateway;
- logs;
- optionally container registry and ECS;
- not the model logic itself.

Add a table like:

```html
<table class="comparison-table">
  <thead>
    <tr>
      <th>Layer</th>
      <th>Terraform quản lý gì</th>
      <th>Terraform không thay thế gì</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AI API infrastructure</td>
      <td>Lambda, IAM, API Gateway, logs</td>
      <td>Business logic inference code</td>
    </tr>
    <tr>
      <td>Data ingestion</td>
      <td>S3, triggers, permissions, observability</td>
      <td>ML preprocessing logic chi tiết</td>
    </tr>
  </tbody>
</table>
```

- [ ] **Step 4: Add shell automation framing**

Explain why scripts like `package_lambda.ps1` or `deploy_ai_api.ps1` matter:

- packaging artifacts;
- deterministic deploy steps;
- cleanup;
- bridging build output with Terraform apply.

- [ ] **Step 5: Verify the AI chapter feels applied, not trendy**

Check:

- it grows naturally from earlier Terraform concepts;
- it uses AWS services concretely;
- it keeps security and cleanup visible.

### Task 11: Build Capstone 1 - AWS Foundation Multi-Tier Application

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Create the capstone intro with architecture overview**

Capstone 1 must explain:

- mục tiêu hệ thống;
- các thành phần AWS;
- vì sao chọn multi-tier;
- module boundaries;
- flow deploy/update/destroy.

- [ ] **Step 2: Add a realistic project tree for Capstone 1**

Use:

```text
capstone-1-foundation-app/
├── versions.tf
├── provider.tf
├── backend.tf
├── variables.tf
├── terraform.tfvars
├── locals.tf
├── main.tf
├── outputs.tf
├── modules/
│   ├── vpc/
│   ├── alb/
│   └── ec2/
└── scripts/
    ├── init.ps1
    ├── plan.ps1
    ├── apply.ps1
    └── destroy.ps1
```

- [ ] **Step 3: Add enough `.tf` code for network + compute + load balancing**

Must include examples for:

- VPC
- public/private subnets
- route tables
- internet gateway
- security groups
- ALB
- target group
- EC2 instances or autoscaling-oriented structure

The HTML must not stop at toy snippets. It should show meaningful file chunks.

- [ ] **Step 4: Add helper script examples**

Use PowerShell scripts similar to:

```powershell
terraform fmt
terraform init
terraform validate
terraform plan -out=tfplan
```

And:

```powershell
terraform apply tfplan
```

- [ ] **Step 5: Verify Capstone 1 is full enough to teach real project organization**

Check:

- tree exists;
- backend exists;
- modules exist;
- scripts exist;
- destroy/cleanup advice exists;
- cost note exists.

### Task 12: Build Capstone 2 - Serverless AI API on AWS

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Create capstone overview and architecture explanation**

Capstone 2 must explain:

- API nhận request gì;
- Lambda xử lý gì;
- API Gateway đóng vai trò gì;
- IAM policy nào cần;
- logs ghi ở đâu;
- shell scripts hỗ trợ packaging thế nào.

- [ ] **Step 2: Add a realistic file tree**

Use:

```text
capstone-2-serverless-ai-api/
├── versions.tf
├── provider.tf
├── variables.tf
├── terraform.tfvars
├── locals.tf
├── main.tf
├── outputs.tf
├── lambda/
│   └── handler.py
└── scripts/
    ├── package_lambda.ps1
    ├── plan.ps1
    ├── apply.ps1
    └── cleanup.ps1
```

- [ ] **Step 3: Add Terraform code for Lambda, IAM, API Gateway, and logs**

At minimum include:

- `aws_iam_role`
- `aws_iam_role_policy`
- `aws_lambda_function`
- `aws_cloudwatch_log_group`
- `aws_apigatewayv2_api`
- route/integration constructs as appropriate

If exact resource selection varies, the logic must still be coherent and deployable in principle.

- [ ] **Step 4: Add packaging and cleanup scripts**

Use PowerShell examples similar to:

```powershell
Remove-Item -Recurse -Force .\dist -ErrorAction SilentlyContinue
New-Item -ItemType Directory -Path .\dist | Out-Null
Compress-Archive -Path .\lambda\* -DestinationPath .\dist\lambda.zip -Force
```

And:

```powershell
terraform destroy -auto-approve
```

Add warning text about cost and accidental public exposure.

- [ ] **Step 5: Verify Capstone 2 ties AI language to actual infrastructure**

Check:

- this capstone is not just “Lambda hello world”;
- it clearly maps AI API concerns to AWS resources;
- it includes logs, IAM, packaging, and cleanup.

### Task 13: Build Capstone 3 - Secure AI Ingestion Pipeline on AWS

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Create capstone intro focused on secure ingestion**

Explain:

- user uploads or upstream data landing in S3;
- event trigger or processing handoff;
- IAM boundaries;
- why security matters more here;
- cleanup and lifecycle concerns.

- [ ] **Step 2: Add file tree and component map**

Use:

```text
capstone-3-secure-ai-ingestion/
├── versions.tf
├── provider.tf
├── backend.tf
├── variables.tf
├── terraform.tfvars
├── locals.tf
├── main.tf
├── outputs.tf
├── scripts/
│   ├── package_ingestion_lambda.ps1
│   ├── plan.ps1
│   ├── apply.ps1
│   └── destroy.ps1
└── lambda/
    └── ingest_handler.py
```

- [ ] **Step 3: Add Terraform examples for secure bucket + trigger + IAM + logs**

At minimum include coherent examples for:

- input bucket
- encryption-related note
- IAM role for ingestion handler
- logging
- event trigger path
- outputs

Even if not every advanced AWS hardening detail is implemented in code, the explanation must flag them.

- [ ] **Step 4: Add threat-aware notes and cleanup workflow**

Must include notes about:

- sensitive documents;
- least privilege;
- retention of logs;
- state sensitivity;
- destroy order and accidental data loss.

- [ ] **Step 5: Verify Capstone 3 is security-aware and not redundant**

Check:

- it differs clearly from Capstone 2;
- it focuses on ingestion pipeline thinking;
- it reinforces state, IAM, logging, and cleanup lessons.

### Task 14: Write Troubleshooting, Cheat Sheets, and Final Recap

**Files:**
- Modify: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`

- [ ] **Step 1: Write `troubleshooting-and-anti-patterns`**

Must cover:

- invalid credentials;
- wrong region;
- missing IAM permissions;
- drift after console edits;
- state lock issues;
- module rename mistakes;
- overusing `depends_on`;
- hard-coded IDs;
- mixing environments in one state.

Use a repeated pattern:

```html
<article class="trouble-card">
  <h3>Terraform báo AccessDenied</h3>
  <p><strong>Nguyên nhân thường gặp:</strong> ...</p>
  <p><strong>Cách kiểm tra:</strong> ...</p>
  <p><strong>Cách sửa:</strong> ...</p>
</article>
```

- [ ] **Step 2: Write `cheat-sheets`**

Must include:

- command cheat sheet;
- lifecycle cheat sheet;
- state/backend cheat sheet;
- module design checklist;
- production apply checklist.

- [ ] **Step 3: Write `final-recap`**

Must recap:

- what Terraform is;
- what to practice next;
- recommended reading order if revisiting;
- how to move from beginner to production confidence.

- [ ] **Step 4: Add a “next learning path” box**

Example topics:

- deeper module design
- Terraform Cloud
- policy-as-code
- testing and review gates
- multi-account AWS

- [ ] **Step 5: Verify the ending gives closure**

Check:

- the recap feels earned;
- it does not introduce major new concepts;
- it helps the reader know what to practice next.

### Task 15: Final QA for Completeness, Design, and Source Grounding

**Files:**
- Review: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_beginner_handbook.html`
- Review: `G:\AIProduction_t6_2026\production\tai_lieu\Learn_Terraform\terraform_aws_html_spec.md`

- [ ] **Step 1: Run a manual completeness pass against the spec**

Use this checklist:

```text
[ ] every locked section exists
[ ] sticky TOC works
[ ] progress bar works
[ ] beginner-first tone maintained
[ ] backend/state/drift/security chapters are substantial
[ ] all 3 capstones exist
[ ] AI chapter exists and is applied
[ ] code inventory is substantially present
[ ] cleanup/cost notes appear in hands-on areas
[ ] DESIGN-claude direction is visible
```

- [ ] **Step 2: Run a no-placeholder scan**

Search the HTML for:

```text
TODO
TBD
lorem
placeholder
your-resource
coming soon
...
```

If any appear in unfinished form, replace them.

- [ ] **Step 3: Run a source-coverage pass**

Confirm the HTML visibly covers:

- IaC and Terraform basics;
- lifecycle;
- functional/HCL patterns;
- modules;
- backend and remote state;
- Terraform Cloud;
- CI/CD;
- blue/green and A/B testing;
- Terraform + Ansible;
- GitLab and Jenkins;
- security and secrets;
- drift/state reconciliation;
- AI deployment topics.

- [ ] **Step 4: Run a readability pass**

Check:

- no section is just a wall of text without structure;
- long sections have subheadings;
- code blocks have explanation around them;
- callout boxes are distributed naturally;
- Vietnamese is clear and not machine-stiff.

- [ ] **Step 5: Open the final HTML in a browser and verify UX**

Expected:

- page loads locally without missing assets;
- desktop layout looks editorial and readable;
- mobile layout stacks correctly;
- code blocks scroll horizontally;
- TOC is navigable;
- no severe visual glitches.

## 11. Chapter Density Targets

To avoid shallow output, use these rough density targets:

- Orientation + setup: medium
- Terraform core + HCL + first project: very deep
- AWS building blocks: very deep
- Modules + backend + state + drift: very deep
- Testing + CI/CD + deployment strategies: medium to deep
- Security: deep
- AI bridge chapter: deep
- Each capstone: very deep
- Troubleshooting + cheat sheets: medium

If time is tight, do not shorten:

- state/backend/drift
- modules
- first project
- capstones
- AI applied sections

Shorten ornamental prose first.

## 12. Content Style Constraints During Execution

While writing the HTML, the implementing agent must:

- explain every new concept before using it heavily;
- introduce code in small steps before showing larger blocks;
- use Vietnamese explanations with English technical terms when clearer;
- keep code comments in English if comments are included;
- distinguish beginner advice from production advice;
- avoid pretending a simplified demo is production-ready;
- clearly label trade-offs.

## 13. Spec Coverage Crosswalk

Use this mapping while implementing:

- Spec Sections 1-5 map to Tasks 1-4
- Spec Section 6 and 7 map to Tasks 3-10 and Task 15
- Spec Section 8 maps to Tasks 3-14
- Spec Section 9 maps to Tasks 5-13
- Spec Sections 10-12 map to Tasks 2-14
- Spec Sections 13-15 map to Task 15
- Spec Section 16 maps to Task 15 final review loop

## 14. Plan Self-Review

Self-check against the writing-plans standard:

- The plan names the exact output file.
- The plan locks the file structure and component structure before writing content.
- The plan provides concrete HTML/CSS/JS starter code for the scaffold and behavior.
- The plan defines exact chapter IDs and chapter order.
- The plan maps source coverage from Viblo and official docs.
- The plan contains explicit verification steps after every major task.
- The plan includes the 3 capstones with distinct responsibilities.
- The plan includes anti-placeholder and UX verification steps.
- The plan is detailed enough that another agent can build the handbook without guessing major structure.

Result:

- Coverage is strong.
- No `TODO` or `TBD` placeholders remain.
- The plan is intentionally long because the requested handbook is intentionally deep and high-stakes for study.
