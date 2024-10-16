# E_Commerce
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-commerce Website</title>
    <style>
        /* CSS Styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 15px 0;
        }
        nav a {
            color: white;
            margin: 0 15px;
            text-decoration: none;
        }
        h1, h2 {
            text-align: center;
        }
        .product-list {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px;
        }
        .product-item {
            background-color: white;
            border: 1px solid #ddd;
            padding: 15px;
            text-align: center;
        }
        .product-item img {
            max-width: 150px;
        }
        footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 10px;
            position: fixed;
            bottom: 0;
            width: 100%;
        }
        #cart-items {
            margin: 20px;
            text-align: center;
        }
        #cart-items p {
            margin: 10px 0;
        }
        button {
            padding: 10px 20px;
            margin: 10px;
            cursor: pointer;
            background-color: #333;
            color: white;
            border: none;
        }
        button:hover {
            background-color: #555;
        }
    </style>
</head>
<body>
    <!-- HTML Content -->
    <header>
        <h1>E-commerce Website</h1>
        <nav>
            <a href="#" onclick="showProducts()">Home</a>
            <a href="#" onclick="showCart()">Cart</a>
        </nav>
    </header>

    <main id="content">
        <!-- Dynamic Content will be inserted here -->
    </main>

    <footer>
        <p>© 2024 E-commerce Website</p>
    </footer>

    <script>
        // JavaScript: Product Database
        const products = [
            { id: 1, name: "Product 1", price: 100, image: "https://via.placeholder.com/150" },
            { id: 2, name: "Product 2", price: 150, image: "https://via.placeholder.com/150" },
        ];

        // Function to display the product list
        function showProducts() {
            const content = document.getElementById("content");
            content.innerHTML = `
                <h2>Products</h2>
                <div class="product-list">
                    ${products.map(product => `
                        <div class="product-item" data-id="${product.id}">
                            <img src="${product.image}" alt="${product.name}">
                            <h3>${product.name}</h3>
                            <p>Price: $${product.price}</p>
                            <button onclick="viewProduct(${product.id})">View Details</button>
                            <button onclick="addToCart(${product.id})">Add to Cart</button>
                        </div>
                    `).join('')}
                </div>
            `;
        }

        // Function to display product details
        function viewProduct(productId) {
            const product = products.find(p => p.id === productId);
            const content = document.getElementById("content");
            content.innerHTML = `
                <div id="product-detail">
                    <img src="${product.image}" alt="${product.name}">
                    <h2>${product.name}</h2>
                    <p>Price: $${product.price}</p>
                    <button onclick="addToCart(${product.id})">Add to Cart</button>
                    <button onclick="showProducts()">Back to Products</button>
                </div>
            `;
        }

        // Cart functionality
        function addToCart(productId) {
            let cart = JSON.parse(localStorage.getItem("cart")) || [];
            const product = products.find(p => p.id === productId);
            cart.push(product);
            localStorage.setItem("cart", JSON.stringify(cart));
            alert("Product added to cart!");
        }

        // Function to show the cart
        function showCart() {
            const cart = JSON.parse(localStorage.getItem("cart")) || [];
            let total = 0;
            const content = document.getElementById("content");

            if (cart.length === 0) {
                content.innerHTML = <h2>Your Cart is Empty</h2>;
                return;
            }

            content.innerHTML = `
                <h2>Your Cart</h2>
                <div id="cart-items">
                    ${cart.map(item => {
                        total += item.price;
                        return <p>${item.name} - $${item.price}</p>;
                    }).join('')}
                </div>
                <p>Total: $${total}</p>
                <button onclick="checkout()">Checkout</button>
                <button onclick="clearCart()">Clear Cart</button>
            `;
        }

        // Checkout function
        function checkout() {
            alert("Checkout Successful!");
            clearCart();
        }

        // Function to clear the cart
        function clearCart() {
            localStorage.removeItem("cart");
            showCart();
        }

        // Show products on page load
        window.onload = showProducts;
    </script>
</body>
</html>
