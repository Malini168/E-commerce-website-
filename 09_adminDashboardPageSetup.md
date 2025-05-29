### Step-by-Step Documentation for Admin Dashboard (`admin/dashboard.php`)

---

#### Purpose
The **Admin Dashboard** serves as the central control panel for managing the e-commerce site. It provides navigation links to key admin functionalities like adding and managing products.

---

#### 1. Session Authentication
Ensure only authenticated admins can access the dashboard:

```php
<?php
session_start();
if (!isset($_SESSION['admin_id'])) {
    header("Location: login.php");
    exit();
}
?>
```

**How It Works**:
- `session_start()` initializes the session.
- The script checks if `admin_id` is set in the session. If not, it redirects to the login page.

---

#### 2. HTML Structure of the Dashboard
The dashboard includes navigation links for admin operations and a logout button:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }
        .container {
            width: 60%;
            margin: 50px auto;
            background-color: #fff;
            padding: 30px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        nav {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        nav a {
            text-decoration: none;
            padding: 12px 25px;
            background-color: #4CAF50;
            color: white;
            font-size: 16px;
            border-radius: 4px;
            transition: background-color 0.3s ease;
        }
        nav a:hover {
            background-color: #45a049;
        }
        .logout {
            background-color: #f44336;
        }
        .logout:hover {
            background-color: #e53935;
        }
        footer {
            text-align: center;
            margin-top: 50px;
            font-size: 14px;
            color: #777;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Admin Dashboard</h2>
        <nav>
            <a href="add_product.php">Add Product</a>
            <a href="manage_products.php">Manage Products</a>
            <a href="logout.php" class="logout">Logout</a>
        </nav>
    </div>
    <footer>
        <p>&copy; <?php echo date("Y"); ?> Admin Dashboard</p>
    </footer>
</body>
</html>
```

---

#### 3. Features
- **Add Product**: Link to `add_product.php` for creating new product entries.
- **Manage Products**: Link to `manage_products.php` for editing or deleting products.
- **Logout**: Ends the admin session and redirects to the login page.

---

#### 4. Testing the Dashboard
1. Log in as an admin.
2. Navigate to `http://localhost/ecommerce/admin/dashboard.php`.
3. Verify:
   - The session check prevents unauthorized access.
   - Links navigate to their respective pages.
   - The logout button works as expected.

---

Next proceed with **Manage Products (`admin/manage_products.php`)**.
