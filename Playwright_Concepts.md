# Playwright Concepts

Consolidated Playwright notes extracted from the uploaded Markdown files. MCP-specific material is organized separately in `MCP_Concepts.md`.

## Source: Locators, Dropdowns and Assertions

# Playwright Locators, Dropdowns and Assertions -- Notes

## 1. Overview

These notes combine three practical Playwright scenarios:

1.  **Create Lead functionality** -- locators, login, navigation, form
    filling, and native select dropdown handling.
2.  **Assertions** -- URL, title, element state, text extraction, hard
    assertions, and soft assertions.
3.  **Non-select dropdown** -- handling a custom dropdown by clicking
    the dropdown and then clicking an option.

------------------------------------------------------------------------

# Part 1 -- Playwright Locators

## 2. What is a Locator?

A locator is a mechanism used by Playwright to identify an element on a
web page so that we can perform actions or assertions on it.

Common locator approaches used in these tests are:

-   `getByRole()`
-   `getByLabel()`
-   `getByText()`
-   `locator()`
-   XPath
-   CSS selectors
-   `first()`
-   `last()`
-   `nth()`

------------------------------------------------------------------------

## 3. `getByRole()`

`getByRole()` locates an element based on its accessible role.

### Example

``` typescript
await page.getByRole("textbox", { name: "Username" }).fill("Demosalesmanager");
```

Here:

-   `textbox` is the role.
-   `Username` is the accessible name.
-   `fill()` enters the username.

Another example:

``` typescript
await page.getByRole("button", { name: "Login" }).click();
```

This locates the Login button using its role and accessible name.

------------------------------------------------------------------------

## 4. `getByLabel()`

`getByLabel()` locates a form control using its associated label.

### Example

``` typescript
await page.getByLabel("Password").fill("crmsfa");
```

This is useful when a form field has a proper accessible label.

------------------------------------------------------------------------

## 5. `getByText()`

`getByText()` locates an element using visible text.

### Example

``` typescript
await page.getByText("CRM/SFA").click();
```

To match text exactly:

``` typescript
await page.getByText("Leads", { exact: true }).click();
```

The `exact: true` option helps avoid matching elements containing
additional text.

------------------------------------------------------------------------

## 6. `getByRole()` for Links

A link can be located using:

``` typescript
await page.getByRole("link", { name: "Create Lead" }).click();
```

This is generally more descriptive than relying only on a CSS or XPath
selector when the accessible role and name are reliable.

------------------------------------------------------------------------

# Part 2 -- `first()`, `last()` and `nth()`

## 7. `first()`

When multiple elements match the same locator, `first()` selects the
first matching element.

``` typescript
await page.getByRole("textbox").first().fill("Demosalesmanager");
```

------------------------------------------------------------------------

## 8. `last()`

`last()` selects the last matching element.

``` typescript
await page.getByRole("textbox").last().fill("crmsfa");
```

------------------------------------------------------------------------

## 9. `nth()`

`nth()` selects an element using a zero-based index.

``` typescript
await page.getByRole("textbox").nth(0).fill("Demosalesmanager");
await page.getByRole("textbox").nth(1).fill("crmsfa");
```

Indexing starts from `0`.

Therefore:

``` text
nth(0) → First element
nth(1) → Second element
nth(2) → Third element
```

### Important

Prefer a unique, meaningful locator over `nth()` when possible because
the order of elements can change when the application UI changes.

------------------------------------------------------------------------

# Part 3 -- CSS and XPath Locators

## 10. ID Selector

An element can be located using its ID.

``` typescript
await page.locator("#createLeadForm_companyName").fill("TestLeaf");
```

The `#` represents an ID selector.

------------------------------------------------------------------------

## 11. Attribute Selector

An element can be located using an attribute.

``` typescript
await page.locator('[name="submitButton"]').click();
```

This locates an element whose `name` attribute is `submitButton`.

------------------------------------------------------------------------

## 12. XPath Locator

XPath can be used when required.

``` typescript
await page.locator("//h5[text()='Type your name']").innerText();
```

This locates an `h5` element whose text is exactly `Type your name`.

------------------------------------------------------------------------

# Part 4 -- Form Handling

## 13. `fill()`

`fill()` is used to enter text into an input field.

Examples:

``` typescript
await page.locator("#createLeadForm_companyName").fill("TestLeaf");

await page.locator("#createLeadForm_firstName").fill("Vineeth");

await page.locator("#createLeadForm_lastName").fill("Rajendran");
```

------------------------------------------------------------------------

# Part 5 -- Native Select Dropdown

## 14. What is a Native Select Dropdown?

A native select dropdown is implemented using the HTML `<select>`
element.

For such elements, Playwright provides:

``` typescript
selectOption()
```

------------------------------------------------------------------------

## 15. Selecting by Value

``` typescript
await page
    .locator("#createLeadForm_dataSourceId")
    .selectOption({ value: "LEAD_EMPLOYEE" });
```

This selects an option based on its `value` attribute.

------------------------------------------------------------------------

## 16. Selecting by Label

``` typescript
await page
    .locator("#createLeadForm_dataSourceId")
    .selectOption({ label: "Partner" });
```

This selects an option based on its visible label.

------------------------------------------------------------------------

## 17. Selecting by Index

``` typescript
await page
    .locator("#createLeadForm_dataSourceId")
    .selectOption({ index: 2 });
```

The index is zero-based.

### Important correction for the Create Lead example

The original code contains:

``` typescript
await page
    .locator("#createLeadForm_dataSourceId")
    .selectOption([{ index: 2 }, { index: 3 }, { index: 5 }]);
```

This syntax requests multiple options and is appropriate when the
`<select>` element supports multiple selection.

If the Leaftaps dropdown is a normal single-select dropdown, use one
option:

``` typescript
await page
    .locator("#createLeadForm_dataSourceId")
    .selectOption({ index: 2 });
```

------------------------------------------------------------------------

# Part 6 -- Non-Select Dropdown

## 18. What is a Non-Select Dropdown?

A non-select dropdown is a custom dropdown that is not implemented using
a native `<select>` element.

It may be implemented using:

-   `div`
-   `button`
-   `ul`
-   `li`
-   Custom JavaScript components
-   ARIA-based components

------------------------------------------------------------------------

## 19. How to Handle a Non-Select Dropdown

The normal approach is:

``` text
Click Dropdown
      ↓
Options Appear
      ↓
Locate Required Option
      ↓
Click Option
```

### Example

``` typescript
await page.locator("//label[text()='Select Country']").click();

await page.getByRole("option", { name: "India" }).click();
```

