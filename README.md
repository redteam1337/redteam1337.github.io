    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Store Management Dashboard</title>
        <link rel="stylesheet" href="styles.css">
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

        .pl-section {
            display: flex;
            justify-content: space-around;
            padding: 20px;
            background-color: #fff;
        }

        .pl-box {
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 1.2em;
        }

        .profit {
            background-color: #d4edda;
            color: #155724;
        }

        .expected-profit {
            background-color: #fff3cd;
            color: #856404;
        }

        .loss {
            background-color: #f8d7da;
            color: #721c24;
        }

        .form-container {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        .currency-input {
            width: 50%;
            margin: 10px 0;
            padding: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .currency-input:focus {
            border-color: #007bff;
            box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
            outline: none;
        }

        label {
            display: block;
            margin: 10px 0 5px;
            font-size: 1em;
            color: #333;
        }

        .current-price {
            margin-top: 5px;
            font-size: 0.9em;
            color: #555;
        }

        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            padding: 20px;
            margin-bottom: 100px;
        }

        .product-card {
            background-color: #fff;
            padding: 10px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        .product-card img {
            max-width: 100%;
            border-radius: 5px;
        }

        .buy-btn,
        .details-btn {
            display: block;
            width: 80%;
            margin: 10px auto;
            padding: 10px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
        }

        .buy-btn {
            background-color: #28a745;
            color: white;
        }

        /* Alert Popup Styles */
        .alert-popup {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .alert-popup .popup-content {
            background-color: #fff;
            padding: 20px 30px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            animation: popupAnimation 0.3s ease-in-out;
            max-width: 400px;
            width: 80%;
        }

        .alert-popup .popup-content p {
            font-size: 1.2em;
            color: #28a745;
            margin-bottom: 20px;
        }

        .popup-content-alert {
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            text-align: center
        }

        .alert-popup .close-alert-btn {
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

        .alert-popup .close-alert-btn:hover {
            background-color: #c82333;
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


        .details-btn {
            background-color: #6c757d;
            color: white;
        }

        .footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 10px 0;
            position: fixed;
            width: 100%;
            bottom: 0;
        }

        /* Existing styles... */

        .popup {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }

        .popup-content {
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            text-align: center;
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

        #store-logo {
            cursor: pointer;
        }

        #enlarged-logo {
            max-width: 80%;
            max-height: 80%;
        }

        .close-logo-btn {
            display: block;
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            background-color: #dc3545;
            color: white;
        }


        .popup img {
            max-width: 100%;
            width: 220px;
            border-radius: 5px;
            height: 220px;
            display: block;
            position: relative;
            left: 25%;
        }

        .popup-content {
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            text-align: center;
        }

        /* Existing styles... */

        .popup-content input[type="text"] {
            width: 80%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .popup-content input[type="text"]:focus {
            border-color: #007bff;
            box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
            outline: none;
        }

        .currency-select {
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .currency-select:focus {
            border-color: #007bff;
            box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
            outline: none;
        }

        .submit-btn,
        .close-btn,
        .close-reject {
            display: block;
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
        }

        .submit-btn {
            background-color: #007bff;
            color: white;
        }

        .close-btn {
            background-color: #dc3545;
            color: white;
        }

        .close-reject {
            background-color: #dc3545;
            color: white;
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

        <section class="pl-section">
            <div class="pl-box profit">Profit: $10,000</div>
            <div class="pl-box expected-profit">Expected Profit: $5,000</div>
            <div class="pl-box loss">Loss: $2,000</div>
        </section>
        <div class="form-container">
            <form action="" method="post">
                <label for="SAR">SAR</label>
                <input type="text" id="SAR" class="currency-input" name="SAR">
                <div class="current-price">Current Price: <?= $_SESSION['SAR'] ?></div>
                <label for="USD">USD</label>
                <input type="number" id="USD" class="currency-input" name="USD">
                <div class="current-price">Current Price: <?= $_SESSION['USD'] ?></div>
                <input type="submit" value="send" name='set_currncy'>
            </form>
        </div>
        <section class="product-grid">
            <?php foreach ($item as $key => $value) : ?>
                <div class="product-card" data-index="<?= $value->product_id ?>">
                    <img src="<?= $value->image_URL ?>" alt="Product 1">
                    <p style="background-color: #d4edda;color: #155724;padding: 10px 20px;border-radius: 5px;font-size: 1.2em;"><?php $reslut= intval($value->currency_YER) / intval($value->amount); echo $reslut;//to get how much the one will be?> YES</p>
                    <p style="background-color: #d4edda;color: #155724;padding: 10px 20px;border-radius: 5px;font-size: 1.2em;"><?= $value->sale_price ?> <?= $value->currency ?></p>
                    <button class="buy-btn">Buy</button>
                    <button class="details-btn">Details</button>
                </div>
            <?php endforeach; ?>
        </section>
        <footer class="footer">
            <p>Contact Info | Store Policies | Other Notes</p>
        </footer>

        <!-- Buy Popup -->
        <div class="popup buy-popup">
            <div class="popup-content">
                <img src="" alt="Product Image" id="popup-image">
                <p id="popup-price"></p>
                <form action="" method="post">
                    <input type="text" name="payed_price" placeholder="Enter currencies price" style="width: 50%;">
                    <input type="text" name="currency_price" placeholder="Enter price">
                    <input type="hidden" name="productID" value="" id="popup-productID">
                    <select class="currency-select" name="currency_type">
                        <option value="USD">USD</option>
                        <option value="EUR">SAR</option>
                        <option value="JPY">YER</option>
                        <!-- Add more currencies as needed -->
                    </select>
                    <input type="submit" class="submit-btn" name="submit_buy" value="Submit">
                </form>
                <button class="close-reject">Close</button>
            </div>
        </div>

        <!-- Details Popup -->
        <div class="popup details-popup">
            <div class="popup-content">
                <img src="" alt="Product 1" id="popup-image">
                <p>Product Name: Example</p>
                <p id="popup-productID">Description: This is a great product.</p>
                <p id="popup-price">Price: $100</p>
                <button class="close-btn">Close</button>
            </div>
        </div>
        <!-- Logo Popup -->
        <div class="logo-popup">
            <div class="popup-content">
                <img src="../store/logo.webp" alt="Store Logo" id="enlarged-logo">
                <button class="close-logo-btn">Close</button>
            </div>
        </div>
        <!-- Custom Alert Popup -->
        <div class="popup alert-popup">
            <div class="popup-content-alert">
                <p>Product added successfully</p>
                <button class="close-alert-btn">Close</button>
            </div>
        </div>

        <script>
            // Function to show the popup
            function showPopup(popup) {
                popup.style.display = 'flex';
            }

            // Function to hide the popup
            function hidePopup(popup) {
                popup.style.display = 'none';
            }

            // Event listeners for Buy buttons
            document.querySelectorAll('.buy-btn').forEach(button => {
                button.addEventListener('click', (event) => {
                    const productCard = event.target.closest('.product-card');
                    const index = productCard.dataset.index;
                    const popup = document.querySelector('.buy-popup');

                    // Update popup content
                    const imageSrc = productCard.querySelector('img').src;
                    const price = productCard.querySelector('p').textContent;
                    const productID = index; // Assuming index is used as productID

                    popup.querySelector('#popup-image').src = imageSrc;
                    popup.querySelector('#popup-price').textContent = `The price is: ${price}`;
                    popup.querySelector('#popup-productID').value = productID;

                    showPopup(popup);
                });
            });

            // Event listeners for Details buttons
            document.querySelectorAll('.details-btn').forEach(button => {
                button.addEventListener('click', (event) => {
                    const productCard = event.target.closest('.product-card');
                    const index = productCard.dataset.index;
                    const popup = document.querySelector('.details-popup');

                    // Update popup content
                    const imageSrc = productCard.querySelector('img').src;
                    const price = productCard.querySelector('p').textContent;
                    const productID = index; // Assuming index is used as productID

                    popup.querySelector('#popup-image').src = imageSrc;
                    popup.querySelector('#popup-price').textContent = `The price is: ${price}`;
                    popup.querySelector('#popup-productID').value = productID;

                    showPopup(popup);
                });
            });

            // Event listener for Submit button in Buy popup
            document.querySelector('.submit-btn').addEventListener('click', (event) => {
                // event.preventDefault(); // Prevent form submission
                showPopup(document.querySelector('.alert-popup'));
                hidePopup(document.querySelector('.buy-popup'));
            });

            // Event listener for Close button in Details popup
            document.querySelectorAll('.close-btn').forEach(button => {
                button.addEventListener('click', () => {
                    hidePopup(button.closest('.popup'));
                });
            });

            // Event listener for Close button in Buy popup
            document.querySelectorAll('.close-reject').forEach(button => {
                button.addEventListener('click', () => {
                    hidePopup(button.closest('.popup'));
                });
            });

            // Event listener for Store Logo
            document.getElementById('store-logo').addEventListener('click', () => {
                showPopup(document.querySelector('.logo-popup'));
            });

            // Event listener for Close button in Logo popup
            document.querySelectorAll('.close-logo-btn').forEach(button => {
                button.addEventListener('click', () => {
                    hidePopup(button.closest('.popup'));
                });
            });

            // Event listener for Close button in Alert popup
            document.querySelectorAll('.close-alert-btn').forEach(button => {
                button.addEventListener('click', () => {
                    hidePopup(button.closest('.popup'));
                });
            });
        </script>
</body>

