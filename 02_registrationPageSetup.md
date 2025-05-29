### Step-by-Step Documentation for the Registration Page

Below is the updated and aligned documentation for creating the register.php page, incorporating the actual code.

---

#### Step 1: Create the register.php File
1. Inside the pages folder, create a file named register.php.

---

#### Step 2: Structure the HTML Form
Add the following code to create the registration form:

*HTML Form for Registration*
php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Register</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .register-container {
            background-color: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
        }
        h2 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }
        label {
            font-size: 1.1em;
            margin-bottom: 5px;
            display: block;
        }
        input[type="email"],
        input[type="password"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
        }
        button {
            width: 100%;
            padding: 12px;
            background-color: #28a745;
            color: white;
            font-size: 1.1em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #218838;
        }
        .error-message {
            color: #e74c3c;
            font-size: 1em;
            text-align: center;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="register-container">
        <h2>Register</h2>
        <form method="POST">
            <label>Email:</label>
            <input type="email" name="email" required>
            <label>Password:</label>
            <input type="password" name="password" required>
            <button type="submit" name="register">Register</button>
        </form>
        <?php if (isset($error_message)): ?>
            <p class="error-message"><?= htmlspecialchars($error_message); ?></p>
        <?php endif; ?>
    </div>
</body>
</html>


---

#### Step 3: Add PHP Logic for Registration
Add this PHP script at the top of the file to handle user registration:

*PHP Script for Handling Registration*
php
<?php
include('../includes/db.php');  // Database connection
session_start();

if (isset($_POST['register'])) {
    $email = $_POST['email'];
    $password = password_hash($_POST['password'], PASSWORD_DEFAULT); // Hash the password
    $role = 'user'; // Default role for users

    // Check if the email already exists
    $stmt = $conn->prepare("SELECT * FROM users WHERE email = ?");
    $stmt->execute([$email]);
    $user = $stmt->fetch(PDO::FETCH_ASSOC);

    if ($user) {
        echo "<script>alert('Email is already registered!');</script>";
    } else {
        // Insert new user
        $stmt = $conn->prepare("INSERT INTO users (email, password, role) VALUES (?, ?, ?)");
        $stmt->execute([$email, $password, $role]);

        // Log the user in after successful registration
        $_SESSION['user_id'] = $conn->lastInsertId();
        header("Location: ../index.php"); // Redirect to the homepage
        exit();
    }
}
?>


---

#### Step 4: Test the Registration Page
1. Start your local server.
2. Navigate to http://localhost/ecommerce/pages/register.php.
3. Register using an email and password.
4. Check the users table in your database to ensure the new user has been added.

---

### Next Steps
1. Build the *Login Page (login.php)* for user authentication.
2. Implement session management to maintain user sessions.
