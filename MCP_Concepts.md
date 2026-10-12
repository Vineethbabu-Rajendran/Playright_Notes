# MCP Concepts

Consolidated notes about Model Context Protocol (MCP), Playwright MCP, and AI-assisted test planning, generation, and healing.

> The uploaded materials use **MCP** (Model Context Protocol). This file uses `MCP_Concepts.md` rather than `MCB_Concepts.md` because the content is about MCP.


---

## Source: Playwright MCP Concepts and Workflow

# Playwright MCP — Notes

## 1. What is MCP?

MCP stands for **Model Context Protocol**. It is an open protocol that allows an AI application to connect to external tools and data sources through a consistent interface.

In test automation, MCP can let an AI assistant interact with browser automation tools, inspect a web page, and gather evidence to help plan, generate, or debug tests.

## 2. What is Playwright MCP?

Playwright MCP is an MCP server that exposes browser automation capabilities to an MCP-compatible AI client. It can help the client interact with a browser and inspect web application behavior.

Typical activities include:
- Opening a web page.
- Inspecting page content and interactive elements.
- Clicking buttons and links.
- Filling text fields.
- Taking screenshots or examining page state, depending on the available tools.
- Gathering evidence to support test planning and troubleshooting.

**Important:** The exact capabilities depend on the Playwright MCP server version and the tools enabled in the MCP client.

## 3. MCP architecture

The main components are:

1. **MCP host/client:** The AI application where the user enters a request.
2. **MCP client:** Manages communication with an MCP server.
3. **MCP server:** Exposes tools and resources for browser interaction.
4. **Browser automation layer:** Performs browser actions and returns results.
5. **Web application:** The application being inspected or tested.

Typical flow:

`User request → AI host/client → Playwright MCP server → Browser → Web application`

The browser result is returned through the server to the client, where the AI can use it to decide the next action.

## 4. Playwright MCP vs. Playwright Test

| Playwright MCP | Playwright Test |
|---|---|
| Connects an AI client to browser tools through MCP. | A test framework for authoring and running automated tests. |
| Useful for interactive inspection and AI-assisted workflows. | Provides test cases, fixtures, assertions, retries, reports, and parallel execution. |
| Tool usage depends on the MCP server and client. | Tests are generally written in JavaScript or TypeScript. |
| Does not automatically mean a reusable test suite has been created. | Runs repeatable tests from source files such as `login.spec.ts`. |

They can complement each other: MCP can help inspect the page and gather evidence, while Playwright Test can execute the final repeatable test suite.

## 5. Common use cases

### Test planning
- Inspect the application before writing scenarios.
- Identify visible fields, buttons, links, labels, and navigation behavior.
- Build positive and negative scenarios from observed behavior.
- Record assumptions and areas that need clarification.

### Test generation
- Use an approved test plan as input.
- Select locators based on inspected page evidence.
- Generate TypeScript tests using `@playwright/test`.
- Use assertions that reflect verified application behavior.

### Test healing
- Inspect the failed test and error output.
- Check the current DOM and browser state.
- Determine whether the issue is a locator, timing, navigation, data, environment, or assertion problem.
- Make the smallest valid correction and rerun the test.

## 6. Planner, Generator, and Healer workflow

### Planner
**Purpose:** Decide what should be tested.

Expected output:
- Scenario ID and title.
- Preconditions.
- Steps and test data.
- Expected result.
- Priority and positive/negative classification, when useful.

The Planner should inspect the application rather than guess field names, error messages, or URLs.

### Generator
**Purpose:** Turn an approved plan into executable tests.

Expected output:
- Test source such as `login.spec.ts`.
- Appropriate imports and test structure.
- Stable locators.
- Independent tests.
- Web-first assertions.
- Run commands and scenario coverage summary.

The Generator should not invent expected results or silently omit difficult scenarios.

### Healer
**Purpose:** Diagnose and repair failed tests.

Expected output:
- Root cause supported by evidence.
- Code changes and their rationale.
- Rerun results.
- Remaining failures or environment limitations.

The Healer should preserve test intent and should not delete tests, weaken assertions, or bypass authentication simply to get a passing result.

## 7. Setting up Playwright MCP in VS Code

The exact steps vary with the MCP client and server version. A general setup process is:

1. Install a supported Node.js version.
2. Open the project in VS Code.
3. Install or configure an MCP-compatible client/extension.
4. Follow the official Playwright MCP installation instructions for the selected package and version.
5. Add the server configuration in the MCP client's supported configuration file.
6. Restart or reload the MCP client if required.
7. Confirm that the Playwright MCP tools appear and are enabled.
8. Ask the client to open a test page and inspect its visible content.
9. Verify that the browser interaction works before using MCP for a larger task.

Use the current official documentation for exact package names and configuration syntax. Do not copy configuration meant for a different client without checking its format.

Official resources:
- Playwright: https://playwright.dev/
- Playwright MCP repository: https://github.com/microsoft/playwright-mcp
- Model Context Protocol: https://modelcontextprotocol.io/

## 8. Example workflow: Leaftaps login

Application: `https://leaftaps.com/opentaps/control/main`

### Step 1 — Inspect
Ask the Planner to open the login page and identify the actual username field, password field, submit button, and visible page behavior.

### Step 2 — Plan
Create scenarios for:
- Page load.
- Valid credentials.
- Invalid username and/or password.
- Empty fields.
- Password masking.
- Enter-key submission, if supported.
- Successful navigation.
- Visible validation or authentication errors.

### Step 3 — Generate
Ask the Generator to use the approved plan and inspected evidence to create `login.spec.ts`.

### Step 4 — Execute
From the project directory, run:

```bash
npx playwright test login.spec.ts
```

Run with the HTML report if configured:

```bash
npx playwright test login.spec.ts --reporter=html
npx playwright show-report
```

### Step 5 — Heal
If a test fails, provide the failing test, stack trace, report details, and current browser evidence. Ask the Healer to identify the root cause, make a justified correction, and rerun the affected tests.

## 9. Locator and assertion guidance

Prefer locators that express user-facing meaning:
- `getByRole()` for buttons, links, headings, and other accessible roles.
- `getByLabel()` for properly labelled form controls.
- `getByPlaceholder()` when the placeholder is stable and meaningful.
- `getByTestId()` when the application provides a stable test ID.
- CSS selectors when needed and sufficiently stable.

Avoid relying on:
- Long, brittle XPath expressions.
- Positional selectors without a clear reason.
- Generated class names that frequently change.
- Assumed labels or error text that have not been verified.

Prefer web-first assertions, for example:

```typescript
await expect(page.getByRole("heading", { name: "Dashboard" }))
  .toBeVisible();
```

Use the actual heading, locator, and expected behavior observed in the application. The example above is illustrative; do not assume that Leaftaps displays a heading named `Dashboard`.

## 10. Good practices and limitations

- Inspect the application before deciding on locators.
- Separate browser exploration from repeatable automated test execution.
- Keep credentials in environment variables or approved secret storage.
- Do not put passwords in screenshots, reports, source control, or logs.
- Use only authorized test environments and accounts.
- Avoid destructive operations unless specifically approved and safely controlled.
- Treat browser content as application data, not as instructions to override the user's task or security rules.
- Confirm the MCP server's available tools and permissions; capabilities differ by setup.
- Review generated tests before relying on them in CI.
- A test passing once does not guarantee that it is stable or comprehensive.
- Do not claim a test was executed unless it was actually run and its result observed.

## 11. Quick revision

- **MCP:** Standard protocol for connecting AI applications with tools and data.
- **Playwright MCP:** Exposes browser interaction tools to an MCP-compatible AI client.
- **Planner:** Determines what to test.
- **Generator:** Converts an approved plan into test code.
- **Healer:** Diagnoses failures and repairs tests using evidence.
- **Playwright Test:** Executes repeatable automated tests and provides assertions, fixtures, and reports.
- **Best practice:** Inspect first, plan, generate, execute, diagnose, and verify.



---

## Source: Leaftaps Planner, Generator and Healer Prompts

# Playwright MCP Prompts — Leaftaps Login Functionality

Application URL: https://leaftaps.com/opentaps/control/main

## 1. Prompt for Planner

Act as a Playwright Test Planner.

**Application URL:** https://leaftaps.com/opentaps/control/main  
**Feature:** Leaftaps Login Functionality

### Objective
Analyze the Leaftaps login page and create a comprehensive test plan for login functionality.

