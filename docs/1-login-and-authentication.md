# Task 1 
## Login & Authentication Flows

Cover the core authentication scenarios a real user would encounter. The app has
multiple user types with different behaviors, and your tests should reflect that.

### Acceptance criteria:
- Successful login with standard_user navigates to the product catalog
- Locked out user sees an appropriate error message and cannot proceed
- Submitting empty credentials shows validation feedback
- After a successful login, the user can log out and the session is cleared
- Tests run without modification on both Android and iOS

### Test scenarios:
- Successful login with user credentials redirects to products catalog
- Invalid login with locked-out user credentials
- Invalid login with empty credentials
- Successful log out

### Other possible scenarios:
- Invalid login with correct username but incorrect password
- Cancel log out