------------------------------------------------------------------------

## 20. Native Select vs Non-Select Dropdown

  Native Select                     Non-Select Dropdown
  --------------------------------- ----------------------------------
  Uses `<select>`                   Usually uses custom HTML
  Use `selectOption()`              Usually use `click()`
  Options are `<option>` elements   Options may be `div`, `li`, etc.
  Browser-native behavior           Application-specific behavior

### Key interview point

Do not identify the dropdown type only by how it looks.

**Inspect the DOM** to determine whether it is a native `<select>` or a
custom component.

------------------------------------------------------------------------

# Part 7 -- Playwright Assertions

## 21. What is an Assertion?

An assertion verifies whether the actual application state matches the
expected result.

Playwright assertions are commonly written using:

``` typescript
expect()
```

------------------------------------------------------------------------

## 22. URL Assertion

``` typescript
await expect.soft(page)
    .toHaveURL("https://leafground.com/input.xhtml");
```

This verifies the current page URL.

------------------------------------------------------------------------

## 23. Title Assertion

``` typescript
await expect.soft(page)
    .toHaveTitle("Input Components");
```

This verifies the page title.

------------------------------------------------------------------------

## 24. Element State Assertion

``` typescript
await expect(
    page.getByRole("textbox", { name: "Babu Manickam" })
).toBeEditable();
```

This verifies that the textbox is editable.

Other commonly used state assertions include:

``` typescript
toBeVisible()
toBeHidden()
toBeEnabled()
toBeDisabled()
toBeChecked()
toBeEditable()
```

------------------------------------------------------------------------

# Part 8 -- Hard and Soft Assertions

## 25. Hard Assertion

A normal assertion is a hard assertion.

``` typescript
expect(textOnEle).toBe("Type your name");
```

If the assertion fails, the test fails at that point and execution does
not continue normally beyond the failure.

------------------------------------------------------------------------

## 26. Soft Assertion

A soft assertion is created using:

``` typescript
expect.soft()
```

Example:

``` typescript
await expect.soft(page)
    .toHaveURL("https://leafground.com/input.xhtml");

await expect.soft(page)
    .toHaveTitle("Input Components");
```

Soft assertions allow the test to continue so that additional assertions
can be evaluated. The test is still reported as failed if a soft
assertion fails.

------------------------------------------------------------------------

## 27. Hard vs Soft Assertion

  -----------------------------------------------------------------------
  Hard Assertion                      Soft Assertion
  ----------------------------------- -----------------------------------
  `expect()`                          `expect.soft()`

  Failure normally stops further test Test continues to collect further
  execution at the failure            assertion failures

  Useful for critical checkpoints     Useful when you want to validate
                                      multiple independent conditions
  -----------------------------------------------------------------------

### Example

``` typescript
expect(textOnEle).toBe("Type your name");
```

versus:

``` typescript
await expect.soft(page).toHaveTitle("Input Components");
```

------------------------------------------------------------------------

# Part 9 -- Retrieving Text

## 28. `innerText()`

`innerText()` retrieves the visible text from an element.

``` typescript
const textOnEle = await page
    .locator("//h5[text()='Type your name']")
    .innerText();
```

The retrieved value can then be verified:

``` typescript
expect(textOnEle).toBe("Type your name");
```

------------------------------------------------------------------------

# Part 10 -- End-to-End Flow in the Create Lead Test

The Create Lead test follows this flow:

``` text
Launch Leaftaps
      ↓
Enter Username
      ↓
Enter Password
      ↓
Click Login
      ↓
Click CRM/SFA
      ↓
Click Leads
      ↓
Click Create Lead
      ↓
Enter Company Name
      ↓
Enter First Name
      ↓
Enter Last Name
      ↓
Select Dropdown Option
      ↓
Click Submit
```

------------------------------------------------------------------------

# Part 11 -- Important Best Practices

## Prefer User-Facing Locators

Prefer:

``` typescript
getByRole()
getByLabel()
getByText()
```

when they provide a reliable unique locator.

------------------------------------------------------------------------

## Use CSS/ID When Appropriate

For stable unique IDs:

``` typescript
page.locator("#createLeadForm_firstName")
```

is perfectly valid.

------------------------------------------------------------------------

## Avoid Unnecessary `nth()`

Instead of:

``` typescript
page.getByRole("textbox").nth(1)
```

prefer:

``` typescript
page.getByLabel("Password")
```

when the label provides a reliable locator.

------------------------------------------------------------------------

## Avoid Unnecessary Waits

Do not add fixed waits such as:

``` typescript
await page.waitForTimeout(3000);
```

just to make the test pass.

Playwright's locator actions and assertions provide automatic waiting
for many common conditions.

------------------------------------------------------------------------

# Part 12 -- Quick Revision

``` text
getByRole()
    → Locate using accessibility role and accessible name

getByLabel()
    → Locate form control using associated label

getByText()
    → Locate using visible text

locator()
    → Use CSS/XPath/other selector strategies

first()
    → First matching element

last()
    → Last matching element

nth()
    → Element at zero-based index

fill()
    → Enter text

selectOption()
    → Select option from native <select>

click()
    → Click buttons, links, custom dropdowns, options

expect()
    → Hard assertion

expect.soft()
    → Soft assertion

innerText()
    → Retrieve visible text
```



---

## Source: Frames and JavaScript Dialogs

# Playwright Frames and Dialogs -- Topic Notes

## 1. Playwright Frames

A frame (iframe) is a webpage embedded inside another webpage.

### Why do we need frame handling?

Elements inside an iframe belong to a different document. We need to use
Playwright frame handling methods to interact with those elements.

### Common Frame Handling Methods

#### `page.frames()`

Returns all the frames available on the page.

``` typescript
const allFrames = page.frames();

console.log(allFrames.length);

for (let i = 0; i < allFrames.length; i++) {
    console.log(allFrames[i].url());
}
```

Use this when you want to inspect or work with the actual `Frame`
objects.

### `page.frameLocator()`

Creates a reference to an iframe and allows us to locate elements inside
it.

``` typescript
const frameReference = page.frameLocator("[id='singleframe']");

await frameReference.locator("//input[@type='text']")
    .fill("kumar@gmail.com");
```

### Nested Frames

A frame can contain another frame. In that case, create the outer frame
reference first and then create the inner frame reference.

``` typescript
const outerFrame = page.frameLocator("[src='MultipleFrames.html']");

const innerFrame = outerFrame.frameLocator("[src='SingleFrame.html']");

await innerFrame.locator("//input[@type='text']")
    .fill("maha@gmail.com");
```

