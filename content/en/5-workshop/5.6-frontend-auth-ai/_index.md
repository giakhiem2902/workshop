---
title: "Module 6: Frontend, Auth & AI Integration"
weight: 6
pre: "<b>5.6. </b>"
---

## Module 6: Frontend, Auth & AI Integration

**Member:** Cong

### 6.1 Amazon Cognito User Pool

![Cognito overview](/images/workshop/44.png)

**Step 1:** AWS Console → Cognito → User pools → Create user pool

![Create user pool](/images/workshop/45.png)
![Authentication providers](/images/workshop/46.png)

- Authentication providers: ☑ Email ☐ Username ☐ Phone number
- Create user pool

**Step 2:** Create App Client

![App integration](/images/workshop/47.png)
![Create app client](/images/workshop/48.png)

- App integration → App clients and analytics → Create app client
- App client name: `budget-tracket-web-dev`
- Application type: Web application
- Create app client
- Copy values: User Pool ID `ap-southeast-1_xxxxxxxxx`, Client ID `53a215kkmh3ojp0okusxxxxxxx`

### 6.2 React Frontend Setup

**Step 1:** Setup environment

```
cd frontend
npm install

# Create .env file
cat > .env << EOF
VITE_API_BASE_URL=https://<api-id>.execute-api.ap-southeast-1.amazonaws.com/dev
VITE_COGNITO_USER_POOL_ID=ap-southeast-1_xxxxxxxxx
VITE_COGNITO_CLIENT_ID=xxxxxxxxxxxxxxxxx
VITE_AWS_REGION=ap-southeast-1
VITE_APP_ENV=development
EOF
```

**Step 2:** Install the React Cognito library

```
npm install amazon-cognito-identity-js
```

**Step 3:** Create the Cognito Auth Service

![Cognito auth service](/images/workshop/49.png)

### 6.3 React Components Setup

Create the Login Component:

```
// src/pages/Auth/Login.jsx
```

![Login component](/images/workshop/50.png)

### 6.4 AI Integration - Google Gemini API

**Step 1:** Get a Gemini API Key
- Visit: https://ai.google.dev/
- Get API Key → Create new API key → Copy key
- Save it to Secrets Manager (Module 4.4)

**Step 2:** Create the AI Service (Backend C#)

```
// BudgetTracket.Core/Services/AiService.cs
```

![AI service implementation](/images/workshop/51.png)

### 6.5 Build & Deploy Frontend

```
npm run build
# Upload to S3
aws s3 sync dist/ s3://budget-tracket-frontend-dev/ --delete
# Invalidate CloudFront (created in a later step)
aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
```
