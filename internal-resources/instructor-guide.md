<h1>
  <span class="headline">Selenium: Page Object Model</span>
  <span class="subhead">Instructor Guide</span>
</h1>

## Introduction to Page Object Model

**Microlesson delivery notes:**

- Use analogies (guidebook or remote control) to make abstract concepts more concrete for all learners.
- Highlight before/after differences visually—encourage learners to compare lines of code, not just read explanations.
- During the activity, check in on pairs or individuals:
  - Ask about their initial impressions of the “old” vs “new” test code.
  - Emphasize the maintainability and reusability gained by adopting POM.
  - Invite shared strategies for updating page objects when UI elements change.
- For remote delivery: Encourage learners to use chat or shared documents for code sharing and feedback.
- Remind learners (especially those from diverse backgrounds) that POM is a globally relevant best practice and is not specific to any one industry or region.

**Knowledge check answers:**

1. B) Locators and actions are grouped, making test maintenance easier.
2. B) It contains locators and methods for interacting with a specific page, separate from test steps.

---

## Refactoring Tests with Page Objects

### Delivery notes:

- Encourage learners to share their procedural and refactored tests so peers can see diverse solutions and code structures.
- Use real-world analogies (like updating recipes or using a toolbox) to make the benefits of the Page Object Model more memorable and globally relatable.
- Highlight the code before and after the refactor — either using a split-screen format or code comparison diagram.
- For group delivery, facilitate a brief code walk-through, inviting learners to point out what changed and why this matters for maintainability.
- When teaching remotely, prompt learners to share their solution files in chat or upload them to a shared workspace.
- Emphasize that organizing test logic via Page Objects is not industry-specific or culture-dependent and is regarded as a global best practice.

### Suggested activity solution

**login_page.py**

```python
from selenium.webdriver.common.by import By

class SignInPage:
    USERNAME_INPUT = (By.ID, "user")
    PASSWORD_INPUT = (By.ID, "pass")
    SIGNIN_BUTTON = (By.ID, "signin")

    def __init__(self, driver):
        self.driver = driver

    def enter_username(self, username):
        self.driver.find_element(*self.USERNAME_INPUT).send_keys(username)

    def enter_password(self, password):
        self.driver.find_element(*self.PASSWORD_INPUT).send_keys(password)

    def click_signin(self):
        self.driver.find_element(*self.SIGNIN_BUTTON).click()

    def sign_in(self, username, password):
        self.enter_username(username)
        self.enter_password(password)
        self.click_signin()

```

**login_test_refactored.py**

```python
from selenium import webdriver
from sign_in_page import SignInPage

driver = webdriver.Chrome()
driver.get("https://demo-app.com/login")

sign_in_page = SignInPage(driver)
sign_in_page.sign_in("beginner123", "password")
# Continue your test here
driver.quit()
```

---

## Implementing Reusable Page Methods

### Delivery notes

- Begin by referencing the previous hands-on refactoring activity to show continuity in organizing test logic.
- Use the “road sign” or “recipe” analogy to explain the value of method naming and abstraction. Encourage learners from various backgrounds to share their own real-world processes where naming conventions or grouped actions matter.
- If teaching remotely, suggest learners use chat or a shared, collaborative workspace to post their exercise files and peer feedback.
- Have learners identify and discuss the most challenging parts of encapsulating page flows, and why certain naming choices were made for clarity and maintainability.
- Remind the group that test automation is a globally relevant practice and that naming methods for clarity is valued no matter where teams work.
- Reinforce that handling waits inside Page Objects creates robust, non-flaky tests for everyone—not just the original author.

### Knowledge check answers

1. B) All tests benefit from more reliable actions without repeated code.
2. B) When the method causes navigation to a different page.

---

## Evaluating POM vs Direct Scripting

### Delivery notes

- Present the code comparisons as a visual narrative—encourage learners to “read” both direct scripting and POM samples and discuss which is more readily understood without background knowledge.
- Remind instructors and learners to define terms like _selector_, _locator_, or _page object_ as needed for clarity, as many students may come from varied backgrounds.
- During the activity, encourage active sharing: learners should present both their code and summary to promote reflection and deeper discussion on maintainability and scalability.
- If remote, use a shared online document or collaborative platform for code sharing and feedback.
- Emphasize that the POM approach is a globally recognized best practice, not tied to any particular language, tool, or region.
- Guide the group through the knowledge check to reinforce the lesson’s key takeaways.

**Knowledge check answers:**

1. B) You only need to update the selector in one place, and all related tests automatically benefit
2. A) For a single-use, quick, throwaway test you do not plan to reuse or maintain

---

🏗️ **Under Construction**

We are constantly working to improve our resources for instructors and students.

**Have something to contribute to this Instructor Guide?** [Let us know](https://pages.git.generalassemb.ly/modular-curriculum-all-courses/universal-resources-internal/module-feedback.html).