### `frameLocator()` vs `frames()`

  -----------------------------------------------------------------------
  Method                              Purpose
  ----------------------------------- -----------------------------------
  `page.frames()`                     Gets all frame objects on the page

  `page.frameLocator()`               Creates a locator reference to an
                                      iframe

  `frame.frameLocator()`              Locates a nested iframe inside
                                      another iframe
  -----------------------------------------------------------------------

### Selenium vs Playwright

Selenium commonly uses:

``` java
driver.switchTo().frame(frame);
```

Playwright can directly interact with an iframe using:

``` typescript
const frame = page.frameLocator("iframe");
await frame.locator("input").fill("value");
```

Playwright does not require the same explicit switch-back approach used
in Selenium.

------------------------------------------------------------------------

# 2. JavaScript Dialogs

JavaScript dialogs include:

-   Alert
-   Confirm
-   Prompt

Playwright handles these dialogs using the `dialog` event.

## `page.on("dialog")`

Use the dialog event to listen for JavaScript dialogs.

``` typescript
page.on("dialog", async (dialog) => {
    // Handle the dialog
});
```

## `dialog.type()`

Returns the type of dialog.

Possible values include:

-   `alert`
-   `confirm`
-   `prompt`

Example:

``` typescript
console.log(dialog.type());
```

## `dialog.message()`

Returns the message displayed in the dialog.

``` typescript
console.log(dialog.message());
```

## `dialog.accept()`

Accepts the dialog.

For a prompt, a value can be entered while accepting:

``` typescript
await dialog.accept("Alert was handled By Us");
```

## `dialog.dismiss()`

Dismisses or cancels the dialog.

``` typescript
await dialog.dismiss();
```

------------------------------------------------------------------------

# 3. Handling Different Dialog Types

A common approach is to use conditional statements.

``` typescript
page.on("dialog", async (dialog) => {

    if (dialog.type() === "prompt") {
        await dialog.accept("Alert was handled By Us");
    }

    else if (dialog.type() === "confirm") {
        await dialog.dismiss();
    }

    else {
        await dialog.accept();
    }
});
```

Here:

-   Prompt → accept with a value
-   Confirm → dismiss
-   Alert → accept

------------------------------------------------------------------------

# 4. Important Dialog Rule

The dialog handler should be registered before clicking the button that
triggers the dialog.

``` typescript
page.on("dialog", async (dialog) => {
    await dialog.accept();
});

await page.getByRole("button", { name: "Show" }).click();
```

This ensures Playwright is listening when the dialog appears.

------------------------------------------------------------------------

# 5. Text Verification After Dialog Handling

After accepting or dismissing a dialog, verify the text displayed on the
page.

Example:

``` typescript
await expect(page.locator("#result"))
    .toHaveText("Hello Kumar");
```

The expected text depends on the action performed.

------------------------------------------------------------------------

# 6. Conditional Text Verification

If the test performs different actions, the expected text can also be
different.

``` typescript
const action = "accept";

if (action === "accept") {
    await dialog.accept("Kumar");
    await expect(result).toHaveText("Hello Kumar");
} else {
    await dialog.dismiss();
    await expect(result).toHaveText("User cancelled the prompt.");
}
```

------------------------------------------------------------------------

# 7. Frame + Dialog Combined Scenario

A typical real-time flow can be:

1.  Navigate to the application.
2.  Identify the iframe.
3.  Create a `frameLocator`.
4.  Locate the button inside the iframe.
5.  Register the dialog handler.
6.  Click the button.
7.  Handle the prompt.
8.  Verify the resulting text.

The important concept is that frame handling and dialog handling solve
two different problems:

-   Frame handling → access elements inside an iframe.
-   Dialog handling → handle browser JavaScript dialogs.

------------------------------------------------------------------------

# 8. Key Methods to Remember

``` text
page.frames()
page.frameLocator()
frame.frameLocator()
page.on("dialog")
dialog.type()
dialog.message()
dialog.accept()
dialog.dismiss()
expect(locator).toHaveText()
```

# 9. Classroom Code -- Simple Alert Handling

``` typescript
import { test } from "@playwright/test";

test("test to verify the user is able handle alert", async ({ page }) => {

    // Load the application URL
    await page.goto("https://leafground.com/alert.xhtml");

    // Handle all types of JavaScript dialogs
    page.on("dialog", async (dialog) => {

        // Check whether the dialog is a prompt
        if (dialog.type() === "prompt") {
            await dialog.accept("Alert was handled By Us");
        }

        // Check whether the dialog is a confirmation
        else if (dialog.type() === "confirm") {
            await dialog.dismiss();
        }

        // Handle the simple alert
        else {
            await dialog.accept();
        }
    });

    // Click the Show button of the Simple Alert
    await page.locator("//h5[text()=' Alert (Simple Dialog)']/following-sibling::button").click();

    // Click the Show button of the Confirmation Alert
    await page.locator("//h5[text()=' Alert (Confirm Dialog)']/following-sibling::button").click();

    // Click the Show button of the Prompt Alert
    await page.locator("//h5[text()=' Alert (Prompt Dialog)']/following-sibling::button").click();
});
```

# 10. Classroom Code -- Single Frame

``` typescript
import { test } from "@playwright/test";

test("test to verify the user is able handle frames", async ({ page }) => {

    // Load the application URL
    await page.goto("https://demo.automationtesting.in/Frames.html");

    // Create a reference to the single frame
    const frameReference = page.frameLocator("[id='singleframe']");

    // Fill the email inside the frame
    await frameReference.locator("//input[@type='text']").fill("kumar@gmail.com");
});
```

# 11. Classroom Code -- Nested Frames

``` typescript
import { test } from "@playwright/test";

test("test to verify the user is able handle frames", async ({ page }) => {

    // Load the application URL
    await page.goto("https://demo.automationtesting.in/Frames.html");

    // Navigate to the nested frame section
    await page.getByRole("link", { name: "frame with in an Iframe" }).click();

    // Create a reference to the outer frame
    const outerFrame = page.frameLocator("[src='MultipleFrames.html']");

    // Create a reference to the inner frame
    const innerFrame = outerFrame.frameLocator("[src='SingleFrame.html']");

    // Fill the email inside the inner frame
    await innerFrame.locator("//input[@type='text']").fill("maha@gmail.com");
});
```



---

## Source: File and Window Handling

# Playwright File Handling and Window Handling - Notes

## 1. File Download

### Basic Flow