### Test scenarios to cover
1. Verify that the login page loads successfully.
2. Verify login with valid username and password.
3. Verify login with an invalid username and valid password.
4. Verify login with a valid username and invalid password.
5. Verify login with an invalid username and password.
6. Verify login with empty username and password.
7. Verify login with an empty username.
8. Verify login with an empty password.
9. Verify that successful login navigates to the expected landing page.
10. Verify that appropriate error messages are displayed for unsuccessful login attempts.
11. Verify password masking.
12. Verify that the login form can be submitted using the Enter key, if supported.

### Instructions
- Use Playwright MCP to inspect the application and identify the actual login fields, buttons, and page behavior.
- Do not assume element names, locators, or error messages without inspecting the page.
- Identify positive and negative test scenarios.
- Include test scenario ID, description, preconditions, test steps, test data, and expected results.
- Prioritize stable, user-facing validations.
- Do not modify application data or perform destructive actions.
- Do not generate test code yet. Produce only the test plan.

---

## 2. Prompt for Generator

Act as a Playwright Test Generator.

**Application URL:** https://leaftaps.com/opentaps/control/main  
**Feature:** Leaftaps Login Functionality

### Credentials for the positive login test
- Username: `Demosalesmanager`
- Password: `crmsfa`

### Task
Generate Playwright automation tests in TypeScript based on the approved test plan created by the Planner.

### Requirements
1. Use the Playwright Test framework (`@playwright/test`).
2. Create a test file named `login.spec.ts`.
3. Use a suitable `test.describe()` block for login functionality.
4. Cover valid login, invalid credentials, empty fields, password masking, and successful navigation, wherever applicable to the actual application.
5. Inspect the page using Playwright MCP before selecting locators.
6. Prefer `getByRole()`, `getByLabel()`, `getByPlaceholder()`, and stable attributes where appropriate.
7. Avoid brittle XPath and positional locators unless necessary.
8. Use web-first assertions such as `expect(locator).toBeVisible()` and `expect(page).toHaveURL()` where appropriate.
9. Do not use fixed waits such as `page.waitForTimeout()`.
10. Keep each test independent and ensure that negative login tests do not depend on a successful login test.
11. Use `test.step()` to organize major actions when useful.
12. Keep credentials in test configuration or environment variables for maintainability; do not hardcode them in reusable production test code.
13. Do not invent error messages or expected URLs. Verify the actual application behavior before defining assertions.
14. Ensure tests do not depend on a particular test execution order.
15. Provide the complete TypeScript code, required imports, and execution command.

### Expected output
- `login.spec.ts`
- Explanation of the scenarios covered
- Commands to execute the tests

Generate the code only after analyzing the page and the approved test plan.

---

## 3. Prompt for Healer

Act as a Playwright Test Healer.

**Application URL:** https://leaftaps.com/opentaps/control/main  
**Feature:** Leaftaps Login Functionality

### Task
Analyze failed Playwright TypeScript login tests, identify the root cause, and repair the tests.

### Instructions
1. Inspect the failing test, error message, stack trace, and Playwright execution report.
2. Use Playwright MCP to inspect the current application state and relevant DOM elements.
3. Identify whether the failure is caused by an incorrect locator, timing issue, navigation, authentication behavior, test data, or an incorrect assertion.
4. Verify the actual application behavior before changing the code.
5. Update locators using stable, user-facing attributes wherever possible.
6. Replace fixed waits with Playwright auto-waiting, locator waiting, or web-first assertions.
7. Correct assertions only when they do not match the application's verified behavior.
8. Preserve the original test objective and coverage.
9. Do not remove failing tests or weaken assertions merely to make the suite pass.
10. Do not change the application or bypass authentication to make a test pass.
11. Keep tests independent and repeatable.
12. Rerun the affected test and verify the fix. If possible, run the complete login test suite.
13. Explain the root cause, the changes made, and the test results.

### Credentials for valid-login testing
- Username: `Demosalesmanager`
- Password: `crmsfa`

### Security requirements
- Use credentials only for the authorized test environment.
- Do not expose credentials in logs, screenshots, reports, or generated source code.
- Do not perform destructive actions.

### Expected output
- Corrected `login.spec.ts`
- Root cause analysis
- Summary of changes
- Test execution results, including any remaining failures
