# Task 2 
## Navigation & UI Assertions

Validate the product catalog and navigation flows. Focus on asserting the right elements are present and the navigation stack behaves correctly, not just on tapping through screens.

### Acceptance criteria:
- Product catalog loads with at least one visible product after login
- Tapping a product navigates to a detail screen with a name, price, and
description visible
- Back navigation returns the user to the catalog with state preserved
- The side menu opens, shows expected navigation options, and closes correctly
- Complete order and checkout flows
- UI assertions use element identifiers or text, not coordinates (?)

### Test scenarios:
- Product catalog loads with at least one visible product after login
- Product selection redirects to detailed product screen
- Product screen displays name, price and description
- Side menu selection displays the navigation options
- Complete purchase not logged in
- Complete purchase already logged in
- Add multiple products to the cart
- Submitting empty address information shows validation feedback

### Other possible scenarios:
- Submitting empty payment information shows validation feedback
- Social media buttons open social media links in a new window
- Select a different product colour successfully displays the chosen colour
- Filter options successfully work
- Close the app without completing the purchase maintains the item in the cart
- Add different products to the cart
- Remove an item from the cart
- Close side menu successfully works




