### Step-by-Step Documentation for Add Product Page (`admin/add_product.php`)

---

#### Purpose
The **Add Product Page** allows administrators to create new product entries by filling out a form with the product’s name, price, description, and image.

---

#### 1. Session Authentication
Ensure only logged-in admins can access this page:

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

#### 2. PHP Logic for Adding Products
The following PHP code handles form submission and saves the new product to the database:

```php
<?php
include '../includes/db.php';

if (isset($_POST['add_product'])) {
    $name = $_POST['name'];
    $price = $_POST['price'];
    $description = $_POST['description'];
    $image = $_FILES['image']['name'];

    // Upload the image to the 'images' folder
    move_uploaded_file($_FILES['image']['tmp_name'], "../images/$image");

    // Insert product details into the database
    $stmt = $conn->prepare("INSERT INTO products (name, price, description, image) VALUES (?, ?, ?, ?)");
    $stmt->execute([$name, $price, $description, $image]);

    echo "Product added successfully!";
}
?>
```

---

#### 3. HTML Form for Adding Products
The form captures all necessary product details:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add Product</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }
        .container {
            width: 50%;
            margin: 50px auto;
            background-color: #fff;
            padding: 30px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        h2 {
            text-align: center;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        label {
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, textarea {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .back-link {
            text-align: center;
            margin-top: 20px;
        }
        .back-link a {
            text-decoration: none;
            color: #4CAF50;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Add Product</h2>
        <form method="POST" enctype="multipart/form-data">
            <label for="name">Product Name:</label>
            <input type="text" name="name" id="name" required>

            <label for="price">Price:</label>
            <input type="number" step="0.01" name="price" id="price" required>

            <label for="description">Description:</label>
            <textarea name="description" id="description" required></textarea>

            <label for="image">Image:</label>
            <input type="file" name="image" id="image" required>

            <button type="submit" name="add_product">Add Product</button>
        </form>
        <div class="back-link">
            <a href="manage_products.php">Back to Manage Products</a>
        </div>
    </div>
</body>
</html>
```

---

#### Features
1. **Form Inputs**:
   - **Product Name** (`name`)
   - **Price** (`price`)
   - **Description** (`description`)
   - **Image Upload** (`image`)

2. **Image Handling**:
   - Images are uploaded to the `images/` folder.
   - The filename is saved in the database.

3. **Database Insertion**:
   - Product details are stored in the `products` table.

4. **Feedback**:
   - Displays a success message after the product is added.

---

#### 4. Testing the Add Product Page
1. Log in as an admin.
2. Navigate to `http://localhost/ecommerce/admin/add_product.php`.
3. Fill out the form and submit.
4. Verify:
   - The product is added to the `products` table.
   - The image file is uploaded to the `images/` folder.

---