1. Navigate to the application.
2. Register the `download` event.
3. Click the Download button.
4. Capture the downloaded file reference.
5. Save the file using `saveAs()`.

### Example

```typescript
import { test } from "@playwright/test";
import path from "path";

test("File Download", async ({ page }) => {

    // Load the application URL.
    await page.goto("https://demoqa.com/upload-download");

    // Register an event listener for the download event.
    const fileDownloadPromise = page.waitForEvent("download");

    // Click the Download button.
    await page.getByRole("button", { name: "Download" }).click();

    // Wait for the download event and get the downloaded file reference.
    const fileDownload = await fileDownloadPromise;

    // Save the file with its original suggested filename.
    await fileDownload.saveAs(
        path.join(__dirname, `../../download/${fileDownload.suggestedFilename()}`)
    );
});
```

### Important Methods

| Method | Purpose |
|---|---|
| `page.waitForEvent("download")` | Waits for a file download event |
| `download.suggestedFilename()` | Gets the original filename suggested by the server |
| `download.saveAs(path)` | Saves the downloaded file to a custom location |
| `download.path()` | Returns the temporary path of the downloaded file |

### Important Point

Register the download event **before** clicking the Download button.

```typescript
const downloadPromise = page.waitForEvent("download");
await page.getByRole("button", { name: "Download" }).click();
const download = await downloadPromise;
```

---

## 2. File Upload Using `setInputFiles()`

### Basic Flow

1. Navigate to the application.
2. Identify the file input element.
3. Use `setInputFiles()` to provide the file path.

### Example

```typescript
import { test } from "@playwright/test";
import path from "path";

test("File Upload", async ({ page }) => {

    // Load the application URL.
    await page.goto("https://demoqa.com/upload-download");

    // Upload the file using the file input element.
    await page.getByRole("button", { name: "Choose File" })
        .setInputFiles(path.join(__dirname, "../../Data/Logo.png"));
});
```

### Why `setInputFiles()`?

`setInputFiles()` directly sets the file on the HTML `<input type="file">` element.

A separate click is normally not required.

### Syntax

```typescript
await locator.setInputFiles("file path");
```

### Multiple Files

```typescript
await locator.setInputFiles([
    path.join(__dirname, "../../Data/File1.txt"),
    path.join(__dirname, "../../Data/File2.txt")
]);
```

---

## 3. File Upload Using `filechooser`

Sometimes the application opens the native file chooser when an element is clicked. In that case, Playwright can handle it using the `filechooser` event.

### Basic Flow

1. Register the `filechooser` event.
2. Click the upload element.
3. Capture the file chooser reference.
4. Use `setFiles()` to select the file.

### Example

```typescript
import { test } from "@playwright/test";
import path from "path";

test("File Upload Using Filechooser", async ({ page }) => {

    // Load the application URL.
    await page.goto("https://blazorise.com/docs/components/file-picker");

    // Register an event listener for the file chooser event.
    const fileUploadPromise = page.waitForEvent("filechooser");

    // Click the Choose files upload element.
    await page.locator("//span[text()='Choose files']").first().click();

    // Wait for the file chooser event.
    const fileUploadRef = await fileUploadPromise;

    // Set the file to be uploaded.
    await fileUploadRef.setFiles(
        path.join(__dirname, "../../Data/TestleafLogo.png")
    );
});
```

### Important Methods

| Method | Purpose |
|---|---|
| `page.waitForEvent("filechooser")` | Waits for the native file chooser event |
| `filechooser.setFiles()` | Selects the file for upload |
| `locator.setInputFiles()` | Directly sets files on a file input |

### `setInputFiles()` vs `filechooser`

`setInputFiles()` is generally simpler when the file input element can be located directly.

Use `filechooser` when clicking the upload control triggers the native file chooser and you need to capture that event.

---

# 4. Window / Tab Handling

In Playwright, a new tab or window opened within the same browser context is represented as a new `Page`.

### Important Concept

```text
Browser
   |
   └── Browser Context
          |
          ├── Page 1
          ├── Page 2
          └── Page 3
```

Multiple tabs or windows in the same context are handled as multiple `Page` objects.

---

## 5. Handling a New Tab Using `context.waitForEvent("page")`

### Basic Flow

1. Register the `page` event.
2. Click the element that opens the new tab.
3. Capture the new page reference.
4. Wait for the new page to load.
5. Perform actions on the new page.

### Example

```typescript
import { test } from "@playwright/test";

test("Window Handling", async ({ page, context }) => {

    // Load the application URL.
    await page.goto("https://leafground.com/window.xhtml");

    // Register an event listener for the newly opened page.
    const newPagePromise = context.waitForEvent("page");

    // Click the button that opens a new tab.
    await page.getByRole("button", { name: "Open", exact: true }).click();

    // Wait for the newly opened page.
    const newPage = await newPagePromise;

    // Wait for the new page to finish loading.
    await newPage.waitForLoadState();

    // Print the title of the new page.
    console.log(await newPage.title());
});
```

---

## 6. Switching Between Pages

Playwright does not use Selenium-style `switchTo().window()`.

Instead, maintain references to the required `Page` objects.

```typescript
await page.bringToFront();
```

This brings the specified page to the front.

### Example

```typescript
await newPage.bringToFront();
```

To return to the original page:

```typescript
await page.bringToFront();
```

---

## 7. `context.waitForEvent("page")` vs `page.waitForEvent("popup")`

### `context.waitForEvent("page")`

Used to detect a new page created in the browser context.

```typescript
const newPagePromise = context.waitForEvent("page");
```

### `page.waitForEvent("popup")`

Used when the current page directly opens a popup.

```typescript
const popupPromise = page.waitForEvent("popup");
```

### General Rule

| Scenario | Recommended Event |
|---|---|
| New page/tab created in the context | `context.waitForEvent("page")` |
| Current page opens a popup | `page.waitForEvent("popup")` |

---

# 8. Common Mistakes

## Mistake 1: Registering the event after clicking

Incorrect:

```typescript
await page.getByRole("button", { name: "Download" }).click();
const downloadPromise = page.waitForEvent("download");
```

Correct:

```typescript
const downloadPromise = page.waitForEvent("download");
await page.getByRole("button", { name: "Download" }).click();
```

The event listener should be registered before the action that triggers the event.

## Mistake 2: Using `waitForTimeout()` instead of waiting for an event

Avoid using:

```typescript
await page.waitForTimeout(5000);
```

as the primary mechanism for waiting for downloads or new tabs.

Prefer event-based synchronization:

