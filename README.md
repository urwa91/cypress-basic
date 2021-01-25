# Cypress

### Installation

1. Install Node Js

   -  https://nodejs.org/en/download/

2. Install npm

   ```bash
   npm install -g npm
   ```

3. Confirm installation

   ```bash
   node -v
   ```

   ```bash
   npm -v
   ```

4. Create a project directory

5. Open project folder in terminal. Run these command to create a cypress project

   ```bash
   npm init -y
   ```

   ```bash
   npm install --save-dev cypress
   ```

6. To Open Cypress interface

   ```bash
   npx cypress open
   ```

### Resources

- Cypress Docs: https://docs.cypress.io/guides/overview/why-cypress.html

### Learning Material

* Test Automation University: https://testautomationu.applitools.com/cypress-tutorial/chapter2.html

### Recommended Tool

- Visual Code: https://code.visualstudio.com/download

### Sample Code

A script for the simple test, which opens a browser, goes to daraz.pk and search for football in a search field.

```javascript
describe('Validate the search result of daraz.pk', () => {
    it('User can search for products', () => {
        cy.visit('https://www.daraz.pk');
        
        cy.get('h3')
            .should('contain','Flash Sale');
        
        cy.get('input[id=q]')
            .type('football');

        cy.get('button[class=search-box__button--1oH7]')
            .click();

        cy.get('[id=J_breadcrumb_list]')
            .should('contain','Search Results');
    });
})
```

### Folder Structure

- cypress\integration (For Test Files)

### File Format

- In cypress\integration folder, save file as: first_test.spec.js

### Command Line

- To run cypress

  ```bash
  npx cypress open
  ```

* To run cypress headless

  ```bash
  npx cypress run
  ```

* To run one spec file

  ```bash
  npx cypress run --spec cypress/integration/file_name.spec.js
  ```

### Test Script

* In order to enable TypeScript support in Cypress, add the following to the top of the main file in the test project.

  ```
  /// <reference types="Cypress" />
  ```

### Example

#### Scenario: 

To test the Sign In functionality of the website by entering valid email and valid password.

#### Test Case: 

**TCID101 | Test Case 1| Happy Path Sign In**
**Title:** Enter correct email address and password.
**Inputs:** url: https://react-redux.realworld.io/e | email: john91@gmail.com | password: qwerty123
**Action:** Enter the given URL in browser. At home page click on "Sign In" button at top. When "Sign In" page is open enter valid email and valid password. Click on "Sign In" Button. 
**Expected Output:** Go to the dashboard page.
**Latest Result:** Pass
**Need to be Automated:** Yes

#### Test Script:

```javascript
describe('Verify the SignIn functionality', () => {
    it('User should SignIn to the dashboard with valid email and valid password', () => {
        cy.visit('https://react-redux.realworld.io/')

        cy.get('h1')
            .invoke('text')
            .should('equal', 'conduit');

        cy.contains('Sign in')
            .click();

        cy.get('h1')
            .invoke('text')
            .should('equal', 'Sign In');

        cy.get('input')
            .eq(0)
            .type('john91@gmail.com');

        cy.get('input')
            .eq(1)
            .type('qwerty123');

        cy.get('[type=submit]')
            .click();

        cy.wait(2000);
        
        cy.get('p')
            .should('contain','Popular Tags');
    });
});
```



------

## Cypress with Cucumber

### Installation

1. Install Cypress (Follow the previous mentioned steps)

2. Install Cucumber Preprocessor

   ```bash
   npm install --save-dev cypress-cucumber-preprocessor
   ```

3. In cypress/plugins/index.js

   ```javascript
   const cucumber = require('cypress-cucumber-preprocessor').default
   
   module.exports = (on, config) => {
     on('file:preprocessor', cucumber())
   }
   ```

4. In cypress.json

   ```json
   {
     "testFiles": "**/*.feature"
   }
   ```

5. In package.json:

   ```json
   "cypress-cucumber-preprocessor": {
     "nonGlobalStepDefinitions": true
   }
   ```

### Resources

- Cypress with Cucumber: https://www.npmjs.com/package/cypress-cucumber-preprocessor 

### Example (Gherkin)

```gherkin
Feature: Verify that user can sign in
    The user should be able to sign in to the application when the email and the password are correct.

    Scenario: Entering valid sig in credentials
        Given I am on the Home page
        When I click on Sign In
        Then the Sign In page opens
        When I enter valid credentials
        And I click on Sign In button
        Then the Dashboard page opens
```



```javascript
/// <reference types = "cypress" />

import { Given, When, Then } from 'cypress-cucumber-preprocessor/steps';

Given(`I am on the Home page`, () => {
    cy.visit('https://react-redux.realworld.io/');

    cy.get('h1')
        .invoke('text')
        .should('equal', 'conduit');
});

When(`I click on Sign In`, () => {
    cy.contains('Sign in')
        .click();
});

Then(`the Sign In page opens`, () => {
    cy.get('h1')
        .invoke('text')
        .should('equal', 'Sign In');

});

When(`I enter valid credentials`, () => {
    cy.get('input')
        .eq(0)
        .type('john91@gmail.com');

    cy.get('input')
        .eq(1)
        .type('qwerty123');
});

And(`I click on Sign In button`, () => {
    cy.get('[type=submit]')
        .click();
});

Then(`the Dashboard page opens`, () => {
    cy.wait(2000);

    cy.get('p')
        .should('contain', 'Popular Tags');
});
```

> Note: Do not forget to add '/steps' at the end of 'cypress-cucumber-preprocessor/steps'
