

<head>
    <style>
    body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #333;
            color: white;
            padding: 10px 20px;
            margin-bottom: 15px;
        }

        .logo {
            width: 150px;
            /* Adjust the size as needed */
            height: auto;
            /* Maintain aspect ratio */
            cursor: pointer;
            transition: transform 0.3s ease-in-out;
        }

        #store-logo:hover {
            transform: scale(1.1);
            /* Slightly enlarge on hover */
        }

        .popup-content img#enlarged-logo:hover {
            transform: scale(1.05);
            /* Slightly enlarge on hover */
        }

        .logo-popup {
            display: none;
            position: fixed;
            top: 100px;
            left: 0;
            width: 100%;
            /* height: 50%; */
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }

        .popup-content {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            height: 400px;

            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            animation: popupAnimation 0.3s ease-in-out;
        }

        @keyframes popupAnimation {
            from {
                transform: scale(0.5);
                opacity: 0;
            }

            to {
                transform: scale(1);
                opacity: 1;
            }
        }

        #enlarged-logo {
            width: 200%;
            height: 100%;
            margin-bottom: 20px;
            transition: transform 0.3s ease-in-out;
        }

        #enlarged-logo:hover {
            transform: scale(1.05);
        }

        .close-logo-btn {
            display: inline-block;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            background-color: #dc3545;
            color: white;
            transition: background-color 0.3s ease-in-out;
        }

        .close-logo-btn:hover {
            background-color: #c82333;
        }


        .nav-links {
            list-style: none;
            display: flex;
            gap: 20px;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            font-size: 1em;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .summary {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }

        .order-header,
        .order {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }

        .order-header {
            font-weight: bold;
            background-color: #f9f9f9;
        }

        .order img {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 8px;
        }

        .order-number,
        .product-name,
        .price-to-pay,
        .price-paid {
            flex: 1;
            text-align: center;
        }

        .price-paid.green {
            color: #28a745;
        }

        .price-paid.red {
            color: #dc3545;
        }

        .price-paid.black {
            color: #000000;
        }

        .delete-btn {
            background-color: #ff4d4d;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
        }

        .delete-btn:hover {
            background-color: #cc0000;
        }

        @media (max-width: 600px) {

            .order-header,
            .order {
                flex-direction: column;
                align-items: flex-start;
            }

            .order img {
                margin-bottom: 10px;
            }

            .order-number,
            .product-name,
            .price-to-pay,
            .price-paid {
                text-align: left;
            }
        }
    </style>
</head>

<body>
<nav class="navbar">
            <img class="logo" id="store-logo" src="../store/logo.webp" alt="test">
            <h1 style="color: white; margin: 0 20px;">AOD ZAIZA</h1>
            <!-- <div class="logo" id="store-logo">Store Logo</div> -->
            <ul class="nav-links">
                <li><a href="../backend/ManagementDashboard.php">Home</a></li>
                <li><a href="../backend/add_new_item.php">insert</a></li>
                <li><a href="../backend/order.php">Orders</a></li>
                <li><a href="../backend/date.php">add dete</a></li>
                <li><a href="../backend/show_date.php">show data</a></li>
                <li><a href="../backend/insert_debtor.php">insert debtor</a></li>
                <li><a href="../backend/Record_Payment.php">insert payment</a></li>
            </ul>
        </nav>

    <div class="container">
        <div class="summary">
            <div>Total Orders: <?=get_total_order_num()?></div>
            <div>Expected Paid: $160.00</div>
            <div>Total Amount to be Paid: <?= get_total_many(); ?></div>
        </div>
        <div class="order-header">
            <div>Image</div>
            <div>Order #</div>
            <div>Product Name</div>
            <div>Price to Pay</div>
            <div>Paid Price</div>
            <div>Delete</div>
        </div>
        <?php foreach ($item as $key => $value) :
        ?>
            <div class="order">
                <img src="https://via.placeholder.com/100" alt="Product Image">
                <div class="order-number">#<?= $value->order_id ?></div>
                <div class="product-name"><?= $value->name ?></div>
                <div class="price-to-pay" id="1"><?= $value->sale_price ?></div>
                <div class="price-paid"><?= $value->payed_price ?></div>
                <button class="delete-btn">X</button>
            </div>
        <?php endforeach; ?>
    </div>

    <script>
        const value1Elements = document.querySelectorAll('.price-to-pay');
        const value2Elements = document.querySelectorAll('.price-paid');
        value1Elements.forEach((div1, index) => {
            const div2 = value2Elements[index];
            const value1 = parseFloat(div1.textContent);
            const value2 = parseFloat(div2.textContent);
            if (value1 > value2) {
                div2.classList.add('red');
            } else if (value1 < value2) {
                div2.classList.add('green');
            } else {
                div2.classList.add('black');
            }
        });
    </script>
</body>

</html>