```typescript
const downloadPromise = page.waitForEvent("download");
```

and:

```typescript
const newPagePromise = context.waitForEvent("page");
```

## Mistake 3: Trying to switch windows using Selenium syntax

Do not use:

```typescript
driver.switchTo().window();
```

In Playwright, use a `Page` reference:

```typescript
await newPage.bringToFront();
```

---

# 9. Path Handling

Node.js `path` is useful for creating platform-independent file paths.

```typescript
import path from "path";
```

Example:

```typescript
path.join(__dirname, "../../Data/Logo.png");
```

### Understanding `__dirname`

`__dirname` represents the directory of the current TypeScript/JavaScript file when using the CommonJS-style Node.js environment.

For example:

```text
Project
│
├── Data
│   └── Logo.png
│
└── tests
    └── file.spec.ts
```

From `file.spec.ts`:

```typescript
path.join(__dirname, "../Data/Logo.png");
```

`..` means move one directory up.

`../..` means move two directories up.

---

# 10. Interview Quick Revision

### File Download

```text
waitForEvent("download")
        ↓
click Download
        ↓
await downloadPromise
        ↓
saveAs()
```

### File Upload

```text
Locate file input
        ↓
setInputFiles()
```

### Filechooser Upload

```text
waitForEvent("filechooser")
        ↓
click upload element
        ↓
await filechooser
        ↓
setFiles()
```

### Window Handling

```text
context.waitForEvent("page")
        ↓
click element
        ↓
await newPagePromise
        ↓
newPage actions
```



---

## Source: Page Object Model and OOP in Automation

# Playwright Page Object Model - Notes

## 1. Objective

The goal is to create a Playwright automation framework using Page Object Model (POM) for this flow:

**Login → CRM/SFA → Leads**

Application:

`https://leaftaps.com/opentaps/control/main`

---

# 2. What is Page Object Model?

Page Object Model is a design pattern used in test automation to separate:

- Page locators
- Page-specific actions
- Test/business flow

The main idea is:

```text
Page Class
    |
    +-- Locators
    +-- Page Actions

Test Class
    |
    +-- Business Flow
    +-- Assertions
```

For this activity:

```text
LoginPage.ts
    → Login page locators and login action

WelcomePage.ts
    → CRM/SFA locator and action

MyHomePage.ts
    → Leads locator and action

CreateLead.spec.ts
    → Test scenario and flow
```

---

# 3. Why Do We Use POM?

Without POM, locators and actions are written directly inside the test.

Example:

```typescript
await page.getByRole("textbox", { name: "Username" }).fill("Demosalesmanager");
await page.getByRole("textbox", { name: "Password" }).fill("crmsfa");
await page.getByRole("button", { name: "Login" }).click();
```

With POM:

```typescript
await loginPageObj.login("Demosalesmanager", "crmsfa");
```

The test becomes easier to read because the test focuses on the business action rather than implementation details.

---

# 4. Project Structure

```text
project
├── pages
│   ├── LoginPage.ts
│   ├── WelcomePage.ts
│   └── MyHomePage.ts
├── testcases
│   └── CreateLead.spec.ts
├── playwright.config.ts
└── package.json
```

---

# 5. LoginPage.ts

## Purpose

`LoginPage.ts` represents the Login page.

It contains:

- Page reference
- Username locator
- Password locator
- Login button locator
- Login action

## Import

```typescript
import { Page, Locator } from "@playwright/test";
```

`Page` represents the Playwright browser page.

`Locator` represents an element locator.

## Class

```typescript
export class LoginPage {
```

A class groups related properties and methods together.

## Properties

```typescript
page: Page;
usernameField: Locator;
passwordField: Locator;
loginButton: Locator;
```

These properties store the Page object and the locators required by the Login page.

## Constructor

```typescript
constructor(page: Page) {

    this.page = page;

    this.usernameField =
        this.page.getByRole("textbox", { name: "Username" });

    this.passwordField =
        this.page.getByRole("textbox", { name: "Password" });

    this.loginButton =
        this.page.getByRole("button", { name: "Login" });
}
```

### What is a constructor?

A constructor is a special method that executes automatically when an object is created.

Example:

```typescript
let loginPageObj = new LoginPage(page);
```

When this statement executes:

1. A `LoginPage` object is created.
2. The `page` object is passed to the constructor.
3. `this.page = page` stores the received page object.
4. The locators are initialized.

## What is `this`?

`this` refers to the current object.

Example:

```typescript
this.page = page;
```

Here:

- `page` on the right = constructor parameter
- `this.page` on the left = class property

---

# 6. Login Method

```typescript
async login(username: string, password: string) {

    await this.usernameField.fill(username);
    await this.passwordField.fill(password);
    await this.loginButton.click();

}
```

The method receives test data:

```text
username
password
```

Then performs:

```text
Fill username
    ↓
Fill password
    ↓
Click Login
```

This hides the implementation details from the test.

The test only needs:

```typescript
await loginPageObj.login("Demosalesmanager", "crmsfa");
```

---

# 7. WelcomePage.ts

## Purpose

`WelcomePage.ts` represents the page displayed after login.

It contains:

```typescript
page: Page;
crmsfaLink: Locator;
```

The CRM/SFA link is identified using:

```typescript
this.page.getByRole("link", { name: "CRM/SFA" });
```

The action is:

```typescript
async clickCrmsfa() {
    await this.crmsfaLink.click();
}
```

The test calls:

```typescript
await welcomePageObj.clickCrmsfa();
```

---

# 8. MyHomePage.ts

## Purpose

`MyHomePage.ts` represents the My Home page.

It contains:

```typescript
page: Page;
leadsLink: Locator;
```

The Leads element is identified using:

```typescript
this.page.getByText("Leads", { exact: true });
```

The action is:

```typescript
async clickLeads() {
    await this.leadsLink.click();
}
```

The test calls:

```typescript
await myHomePageObj.clickLeads();
```

---

# 9. Why Pass `page` to Every Page Class?

The Playwright test provides a `page` object:

```typescript
test("To verify Create Lead", async ({ page }) => {
```

The same page object is passed to every Page Object:

```typescript
let loginPageObj = new LoginPage(page);
let welcomePageObj = new WelcomePage(page);
let myHomePageObj = new MyHomePage(page);
```

So the flow is:

```text
Playwright Page
      |
      +----> LoginPage
      |
      +----> WelcomePage
      |
      +----> MyHomePage
```

All Page Objects operate on the same browser tab/page.

---

# 10. Test Case

The test imports the Page Object classes:

