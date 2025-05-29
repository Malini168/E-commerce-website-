### Step-by-Step Documentation for the Logout Page

Below is the aligned and concise guide for implementing the logout.php page.

---

#### Step 1: Create the logout.php File
1. Inside the pages folder, create a file named logout.php.

---

#### Step 2: Add PHP Logic to Destroy the Session
Add the following PHP code to handle the logout functionality:

php
<?php
session_start(); // Start the session

// Destroy the session
session_unset(); // Unset all session variables
session_destroy(); // Destroy the session

// Redirect to the login page
header('Location: login.php');
exit();
?>


*Explanation*:
- session_start(): Initializes the session.
- session_unset(): Frees all session variables.
- session_destroy(): Completely terminates the session.
- header('Location: login.php'): Redirects the user to the login page after the session ends.

---

#### Step 3: Add a Logout Link to Other Pages
To ensure users can log out from anywhere, add a logout link to the navigation bar on user-facing pages like index.php:

html
<li><a href="pages/logout.php">Logout</a></li>


---

#### Step 4: Test the Logout Page
1. Log in as a user on your site.
2. Navigate to http://localhost/ecommerce/pages/logout.php.
3. Confirm the following:
   - The session is destroyed (e.g., you are logged out).
   - You are redirected to the login page.
   - Attempting to access a protected page (e.g., index.php) after logging out redirects you to login.php if session checks are implemented.

---

### Next Steps
Now that the logout functionality is implemented, the core user management system (registration, login, logout) is complete. Next, we can move to:
1. *Home Page (index.php)* for displaying products.
