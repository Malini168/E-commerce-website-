### *Project Overview*
This e-commerce platform is designed for *Customers* and *Admins* to handle shopping and management functionalities. Below are concise, sectioned explanations for each part of the project.

---

### *1. User Section*
This section explains how users interact with the website.

#### *1.1. How can users register on the platform?*
- *Answer*: Users can create an account on the register.php page by providing their name, email, and password. This allows them to access personalized features like the shopping cart.

#### *1.2. How can users log in and log out?*
- *Login*: Users log in on the login.php page using their email and password.
- *Logout*: The logout.php page ends the session, ensuring user data is secure.

#### *1.3. How can users view products?*
- *Answer*: All products are displayed on the homepage (index.php). Users can see product names, prices, descriptions, and images.
- #### *1.4. How can users add products to their cart?*
- *Answer*: On the index.php page, users click "Add to Cart" to save items. The system records these items in the cart for the logged-in user.

#### *1.5. How can users manage their cart?*
- *Answer*: The cart.php page lets users view, update, or remove items from their cart. It also shows the total cost of selected products.

---

### *2. Admin Section*
This section explains how admins manage the platform.

#### *2.1. How do admins log in and log out?*
- *Login*: Admins log in via admin/login.php using their credentials.
- *Logout*: The admin/logout.php page ends the admin session securely.

#### *2.2. What is the admin dashboard?*
- *Answer*: The admin/dashboard.php page provides a control panel with options to add, edit, and delete products.

#### *2.3. How do admins add products?*
- *Answer*: The admin/add_product.php page allows admins to add new products by filling out a form with product details and uploading an image.

#### *2.4. How do admins manage products?*
- *Answer*: The admin/manage_products.php page shows all products in a table with options to:
  - Edit product details.
  - Delete products from the store.

---
### *3. Database Section*
This section explains how the database is structured.

#### *3.1. What does the users table do?*
- *Answer*: The users table stores information about all users (customers and admins):
  - Usernames, emails, hashed passwords.
  - A role field to differentiate between customers (user) and admins (admin).

#### *3.2. What does the products table do?*
- *Answer*: The products table contains product details:
  - Names, prices, descriptions, and image filenames.

#### *3.3. What does the cart table do?*
- *Answer*: The cart table keeps track of items added to users' carts:
  - Links users to products and stores the quantity of each item.

---

### *4. Flow of the Website*
This section explains the flow of user actions.

#### *4.1. What happens when a user registers?*
- *Answer*: The system validates the input, hashes the password, and saves the user data in the users table.

#### *4.2. What happens when a user logs in?*
- *Answer*: The system verifies the email and password, then starts a session to allow personalized access.

#### *4.3. What happens when a product is added to the cart?*
- *Answer*: The system saves the product details in the cart table, linked to the logged-in user's ID.

#### *4.4. What happens when an admin adds a product?*
- *Answer*: The system uploads the product image, saves the product details in the products table, and displays it on the homepage.

#### *4.5. What happens when an admin deletes a product?*
- *Answer*: The system removes the product entry from the products table, making it unavailable on the website.

---
### *5. Security Measures*
This section explains how the website ensures security.

#### *5.1. How are passwords secured?*
- *Answer*: Passwords are hashed using password_hash() before being stored in the database.

#### *5.2. How is session management handled?*
- *Answer*: Sessions track logged-in users ($_SESSION['user_id'] for customers, $_SESSION['admin_id'] for admins) to restrict access to sensitive pages.

#### *5.3. How is admin access secured?*
- *Answer*: Admin login checks the role field in the users table to ensure only admins can access the control panel.

---

### How to Use This Guide
Follow the sections to understand:
- How users and admins interact with the platform.
- How the database stores and retrieves data.
- The flow of actions across the website.

For detailed implementation, refer to the individual PHP files for each feature. Let me know if this structure works for you!
