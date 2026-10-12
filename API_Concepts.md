# API Concepts

This file contains API-related material found in the uploaded Markdown files.

> **Coverage note:** The uploaded files did not include a dedicated API/Postman/ServiceNow API notes file. The material below is limited to the API-related references present in the supplied Playwright notes; upload your API notes to expand this file with HTTP methods, authentication, status codes, CRUD, Postman, and service integrations.


---

## Source: API requests mentioned in Playwright overview

## 2. Playwright

Playwright is a browser automation library developed by Microsoft.

It is used to automate web browsers and perform actions such as:

-   Launching browsers
-   Opening web pages
-   Locating elements
-   Clicking elements
-   Entering text
-   Selecting options
-   Handling dialogs
-   Handling multiple pages
-   Uploading files
-   Taking screenshots
-   Performing API requests

### Common Playwright APIs

``` typescript
await page.goto("https://example.com");
await page.locator("#username").fill("admin");
await page.getByRole("button", { name: "Login" }).click();
```

Playwright focuses mainly on browser automation and application
interaction.



---

## Source: Playwright request fixture reference

## 9. Fixtures

Fixtures provide objects and resources required by tests.

The most commonly used fixture is `page`.

``` typescript
test("Login test", async ({ page }) => {
    await page.goto("https://example.com");
});
```

The `page` fixture represents a browser page.

Other commonly used fixtures include:

-   `browser`
-   `context`
-   `page`
-   `request`

Fixtures help create reusable and isolated test environments.



---

## Source: External data sources and API responses

# 22. JSON vs CSV vs `.env`

| Type | Primary Use | Structure |
|---|---|---|
| JSON | Structured test data | Objects and arrays |
| CSV | Tabular/large test data | Rows and columns |
| `.env` | Configuration and environment values | Key-value pairs |

### Simple Rule

**JSON:** Use when test data has a structured or nested format.

**CSV:** Use when test data is mainly tabular and there are many records.

**`.env`:** Use for environment-specific configuration and sensitive values such as URLs, usernames, tokens and passwords.

---
