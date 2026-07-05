---
title: "Module 7: Authentication & Edge Layer"
weight: 7
pre: "<b>5.7. </b>"
---

## Module 7: Authentication & Edge Layer

**Member:** Khiem

### 7.1 API Gateway Cognito Authorizer Configuration

**Purpose:** protect all API endpoints — only requests with a valid JWT from Cognito are allowed to call Lambda.

> Note: JWT validation happens at the API Gateway level (offloaded to a managed service), not in the Lambda code. Lambda only reads the pre-validated claims from `request.RequestContext.Authorizer.Claims`. This is the idiomatic AWS pattern — simpler than manual validation.

**Step 1:** Configure API Gateway Authorizer (AWS Console)

![API Gateway console](/images/workshop/52.png)

AWS Console → API Gateway → select `BudgetTracketAPI`

![Authorizers menu](/images/workshop/53.png)

- Authorizers (left menu) → Create Authorizer
- Name: `CognitoAuthorizer`
- Type: Cognito
- Cognito User Pool: select the one from Module 6 (pool name: `budget-tracket-dev`)
- Token source: `Authorization` (client sends `Authorization: Bearer <token>`)
- Token validation expression: leave blank (default is `Authorization`)
- Create Authorizer
- Copy the Authorizer ARN (used in the SAM template)

**Step 2:** Attach Authorizer to API Resources

![Attach authorizer to a method](/images/workshop/54.png)

For every method in the API (POST, GET, PUT, DELETE):
- Click Resource → Method (e.g., GET `/api/v1/transactions`)
- Method Request
- Authorization: select `CognitoAuthorizer`
- Save

Or (recommended): configure it once for all methods in the SAM template.

**Step 3:** SAM Template Configuration (Recommended)

File: `infrastructure/template.yaml`

![SAM template authorizer config](/images/workshop/55.png)

**Step 4:** Lambda Code Pattern (Extract Claims)

```
// BudgetTracket.Lambda/Functions/TransactionFunction.cs
```

![Extract claims code](/images/workshop/56.png)
![Claims usage](/images/workshop/57.png)

Key points:
- `request.RequestContext.Authorizer.Claims` contains the already-validated JWT claims.
- `sub` = userId (Cognito subject identifier).
- `email`, `name`, etc. come from the Cognito user attributes.
- No manual JWT parsing/validation needed — API Gateway already handles it.

**Step 5:** Test the Authorizer

```
# Get a JWT token (login via the React app or CLI)
curl -X POST https://cognito-idp.ap-southeast-1.amazonaws.com/<UserPoolId>/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=password&client_id=<ClientId>&username=test@example.com&password=Password123!"

# Extract access_token from the response

# Call the API with the token
curl -X GET https://<api-id>.execute-api.ap-southeast-1.amazonaws.com/dev/api/v1/transactions \
  -H "Authorization: Bearer <access_token>"

# Expected: 200 OK with the transaction list
# Without a token or with an invalid token: 401 Unauthorized
```

**Step 6:** Cross-Origin (CORS) with Authorizer

API Gateway → Resources → select resource → Actions → Enable CORS

![Enable CORS with authorizer](/images/workshop/58.png)

- Default 4XX and 5XX CORS headers: Check
- Access-Control-Allow-Headers: `Content-Type,Authorization`
- Enable CORS and replace existing CORS headers

### 7.2 CloudFront + Lambda@Edge Setup

![CloudFront distributions](/images/workshop/59.png)

**Step 1:** AWS Console → CloudFront → Create distribution

![Create distribution](/images/workshop/60.png)
![Origin access control](/images/workshop/61.png)

- Origin domain: `budget-tracket-frontend-dev.s3.ap-southeast-1.amazonaws.com`
- S3 access: Origin access control (OAC) → Create OAC
- OAC name: `BudgetTracketOAC` → Create

**Step 2:** Behaviors

![Behavior settings](/images/workshop/62.png)

- Path pattern: `/*`
- Viewer protocol policy: Redirect HTTP to HTTPS
- Allowed HTTP methods: GET, HEAD
- Caching policy: CachingOptimized (S3)
- Origin request policy: CORS-S3Origin
- Compress objects automatically: Yes

**Step 3:** Web ACL
- AWS WAF Web ACL: select `BudgetTracketWAF` (from Module 3.3)

**Step 4:** Create Distribution
- Copy the Distribution domain name: `d123abc456.cloudfront.net`

**Step 5:** Update the S3 Bucket Policy

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
- Record name: `app` (or the root domain)
- Type: A
- Alias: Yes
- Route to: CloudFront distribution → select the distribution from step 7.2
- Create record

![Route 53 A record](/images/workshop/63.png)
