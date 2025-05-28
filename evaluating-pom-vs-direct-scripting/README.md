<h1>
  <span class="headline">Selenium: Page Object Model</span>
  <span class="subhead">Evaluating POM vs Direct Scripting</span>
</h1>

**Learning Objective:** Compare the Page Object Model (POM) with direct scripting to understand trade-offs in readability, reuse, and long-term maintenance.

## What’s the difference?

**Direct scripting** means writing all your selectors and actions directly in the test file.  
**POM** (Page Object Model) organizes this logic into reusable classes for each page.

### Example:

**Direct script:**

```python
driver.find_element(By.ID, "username").send_keys("user1")
driver.find_element(By.ID, "password").send_keys("mypassword")
driver.find_element(By.ID, "login-button").click()
```

**POM:**

```python
login_page = LoginPage(driver)
login_page.login("user1", "mypassword")
```

With POM, your test focuses on _what_ the user does, not _how_ to click each button.

## Why POM scales better

As your test suite grows, these differences matter more:

| Feature                    | Direct Scripting                   | Page Object Model (POM)                |
| -------------------------- | ---------------------------------- | -------------------------------------- |
| **Readability**            | Mixed logic/selectors; verbose     | Test logic reads like user workflow    |
| **Maintainability**        | Duplicate code, many update points | One point of update per page/component |
| **Reuse of actions**       | Limited, often copied              | Highly reusable methods                |
| **Scalability**            | Painful as codebase grows          | Designed to handle growth              |
| **Adapting to UI changes** | Tedious, error-prone               | Quick, low-risk, centralized updates   |

## Code Comparison: Updating a Selector

If the login button ID changes:

**Direct script:**

```python
# Update everywhere:
driver.find_element(By.ID, "login-button").click()
```

**POM:**

```python
# Update once in LoginPage class:
LOGIN_BUTTON = (By.ID, "sign-in")
```

All tests using that page now work without any other changes.

## When to use each approach

- Use **direct scripting** only for short, one-time test scripts.
- Use **POM** when:
  - Your site has multiple pages or flows
  - You’re working with a team
  - You want to maintain tests over time

> 🏗️ POM turns your tests into reusable building blocks that can grow with your application.

## Final Takeaway

Direct scripting is fast to start, but POM is built to last. If you’re writing more than a few tests, POM helps you:

- Keep code readable and consistent
- Update tests faster when the UI changes
- Share work easily with others

> 📘 Good tests are like good documentation—they should tell a clear story and be easy to keep up to date.

## Knowledge check

❓ Which is the main advantage of updating a selector in the Page Object Model, compared to direct scripting?

- A) You always need to rewrite fewer lines of code
- B) You only need to update the selector in one place, and all related tests automatically benefit
- C) It makes the Selenium browser run faster
- D) You never have to update your tests again

❓ In which situation might direct scripting make sense even if you are familiar with POM?

- A) For a single-use, quick, throwaway test you do not plan to reuse or maintain
- B) For all large, critical test suites
- C) When your selectors never change
- D) Whenever testing page navigation
