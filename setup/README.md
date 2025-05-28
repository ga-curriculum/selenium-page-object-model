<h1>
  <span class="headline">Selenium: Page Object Model</span>
  <span class="subhead">Setup</span>
</h1>

## Setup

### 1: Create Your Project Folder

In this lesson, you’ll start fresh with a new project just for testing waits, alerts and dynamic uis.

Open a terminal and run:

```bash
mkdir selenium-page-object-model
cd selenium-page-object-model
```

### 2: Set Up a Virtual Environment

Create and activate a virtual environment inside this new folder:

```bash
python -m venv venv
```

Activate it:

**macOS/Linux:**

```bash
source venv/bin/activate
```

**Windows:**

```bash
venv\Scripts\activate
```

You should now see (venv) at the start of your terminal prompt.

### 3: Install Selenium

With the virtual environment active, install Selenium using pip:

```bash
pip install selenium
```

Check that it installed correctly:

```bash
pip show selenium
```

> ✅ If Selenium installed correctly, you’ll see output with its version and location.

### 4: Create Your Project Files

Inside your `selenium-page-object-model` folder, create the following files:

- `sign_in.html`
- `checkout_page.html`

## 5. Add your starter code

For this lesson we will be using local html files as mock sites for testing.

### Add the following starter code to `sign_in.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Sign-In Page for Selenium Test</title>
    <style>
      body {
        font-family: sans-serif;
        padding: 2rem;
      }
      .signin-box {
        max-width: 300px;
        margin: auto;
      }
      input,
      button {
        display: block;
        width: 100%;
        padding: 0.5rem;
        margin-top: 1rem;
      }
    </style>
  </head>
  <body>
    <div class="signin-box">
      <h2>Sign In</h2>
      <form id="signin-form">
        <input type="text" id="user" placeholder="Username" />
        <input type="password" id="pass" placeholder="Password" />
        <button type="submit" id="signin">Sign In</button>
      </form>
      <p id="message" style="color: green; display: none;">
        Sign-in submitted!
      </p>
    </div>

    <script>
      document
        .getElementById('signin-form')
        .addEventListener('submit', function (e) {
          e.preventDefault();
          document.getElementById('message').style.display = 'block';
        });
    </script>
  </body>
</html>
```

### Add the following starter code to `checkout_page.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Checkout Page</title>
    <style>
      body {
        font-family: sans-serif;
        background-color: #f4f4f4;
        padding: 2rem;
      }
      .checkout-box {
        background: #fff;
        border: 1px solid #ccc;
        border-radius: 6px;
        max-width: 500px;
        margin: auto;
        padding: 1.5rem;
      }
      label {
        display: block;
        margin: 1rem 0 0.3rem;
      }
      input,
      select,
      button {
        width: 100%;
        padding: 0.6rem;
        margin-bottom: 1rem;
        font-size: 1rem;
      }
      button {
        background-color: #28a745;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
      }
      button:hover {
        background-color: #218838;
      }
    </style>
  </head>
  <body>
    <div class="checkout-box">
      <h2>Checkout</h2>
      <form id="checkout-form">
        <label for="shipping-address">Shipping Address</label>
        <input
          id="shipping-address"
          type="text"
          placeholder="Enter your address"
        />

        <label for="payment-method">Payment Method</label>
        <select id="payment-method">
          <option>Select payment</option>
          <option>Visa</option>
          <option>MasterCard</option>
          <option>UnionPay</option>
        </select>

        <button id="confirm-order" type="button">Confirm Order</button>
      </form>
    </div>

    <script>
      document
        .getElementById('confirm-order')
        .addEventListener('click', function () {
          alert('Order confirmed!');
        });
    </script>
  </body>
</html>
```

## Setup Complete!

Once everything is set up, you should be able to:

- Open both `html` files in Chrome with no errors.

You're ready to move on!
