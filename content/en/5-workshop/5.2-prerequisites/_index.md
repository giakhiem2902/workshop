---
title: "Module 2: Prerequisites"
weight: 2
pre: "<b>5.2. </b>"
---

## Module 2: Shared Prerequisites

Common setup for all team members.

### 2.1 AWS Account Setup

**Step 1: Access the AWS Console**
- URL: https://console.aws.amazon.com/
- Sign in with your AWS account.
- Select Region: `ap-southeast-1` (Singapore).

**Step 2: Create an IAM User for development**

![Search for IAM in the console](/images/workshop/0.png)

Go to IAM → Users → Create user

![IAM users list, Create user](/images/workshop/1.png)

- User name: `budget-tracket-dev`

![User details form](/images/workshop/2.png)

**Step 3: Grant permissions to the IAM User**

![Grant permissions](/images/workshop/3.png)

**Step 4: Create Access Keys**

![Create access keys](/images/workshop/4.png)
![Access key details](/images/workshop/5.png)
![Access key confirmation](/images/workshop/6.png)

- Copy the Access Key ID & Secret Access Key.

### 2.2 Local Development Tools

Install:

![Local tools installed](/images/workshop/7.png)

### 2.3 Configure AWS CLI

```
aws configure
AWS Access Key ID: <paste from step 2.4>
AWS Secret Access Key: <paste from step 2.4>
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
