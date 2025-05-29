### **1. Why There is No Admin Register Page**
An **Admin Register Page** is typically excluded in secure systems for the following reasons:

1. **Security Concerns**:
   - Allowing anyone to register as an admin could expose the system to unauthorized access.
   - Admin creation is restricted to superusers or developers who have direct access to the database or backend.

2. **Controlled Access**:
   - Admins are added manually by authorized personnel (e.g., via a secure backend or database query).
   - This ensures only trusted individuals are granted administrative privileges.

3. **Simpler Role Management**:
   - Using a `role` field in the `users` table (`user` vs `admin`) simplifies user management without requiring separate registration flows.

---

### **2. Adding an Admin User to the Database**

To add an admin user manually in the database, follow these steps:

#### Using **phpMyAdmin** or SQL Console:
1. **Insert Admin User**:
   Run the following SQL query:
   ```sql
   INSERT INTO users (username, email, password, role, created_at) 
   VALUES ('Admin Name', 'admin@example.com', '<hashed_password>', 'admin', NOW());
   ```
   Replace:
   - `'Admin Name'` with the admin's name.
   - `'admin@example.com'` with the admin's email.
   - `'<hashed_password>'` with the hashed password.

#### Example Query:
```sql
INSERT INTO users (username, email, password, role, created_at) 
VALUES ('Super Admin', 'admin@ecommerce.com', '$2y$10$abcdefghijk1234567890LMNOPQRSTUVWXyz12345678', 'admin', NOW());
```

2. **Verify the Inserted Admin**:
   Query the `users` table to confirm the new admin user:
   ```sql
   SELECT * FROM users WHERE role = 'admin';
   ```

---

### **3. Next: Admin Logout Page**

### Step-by-Step Documentation for Admin Logout Page (`admin/logout.php`)

---

#### Purpose
The **Admin Logout Page** securely ends the admin session and redirects the user to the admin login page.

---

#### Code Breakdown
The code for `admin/logout.php` is simple yet effective:

```php
<?php
session_start(); // Start the session
session_unset(); // Unset all session variables
session_destroy(); // Destroy the session
header("Location: login.php"); // Redirect to the admin login page
exit(); // Ensure no further code executes
?>
```

---

#### How It Works
1. **Start the Session**:
   - The session is initiated with `session_start()` to access and manage session variables.

2. **Unset All Variables**:
   - `session_unset()` removes all session variables, ensuring no leftover data persists.

3. **Destroy the Session**:
   - `session_destroy()` completely terminates the session, effectively logging out the admin.

4. **Redirect**:
   - After ending the session, the admin is redirected to `login.php` using `header("Location: login.php");`.

---

#### Implementation Steps
1. Place the `logout.php` file in the `admin/` folder.
2. Add a **Logout Link** to the admin dashboard (`dashboard.php`):
   ```html
   <li><a href="logout.php">Logout</a></li>
   ```

---

#### Testing the Logout Page
1. Log in as an admin.
2. Navigate to `http://localhost/ecommerce/admin/logout.php`.
3. Confirm:
   - The session is ended.
   - You are redirected to the admin login page.
   - Attempting to access the dashboard (`dashboard.php`) redirects to the login page if session checks are implemented.

---

Next proceed with the **Admin Dashboard (`dashboard.php`)**
