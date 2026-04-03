<div align="center">

```
███████╗ ██████╗  ██████╗ ██████╗ ██╗  ██╗   ██╗███╗   ██╗██╗  ██╗
██╔════╝██╔═══██╗██╔═══██╗██╔══██╗██║  ╚██╗ ██╔╝████╗  ██║██║ ██╔╝
█████╗  ██║   ██║██║   ██║██║  ██║██║   ╚████╔╝ ██╔██╗ ██║█████╔╝ 
██╔══╝  ██║   ██║██║   ██║██║  ██║██║    ╚██╔╝  ██║╚██╗██║██╔═██╗ 
██║     ╚██████╔╝╚██████╔╝██████╔╝███████╗██║   ██║ ╚████║██║  ██╗
╚═╝      ╚═════╝  ╚═════╝ ╚═════╝ ╚══════╝╚═╝   ╚═╝  ╚═══╝╚═╝  ╚═╝
```

### *A food ordering platform for restaurants and clients — built to learn PHP.*

<br>

[![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Apache](https://img.shields.io/badge/Apache-D22128?style=flat-square&logo=apache&logoColor=white)](https://httpd.apache.org/)
![Type](https://img.shields.io/badge/project-personal-orange?style=flat-square)
![Status](https://img.shields.io/badge/status-learning-yellow?style=flat-square)

<br>

> *"You don't learn PHP by reading about it. You learn it by breaking things and figuring out why."*

</div>

# 🍔 FoodLynk — A PHP Learning Project

> A food ordering web platform built from scratch as a personal practice project to learn PHP, MySQL, and full-stack web fundamentals.

---

## 📌 What Is This?

**FoodLynk** is a food ordering web application where restaurants and food brands can register, create their own page, and list their meals — and clients can browse those brands, filter meals, add them to a cart, and place orders.

This project is **purely a learning exercise**. I built it to get hands-on with PHP — understanding how server-side logic works, how to talk to a database, how to manage user sessions, and how to build a real multi-page web app step by step. No frameworks, no shortcuts — just raw PHP, MySQL, HTML, and CSS.

---

## 🎯 Why I Built This

I'm on my PHP learning path and wanted something real to practice on — not just small isolated scripts, but an actual project with multiple user roles, a real database, forms, authentication, and business logic. I didn’t worry too much about the CSS and mostly left the styling to AI so I could stay focused on learning and building the PHP/backend side.

FoodLynk gave me exactly that. Every version I released taught me something new:

- How to connect to a database and run queries
- How to handle form submissions and validate input
- How to use sessions to keep users logged in
- How to handle file uploads
- How to manage multiple user types (brands, clients, admin)
- How to build a cart and checkout flow

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | PHP (procedural, no framework) |
| Database | MySQL via phpMyAdmin |
| Frontend | HTML5, CSS3 (custom, no libraries) |
| Server | Apache (XAMPP / localhost) |

---

## 🗄️ Database Structure

The database is named `foodlynk` and has four tables. I set this up manually using phpMyAdmin and included the raw `CREATE TABLE` queries in `DATABASE.md`.

### `brands`
Stores all brand/restaurant accounts. Each brand has a name, owner info, category, a cover image, a hashed password, and a `status` field (`pending`, `approve`, `reject`) — because I wanted admin approval before a brand goes live.

```sql
CREATE TABLE brands (
    id INT(10) UNSIGNED NOT NULL AUTO_INCREMENT,
    username VARCHAR(100) NOT NULL,
    first_name VARCHAR(20) NOT NULL,
    last_name VARCHAR(20) NOT NULL,
    phone_number VARCHAR(20) NOT NULL,
    email VARCHAR(100) NOT NULL,
    address VARCHAR(255) NOT NULL,
    brand_name VARCHAR(100) NOT NULL,
    brand_image BLOB NOT NULL,
    password VARCHAR(255) NOT NULL,
    category VARCHAR(100) NOT NULL,
    status VARCHAR(50) NOT NULL,
    PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### `clients`
Stores client accounts. Clients have personal info, a card ID for identification, a hashed password, and a profile image.

```sql
CREATE TABLE clients (
    id INT(10) UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    card_id VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    address VARCHAR(255) NOT NULL,
    phone_number VARCHAR(20) NOT NULL,
    password VARCHAR(255) NOT NULL,
    profile_image BLOB NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### `mealsnew`
This is where all meals are stored. Each meal belongs to a brand (identified by `brand_name` and `email`), has a category (starter, main, drink), a price, a quantity, a status (active/deactivated), and a bunch of dietary flags as `TINYINT(1)` booleans — like `is_vegan`, `is_halal`, `is_spicy`, etc. I also added a `created_at` timestamp so meals are sortable by when they were added.

```sql
CREATE TABLE mealsnew (
    meal_id INT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    brand_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    meal_name VARCHAR(150) NOT NULL,
    meal_description TEXT DEFAULT NULL,
    meal_image VARCHAR(255) DEFAULT NULL,
    meal_quantity INT(11) DEFAULT 0,
    meal_price DECIMAL(10,2) NOT NULL,
    category ENUM('starter','main','drink') DEFAULT 'main',
    is_vegan TINYINT(1) DEFAULT 0,
    is_spicy TINYINT(1) DEFAULT 0,
    is_gluten_free TINYINT(1) DEFAULT 0,
    is_nut_free TINYINT(1) DEFAULT 0,
    is_halal TINYINT(1) DEFAULT 0,
    is_low_carb TINYINT(1) DEFAULT 0,
    is_low_sugar TINYINT(1) DEFAULT 0,
    rating INT(11) DEFAULT 0,
    status VARCHAR(20) DEFAULT 'available',
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### `orders`
Stores every placed order. Each row is one meal from one order, with the buyer's info, the payment method, and the brand/meal details. I kept it flat (one row per meal line) rather than using a separate order-items table — simpler to query while I'm still learning.

```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    card_id VARCHAR(50),
    email VARCHAR(150),
    phone_number VARCHAR(50),
    address TEXT,
    payment_method VARCHAR(50),
    card_number VARCHAR(50),
    expiry VARCHAR(10),
    cvv VARCHAR(10),
    brand_name VARCHAR(100),
    meal_name VARCHAR(150),
    price DECIMAL(10,2),
    quantity INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

---

## 📁 File Overview

| File | What it does |
|---|---|
| `index.php` | Landing page — fetches approved brands from the DB and renders them as cards |
| `brand_creation.php` | Brand registration form — validates, hashes password, uploads image, inserts into DB |
| `brand_login.php` | Brand login — fetches by email, verifies hashed password, starts session |
| `brand_dashboard.php` | Brand control panel — add/delete/toggle meals, manage the brand's menu |
| `brand_waiting.php` | Shown after registration — brand waits for admin approval |
| `brand_status.php` | Checks and shows the current approval status of a brand |
| `client_signing.php` | Client registration — same pattern as brand, inserts into `clients` table |
| `client_login.php` | Client login — session-based authentication |
| `client_account.php` | Client profile page — shows info and past orders grouped from the DB |
| `client_edit_profile.php` | Lets the client update their personal info and profile picture |
| `menu.php` | Shows all meals from a specific brand — with filtering, sorting, search, and a cart |
| `checkout.php` | Pre-order review page — shows cart items and pre-fills client info from session |
| `confirm.php` | Validates the order and writes each cart item into the `orders` table |
| `success.php` | Order success confirmation page |
| `master_admin_dashboard.php` | Admin-only page to approve or reject brand registrations |
| `DATABASE.md` | Raw SQL `CREATE TABLE` queries for all four tables |

---

## 🔑 PHP Concepts I Practiced

### 1. Connecting to MySQL with `mysqli`

Everything starts with `mysqli_connect()`. I wrote this line in almost every file:

```php
$connection = mysqli_connect("localhost", "root", "", "foodlynk");
```

I learned how to check if the connection fails with `mysqli_connect_error()`, how to run `SELECT` queries with `mysqli_query()`, and how to fetch results row by row using `mysqli_fetch_assoc()`.

---

### 2. Inserting Data with Form Handling

In `brand_creation.php` and `client_signing.php`, I learned to handle `$_POST` data — reading what the user submitted, sanitizing it, and inserting it into the database.

```php
if (isset($_POST["submit"])) {
    $username = mysqli_real_escape_string($connection, $_POST['username']);
    $email    = mysqli_real_escape_string($connection, $_POST['email']);
    // ...
    $query = "INSERT INTO brands (...) VALUES (...)";
    mysqli_query($connection, $query);
}
```

I used `mysqli_real_escape_string()` to prevent basic SQL injection — this was one of the first security things I learned to think about.

---

### 3. Password Hashing

I never store passwords in plain text. I used PHP's built-in `password_hash()` on registration:

```php
$password = password_hash($_POST['password'], PASSWORD_DEFAULT);
```

And `password_verify()` on login to check if what the user typed matches the stored hash:

```php
if (password_verify($_POST['password'], $stored_hash)) {
    // correct password
}
```

This was a big learning moment — understanding why you never compare passwords directly.

---

### 4. Sessions for Authentication

I use `$_SESSION` to keep users logged in across pages. After a successful login:

```php
session_start();
$_SESSION['client_email'] = $email;
header("Location: client_account.php");
exit();
```

Then on protected pages, I check if the session exists:

```php
if (!isset($_SESSION['client_email'])) {
    header("location: client_login.php");
    exit();
}
```

Logout just destroys the session:

```php
session_destroy();
header("location: client_login.php");
```

---

### 5. File Uploads

In `brand_creation.php` and `brand_dashboard.php`, brands can upload a cover image or meal image. I learned how `$_FILES` works:

```php
$image_name = $_FILES['brand_image']['name'];
$image_tmp  = $_FILES['brand_image']['tmp_name'];
$image_path = "cover_images/" . basename($image_name);
move_uploaded_file($image_tmp, $image_path);
```

The path gets stored in the database and used in the HTML `<img>` tag later. Simple but it took me a minute to understand the `tmp_name` concept.

---

### 6. Uniqueness Checks Before Insert

In `brand_creation.php`, I check if the email or brand name is already taken before inserting:

```php
$check = "SELECT email FROM brands WHERE email = '$email'";
$result = mysqli_query($connection, $check);

if (mysqli_num_rows($result) > 0) {
    $email_error = 1;
    $email_placeholder = "Email already taken";
}
```

I also keep the user's input in the placeholder so they don't have to retype everything — a small UX thing I figured out on my own.

---

### 7. Toggling Status in the Database

In `brand_dashboard.php`, I have a toggle for meal activation/deactivation. I query the current status first, then flip it:

```php
$current = "SELECT status FROM mealsnew WHERE meal_name = '$name' AND brand_name = '$brand'";
$result = mysqli_query($connection, $current);
$row = mysqli_fetch_assoc($result);

$new_status = ($row['status'] === 'Deactivate') ? 'Activate' : 'Deactivate';

$update = "UPDATE mealsnew SET status = '$new_status' WHERE ...";
mysqli_query($connection, $update);
```

This was the first time I wrote an `UPDATE` query with conditional logic and I was pretty happy when it worked.

---

### 8. Conditional Navigation with Sessions

On `index.php`, I use PHP inside HTML to conditionally show different nav links based on who's logged in:

```php
<?php if (isset($_SESSION['client_email'])): ?>
    <a href="client_account.php">My Account</a>
<?php else: ?>
    <a href="client_login.php">Login</a>
<?php endif; ?>
```

This was a cool moment — realizing PHP can live right inside HTML to make pages dynamic without JavaScript.

---

### 9. Fetching and Displaying Database Records Dynamically

In `index.php`, I fetch only approved brands and loop through them to render cards:

```php
$query = "SELECT * FROM brands WHERE status = 'approve'";
$result = mysqli_query($connection, $query);

while ($brand = mysqli_fetch_assoc($result)) {
    echo "<div class='brand-card'>";
    echo "<h3>" . htmlspecialchars($brand['brand_name']) . "</h3>";
    echo "</div>";
}
```

Same pattern in `menu.php` for meals, and in `client_account.php` for order history. Once I understood this loop pattern, building pages felt a lot more natural.

---

### 10. The Cart and Checkout Flow

The cart in `menu.php` is stored in `$_SESSION['cart']` — an array of meals with quantities. On `checkout.php`, the cart is read and displayed. On `confirm.php`, each item is looped through and inserted into the `orders` table one by one:

```php
foreach ($_SESSION['cart'] as $item) {
    $insert = "INSERT INTO orders (first_name, meal_name, price, quantity, ...) 
               VALUES ('$first_name', '{$item['meal_name']}', ...)";
    mysqli_query($connection, $insert);
}
```

Building this multi-step flow (menu → checkout → confirm → success) was the most complex thing I did in this project, and it really helped me understand how pages communicate through sessions and redirects.

---

## 🚀 Version History

### v1.0 — Foundation
Started with the core structure: `index.php`, login pages, sign-in pages, and the brand creation page — just HTML/CSS, no PHP logic yet.

### v1.1 — First Database Work
Created the MySQL database. Added real PHP logic to `client_signing.php` and `brand_creation.php` to insert data, and to both login pages to fetch and validate credentials. First time I wrote SQL queries inside PHP.

### v1.2 — Refactoring and New Pages
Updated naming conventions, rewrote some PHP logic, and added `master_admin_dashboard.php`, `brand_waiting.php`, and `brand_status.php` to handle the brand approval flow.

### v1.3 — Brand Dashboard + Uniqueness
Added `brand_dashboard.php` so brands can insert meals. Made brand names unique (duplicate check before insert). Fixed redirects in `brand_login.php` and `index.php`. Added `DATABASE.md` with raw SQL.

### v1.4 — Logout and Unlimited Quantity
Added a logout button to the brand dashboard. Added an "unlimited quantity" option for meals. Updated `index.php` to only fetch approved brands and render them as cards.

### v1.5 — Menu Page and Ordering
Added `menu.php` with full meal display, and wired up the ability for clients to purchase meals and write order data to the database. First real end-to-end user flow.

### v1.6 — Back to It
Small version, just catching up after a break. Kept the project alive.

### v1.7 — Major Design Overhaul
Big visual update: new color scheme, animations, renamed HTML elements, deleted old files, and merged some files to clean up the structure.

### v1.8 — Dashboard Power-Up and Client Account
Enhanced `brand_dashboard.php` with delete and disable buttons for meals, redesigned the add-meal popup form. Added sorting, filtering, searching, and a cart to `menu.php`. Added `client_account.php` and `client_edit_profile.php`.

### v1.9 — Full Checkout Flow
Made the activate button functional with confirmation popups. Grouped order history by order in `client_account.php`. Improved `add_to_cart` so it remembers scroll position. Added `checkout.php`, `confirm.php`, and `success.php` to complete the order flow.

---

## ⚠️ Things I Know Need Improvement

Since this is a learning project, there are things I'm aware of but haven't refactored yet:

- **SQL Injection** — I use `mysqli_real_escape_string()` but I know prepared statements with `mysqli_prepare()` are the proper way. That's next on my list.
- **No input validation on the server side for types/lengths** — I relied mostly on HTML `required` attributes.
- **Flat order table** — A proper setup would have an `orders` parent and an `order_items` child table. I kept it flat to stay focused on learning basics first.
- **Passwords in sessions** — I only store the email in session, not the password, but some pages could use extra authorization checks.
- **No `.env` or config file** — Database credentials are hardcoded. I'll move them to a config file eventually.

---

## 🧠 What I Learned Overall

This project taught me more in practice than any tutorial did. The moment something broke and I had to debug why a query returned nothing, or why a session wasn't persisting, or why a file wasn't uploading — that's where the real learning happened.

PHP's ability to mix directly with HTML makes it really beginner-friendly for getting things to show up fast. MySQL + `mysqli` gave me a solid foundation for understanding relational databases before moving to more advanced tools. And building the whole thing myself, version by version, made every concept stick.

Still learning. More versions to come.

---

## 📂 How to Run Locally

1. Install [XAMPP](https://www.apachefriends.org/) (or any Apache + PHP + MySQL stack)
2. Clone or copy this project into your `htdocs` folder
3. Open phpMyAdmin and create a database named `foodlynk`
4. Run the SQL queries from `DATABASE.md` to create all four tables
5. Start Apache and MySQL in XAMPP
6. Visit `http://localhost/fodlynk/index.php`

---

*Built by me, for learning. Not production-ready — and that's the whole point.*