```typescript
import { test } from "@playwright/test";

import { LoginPage } from "../pages/LoginPage";
import { WelcomePage } from "../pages/WelcomePage";
import { MyHomePage } from "../pages/MyHomePage";
```

Page Objects are created:

```typescript
let loginPageObj = new LoginPage(page);
let welcomePageObj = new WelcomePage(page);
let myHomePageObj = new MyHomePage(page);
```

Application is opened:

```typescript
await page.goto("https://leaftaps.com/opentaps/control/main");
```

Login is performed:

```typescript
await loginPageObj.login("Demosalesmanager", "crmsfa");
```

CRM/SFA is clicked:

```typescript
await welcomePageObj.clickCrmsfa();
```

Leads is clicked:

```typescript
await myHomePageObj.clickLeads();
```

---

# 11. Complete Execution Flow

```text
CreateLead.spec.ts
        |
        v
LoginPage.login()
        |
        v
WelcomePage.clickCrmsfa()
        |
        v
MyHomePage.clickLeads()
        |
        v
Leads Page
```

---

# 12. Page Class vs Test Class

## Page Class

Responsible for:

- Locators
- Page-specific actions

Example:

```typescript
usernameField: Locator;

async login(username: string, password: string) {
    await this.usernameField.fill(username);
}
```

## Test Class

Responsible for:

- Business flow
- Test data
- Assertions

Example:

```typescript
await loginPageObj.login("Demosalesmanager", "crmsfa");
await welcomePageObj.clickCrmsfa();
await myHomePageObj.clickLeads();
```

---

# 13. Constructor Theory

A constructor is automatically called when an object is created.

Example:

```typescript
class LoginFunction {

    username: string;

    constructor(username: string) {
        this.username = username;
        console.log(this.username);
    }

}
```

Object creation:

```typescript
let loginObj = new LoginFunction("Demosales");
```

The value `"Demosales"` is passed to the constructor.

Then:

```typescript
this.username = username;
```

stores it in the object.

This is the same concept used in Playwright POM:

```typescript
constructor(page: Page) {
    this.page = page;
}
```

The Page object is passed from the test and stored inside the Page Object.

---

# 14. Access Modifiers in TypeScript

The commonly used access modifiers are:

```text
public
private
protected
```

There is also:

```text
readonly
```

`readonly` controls reassignment rather than normal visibility.

---

# 15. Public

`public` members can be accessed from outside the class.

Example:

```typescript
export class BankAccount {

    public depositCash() {
        this.withdraw();
        console.log("Amount is deposited");
    }

}
```

Object:

```typescript
let bankOptions = new BankAccount();
bankOptions.depositCash();
```

The `depositCash()` method is accessible from outside the class.

---

# 16. Protected

A `protected` member can be accessed:

- Inside the same class
- Inside a child/derived class

Example:

```typescript
export class BankAccount {

    public depositCash() {
        this.withdraw();
        console.log("Amount is deposited");
    }

    protected withdraw() {
        console.log("Amount is deposited");
    }

}
```

A child class can access `withdraw()`:

```typescript
class FetchAccountDetails extends BankAccount {

    public details() {
        this.withdraw();
    }

}
```

But a normal external object should not directly access the protected member:

```typescript
let bankOptions = new BankAccount();

// bankOptions.withdraw(); // Not accessible
```

The supplied example also shows that the child object can access the inherited public method:

```typescript
let accountObj = new FetchAccountDetails();
accountObj.depositCash();
```

---

# 17. Private

A `private` member is intended to be accessed only inside the class where it is declared.

Example:

```typescript
class AccountDetails {

    private amount: number = 1000;

    public getAmount(): number {
        return this.amount;
    }

}
```

Direct access is not allowed:

```typescript
// console.log(accObj.amount);
```

Instead, the class exposes a public method:

```typescript
console.log(accObj.getAmount());
```

---

# 18. Encapsulation

Encapsulation means controlling access to the internal data of a class and exposing controlled operations to work with that data.

Example:

```typescript
class AccountDetails {

    private amount: number = 1000;

    public getAmount(): number {
        return this.amount;
    }

}
```

Here:

```text
private amount
      ↓
Hidden from direct external access
      ↓
public getAmount()
      ↓
Controlled access
```

The important idea is not simply "make variables private."

The idea is:

**Hide internal data and provide controlled access through methods.**

---

# 19. How Encapsulation Works in the Example

This is the internal data:

```typescript
private amount: number = 1000;
```

External code cannot directly access it:

```typescript
// console.log(accObj.amount);
```

The class provides a public method:

```typescript
public getAmount(): number {
    return this.amount;
}
```

External code uses:

```typescript
console.log(accObj.getAmount());
```

So the object controls how its internal data is accessed.

---

# 20. Connection Between Encapsulation and POM

POM follows a similar idea.

The Page Object stores the locator:

```typescript
usernameField: Locator;
```

The test does not need to know how the locator is implemented.

Instead, the test calls:

```typescript
await loginPageObj.login("Demosalesmanager", "crmsfa");
```

The Page Object controls the actual interaction:

```typescript
await this.usernameField.fill(username);
await this.passwordField.fill(password);
await this.loginButton.click();
```

So:

```text
Test
  |
  | calls method
  v
Page Object
  |
  | uses internal locators
  v
Application
```

---

# 21. Why Locators Are Kept Inside Page Classes

If a locator changes, ideally the change should be made in the Page Object rather than every test.

For example:

```typescript
this.usernameField =
    this.page.getByRole("textbox", { name: "Username" });
```

The test remains:

```typescript
await loginPageObj.login(username, password);
```

This improves maintainability.

---

# 22. Hard Wait vs Playwright Waiting

The activity contains:

```typescript
await page.waitForTimeout(5000);
```

This is useful for classroom observation.

However, it should not normally be used as the actual synchronization mechanism in automation.

Prefer:

- Playwright auto-waiting
- Locator actions
- Assertions
- Explicit waits only when there is a real synchronization requirement

---

# 23. Important Terms

| Term | Meaning |
|---|---|
| Class | Blueprint containing properties and methods |
| Object | Instance created from a class |
| Constructor | Special method executed during object creation |
| `this` | Refers to the current object |
| Page | Playwright browser page object |
| Locator | Playwright representation of an element |
| POM | Design pattern separating page implementation from test flow |
| Encapsulation | Controlling access to internal class data |
| Public | Accessible from outside the class |
| Private | Accessible only within the declaring class |
| Protected | Accessible within the class and derived classes |

---

# 24. Key Takeaways

