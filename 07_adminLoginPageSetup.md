### Step-by-Step Documentation for Admin Login Page (`admin/login.php`)

---

#### Purpose
The **Admin Login Page** authenticates administrators, granting access to the admin dashboard.

---

#### 1. PHP Logic for Authentication
The PHP code at the top handles login functionality:

```php
<?php
include '../includes/db.php';
session_start();

if (isset($_POST['login'])) {
    $email = $_POST['email'];
    $password = $_POST['password'];

    // Check if the email belongs to an admin
    $stmt = $conn->prepare("SELECT * FROM users WHERE email = ? AND role = 'admin'");
    $stmt->execute([$email]);
    $user = $stmt->fetch(PDO::FETCH_ASSOC);

    if ($user && password_verify($password, $user['password'])) {
        // Start admin session and redirect to dashboard
        $_SESSION['admin_id'] = $user['id'];
        header("Location: dashboard.php");
        exit();
    } else {
        echo "<p style='color:red; text-align:center;'>Invalid credentials or not an admin.</p>";
    }
}
?>
```

**Key Features:**
- Validates that the `email` belongs to an admin.
- Verifies the password using `password_verify()`.
- Starts a session for authenticated admins.
- Redirects to the `dashboard.php` page upon successful login.

---

#### 2. HTML Form for Login
This is the front-end structure for the admin login page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7fa;
        }
        .login-container {
            width: 100%;
            max-width: 400px;
            margin: 100px auto;
            background-color: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 10px 0 20px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #28a745;
            border: none;
            color: white;
            font-size: 16px;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>

    <div class="login-container">
        <h2>Admin Login</h2>
        <form method="POST">
            <label for="email">Email</label>
            <input type="email" name="email" id="email" required>

            <label for="password">Password</label>
            <input type="password" name="password" id="password" required>

            <button type="submit" name="login">Login</button>
        </form>
    </div>

</body>
</html>
```

**Features:**
- The form uses `POST` to securely submit credentials.
- Fields include `email` and `password`.

---

#### 3. Test the Admin Login Page
1. Ensure the `users` table has an admin user (`role = 'admin'`).
2. Open the page at `http://localhost/ecommerce/admin/login.php`.
3. Test login with valid and invalid admin credentials.

---

### Next Step
The next page is **Admin Logout (`admin/logout.php`)** to securely end admin sessions. Let’s proceed!
