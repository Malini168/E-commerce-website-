### Brief Documentation for the Cart Page (`cart.php`)

---

#### Step 1: Create `cart.php`
1. Place the file in the `pages` folder.

---

#### Step 2: Display Cart Items
Use the following PHP to fetch and display cart items for the logged-in user:

```php
<?php
session_start();
if (!isset($_SESSION['user_id'])) {
    header("Location: login.php");
    exit();
}

include '../includes/db.php';

// Fetch the user's cart items
$user_id = $_SESSION['user_id'];
$stmt = $conn->prepare("SELECT cart.id AS cart_id, products.name, products.price, cart.quantity 
                        FROM cart 
                        JOIN products ON cart.product_id = products.id 
                        WHERE cart.user_id = ?");
$stmt->execute([$user_id]);
$cart_items = $stmt->fetchAll(PDO::FETCH_ASSOC);

$total_cost = 0;
?>
```

In the HTML, iterate over the `$cart_items` to display them dynamically:

```php
<?php foreach ($cart_items as $item): ?>
<tr>
    <td><?= htmlspecialchars($item['name']); ?></td>
    <td>$<?= number_format($item['price'], 2); ?></td>
    <td><?= $item['quantity']; ?></td>
    <td>$<?= number_format($item['price'] * $item['quantity'], 2); ?></td>
    <td>
        <form method="POST">
            <input type="hidden" name="product_id" value="<?= $item['cart_id']; ?>">
            <button type="submit" name="remove_from_cart">Remove</button>
        </form>
    </td>
</tr>
<?php endforeach; ?>
```

---

#### Step 3: Handle Cart Updates
Add functionality to update quantities and remove items:

- **Update Quantity:**
```php
if (isset($_POST['update_quantity'])) {
    $product_id = $_POST['product_id'];
    $quantity = (int)$_POST['quantity'];
    $stmt = $conn->prepare("UPDATE cart SET quantity = ? WHERE user_id = ? AND product_id = ?");
    $stmt->execute([$quantity, $user_id, $product_id]);
}
```

- **Remove Item:**
```php
if (isset($_POST['remove_from_cart'])) {
    $product_id = $_POST['product_id'];
    $stmt = $conn->prepare("DELETE FROM cart WHERE user_id = ? AND product_id = ?");
    $stmt->execute([$user_id, $product_id]);
}
```

---

#### Step 4: Styling
Add CSS to style the cart page:
```css
.cart-container {
    max-width: 800px;
    margin: 20px auto;
    padding: 20px;
    background: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 8px;
}
```

---

#### Step 5: Test the Cart Page
1. Log in as a user.
2. Add items to the cart from the product page.
3. Verify items are displayed correctly.
4. Check quantity updates and removal functionality.

---

Next Step is Admin Dashboard Pages
