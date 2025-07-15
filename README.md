# 🚀 Way2Automation Cypress Automation Test Suite

This project automates key user flows on [Way2Automation](https://www.way2automation.com/demo.html#) using **Cypress v9**, **Mocha**, and **Node v16.14**. It simulates real-world testing scenarios including navigating dynamic UI elements, form submission, course exploration, and verifying payment interactions.

---

## 📌 What This Test Covers

| Step        | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| Step 3–4    | Navigate to **Dynamic Elements** and click on the **Submit Button Clicked** card |
| Step 5      | Complete the dummy registration form using a generated email from `getnada.com` |
| Step 6–7    | Scroll to **"30+ Courses video library FREE ACCESS"** on the Membership page |
| Step 14–17  | Select **"Pay in USD"**, verify **$29** price, click **Enroll in Course**, and assert it changes to **"Processing..."** |

---

## ⚙️ Tech Stack

- ✅ Cypress v9
- ✅ Mocha (default test runner)
- ✅ Node.js v16.14
- ✅ getnada.com (for disposable test email)

---

## 🛠 Installation & Setup

### 1. Clone the repo

```bash
git clone https://bitbucket.org/your-username/way2automation-tests.git
cd way2automation-tests
```

### 2. Install dependencies

```bash
npm install
```

### 3. Run tests (with Cypress GUI)

```bash
npx cypress open
```

### 4. Run tests (in headless mode)

```bash
npx cypress run
```

---

## 🧪 Tests Summary (template_spec.js)

```javascript
Cypress.on('uncaught:exception', () => false); // Suppress jQuery errors

describe('template spec', () => {
  const baseUrl = 'https://www.way2automation.com/demo.html#';

  it('Step 3–4: Visit Submit Button Clicked URL', () => {
    cy.visit(baseUrl);
    cy.contains('Dynamic Elements').scrollIntoView();
    cy.contains('h2', 'Submit Button Clicked').should('be.visible').click();
  });

  it('Step 5: Completes the form with dummy data', () => {
    cy.visit('https://www.way2automation.com/way2auto_jquery/index.php');
    cy.get('input[name="name"]').type('Test User');
    cy.get('input[name="phone"]').type('09171234567');
    const email = `user_${Date.now()}@getnada.com`;
    cy.get('input[name="email"]').type(email);
    cy.get('select[name="country"]').select('Philippines');
    cy.get('input[name="city"]').type('Manila');
    cy.get('input[name="username"]:visible').type('testuser123');
    cy.get('input[name="password"]:visible').type('SecurePass123');
    cy.get('input[type="submit"]:visible').click();
  });

  it('Step 6–7: Scrolls to course section', () => {
    cy.visit('https://www.way2automation.com/lifetime-membership-club/');
    cy.contains('30+ Courses video library FREE ACCESS', { timeout: 10000 })
      .scrollIntoView()
      .should('be.visible');
  });

  it('Step 14–17: Payment and enrollment process', () => {
    cy.visit('https://www.selenium-tutorial.com/p/automation-architect-in-selenium-7-live-projects/');
    cy.contains('Get started now!', { timeout: 10000 }).scrollIntoView().should('be.visible');
    cy.get('input[type="radio"][value="4632690"]').should('exist').check({ force: true });
    cy.contains('$29').should('be.visible');
    cy.get('#enroll-button').should('be.visible').click();
    cy.get('#enroll-button', { timeout: 10000 }).should('contain.text', 'Processing...');
  });
});
```

---

## 📁 Folder Structure

```
project-root/
├── cypress/
│   └── integration/
│       └── template_spec.js
├── cypress.json
├── package.json
└── README.md
```

---

## 💡 Tips

- All tests use proper waits and `should()` assertions to ensure elements are interactable.
- Dynamic email generation ensures repeatable test runs.
- Suppressed non-critical jQuery errors using:
  ```js
  Cypress.on('uncaught:exception', () => false);
  ```

---

## 🧑‍💻 Author

**Jheniel Sala**  
Software QA Engineer | Test Automation | Cypress | Selenium | API Testing  
📫 Email: jhenielsala@email.com  
🌐 LinkedIn: [https://www.linkedin.com/in/jhenielsala/]

---

## 📜 License

This project is for demonstration and learning purposes.  
No affiliation with Way2Automation or Selenium Tutorial.
