---
title: "Module 7: Authentication & Edge Layer"
weight: 7
pre: "<b>5.7. </b>"
---

## Module 7: Authentication & Edge Layer

**Thành viên:** Khiêm

### 7.1 API Gateway Cognito Authorizer Configuration

**Mục đích:** Protect all API endpoints — chỉ request với valid JWT từ Cognito mới được phép gọi Lambda.

> Note: JWT validation xảy ra ở API Gateway level (offload sang managed service), không trong Lambda code. Lambda chỉ đọc pre-validated claims từ `request.RequestContext.Authorizer.Claims`. Đây là idiomatic AWS pattern — đơn giản hơn manual validation.

**Bước 1:** Configure API Gateway Authorizer (AWS Console)

![API Gateway console](/images/workshop/52.png)

AWS Console → API Gateway → Select `BudgetTracketAPI`

![Menu Authorizers](/images/workshop/53.png)

- Authorizers (left menu) → Create Authorizer
- Name: `CognitoAuthorizer`
- Type: Cognito
- Cognito User Pool: Select từ Module 6 (tên pool: `budget-tracket-dev`)
- Token source: Authorization (client gửi `Authorization: Bearer <token>`)
- Token validation expression: (để trống, default là Authorization)
- Create Authorizer
- Copy Authorizer ARN (sẽ dùng trong SAM template)

**Bước 2:** Attach Authorizer to API Resources

![Gắn authorizer vào method](/images/workshop/54.png)

Cho mỗi method trong API (POST, GET, PUT, DELETE):
- Click Resource → Method (e.g., GET `/api/v1/transactions`)
- Method Request
- Authorization: Select `CognitoAuthorizer`
- Save

Hoặc (recommended): Config trong SAM template một lần cho tất cả methods.

**Bước 3:** SAM Template Configuration (Recommended)

File: `infrastructure/template.yaml`

![Cấu hình authorizer trong SAM template](/images/workshop/55.png)

**Bước 4:** Lambda Code Pattern (Extract Claims)

```
// BudgetTracket.Lambda/Functions/TransactionFunction.cs
```

![Code trích xuất claims](/images/workshop/56.png)
![Sử dụng claims](/images/workshop/57.png)

Key points:
- `request.RequestContext.Authorizer.Claims` chứa JWT claims đã được validate.
- `sub` = userId (Cognito subject identifier).
- `email`, `name`, v.v. từ Cognito user attributes.
- Không cần manual JWT parsing/validation — API Gateway xử lý rồi.

**Bước 5:** Test Authorizer

```
# Get JWT token (login via React app hoặc CLI)
curl -X POST https://cognito-idp.ap-southeast-1.amazonaws.com/<UserPoolId>/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=password&client_id=<ClientId>&username=test@example.com&password=Password123!"

# Extract access_token từ response

# Call API with token
curl -X GET https://<api-id>.execute-api.ap-southeast-1.amazonaws.com/dev/api/v1/transactions \
  -H "Authorization: Bearer <access_token>"

# Expected: 200 OK với transaction list
# Without token hoặc invalid token: 401 Unauthorized
```

**Bước 6:** Cross-Origin (CORS) with Authorizer

API Gateway → Resources → Select resource → Actions → Enable CORS

![Enable CORS kèm authorizer](/images/workshop/58.png)

- Default 4XX and 5XX CORS headers: Check
- Access-Control-Allow-Headers: `Content-Type,Authorization`
- Enable CORS and replace existing CORS headers

### 7.2 CloudFront + Lambda@Edge Setup

![Danh sách CloudFront distributions](/images/workshop/59.png)

**Bước 1:** AWS Console → CloudFront → Create distribution

![Create distribution](/images/workshop/60.png)
![Origin access control](/images/workshop/61.png)

- Origin domain: `budget-tracket-frontend-dev.s3.ap-southeast-1.amazonaws.com`
- S3 access: Origin access control (OAC) → Create OAC
- OAC name: `BudgetTracketOAC` → Create

**Bước 2:** Behaviors

![Cấu hình behavior](/images/workshop/62.png)

- Path pattern: `/*`
- Viewer protocol policy: Redirect HTTP to HTTPS
- Allowed HTTP methods: GET, HEAD
- Caching policy: CachingOptimized (S3)
- Origin request policy: CORS-S3Origin
- Compress objects automatically: Yes

**Bước 3:** Web ACL
- AWS WAF Web ACL: Select `BudgetTracketWAF` (từ Module 3.3)

**Bước 4:** Create Distribution
- Copy Distribution domain name: `d123abc456.cloudfront.net`

**Bước 5:** Update S3 Bucket Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontAccess",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::budget-tracket-frontend-dev/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::<account-id>:distribution/<DISTRIBUTION_ID>"
        }
      }
    }
  ]
}
```

### 7.3 Update Route 53 A Record

Route 53 → Hosted zones → `budget-tracket.com` → Create record
- Record name: `app` (hoặc root domain)
- Type: A
- Alias: Yes
- Route to: CloudFront distribution → select distribution from 7.2
- Create record

![Route 53 A record](/images/workshop/63.png)