1. Create one Page Object class for each relevant application page.
2. Store locators inside Page Object classes.
3. Store page-specific actions inside Page Object classes.
4. Pass the Playwright `page` object through the constructor.
5. Use the same `page` object across the Page Objects for the flow.
6. Keep business flow inside the test.
7. Use access modifiers to control class member access.
8. Use private data with public methods when controlled access is required.
9. Use protected members when child classes need access.
10. Avoid unnecessary hard waits in real automation.



---

## Source: Playwright Test Runner, Fixtures, Execution and Test Data

# Playwright Test -- Notes

## 1. Topics Covered

-   Playwright vs Playwright Test
-   Playwright Test Runner
-   `test()`
-   `test.describe()`
-   Test Annotations
-   `test.only()`
-   `test.skip()`
-   `test.fail()`
-   `test.slow()`
-   `test.describe.configure()`
-   Parallel Test Execution
-   Test Timeout
-   Fixtures
-   Test Isolation
-   Test Organization
-   Test Execution and Reporting
-   Browser and Page Interaction
-   `page.goto()`
-   `page.locator()`
-   Console Logging
-   Smoke Testing
-   Valid, Invalid and Negative Test Scenarios

------------------------------------------------------------------------

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

------------------------------------------------------------------------

## 3. Playwright Test

Playwright Test is the test runner provided by Playwright.

It provides features required for building and executing automated test
suites.

### Major Playwright Test Features

-   Test execution
-   Assertions
-   Fixtures
-   Hooks
-   Annotations
-   Parallel execution
-   Retries
-   Timeouts
-   Test isolation
-   Screenshots
-   Videos
-   Traces
-   HTML reports
-   Projects
-   Tags and test filtering

### Simple Difference

**Playwright:** Browser automation.

**Playwright Test:** Test automation framework/test runner built around
Playwright.

------------------------------------------------------------------------

## 4. `test()`

The `test()` function is used to define an individual test case.

Example:

``` typescript
test("Test to verify login", async ({ page }) => {
    await page.goto("https://example.com");
});
```

The first argument is the test name.

The second argument is the test function.

------------------------------------------------------------------------

## 5. `test.describe()`

`test.describe()` is used to group related test cases.

Example:

``` typescript
test.describe("Smoke Testcases", () => {

    test("Login test", async ({ page }) => {
        // Test steps
    });

    test("Logout test", async ({ page }) => {
        // Test steps
    });

});
```

### Benefits

-   Organizes test cases
-   Groups related scenarios
-   Allows configuration for a group of tests
-   Makes reports easier to understand

------------------------------------------------------------------------

## 6. Test Annotations

Annotations provide additional instructions to Playwright Test about how
a test should be executed.

Important annotations include:

### `test.only()`

Executes only the selected test.

``` typescript
test.only("Login test", async ({ page }) => {
});
```

Useful during debugging.

**Important:** Do not commit `test.only()` to the main branch because it
can prevent other tests from executing.

------------------------------------------------------------------------

### `test.skip()`

Skips a test.

``` typescript
test.skip("Login test", async ({ page }) => {
});
```

It can also be used conditionally.

``` typescript
test.skip(browserName === "firefox", "Not supported in Firefox");
```

------------------------------------------------------------------------

### `test.fail()`

Marks a test as expected to fail.

``` typescript
test.fail("Known failing test", async ({ page }) => {
});
```

If the test fails as expected, Playwright considers that expected
behavior.

This is useful for known bugs or scenarios that are intentionally
expected to fail.

------------------------------------------------------------------------

### `test.slow()`

Marks a test as slow and increases its timeout.

``` typescript
test.slow();
```

It is useful when a particular test needs more time than the normal
timeout.

You can also provide a reason:

``` typescript
test.slow(true, "Application takes longer to load");
```

------------------------------------------------------------------------

## 7. Parallel Execution

Playwright can execute tests in parallel.

Example:

``` typescript
test.describe.configure({ mode: "parallel" });
```

This configures tests inside the `describe` block to run in parallel.

### Sequential vs Parallel

Sequential:

``` text
Test 1 → Test 2 → Test 3
```

Parallel:

``` text
Test 1 ─┐
Test 2 ─┼─ Execute simultaneously
Test 3 ─┘
```

### Benefits

-   Reduces overall execution time
-   Improves CI/CD execution speed
-   Useful for independent test cases

### Important Consideration

Tests running in parallel should ideally be independent.

If multiple tests modify the same data or depend on the execution order,
parallel execution can cause failures.

------------------------------------------------------------------------

## 8. Test Timeout

A timeout defines how long Playwright waits before considering a test or
operation timed out.

Example:

``` typescript
test.setTimeout(120000);
```

For a slow test:

``` typescript
test.slow();
```

The exact timeout values depend on the Playwright configuration.

### Best Practice

Do not increase timeouts unnecessarily.

First investigate whether the issue is caused by:

-   Incorrect locator
-   Missing wait condition
-   Application performance
-   Network issue
-   Synchronization problem

------------------------------------------------------------------------

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

------------------------------------------------------------------------

## 10. Test Isolation

Playwright Test provides isolation between tests.

Typically, each test gets its own browser context and page.

This helps prevent one test from affecting another.

Example:

``` text
Test 1 → Context 1 → Page 1

Test 2 → Context 2 → Page 2

Test 3 → Context 3 → Page 3
```

This is particularly important when tests run in parallel.

------------------------------------------------------------------------

## 11. Smoke Testing

Smoke testing is a basic level of testing used to verify that the major
functionality of an application is working.

Typical smoke scenarios may include:

-   Application launches
-   Login works
-   Main menu is accessible
-   Important module can be opened
-   Critical workflow works

Smoke tests are usually:

-   High priority
-   Fast to execute
-   Focused on critical functionality

------------------------------------------------------------------------

## 12. Negative Testing

Negative testing verifies how the application behaves when invalid or
unexpected input is provided.

Examples:

-   Invalid username
-   Invalid password
-   Empty username
-   Empty password
-   Invalid data format

Example:

``` typescript
test("Login with invalid credentials", async ({ page }) => {
    // Negative scenario
});
```

------------------------------------------------------------------------

## 13. `page.goto()`

`page.goto()` navigates to a URL.

``` typescript
await page.goto("https://leaftaps.com/opentaps/control/main");
```

It is commonly used as the first step of a browser-based test.

------------------------------------------------------------------------

## 14. `page.locator()`

`page.locator()` creates a locator for an element.

``` typescript
page.locator(".id")
```

The locator can then be used for actions such as:

