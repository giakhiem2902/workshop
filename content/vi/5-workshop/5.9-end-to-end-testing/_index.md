---
title: "Module 9: End-to-End Testing"
weight: 9
pre: "<b>5.9. </b>"
---

## Module 9: End-to-End Testing

**Thành viên:** Cả nhóm

### 9.1 Frontend Unit Tests (Vitest)

```
cd frontend
npm install -D vitest @testing-library/react @testing-library/jest-dom
```

`package.json` có vitest + script `npm run test`.

### 9.2 Backend Unit Tests (xUnit)

```csharp
// BudgetTracket.Core.Tests/Services/TransactionServiceTests.cs
public class TransactionServiceTests
{
    private readonly TransactionService _service;
    private readonly Mock<ITransactionRepository> _mockRepo;

    public TransactionServiceTests()
    {
        _mockRepo = new Mock<ITransactionRepository>();
        _service = new TransactionService(_mockRepo.Object);
    }

    [Fact]
    public async Task CreateTransaction_WithValidInput_ShouldReturnSuccess()
    {
        // Arrange
        var txn = new CreateTransactionRequest { Amount = 100000, Category = "food" };

        // Act
        var result = await _service.CreateAsync(txn);

        // Assert
        Assert.NotNull(result);
        _mockRepo.Verify(r => r.CreateAsync(It.IsAny<Transaction>()), Times.Once);
    }
}
```

```
cd backend
dotnet test
```

### 9.3 E2E Tests (Playwright)

```
npm install -D @playwright/test
```

```javascript
// frontend/tests/e2e/login.spec.js
import { test, expect } from '@playwright/test';

test('User can login and view dashboard', async ({ page }) => {
  await page.goto('https://localhost:3000/login');

  await page.fill('[type="email"]', 'test@example.com');
  await page.fill('[type="password"]', 'password123');
  await page.click('button[type="submit"]');

  await page.waitForURL('**/dashboard');
  await expect(page.locator('h1')).toContainText('Dashboard');
});
```

```
npx playwright test
```
