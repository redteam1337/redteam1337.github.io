<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Record Payment</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #333;
            color: white;
            padding: 10px 20px;
            width: 100%;
        }

        .logo {
            width: 150px;
            height: auto;
            cursor: pointer;
            transition: transform 0.3s ease-in-out;
        }

        #store-logo:hover {
            transform: scale(1.1);
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
            max-width: 600px;
            width: 100%;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 20px;
        }

        h1 {
            color: #333;
        }

        .card {
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .form-group {
            margin-bottom: 15px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }

        .form-group textarea {
            resize: vertical;
        }

        .form-group small {
            display: block;
            margin-top: 5px;
            color: #666;
        }

        .form-actions {
            display: flex;
            justify-content: space-between;
        }

        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }

        .save-btn {
            background-color: #007bff;
            color: #fff;
        }

        .save-btn:hover {
            background-color: #0056b3;
        }

        .cancel-btn {
            background-color: #f44336;
            color: #fff;
        }

        .cancel-btn:hover {
            background-color: #c82333;
        }

        #proof-preview {
            margin-top: 10px;
            max-width: 100%;
            height: auto;
            border-radius: 5px;
            box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
        }

        .modal {
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

        .modal-content {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
            text-align: center;
        }

        .close-btn {
            float: right;
            font-size: 24px;
            cursor: pointer;
        }

        .help-icon {
position: absolute;
top: 50%;
right: 10px;
transform: translateY(-50%);
background-color: #007bff;
color: #fff;
border-radius: 50%;
width: 20px;
height: 20px;
display: flex;
justify-content: center;
align-items: center;
cursor: pointer;
font-size: 14px;
}
    </style>
</head>

<body>
    <nav class="navbar"> 
        <img class="logo" style="margin-left: 10px;" id="store-logo" src="../store/logo.webp" alt="Store Logo">
        <h1 style="color: white;">AOD ZAIZA</h1>
        <ul class="nav-links">
            <li><a href="../backend/ManagementDashboard.php">Home</a></li>
            <li><a href="../backend/add_new_item.php">Insert</a></li>
            <li><a href="../backend/order.php">Orders</a></li>
            <li><a href="../backend/date.php">Add Date</a></li>
            <li><a href="../backend/show_date.php">Show Data</a></li>
            <li><a href="../backend/insert_debtor.php">Insert Debtor</a></li>
            <li><a href="../backend/Record_Payment.php">Insert Payment</a></li>
        </ul>
    </nav>
    <div class="container">
        <header>
            <h1>Record Payment</h1>
        </header>
        <div class="card">
            <form id="payment-form" method="post" action="">
                <div class="form-group"> <label for="debtor">Select Debtor:</label> <select id="debtor" name="debtor" required> <?php foreach (get_debtor() as $key => $value) : ?> <option value="<?= $value ?>"><?= $value ?></option> <?php endforeach; ?> </select> <span class="help-icon" title="Choose the debtor from the list.">?</span> </div>
                <div class="form-group"> <label for="date">Payment Date:</label> <input type="date" id="date" name="date" required> <span class="help-icon" title="Select the date when the payment was made.">?</span> </div>
                <div class="form-group"> <label for="amount">Amount Paid:</label> <input type="number" id="amount" name="amount" required> <small>Enter the total amount paid by the debtor.</small> <span class="help-icon" title="Enter the payment amount.">?</span> </div>
                <div class="form-group"> <label for="currency">Currency:</label> <select id="currency" name="currency" required>
                        <option value="USD">USD</option>
                        <option value="SAR">SAR</option>
                        <option value="YEM">YEM</option>
                    </select> <span class="help-icon" title="Select the currency of the payment.">?</span> </div>
                <div class="form-group"> <label for="method">Payment Method:</label> <select id="method" name="method" required>
                        <option value="cash">Cash</option>
                        <option value="bank_transfer">Bank Transfer</option>
                    </select> <span class="help-icon" title="Select the payment method.">?</span> </div>
                <div class="form-group"> <label for="notice">Notice:</label> <textarea id="notice" name="notice" placeholder="Enter any additional remarks..."></textarea> <span class="help-icon" title="Add any notes or remarks related to the payment.">?</span> </div>
                <div class="form-group"> <label for="proof">Upload Proof of Payment:</label> <input type="file" id="proof" name="image_URL" accept="image/*" required> <img id="proof-preview" src="#" alt="Proof of Payment Preview" style="display: none;"> <span class="help-icon" title="Attach an image or receipt as proof of payment.">?</span> </div>
                <div class="form-actions"> <button type="submit" id="submit" name="submit" class="btn save-btn">Save Payment</button> <button type="reset" class="btn cancel-btn">Cancel</button> </div>
            </form>
        </div>
        <div id="confirmation-modal" class="modal">
            <div class="modal-content"> <span class="close-btn">&times;</span>
                <p>Payment recorded successfully!</p>
            </div>
        </div>
    </div>
    <script>
        document.getElementById('proof').addEventListener('change', function(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const proofPreview = document.getElementById('proof-preview');
                    proofPreview.src = e.target.result;
                    proofPreview.style.display = 'block';
                };
                reader.readAsDataURL(file);
            }
        });

        document.getElementById('payment-form').addEventListener('submit', function(event) {
            // event.preventDefault();
            // Perform form validation and submission logic here

            // Show confirmation modal
            const modal = document.getElementById('confirmation-modal');
            modal.style.display = 'flex';
        });

        document.querySelector('.close-btn').addEventListener('click', function() {
            const modal = document.getElementById('confirmation-modal');
            modal.style.display = 'none';
        });
        document.addEventListener('DOMContentLoaded', function() {
            // Set default date to today's date
            const dateInput = document.getElementById('date');
            const today = new Date().toISOString().split('T')[0];
            dateInput.value = today;
        });

        // let submit = document.getElementById('submit');
        // submit.onclick = () => {

        //     let debtor = document.getElementById('debtor').value;
        //     let date = document.getElementById('date').value;
        //     let currency = document.getElementById('currency').value;
        //     let method = document.getElementById('method').value;
        //     let notice = document.getElementById('notice').value;

        //     const senditems = new XMLHttpRequest();
        //     senditems.open('post', '../frontend/test.php');
        //     senditems.onreadystatechange = function() {

        //         if (this.status == 200 && this.readyState == 4) {
        //             console.log(this.responseText);
        //         }

        //     }
        //     const data = JSON.stringify({
        //         debtors: debtor
        //     })
        //     senditems.send(data);
        // }
    </script>
</body>

</html>
