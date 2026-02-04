# Coffee Blend - Coffee Shop Web Application

A full-featured PHP web application for a coffee shop that allows customers to browse menu items, place orders, make table reservations, and leave reviews. Includes a complete admin panel for managing the business.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Technology Stack](#technology-stack)
3. [Project Structure](#project-structure)
4. [Database Schema](#database-schema)
5. [Features](#features)
6. [Installation Guide](#installation-guide)
7. [Configuration](#configuration)
8. [User Guide](#user-guide)
9. [Admin Panel Guide](#admin-panel-guide)
10. [Security Considerations](#security-considerations)
11. [File Reference](#file-reference)

---

## Project Overview

**Coffee Blend** is a web-based coffee shop management system built with PHP and MySQL. It provides a complete e-commerce solution for coffee shops, including:

- Public-facing website with menu display
- User registration and authentication
- Shopping cart and checkout system
- Table booking/reservation system
- Customer reviews
- Admin panel for business management

---

## Technology Stack

| Component | Technology |
|-----------|------------|
| **Backend** | PHP 8.x |
| **Database** | MySQL / MariaDB (PDO) |
| **Frontend** | HTML5, CSS3, JavaScript |
| **CSS Framework** | Bootstrap 4 |
| **JavaScript Libraries** | jQuery, Owl Carousel, AOS, Magnific Popup |
| **Server** | Apache (Laragon recommended) |
| **Font Libraries** | Poppins, Josefin Sans, Great Vibes, Ionicons, Flaticon, IcoMoon |

---

## Project Structure

```
coffee-blend/
├── index.php                    # Homepage
├── menu.php                     # Menu page (drinks & desserts)
├── about.php                    # About page
├── contact.php                  # Contact page
├── services.php                 # Services page
├── 404.php                      # Error page
│
├── admin-panel/                 # Admin dashboard
│   ├── index.php                # Admin home (dashboard statistics)
│   ├── layouts/                 # Admin layout templates
│   │   ├── header.php
│   │   └── footer.php
│   ├── styles/
│   │   └── style.css
│   ├── admins/                  # Admin user management
│   │   ├── admins.php           # List admins
│   │   ├── create-admins.php    # Create new admin
│   │   ├── login-admins.php     # Admin login
│   │   └── logout.php           # Admin logout
│   ├── products-admins/         # Product management
│   │   ├── show-products.php    # List products
│   │   ├── create-products.php  # Add new product
│   │   ├── delete-products.php  # Delete product
│   │   └── images/              # Product images storage
│   ├── orders-admins/           # Order management
│   │   ├── show-orders.php      # List orders
│   │   ├── change-status.php    # Update order status
│   │   └── delete-orders.php    # Delete order
│   └── bookings-admins/         # Booking management
│       ├── show-bookings.php    # List bookings
│       ├── change-status.php    # Update booking status
│       └── delete-bookings.php  # Delete booking
│
├── auth/                        # User authentication
│   ├── login.php                # User login
│   ├── register.php             # User registration
│   └── logout.php               # User logout
│
├── booking/                     # Table reservations
│   └── book.php                 # Book a table
│
├── products/                    # Product & cart functionality
│   ├── product-single.php       # Single product view
│   ├── cart.php                 # Shopping cart
│   ├── checkout.php             # Checkout process
│   ├── pay.php                  # Payment processing
│   ├── delete-cart.php          # Remove from cart
│   └── delete-product.php       # Delete cart item
│
├── users/                       # User dashboard
│   ├── bookings.php             # View user bookings
│   └── Orders.php               # View user orders
│
├── reviews/                     # Customer reviews
│   └── write-review.php         # Submit review
│
├── includes/                    # Common includes
│   ├── header.php               # Site header & navigation
│   └── footer.php               # Site footer
│
├── config/
│   └── config.php               # Database configuration
│
├── css/                         # Stylesheets
├── js/                          # JavaScript files
├── fonts/                       # Font files
├── images/                      # Site images
├── scss/                        # SCSS source files
│
└── SQL_FILE/
    └── coffee-blend.sql         # Database schema & sample data
```

---

## Database Schema

The application uses **6 main tables**:

### 1. `users` - Customer Accounts
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| username | VARCHAR(200) | Username |
| email | VARCHAR(200) | Email address |
| password | VARCHAR(200) | Hashed password (bcrypt) |
| created_at | TIMESTAMP | Creation date |

### 2. `admins` - Admin Accounts
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| adminname | VARCHAR(200) | Admin username |
| email | VARCHAR(200) | Email address |
| password | VARCHAR(200) | Hashed password (bcrypt) |
| created_at | TIMESTAMP | Creation date |

### 3. `products` - Menu Items
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| name | VARCHAR(200) | Product name |
| image | VARCHAR(200) | Image filename |
| description | TEXT | Product description |
| price | VARCHAR(10) | Price |
| type | VARCHAR(200) | Category: 'drink' or 'dessert' |
| created_at | TIMESTAMP | Creation date |

### 4. `cart` - Shopping Cart Items
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| name | VARCHAR(200) | Product name |
| image | VARCHAR(200) | Image filename |
| price | VARCHAR(10) | Unit price |
| pro_id | INT(10) | Product reference |
| description | TEXT | Product description |
| quantity | INT(10) | Quantity |
| user_id | INT(10) | User reference |
| created_at | TIMESTAMP | Creation date |

### 5. `orders` - Customer Orders
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| first_name | VARCHAR(200) | Customer first name |
| last_name | VARCHAR(200) | Customer last name |
| state | VARCHAR(200) | State/Country |
| street_address | VARCHAR(200) | Street address |
| town | VARCHAR(200) | Town/City |
| zip_code | VARCHAR(20) | Postal code |
| phone | VARCHAR(20) | Phone number |
| user_id | INT(10) | User reference |
| status | VARCHAR(200) | Order status |
| total_price | INT(10) | Total price |
| created_at | TIMESTAMP | Creation date |

### 6. `bookings` - Table Reservations
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| first_name | VARCHAR(200) | Customer first name |
| last_name | VARCHAR(200) | Customer last name |
| date | VARCHAR(200) | Booking date |
| time | VARCHAR(200) | Booking time |
| phone | VARCHAR(100) | Phone number |
| message | TEXT | Special requests |
| status | VARCHAR(200) | Status (Pending/Confirmed/Done) |
| user_id | INT(7) | User reference |
| created_at | TIMESTAMP | Creation date |

### 7. `reviews` - Customer Reviews
| Column | Type | Description |
|--------|------|-------------|
| id | INT(10) | Primary key |
| review | VARCHAR(200) | Review text |
| username | VARCHAR(200) | Reviewer username |
| created_at | TIMESTAMP | Creation date |

---

## Features

### Customer Features

| Feature | Description |
|---------|-------------|
| **User Registration** | Create account with username, email, password |
| **User Login/Logout** | Secure session-based authentication |
| **Browse Menu** | View drinks and desserts with images and prices |
| **Product Details** | View individual product with related items |
| **Shopping Cart** | Add products, view cart, remove items |
| **Checkout** | Complete order with billing details |
| **Table Booking** | Reserve tables with date, time, and message |
| **View Orders** | Track order history and status |
| **View Bookings** | Track booking history and status |
| **Write Reviews** | Submit reviews after order delivery or booking completion |

### Admin Features

| Feature | Description |
|---------|-------------|
| **Dashboard** | View statistics (products, orders, bookings, admins count) |
| **Product Management** | Create, view, delete products with image upload |
| **Order Management** | View orders, update status, delete orders |
| **Booking Management** | View bookings, update status, delete bookings |
| **Admin Management** | View admins, create new admin accounts |

---

## Installation Guide

### Prerequisites

- PHP 8.0 or higher
- MySQL 5.7+ or MariaDB 10.4+
- Apache Web Server (with mod_rewrite)
- Laragon, XAMPP, WAMP, or similar local development environment

### Step-by-Step Installation

1. **Clone or Download** the project to your web server directory:
   ```
   C:\laragon\www\coffee-blend\
   ```

2. **Create Database**:
   - Open phpMyAdmin or MySQL client
   - Create a new database named `coffee-blend` (or your preferred name)

3. **Import Database Schema**:
   ```sql
   -- Import the SQL file
   SOURCE SQL_FILE/coffee-blend.sql;
   ```
   Or use phpMyAdmin to import `SQL_FILE/coffee-blend.sql`

4. **Configure Database Connection**:
   Edit `config/config.php`:
   ```php
   define("HOST", "localhost");
   define("DBNAME", "coffee-blend");  // Your database name
   define("USER", "root");            // Your MySQL username
   define("PASS", "");                // Your MySQL password
   ```

5. **Configure URLs**:
   Edit `includes/header.php`:
   ```php
   define("APPURL", "http://localhost/coffee-blend");
   define("IMAGEPRODUCTS", "http://localhost/coffee-blend/admin-panel/products-admins/images");
   ```

   Edit `admin-panel/layouts/header.php`:
   ```php
   define("ADMINURL", "http://localhost/coffee-blend/admin-panel");
   ```

6. **Access the Application**:
   - Frontend: `http://localhost/coffee-blend/`
   - Admin Panel: `http://localhost/coffee-blend/admin-panel/`

---

## Configuration

### Database Configuration (`config/config.php`)

```php
<?php
try {
    define("HOST", "localhost");     // Database host
    define("DBNAME", "coffee-blend"); // Database name
    define("USER", "root");          // Database username
    define("PASS", "");              // Database password

    $conn = new PDO("mysql:host=".HOST.";dbname=".DBNAME."", USER, PASS);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $Exception) {
    echo $Exception->getMessage();
}
```

### URL Constants

| Constant | Location | Purpose |
|----------|----------|---------|
| `APPURL` | `includes/header.php` | Base URL for frontend |
| `IMAGEPRODUCTS` | `includes/header.php` | Product images URL |
| `ADMINURL` | `admin-panel/layouts/header.php` | Admin panel base URL |

---

## User Guide

### Registration

1. Navigate to the website
2. Click "Register" in the navigation
3. Enter username, email, and password
4. Click "Register" button

### Login

1. Click "Login" in the navigation
2. Enter email and password
3. Click "Login" button

### Browsing Menu

1. Click "Menu" in the navigation
2. View drinks and desserts sections
3. Click on a product to view details

### Adding to Cart

1. View a product's detail page
2. Select quantity
3. Click "Add to Cart"

### Checkout Process

1. Click the cart icon in navigation
2. Review cart items
3. Click "Proceed to Checkout"
4. Fill in billing details
5. Complete payment

### Table Booking

1. Find the booking form on homepage or menu page
2. Enter name, date, time, phone, and message
3. Click "Book Table" (must be logged in)

### Viewing Orders & Bookings

1. Click your username dropdown in navigation
2. Select "Your Orders" or "Your Bookings"
3. View status and history

### Writing Reviews

1. After an order is "Delivered" or booking is "Done"
2. Click "Write Review" button
3. Enter your review
4. Submit

---

## Admin Panel Guide

### Accessing Admin Panel

- URL: `http://localhost/coffee-blend/admin-panel/`
- Default Admin Credentials (from sample data):
  - Email: `admin.first@gmail.com`
  - Password: (hashed in database - set during creation)

### Dashboard

Displays quick statistics:
- Total Products
- Total Orders
- Total Bookings
- Total Admins

### Managing Products

1. Navigate to "Products" in sidebar
2. **View Products**: See all products with images, prices, types
3. **Create Product**: Click "Create Products" button
   - Enter name, price, description
   - Upload image
   - Select type (drink/dessert)
4. **Delete Product**: Click "Delete" button on product row

### Managing Orders

1. Navigate to "Orders" in sidebar
2. View all orders with details
3. **Update Status**: Click "Update" to change status (Pending/Delivered)
4. **Delete Order**: Click "Delete" button

### Managing Bookings

1. Navigate to "Bookings" in sidebar
2. View all table reservations
3. **Update Status**: Click "Update" to change status (Pending/Confirmed/Done)
4. **Delete Booking**: Click "Delete" button

### Managing Admins

1. Navigate to "Admins" in sidebar
2. View all admin accounts
3. **Create Admin**: Click "Create Admin" button
   - Enter admin name, email, password

---

## Security Considerations

### Current Security Measures

- **Password Hashing**: Uses `password_hash()` with `PASSWORD_DEFAULT` (bcrypt)
- **Session-Based Authentication**: Separate sessions for users and admins
- **Access Control**: Protected pages check session variables
- **HTTP Referer Check**: Some pages validate referrer to prevent direct access

### Security Recommendations

> ⚠️ **Important**: This is a learning/demo project. For production use, consider:

1. **SQL Injection Prevention**
   - Use prepared statements consistently (some queries use direct variable interpolation)
   - Example fix:
     ```php
     // Instead of:
     $login = $conn->query("SELECT * FROM users WHERE email='$email'");
     
     // Use:
     $login = $conn->prepare("SELECT * FROM users WHERE email=:email");
     $login->execute([':email' => $email]);
     ```

2. **XSS Prevention**
   - Escape output with `htmlspecialchars()`
   - Example:
     ```php
     <?php echo htmlspecialchars($product->name); ?>
     ```

3. **CSRF Protection**
   - Add CSRF tokens to forms
   
4. **Input Validation**
   - Validate and sanitize all user inputs
   - Validate file uploads (type, size, name)

5. **HTTPS**
   - Use HTTPS in production

6. **Error Handling**
   - Disable error display in production
   - Log errors instead of displaying

---

## File Reference

### Core Files

| File | Purpose |
|------|---------|
| `index.php` | Homepage with slider, info, booking form, products, reviews |
| `menu.php` | Full menu with drinks and desserts |
| `about.php` | About page |
| `contact.php` | Contact information |
| `services.php` | Services offered |
| `404.php` | 404 Error page |

### Authentication Files

| File | Purpose |
|------|---------|
| `auth/login.php` | User login form and processing |
| `auth/register.php` | User registration form and processing |
| `auth/logout.php` | User logout (session destroy) |

### Product & Cart Files

| File | Purpose |
|------|---------|
| `products/product-single.php` | Single product view, add to cart |
| `products/cart.php` | Shopping cart display |
| `products/checkout.php` | Checkout form with billing details |
| `products/pay.php` | Payment processing |
| `products/delete-product.php` | Remove item from cart |

### Booking & Review Files

| File | Purpose |
|------|---------|
| `booking/book.php` | Table reservation processing |
| `reviews/write-review.php` | Submit customer review |

### User Dashboard Files

| File | Purpose |
|------|---------|
| `users/bookings.php` | View user's bookings |
| `users/Orders.php` | View user's orders |

### Admin Panel Files

| File | Purpose |
|------|---------|
| `admin-panel/index.php` | Admin dashboard with statistics |
| `admin-panel/admins/login-admins.php` | Admin login |
| `admin-panel/admins/logout.php` | Admin logout |
| `admin-panel/admins/admins.php` | List admins |
| `admin-panel/admins/create-admins.php` | Create admin |
| `admin-panel/products-admins/show-products.php` | List products |
| `admin-panel/products-admins/create-products.php` | Add product |
| `admin-panel/products-admins/delete-products.php` | Delete product |
| `admin-panel/orders-admins/show-orders.php` | List orders |
| `admin-panel/orders-admins/change-status.php` | Update order status |
| `admin-panel/orders-admins/delete-orders.php` | Delete order |
| `admin-panel/bookings-admins/show-bookings.php` | List bookings |
| `admin-panel/bookings-admins/change-status.php` | Update booking status |
| `admin-panel/bookings-admins/delete-bookings.php` | Delete booking |

### Include Files

| File | Purpose |
|------|---------|
| `includes/header.php` | Site header, navigation, CSS links |
| `includes/footer.php` | Site footer, JS scripts |
| `admin-panel/layouts/header.php` | Admin header, navigation |
| `admin-panel/layouts/footer.php` | Admin footer |

---

## Session Variables

### User Session

| Variable | Description |
|----------|-------------|
| `$_SESSION['username']` | Logged-in user's username |
| `$_SESSION['email']` | Logged-in user's email |
| `$_SESSION['user_id']` | Logged-in user's ID |
| `$_SESSION['total_price']` | Cart total for checkout |

### Admin Session

| Variable | Description |
|----------|-------------|
| `$_SESSION['admin_name']` | Logged-in admin's name |
| `$_SESSION['email']` | Logged-in admin's email |
| `$_SESSION['admin_id']` | Logged-in admin's ID |

---

## Order & Booking Statuses

### Order Status

| Status | Description |
|--------|-------------|
| Pending | Order placed, awaiting processing |
| Delivered | Order has been delivered |

### Booking Status

| Status | Description |
|--------|-------------|
| Pending | Booking submitted, awaiting confirmation |
| Confirmed | Booking confirmed |
| Done | Booking completed |

---

## Credits

- **Template**: Colorlib Coffee Template (Bootstrap 4)
- **Icons**: Ionicons, Flaticon, IcoMoon, Open Iconic
- **Fonts**: Google Fonts (Poppins, Josefin Sans, Great Vibes)
- **Libraries**: jQuery, Owl Carousel, AOS, Magnific Popup, Bootstrap Datepicker

---

## License

This project is for educational and demonstration purposes.

---

*Documentation generated: January 2026*
