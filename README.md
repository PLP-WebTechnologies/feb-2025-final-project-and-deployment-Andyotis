#!/bin/ksh

# Define product information with prices in Kenyan Shillings (KES)
product1_name="Product 1"
product1_price="KES 2,000"
product1_image="https://via.placeholder.com/200"

product2_name="Product 2"
product2_price="KES 3,500"
product2_image="https://via.placeholder.com/200"

product3_name="Product 3"
product3_price="KES 4,800"
product3_image="https://via.placeholder.com/200"

# Generate the HTML dynamically with Ksh variables
cat << EOF > ecommerce_page.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>My E-Commerce Store</title>
    <style>
        /* Basic CSS Styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
        }

        header, footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 1em;
        }

        header {
            position: sticky;
            top: 0;
            z-index: 100;
        }

        main {
            padding: 20px;
        }

        .product {
            border: 1px solid #ddd;
            padding: 15px;
            margin: 10px;
            text-align: center;
            background-color: white;
        }

        .product img {
            max-width: 100%;
            height: auto;
        }

        .product h3 {
            margin-top: 10px;
            color: #333;
        }

        .product button {
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .product button:hover {
            background-color: #0056b3;
        }

        .cart {
            margin-top: 20px;
            padding: 10px;
            background-color: #eee;
        }

        .cart h2 {
            margin: 0;
        }

        .cart ul {
            list-style-type: none;
            padding: 0;
        }

        .cart ul li {
            padding: 5px 0;
        }

        .cart button {
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
        }

        .cart button:hover {
            background-color: #218838;
        }

        /* Responsive Design */
        @media (max-width: 600px) {
            .product {
                width: 100%;
                box-sizing: border-box;
            }
        }
    </style>
</head>
<body>

<header>
    <h1>Welcome to My E-Commerce Store</h1>
</header>

<main>
    <section id="product-list">
        <h2>Our Products</h2>
        <div class="product" data-id="1">
            <img src="$product1_image" alt="Product 1">
            <h3>$product1_name</h3>
            <p>$product1_price</p>
            <button class="add-to-cart-btn">Add to Cart</button>
        </div>
        <div class="product" data-id="2">
            <img src="$product2_image" alt="Product 2">
            <h3>$product2_name</h3>
            <p>$product2_price</p>
            <button class="add-to-cart-btn">Add to Cart</button>
        </div>
        <div class="product" data-id="3">
            <img src="$product3_image" alt="Product 3">
            <h3>$product3_name</h3>
            <p>$product3_price</p>
            <button class="add-to-cart-btn">Add to Cart</button>
        </div>
    </section>

    <section class="cart">
        <h2>Your Cart</h2>
        <ul id="cart-items"></ul>
        <button id="checkout-btn">Checkout</button>
    </section>
</main>

<footer>
    <p>&copy; 2025 My E-Commerce Store | <a href="#">Privacy Policy</a> | <a href="#">Terms of Service</a></p>
</footer>

<script>
    // JavaScript to handle cart functionality
    const addToCartButtons = document.querySelectorAll('.add-to-cart-btn');
    const cartItemsList = document.getElementById('cart-items');

    const cart = [];

    addToCartButtons.forEach(button => {
        button.addEventListener('click', function() {
            const productElement = this.parentElement;
            const productId = productElement.getAttribute('data-id');
            const productName = productElement.querySelector('h3').textContent;
            const productPrice = productElement.querySelector('p').textContent;
            
            // Add item to cart array
            cart.push({ id: productId, name: productName, price: productPrice });
            updateCart();
        });
    });

    // Update the cart display
    function updateCart() {
        cartItemsList.innerHTML = ''; // Clear the cart list

        // Loop through each item in the cart and display it
        cart.forEach(item => {
            const li = document.createElement('li');
            li.textContent = `${item.name} - ${item.price}`;
            cartItemsList.appendChild(li);
        });
    }

    // Checkout button functionality
    document.getElementById('checkout-btn').addEventListener('click', function() {
        if (cart.length === 0) {
            alert('Your cart is empty!');
        } else {
            alert('Proceeding to checkout...');
            // Ideally, integrate checkout system or page here
        }
    });
</script>

</body>
</html>
EOF

echo "E-commerce page has been generated: ecommerce_page.html"
