### Step-by-Step Documentation for Admin Manage Products Page (`admin/manage_products.php`)

---

#### Purpose
The **Manage Products Page** allows administrators to view, edit, and delete existing products in the e-commerce database.

---

#### 1. Session Authentication
Ensure only logged-in admins can access the page:

```php
<?php
session_start();
if (!isset($_SESSION['admin_id'])) {
    header("Location: login.php");
    exit();
}
?>
```

---

#### 2. Fetch Products from the Database
Fetch all products from the database to display in a table:

```php
<?php
include '../includes/db.php';
$stmt = $conn->query("SELECT * FROM products");
$products = $stmt->fetchAll(PDO::FETCH_ASSOC);
?>
```

---

#### 3. HTML Structure
Display the fetched products in a structured table:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manage Products</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7fa;
        }
        .container {
            width: 80%;
            margin: 50px auto;
            padding: 30px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            color: #333;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border: 1px solid #ddd;
        }
        th {
            background-color: #28a745;
            color: white;
        }
        td img {
            width: 50px;
            height: auto;
        }
        .actions a {
            margin: 0 10px;
            padding: 5px 10px;
            color: #007bff;
            text-decoration: none;
            border: 1px solid #007bff;
            border-radius: 4px;
        }
        .actions a:hover {
            background-color: #007bff;
            color: white;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Manage Products</h2>
    <table>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Price</th>
            <th>Description</th>
            <th>Image</th>
            <th>Actions</th>
        </tr>
        <?php foreach ($products as $product) : ?>
            <tr>
                <td><?= $product['id']; ?></td>
                <td><?= htmlspecialchars($product['name']); ?></td>
                <td>$<?= number_format($product['price'], 2); ?></td>
                <td><?= htmlspecialchars($product['description']); ?></td>
                <td><img src="../images/<?= htmlspecialchars($product['image']); ?>" alt="Product Image"></td>
                <td class="actions">
                    <a href="edit_product.php?id=<?= $product['id']; ?>">Edit</a>
                    <a href="delete_product.php?id=<?= $product['id']; ?>" onclick="return confirm('Are you sure you want to delete this product?');">Delete</a>
                </td>
            </tr>
        <?php endforeach; ?>
    </table>
    <a href="dashboard.php" class="btn-back">Back to Dashboard</a>
</div>

</body>
</html>
```

---

#### Features
1. **View Products**:
   - Display all products with details (ID, name, price, description, and image).

2. **Edit Products**:
   - Clicking the **Edit** link redirects to `edit_product.php` for modifying product details.

3. **Delete Products**:
   - Clicking the **Delete** link removes a product from the database after confirmation.

4. **Back to Dashboard**:
   - Provides a link to return to the admin dashboard.

---

#### 4. Testing the Manage Products Page
1. Log in as an admin.
2. Navigate to `http://localhost/ecommerce/admin/manage_products.php`.
3. Verify:
   - All products are displayed correctly.
   - Edit and delete actions link to their respective pages.
   - The dashboard link works as expected.

---

Next proceed with **Add Product (`admin/add_product.php`)**.
