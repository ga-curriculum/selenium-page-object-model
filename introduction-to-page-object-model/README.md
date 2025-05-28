<h1>
  <span class="headline">Selenium: Page Object Model</span>
  <span class="subhead">Introduction to Page Object Model</span>
</h1>

**Learning Objective:** Define the Page Object Model and explain its role in building scalable, maintainable Selenium test suites.

## The Page Object Model

As your test suites grow more complex, organizing and maintaining code can quickly become a challenge. This is where the _Page Object Model_ (POM) steps in as a helpful design pattern for Selenium automation. With POM, each page of your web application is represented by a dedicated Python class—these are your _Page Objects_. Each _Page Object_ contains all the routines and information your tests need to interact with that page.

> 📚 A _design pattern_ is a reusable approach to solving a common programming problem.

By using POM, you keep all the details about _how_ to interact with a page (such as how to locate buttons or fields) inside that page's class, rather than scattering them across every test. This separation means that when a page changes—for instance, a button moves or its code changes—you only need to update the locator in one place, rather than in every test script referencing it.

> 💡 Think of the Page Object Model as a personal guidebook for your application’s pages. Rather than remembering the detailed layout of each page every time, you refer to your guidebook, which always has the latest information.

| **Benefit**         | **What It Means**                                                                        | **Why It Matters**                                                                     |
| ------------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Scalability**     | Encapsulates logic and locators for each page in one place.                              | Reuse page classes across new tests as your application grows, avoiding repeated code. |
| **Maintainability** | Update one locator in a page class and all dependent tests are automatically fixed.      | Saves time and reduces errors when the UI changes.                                     |
| **Readability**     | Test logic focuses on _what_ is being tested rather than _how_ each interaction happens. | Improves onboarding and collaboration—tests read like a checklist of user actions.     |
| **Reusability**     | Encapsulates routines like login or checkout in reusable methods.                        | Write less code, avoid duplication, and increase coverage quickly.                     |

#### Example:

Without POM, you would write:

```python
driver.find_element(By.ID, 'username').send_keys('student1')
driver.find_element(By.ID, 'password').send_keys('abc123')
driver.find_element(By.ID, 'login-button').click()
```

With POM, that logic becomes:

```python
login_page = LoginPage(driver)
login_page.login('student1', 'abc123')
```

Now, if the login button changes, you update `LoginPage` only.

## Structure of a typical Page Object

A Page Object typically features:

- A constructor (using `__init__`) to pass in your Selenium webdriver.
- Locator variables for key elements on the page.
- Methods to interact with these elements (filling fields, clicking buttons).
- Optional helper methods to return information for assertions.

Below is a simplified example of what a `LoginPage` class might look like in Python.

```python
from selenium.webdriver.common.by import By

class LoginPage:
    USERNAME_INPUT = (By.ID, 'username')
    PASSWORD_INPUT = (By.ID, 'password')
    LOGIN_BUTTON = (By.ID, 'login-button')

    def __init__(self, driver):
        self.driver = driver

    def enter_username(self, username):
        self.driver.find_element(*self.USERNAME_INPUT).send_keys(username)

    def enter_password(self, password):
        self.driver.find_element(*self.PASSWORD_INPUT).send_keys(password)

    def click_login(self):
        self.driver.find_element(*self.LOGIN_BUTTON).click()

    def login(self, username, password):
        self.enter_username(username)
        self.enter_password(password)
        self.click_login()
```

**Notice how all the details for interacting with the login page live in this class, ready to be _reused_.**

## Separation of concerns

One of POM’s main strengths is the _separation of concerns_: each class has a clear, limited responsibility:

- **Locators:** Placed as variables at the top of the class, these identify specific elements.
- **Actions:** Methods that interact with those elements.
- **Assertions:** Typically exist in your tests but can rely on helper methods from your Page Object class.

> 💡 Analogy: Think of a television remote control. The remote (Page Object) offers labeled buttons (methods) for changing channels or volume—no need to know how the circuits inside the TV work.

## Real-world example: Comparing a traditional Selenium test to POM structure

Let’s compare two approaches to the same task: logging in.

### Traditional Selenium test (without POM)

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get('https://example.com/login')

driver.find_element(By.ID, 'username').send_keys('student1')
driver.find_element(By.ID, 'password').send_keys('abc123')
driver.find_element(By.ID, 'login-button').click()

# ...further test logic...

driver.quit()
```

Each time you need to log in, you rewrite **these same few lines.** If locators change, every test must change.

### The same logic with Page Object Model

```python
from selenium import webdriver
from login_page import LoginPage

driver = webdriver.Chrome()
driver.get('https://example.com/login')

login_page = LoginPage(driver)
login_page.login('student1', 'abc123')

# ...further test logic...

driver.quit()
```

With POM, login logic is encapsulated. Any change needed—such as a new login button ID—requires editing `LoginPage` only.

## Knowledge check:

❓ Which of the following is a primary benefit of adopting the Page Object Model in Selenium tests?

- A) Tests will always run faster.
- B) Locators and actions are grouped, making test maintenance easier.
- C) POM increases the need to update multiple files when a UI changes.
- D) POM eliminates the need to write any assertions in tests.

❓ In the Page Object Model pattern, which statement best describes the Page Object class?

- A) It combines test logic and web page structure in one place.
- B) It contains locators and methods for interacting with a specific page, separate from test steps.
- C) It is only used to write assertions for tests.
- D) It stores data but does not interact with Selenium.
