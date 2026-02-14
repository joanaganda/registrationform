<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title> Registration Form</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #f4f4f9; display: flex; justify-content: center; padding: 40px; }
        .form-card { 
            background: white; 
            padding: 25px; 
            width: 100%;
            max-width: 400px; 
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        h2 { margin-top: 0; color: #333; text-align: center; }
        
        .field { margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; font-size: 14px; font-weight: 600; color: #555; }
        input { 
            width: 100%; 
            padding: 10px; 
            border: 1px solid #ddd; 
            border-radius: 5px; 
            box-sizing: border-box; 
            font-size: 14px;
        }
        
    
        .name-row { display: flex; gap: 10px; }
        .name-row .field { flex: 1; }

        .error-msg { color: #d9534f; font-size: 12px; display: none; margin-top: 4px; }
        input.invalid { border-color: #d9534f; background-color: #fff8f8; }
        
        button { 
            width: 100%; 
            padding: 12px; 
            background: #007bff; 
            color: white; 
            border: none; 
            border-radius: 5px; 
            font-size: 16px; 
            cursor: pointer; 
            margin-top: 10px;
        }
        button:hover { background: #0056b3; }
    </style>
</head>
<body>

<div class="form-card">
    <h2>Registration Form</h2>
    <form id="regForm" novalidate>
        <div class="name-row">
            <div class="field">
                <label for="firstName">First Name</label>
                <input type="text" id="firstName" placeholder="Jane">
                <span class="error-msg">Required</span>
            </div>
            <div class="field">
                <label for="lastName">Last Name</label>
                <input type="text" id="lastName" placeholder="Doe">
                <span class="error-msg">Required</span>
            </div>
        </div>

        <div class="field">
            <label for="birthday">Birthday</label>
            <input type="date" id="birthday">
            <span class="error-msg">Must be at least 13 years old</span>
        </div>

        <div class="field">
            <label for="email">Email Address</label>
            <input type="email" id="email" placeholder="jane.doe@example.com">
            <span class="error-msg">Enter a valid email</span>
        </div>

        <button type="submit">Create Account</button>
    </form>
</div>

<script>
    const form = document.getElementById('regForm');

    form.addEventListener('submit', function(e) {
        e.preventDefault();

        // Elements
        const fName = document.getElementById('firstName');
        const lName = document.getElementById('lastName');
        const bday = document.getElementById('birthday');
        const email = document.getElementById('email');

        let isValid = true;

        // 1. Validate First Name
        if (fName.value.trim() === "") {
            showError(fName, true);
            isValid = false;
        } else {
            showError(fName, false);
        }

        // 2. Validate Last Name
        if (lName.value.trim() === "") {
            showError(lName, true);
            isValid = false;
        } else {
            showError(lName, false);
        }

        // 3. Validate Birthday (Age Logic)
        if (bday.value === "") {
            showError(bday, true);
            isValid = false;
        } else {
            const birthDate = new Date(bday.value);
            const today = new Date();
            let age = today.getFullYear() - birthDate.getFullYear();
            const monthDiff = today.getMonth() - birthDate.getMonth();
            
            if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
                age--;
            }

            if (age < 13) {
                showError(bday, true);
                isValid = false;
            } else {
                showError(bday, false);
            }
        }

        // 4. Validate Email
        if (!email.value.includes("@") || email.value.length < 5) {
            showError(email, true);
            isValid = false;
        } else {
            showError(email, false);
        }

        if (isValid) {
            alert("Success! Welcome, " + fName.value);
            form.reset();
        }
    });

    function showError(input, isError) {
        const msg = input.nextElementSibling;
        if (isError) {
            input.classList.add('invalid');
            msg.style.display = 'block';
        } else {
            input.classList.remove('invalid');
            msg.style.display = 'none';
        }
    }
</script>

</body>
</html>
