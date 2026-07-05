---
title: "Module 2: Prerequisites"
weight: 2
pre: "<b>5.2. </b>"
---

## Module 2: Shared Prerequisites

Setup Chung cho tất cả thành viên nhóm.

### 2.1 AWS Account Setup

**Bước 1: Truy cập AWS Console**
- URL: https://console.aws.amazon.com/
- Đăng nhập bằng AWS account.
- Chọn Region: `ap-southeast-1` (Singapore).

**Bước 2: Tạo IAM User cho development**

![Tìm kiếm IAM trong console](/images/workshop/0.png)

Vào IAM → Users → Create user

![Danh sách IAM users, Create user](/images/workshop/1.png)

- User name: `budget-tracket-dev`

![Form User details](/images/workshop/2.png)

**Bước 3: Gán quyền cho IAM User**

![Gán quyền](/images/workshop/3.png)

**Bước 4: Tạo Access Keys**

![Tạo access keys](/images/workshop/4.png)
![Chi tiết access key](/images/workshop/5.png)
![Xác nhận access key](/images/workshop/6.png)

- Copy: Access Key ID & Secret Access Key.

### 2.2 Local Development Tools

Cài đặt:

![Cài đặt công cụ local](/images/workshop/7.png)

### 2.3 Configure AWS CLI

```
aws configure
AWS Access Key ID: <paste từ bước 2.4>
AWS Secret Access Key: <paste từ bước 2.4>
Default region: ap-southeast-1
Default output format: json
```

Verify:

```
aws sts get-caller-identity
```

Output: UserId, Account, Arn

### 2.4 Clone Repository

```
git clone https://github.com/giakhiem2902/budget-tracket.git
cd budget-tracket
```

Verify folder structure:

```
ls -la
├── frontend/
├── backend/
├── infrastructure/
└── CLAUDE.md
```