``` typescript
await page.locator(".id").click();
await page.locator("#username").fill("admin");
```

------------------------------------------------------------------------

## 15. Console Logging

`console.log()` prints information to the terminal.

``` typescript
console.log("Valid credentials entered");
```

It can be useful for debugging and understanding test execution.

However, assertions should be used to actually validate expected
application behavior.

------------------------------------------------------------------------

## 16. Assertions vs Console Logs

A console message does not make a test pass or fail.

Example:

``` typescript
console.log("Login successful");
```

This only prints text.

For validation, use an assertion:

``` typescript
await expect(page).toHaveURL(/dashboard/);
```

Therefore:

**Console log = Information**

**Assertion = Validation**

------------------------------------------------------------------------

## 17. Standard Test Flow

A typical Playwright Test execution flow is:

``` text
Test Definition
      ↓
Fixture Creation
      ↓
Browser/Page Setup
      ↓
Navigate to Application
      ↓
Locate Element
      ↓
Perform Action
      ↓
Validate Result
      ↓
Test Pass/Fail
      ↓
Report Generation
```

------------------------------------------------------------------------

## 18. Industry Best Practices

-   Prefer `import { test } from "@playwright/test"`.
-   Use meaningful test names.
-   Group related tests using `test.describe()`.
-   Avoid `test.only()` in committed code.
-   Use `test.skip()` only when there is a valid reason.
-   Use `test.fail()` for known expected failures.
-   Avoid unnecessary `waitForTimeout()`.
-   Prefer Playwright's auto-waiting and assertions.
-   Keep parallel tests independent.
-   Use Page Object Model for maintainability.
-   Use assertions to validate functionality.
-   Keep smoke tests short and focused.


---

# 19. Reading Test Data from JSON

JSON (JavaScript Object Notation) is commonly used to store structured test data.

Example:

```json
[
    {
        "url": "https://leaftaps.com/opentaps/control/main",
        "username": "Demosalesmanager1",
        "password": "crmsfa"
    }
]
```

### Import JSON Data

With TypeScript configuration supporting JSON modules:

```typescript
import loginData from "../../data/loginData.json";
```

The data can then be accessed using:

```typescript
loginData[0].username
loginData[0].password
loginData[0].url
```

### Typical JSON Data-Driven Flow

```text
JSON File
   ↓
Import JSON
   ↓
Array/Object
   ↓
Read Test Data
   ↓
Execute Test
```

### Advantages of JSON

- Easy to read
- Supports nested objects and arrays
- Useful for structured test data
- Convenient for configuration and test data
- Easy to consume from JavaScript/TypeScript

---

# 20. Reading Test Data from CSV

CSV (Comma-Separated Values) stores data in rows and columns.

Example:

```csv
url,username,password
https://leaftaps.com/opentaps/control/main,Demosalesmanager1,crmsfa
https://leaftaps.com/opentaps/control/main,DemoSalesManager2,crmsfa
```

### Read CSV Using Node.js

First import the file system module:

```typescript
import fs from "fs";
```

Read the CSV file:

```typescript
const csvData = fs.readFileSync("data/logindata.csv", "utf-8");
```

The `utf-8` encoding converts the file bytes into readable characters/text.

### Parse CSV

Using `csv-parse`:

```typescript
import { parse } from "csv-parse/sync";

const records = parse(csvData, {
    columns: true,
    skip_empty_lines: true
});
```

`columns: true` uses the first row as property names.

For example:

```typescript
records[0].username
records[0].password
records[0].url
```

### Typical CSV Data-Driven Flow

```text
CSV File
   ↓
fs.readFileSync()
   ↓
CSV Text
   ↓
parse()
   ↓
Array of Objects
   ↓
for loop
   ↓
Execute Tests
```

### Advantages of CSV

- Easy to maintain tabular data
- Useful for large sets of rows
- Easy to edit using Excel
- Suitable for parameterized testing

---

# 21. Reading Environment Variables from `.env`

A `.env` file is commonly used to store environment-specific configuration and sensitive values that should not be hard-coded in test files.

Example:

```env
BASE_URL=https://leaftaps.com/opentaps/control/main
USERNAME=Demosalesmanager1
PASSWORD=crmsfa
```

### Load `.env` Values

Using the `dotenv` package:

```typescript
import dotenv from "dotenv";

dotenv.config();
```

Read a value:

```typescript
process.env.BASE_URL
process.env.USERNAME
process.env.PASSWORD
```

Example:

```typescript
await page.goto(process.env.BASE_URL!);
```

### Typical `.env` Flow

```text
.env File
   ↓
dotenv.config()
   ↓
process.env
   ↓
Test Code
```

### Why Use `.env`?

- Avoid hard-coding environment-specific values
- Keep credentials/configuration outside test code
- Easily switch between environments
- Useful for local, QA, staging and production configurations

### Important Best Practice

Do not commit real credentials or secrets to Git.

Add `.env` to `.gitignore` when it contains sensitive values.

---

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

# 23. Data-Driven Testing

Data-driven testing means executing the same test logic with multiple sets of input data.

Example:

```text
Test Logic
    +
Data Set 1
    +
Data Set 2
    +
Data Set 3
```

With Playwright, data can come from:

- JSON
- CSV
- `.env`
- API responses
- Databases
- Other external files

### Example

```typescript
for (let i = 0; i < records.length; i++) {
    test(`Create Lead ${i + 1}`, async ({ page }) => {
        // Use records[i] as test data
    });
}
```

This dynamically creates tests based on the available data.

---

# 24. JSON, CSV and `.env` in Page Object Model

Data files can be used together with Page Object Model.

The test file is responsible for:

- Reading test data
- Creating page objects
- Passing data to page object methods

The Page Object is responsible for:

- Locators
- Page interactions
- Application-specific actions

Example:

```typescript
await loginPage.login(
    records[i].username,
    records[i].password
);
```

This keeps test data and page interaction logic separated.

---

# 25. Recommended Industry Structure

A simple Playwright project can organize these files as:

```text
Project
│
├── data
│   ├── loginData.json
│   └── logindata.csv
│
├── pages
│   ├── LoginPage.ts
│   ├── HomePage.ts
│   └── CreateLeadPage.ts
│
├── tests
│   └── testcases
│
├── .env
├── playwright.config.ts
└── package.json
```

### Separation of Responsibility

```text
Test Data
   ↓
JSON / CSV / .env

Test Logic
   ↓
.spec.ts

Page Interaction
   ↓
Page Object Model

Execution
   ↓
Playwright Test
```
