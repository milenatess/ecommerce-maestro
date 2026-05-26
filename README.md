# README.md

## Overview

This project contains automated mobile tests developed with Maestro for the Sauce Labs sample application.

The goal of this challenge was to automate critical user flows while maintaining readability, scalability, and cross-platform compatibility between Android and iOS.

---

## Project Setup

### Prerequisites

Before running the project, ensure the following tools are installed:

- Maestro
- Android Studio
- Android Emulator

### Installation Steps

1. Install Maestro following the official documentation:

https://maestro.mobile.dev

2. Install and configure Android Studio:

https://developer.android.com/studio

3. Start an emulator.

4. Install the provided APK into the emulator.

5. Open the project repository in Maestro Studio or your preferred IDE.

---

## Running the Tests

Tests can be executed directly through Maestro.

To run a test:

1. Open the desired flow file inside Maestro
2. Select the platform/environment variables (example: `android`)
3. Run the flow directly from Maestro

This approach was preferred during the challenge because it allows easier visualization and debugging of individual flows while developing the automation suite.

---

## Project Structure

```text
C:\Repo\ecommerce-maestro\
└── Maestro\
|   ├── auth-flows\
|   ├── navigation-flows\
└── docs\
└── README.md
```

### Folder Description

- `auth-flows/` → Authentication and login-related test flows.
- `navigation-flows/` → Navigation, catalog, cart, and checkout-related flows.
- `docs/` → Auxiliates on visualizing acceptance criteria and writing the test cases.
---

## Automation Approach

### Exploratory Testing Before Automation

Before implementing automation, the application was explored manually to better understand:

- Main user journeys
- Navigation behavior
- UI structure
- Potential edge cases
- Priority areas for automation

This exploratory phase also helped identify usability issues, missing identifiers, and inconsistencies within the app.

---

### Documentation-Driven Approach

A `docs` folder was initially created to organize:

- Tasks
- Acceptance criteria
- Candidate test scenarios
- Bugs and improvements identified during exploratory testing

This made it easier to visualize the automation scope and prioritize the most relevant flows.

---

### Learning & Initial Maestro Implementation

The first automated scenario implemented was the successful login flow.

At the beginning of the challenge, AI assistance was used to understand the basic structure and syntax patterns used by Maestro. After understanding the flow structure and how to inspect UI element identifiers, the remaining test implementation was developed independently based on the desired user flows.

The login automation flow included actions such as:

- Opening the side menu
- Navigating to the login screen
- Entering username and password
- Validating successful authentication

This initial implementation helped establish the automation pattern used throughout the remaining test suite.

---

## Cross-Platform Strategy (Android & iOS)

During my initial research about Maestro and mobile automation best practices, I identified that Android and iOS use different locator strategies and accessibility identifiers.

To support cross-platform scalability, environment variables were created to centralize and separate platform-specific locators.

This approach allows:

- Reuse of the same test logic across platforms
- Easier maintenance
- Cleaner and more scalable test files
- Separation of configuration from test implementation

Different variables were created for Android and iOS. However, due to time constraints and prioritization decisions, not all iOS variables were fully implemented, since the main execution focus of the challenge was Android. Additionally, iOS IDs aren't real.

Tests were executed only on Android due to the absence of a macOS environment for iOS execution.

---

## Test Design Decisions & Trade-offs

### Explicit Test Naming

Test files were created with descriptive names to simplify future maintenance and debugging.

Examples:

```text
successful-login
invalid-login-locked-user
complete-purchase-logged-in
```

---

### Readability Improvements Using Tags

To improve readability and make the automation flows easier to understand and maintain, tags/comments were added throughout the test files to separate logical sections of the user journey.

Example:

```yaml
#Login
- tapOn: ${MENU_BUTTON}
- tapOn: ${MENU_LOGIN}
- tapOn:
    id: ${USERNAME_FIELD}
- inputText: "bod@example.com"
- tapOn:
    id: ${PASSWORD_FIELD}
- inputText: "10203040"
- tapOn: ${LOGIN_BUTTON}

#Product selection
- assertVisible: ${PRODUCTS_TITLE}
- assertVisible: "Sauce Labs Backpack"
- tapOn: ${PRODUCT_IMAGE}

#Add item to cart
- assertVisible: "Sauce Labs Backpack"
- tapOn: ${ADD_TO_CART}
- tapOn: ${VIEW_CART}

- assertVisible: ${ITEM_QUANTITY_1}
- tapOn: "Proceed To Checkout"
```

This structure helps future debugging and makes the flows easier to read for both technical and non-technical reviewers.

---

### Reusability Considerations

During implementation, it became clear that several tests shared common initial steps, especially authentication-related flows.

Research was conducted on how to reuse common steps in Maestro to reduce duplication and improve maintainability. Although this was not implemented due to time constraints, it was identified as an important future improvement and a recommended best practice for keeping tests smaller and easier to maintain.

---

## Automated Test Coverage

### Login & Authentication Flows

These scenarios cover core authentication behaviors and different user outcomes.

Implemented scenarios:

- Successful login with valid credentials redirects to the product catalog
- Invalid login with locked-out user credentials
- Invalid login with empty credentials
- Successful logout

Possible future scenarios:

- Invalid login with valid username and incorrect password
- Cancel logout flow

---

### Navigation & UI Assertions

These scenarios validate navigation behavior and important UI elements.

Implemented scenarios:

- Product catalog loads with at least one visible product after login
- Product selection redirects to detailed product screen
- Product screen displays product name, price, and description
- Side menu displays navigation options
- Complete purchase while not logged in
- Complete purchase while already logged in
- Add multiple products to the cart
- Submitting empty address information shows validation feedback

Possible future scenarios:

- Submitting empty payment information shows validation feedback
- Social media buttons open social media links in a new window
- Select a different product colour successfully displays the chosen colour
- Filter options successfully work
- Close the app without completing the purchase maintains the item in the cart
- Add different products to the cart
- Remove an item from the cart
- Close side menu successfully works

---

## Bugs & Improvements Identified During Testing

During exploratory and automation testing, the following issues were identified in the application:

### Product Images

All product images share the same identifier (`Product Image`) and redirect to the same product detail screen (Sauce Labs Backpack), regardless of the selected product.

---

### Incorrect Product Strings

Some product names and descriptions display method names instead of user-facing text values.

Example:

```text
carry.allTheThings()
```

---

### Missing IDs on Payment Page

The payment page does not expose stable or meaningful element identifiers.

Some identifiers appear to contain dynamically populated information instead of fixed IDs, which makes automation more difficult and less stable.

---

### Incomplete Validation Message

The validation feedback for the `Country` field on the shipping page displays an incomplete message.

Expected:

```text
Please provide your country
```

Actual:

```text
Please provide your
```

---

## Possible Improvements

Possible future enhancements include:

- Implement reusable authentication/setup flows
- Expand negative test coverage
- Increase checkout and cart validation coverage
- Improve selector strategy once the app exposes more stable identifiers
- Add iOS execution and validation