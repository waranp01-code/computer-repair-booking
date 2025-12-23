const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/AKfycby0oouUQTLE5urOoN9sR_3of4he2QgniwvC5Hcbb4pdmtGOzLHeY-VH3oHuY6IfNzI/exec";
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ICT Branch MPP - Mobile Repair Booking</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #3498db;
            --secondary: #2c3e50;
            --success: #2ecc71;
            --danger: #e74c3c;
            --warning: #f39c12;
            --light: #ecf0f1;
            --dark: #34495e;
        }
       
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
       
        body {
            background-color: #f5f7fa;
            color: var(--dark);
            line-height: 1.6;
            padding-bottom: 70px; /* Space for mobile nav */
        }
       
        .container {
            max-width: 100%;
            margin: 0 auto;
            padding: 15px;
        }
       
        header {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            padding: 1rem 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }
       
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 15px;
        }
       
        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 10px;
        }
       
        .logo i {
            font-size: 1.8rem;
        }
       
        .nav-tabs {
            display: none; /* Hidden on mobile, replaced by bottom nav */
        }
       
        .tab-content {
            display: none;
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
            box-shadow: 0 2px 15px rgba(0,0,0,0.05);
        }
       
        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }
       
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
       
        h2 {
            margin-bottom: 20px;
            color: var(--secondary);
            border-bottom: 2px solid var(--light);
            padding-bottom: 10px;
            font-size: 1.5rem;
        }
       
        .form-group {
            margin-bottom: 20px;
        }
       
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            font-size: 0.95rem;
        }
       
        input, select, textarea {
            width: 100%;
            padding: 14px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px; /* Prevents zoom on iOS */
            background-color: #f9f9f9;
            transition: border 0.3s;
        }
       
        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
            outline: none;
            background-color: white;
        }
       
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 16px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }
       
        button:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
       
        .btn-danger {
            background-color: var(--danger);
        }
       
        .btn-danger:hover {
            background-color: #c0392b;
        }
       
        .btn-success {
            background-color: var(--success);
        }
       
        .btn-success:hover {
            background-color: #27ae60;
        }
       
        .btn-secondary {
            background-color: var(--secondary);
        }
       
        .btn-secondary:hover {
            background-color: #1a252f;
        }
       
        .booking-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            border-left: 5px solid var(--primary);
        }
       
        .booking-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
       
        .booking-id {
            font-weight: bold;
            color: var(--primary);
            font-size: 1.1rem;
        }
       
        .booking-status {
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
        }
       
        .status-pending {
            background-color: #fff3cd;
            color: #856404;
        }
       
        .status-in-progress {
            background-color: #cce7ff;
            color: #004085;
        }
       
        .status-completed {
            background-color: #d4edda;
            color: #155724;
        }
       
        .status-cancelled {
            background-color: #f8d7da;
            color: #721c24;
        }
       
        .booking-details {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
            margin-bottom: 15px;
        }
       
        .detail-item strong {
            display: block;
            font-size: 12px;
            color: #7f8c8d;
            margin-bottom: 5px;
        }
       
        .booking-actions {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
       
        .booking-actions button {
            padding: 12px;
            font-size: 14px;
        }
       
        .admin-login {
            max-width: 100%;
            margin: 20px auto;
            padding: 25px;
            background: white;
            border-radius: 12px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.1);
        }
       
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-weight: 500;
        }
       
        .alert-success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
       
        .alert-danger {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
       
        .hidden {
            display: none;
        }
       
        .stats-cards {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 25px;
        }
       
        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
        }
       
        .stat-number {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--primary);
            margin: 10px 0;
        }
       
        .stat-label {
            color: #7f8c8d;
            font-size: 14px;
        }
       
        /* Mobile Bottom Navigation */
        .mobile-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: white;
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
            z-index: 100;
        }
       
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #7f8c8d;
            font-size: 12px;
            transition: all 0.3s;
        }
       
        .nav-item i {
            font-size: 1.2rem;
            margin-bottom: 5px;
        }
       
        .nav-item.active {
            color: var(--primary);
        }
       
        .nav-item.active i {
            transform: translateY(-2px);
        }
       
        /* Welcome Screen */
        .welcome-screen {
            text-align: center;
            padding: 30px 20px;
        }
       
        .welcome-icon {
            font-size: 4rem;
            color: var(--primary);
            margin-bottom: 20px;
        }
       
        .welcome-screen h1 {
            font-size: 1.8rem;
            margin-bottom: 15px;
            color: var(--secondary);
        }
       
        .welcome-screen p {
            color: #7f8c8d;
            margin-bottom: 30px;
            font-size: 1.1rem;
        }
       
        .action-buttons {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 30px;
        }
       
        /* Desktop Styles */
        @media (min-width: 768px) {
            .container {
                max-width: 750px;
                padding: 20px;
            }
           
            .nav-tabs {
                display: flex;
                gap: 10px;
            }
           
            .tab-btn {
                background: transparent;
                border: none;
                color: white;
                padding: 10px 15px;
                border-radius: 4px;
                cursor: pointer;
                transition: background 0.3s;
            }
           
            .tab-btn:hover {
                background: rgba(255,255,255,0.1);
            }
           
            .tab-btn.active {
                background: var(--primary);
            }
           
            .mobile-nav {
                display: none;
            }
           
            body {
                padding-bottom: 0;
            }
           
            .booking-details {
                grid-template-columns: repeat(2, 1fr);
            }
           
            .booking-actions {
                flex-direction: row;
            }
           
            .booking-actions button {
                width: auto;
                flex: 1;
            }
           
            .stats-cards {
                grid-template-columns: repeat(4, 1fr);
            }
           
            .action-buttons {
                flex-direction: row;
                justify-content: center;
            }
           
            .action-buttons button {
                width: auto;
                padding: 16px 30px;
            }
        }
       
        @media (min-width: 992px) {
            .container {
                max-width: 970px;
            }
           
            .booking-details {
                grid-template-columns: repeat(3, 1fr);
            }
        }
       
        @media (min-width: 1200px) {
            .container {
                max-width: 1140px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-laptop-medical"></i>
                    <span>ICT Branch MPP</span>
                </div>
                <div class="nav-tabs">
                    <button class="tab-btn active" data-tab="welcome">
                        <i class="fas fa-home"></i> Home
                    </button>
                    <button class="tab-btn" data-tab="customer">
                        <i class="fas fa-tools"></i> Book Repair
                    </button>
                    <button class="tab-btn" data-tab="admin">
                        <i class="fas fa-user-cog"></i> Admin
                    </button>
                </div>
            </div>
        </div>
    </header>

    <div class="container">
        <!-- Welcome Screen Tab -->
        <div id="welcome" class="tab-content active">
            <div class="welcome-screen">
                <div class="welcome-icon">
                    <i class="fas fa-laptop-medical"></i>
                </div>
                <h1>Computer Repair </h1>
                <p>Fast, reliable computer repair services at your fingertips. Book a repair appointment in just a few taps!</p>
               
                <div class="action-buttons">
                    <button class="btn-success" data-tab="customer">
                        <i class="fas fa-tools"></i> Book a Repair
                    </button>
                    <button class="btn-secondary" data-tab="admin">
                        <i class="fas fa-user-cog"></i> Admin Login
                    </button>
                </div>
            </div>
        </div>

        <!-- Customer Booking Tab -->
        <div id="customer" class="tab-content">
            <h2><i class="fas fa-tools"></i> Book a Computer Repair</h2>
            <div id="customer-alert" class="alert hidden"></div>
            <form id="booking-form">
                <div class="form-group">
                    <label for="customer-name"><i class="fas fa-user"></i> Full Name</label>
                    <input type="text" id="customer-name" required placeholder="Enter your full name">
                </div>
               
                <div class="form-group">
                    <label for="customer-email"><i class="fas fa-envelope"></i> Email</label>
                    <input type="email" id="customer-email" required placeholder="Enter your email address">
                </div>
               
                <div class="form-group">
                    <label for="customer-phone"><i class="fas fa-phone"></i> Phone Number</label>
                    <input type="tel" id="customer-phone" required placeholder="Enter your phone number">
                </div>
               
                <div class="form-group">
                    <label for="device-type"><i class="fas fa-laptop"></i> Device Type</label>
                    <select id="device-type" required>
                        <option value="">Select Device Type</option>
                        <option value="Laptop">Laptop</option>
                        <option value="Desktop">Desktop</option>
                        <option value="MacBook">MacBook</option>
                        <option value="iMac">iMac</option>
                        <option value="Tablet">Tablet</option>
                        <option value="Other">Other</option>
                    </select>
                </div>
               
                <div class="form-group">
                    <label for="device-brand"><i class="fas fa-microchip"></i> Device Brand</label>
                    <input type="text" id="device-brand" required placeholder="e.g., Dell, HP, Apple">
                </div>
               
                <div class="form-group">
                    <label for="device-model"><i class="fas fa-laptop-code"></i> Device Model</label>
                    <input type="text" id="device-model" required placeholder="e.g., Inspiron 15, MacBook Pro">
                </div>
               
                <div class="form-group">
                    <label for="issue"><i class="fas fa-exclamation-triangle"></i> Issue Description</label>
                    <textarea id="issue" rows="4" required placeholder="Describe the problem you're experiencing"></textarea>
                </div>
               
                <div class="form-group">
                    <label for="preferred-date"><i class="fas fa-calendar-alt"></i> Preferred Date</label>
                    <input type="date" id="preferred-date" required>
                </div>
               
                <button type="submit">
                    bookings.push(booking);
			saveBookings();
		// Save locally (optional – keep admin dashboard working)
		bookings.push(booking);
		saveBookings();

		// Send to Google Sheet
		fetch(GOOGLE_SCRIPT_URL, {
    		method: "POST",
    		mode: "no-cors",
    		headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(booking)
});
                </button>
            </form>
        </div>

        <!-- Admin Dashboard Tab -->
        <div id="admin" class="tab-content">
            <div id="admin-login" class="admin-login">
                <h2><i class="fas fa-user-cog"></i> Admin Login</h2>
                <div id="login-alert" class="alert hidden"></div>
                <form id="login-form">
                    <div class="form-group">
                        <label for="admin-username"><i class="fas fa-user"></i> Username</label>
                        <input type="text" id="admin-username" required placeholder="Enter admin username">
                    </div>
                   
                    <div class="form-group">
                        <label for="admin-password"><i class="fas fa-lock"></i> Password</label>
                        <input type="password" id="admin-password" required placeholder="Enter admin password">
                    </div>
                   
                    <button type="submit">
                        <i class="fas fa-sign-in-alt"></i> Login
                    </button>
                </form>
            </div>
           
            <div id="admin-dashboard" class="hidden">
                <h2><i class="fas fa-tachometer-alt"></i> Admin Dashboard</h2>
               
                <div class="stats-cards">
                    <div class="stat-card">
                        <div class="stat-label">Total Bookings</div>
                        <div class="stat-number" id="total-bookings">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Pending</div>
                        <div class="stat-number" id="pending-bookings">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">In Progress</div>
                        <div class="stat-number" id="progress-bookings">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Completed</div>
                        <div class="stat-number" id="completed-bookings">0</div>
                    </div>
                </div>
               
                <h3><i class="fas fa-list"></i> All Bookings</h3>
                <div id="bookings-list">
                    <!-- Bookings will be populated here -->
                </div>
               
                <button class="btn-danger" onclick="logoutAdmin()" style="margin-top: 20px;">
                    <i class="fas fa-sign-out-alt"></i> Logout
                </button>
            </div>
        </div>
    </div>

    <!-- Mobile Bottom Navigation -->
    <div class="mobile-nav">
        <div class="nav-item active" data-tab="welcome">
            <i class="fas fa-home"></i>
            <span>Home</span>
        </div>
        <div class="nav-item" data-tab="customer">
            <i class="fas fa-tools"></i>
            <span>Book Repair</span>
        </div>
        <div class="nav-item" data-tab="admin">
            <i class="fas fa-user-cog"></i>
            <span>Admin</span>
        </div>
    </div>

    <script>
        // Sample admin credentials
        const ADMIN_CREDENTIALS = {
            username: "dsoffmpp",
            password: "dsoffmpp123"
        };

        // Initialize bookings from localStorage or create empty array
        let bookings = JSON.parse(localStorage.getItem('computerRepairBookings')) || [];
        let nextId = bookings.length > 0 ? Math.max(...bookings.map(b => b.id)) + 1 : 1;

        // DOM Elements
        const tabBtns = document.querySelectorAll('.tab-btn');
        const navItems = document.querySelectorAll('.nav-item');
        const tabContents = document.querySelectorAll('.tab-content');
        const bookingForm = document.getElementById('booking-form');
        const customerAlert = document.getElementById('customer-alert');
        const loginForm = document.getElementById('login-form');
        const loginAlert = document.getElementById('login-alert');
        const adminLogin = document.getElementById('admin-login');
        const adminDashboard = document.getElementById('admin-dashboard');
        const bookingsList = document.getElementById('bookings-list');
        const totalBookingsEl = document.getElementById('total-bookings');
        const pendingBookingsEl = document.getElementById('pending-bookings');
        const progressBookingsEl = document.getElementById('progress-bookings');
        const completedBookingsEl = document.getElementById('completed-bookings');
        const actionButtons = document.querySelectorAll('.action-buttons button');

        // Set minimum date to today for date input
        document.getElementById('preferred-date').min = new Date().toISOString().split('T')[0];

        // Tab switching functionality
        function switchTab(tabId) {
            // Update active tab button (desktop)
            tabBtns.forEach(b => b.classList.remove('active'));
            document.querySelector(`.tab-btn[data-tab="${tabId}"]`)?.classList.add('active');
           
            // Update active nav item (mobile)
            navItems.forEach(item => item.classList.remove('active'));
            document.querySelector(`.nav-item[data-tab="${tabId}"]`).classList.add('active');
           
            // Update active tab content
            tabContents.forEach(content => content.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
           
            // If switching to admin tab and already logged in, show dashboard
            if (tabId === 'admin' && localStorage.getItem('adminLoggedIn') === 'true') {
                adminLogin.classList.add('hidden');
                adminDashboard.classList.remove('hidden');
                renderAdminDashboard();
            } else if (tabId === 'admin') {
                adminLogin.classList.remove('hidden');
                adminDashboard.classList.add('hidden');
            }
        }

        // Add event listeners for desktop tabs
        tabBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                const tabId = btn.getAttribute('data-tab');
                switchTab(tabId);
            });
        });

        // Add event listeners for mobile nav items
        navItems.forEach(item => {
            item.addEventListener('click', () => {
                const tabId = item.getAttribute('data-tab');
                switchTab(tabId);
            });
        });

        // Add event listeners for action buttons on welcome screen
        actionButtons.forEach(button => {
            button.addEventListener('click', () => {
                const tabId = button.getAttribute('data-tab');
                switchTab(tabId);
            });
        });

        // Customer booking form submission
        bookingForm.addEventListener('submit', function(e) {
            e.preventDefault();
           
            const booking = {
                id: nextId++,
                customerName: document.getElementById('customer-name').value,
                customerEmail: document.getElementById('customer-email').value,
                customerPhone: document.getElementById('customer-phone').value,
                deviceType: document.getElementById('device-type').value,
                deviceBrand: document.getElementById('device-brand').value,
                deviceModel: document.getElementById('device-model').value,
                issue: document.getElementById('issue').value,
                preferredDate: document.getElementById('preferred-date').value,
                status: 'pending',
                createdAt: new Date().toISOString()
            };
           
            bookings.push(booking);
            saveBookings();
           
            // Show success message
            showAlert(customerAlert, 'Booking submitted successfully! We will contact you soon.', 'success');
           
            // Reset form
            bookingForm.reset();
           
            // Set focus back to name field
            document.getElementById('customer-name').focus();
        });

        // Admin login form submission
        loginForm.addEventListener('submit', function(e) {
            e.preventDefault();
           
            const username = document.getElementById('admin-username').value;
            const password = document.getElementById('admin-password').value;
           
            if (username === ADMIN_CREDENTIALS.username && password === ADMIN_CREDENTIALS.password) {
                localStorage.setItem('adminLoggedIn', 'true');
                adminLogin.classList.add('hidden');
                adminDashboard.classList.remove('hidden');
                renderAdminDashboard();
            } else {
                showAlert(loginAlert, 'Invalid username or password!', 'danger');
            }
        });

        // Check if admin is already logged in
        if (localStorage.getItem('adminLoggedIn') === 'true') {
            adminLogin.classList.add('hidden');
            adminDashboard.classList.remove('hidden');
            renderAdminDashboard();
        }

        // Save bookings to localStorage
        function saveBookings() {
            localStorage.setItem('computerRepairBookings', JSON.stringify(bookings));
        }

        // Show alert message
        function showAlert(alertElement, message, type) {
            alertElement.textContent = message;
            alertElement.className = `alert alert-${type}`;
            alertElement.classList.remove('hidden');
           
            setTimeout(() => {
                alertElement.classList.add('hidden');
            }, 5000);
        }

        // Render admin dashboard with bookings
        function renderAdminDashboard() {
            // Update statistics
            totalBookingsEl.textContent = bookings.length;
            pendingBookingsEl.textContent = bookings.filter(b => b.status === 'pending').length;
            progressBookingsEl.textContent = bookings.filter(b => b.status === 'in-progress').length;
            completedBookingsEl.textContent = bookings.filter(b => b.status === 'completed').length;
           
            // Clear bookings list
            bookingsList.innerHTML = '';
           
            if (bookings.length === 0) {
                bookingsList.innerHTML = '<div class="booking-card" style="text-align: center; padding: 30px;"><p>No bookings found.</p></div>';
                return;
            }
           
            // Sort bookings by creation date (newest first)
            const sortedBookings = [...bookings].sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
           
            // Render each booking
            sortedBookings.forEach(booking => {
                const bookingCard = document.createElement('div');
                bookingCard.className = 'booking-card';
               
                bookingCard.innerHTML = `
                    <div class="booking-header">
                        <div class="booking-id">Booking #${booking.id}</div>
                        <div class="booking-status status-${booking.status}">${formatStatus(booking.status)}</div>
                    </div>
                    <div class="booking-details">
                        <div class="detail-item">
                            <strong>Customer</strong>
                            ${booking.customerName}
                        </div>
                        <div class="detail-item">
                            <strong>Contact</strong>
                            ${booking.customerEmail}<br>${booking.customerPhone}
                        </div>
                        <div class="detail-item">
                            <strong>Device</strong>
                            ${booking.deviceType} - ${booking.deviceBrand} ${booking.deviceModel}
                        </div>
                        <div class="detail-item">
                            <strong>Preferred Date</strong>
                            ${formatDate(booking.preferredDate)}
                        </div>
                        <div class="detail-item">
                            <strong>Issue</strong>
                            ${booking.issue}
                        </div>
                    </div>
                    <div class="booking-actions">
                        ${booking.status === 'pending' ?
                            `<button class="btn-success" onclick="updateStatus(${booking.id}, 'in-progress')">
                                <i class="fas fa-play-circle"></i> Start Repair
                            </button>` :
                            ''}
                        ${booking.status === 'in-progress' ?
                            `<button class="btn-success" onclick="updateStatus(${booking.id}, 'completed')">
                                <i class="fas fa-check-circle"></i> Mark Complete
                            </button>` :
                            ''}
                        ${booking.status !== 'cancelled' && booking.status !== 'completed' ?
                            `<button class="btn-danger" onclick="updateStatus(${booking.id}, 'cancelled')">
                                <i class="fas fa-times-circle"></i> Cancel
                            </button>` :
                            ''}
                        <button onclick="deleteBooking(${booking.id})">
                            <i class="fas fa-trash-alt"></i> Delete
                        </button>
                    </div>
                `;
               
                bookingsList.appendChild(bookingCard);
            });
        }

        // Update booking status
        function updateStatus(bookingId, newStatus) {
            const bookingIndex = bookings.findIndex(b => b.id === bookingId);
            if (bookingIndex !== -1) {
                bookings[bookingIndex].status = newStatus;
                saveBookings();
                renderAdminDashboard();
               
                // Show confirmation
                const statusName = formatStatus(newStatus);
                alert(`Booking #${bookingId} status updated to ${statusName}`);
            }
        }

        // Delete booking
        function deleteBooking(bookingId) {
            if (confirm('Are you sure you want to delete this booking?')) {
                bookings = bookings.filter(b => b.id !== bookingId);
                saveBookings();
                renderAdminDashboard();
                alert('Booking deleted successfully');
            }
        }

        // Logout admin
        function logoutAdmin() {
            localStorage.setItem('adminLoggedIn', 'false');
            adminLogin.classList.remove('hidden');
            adminDashboard.classList.add('hidden');
            loginForm.reset();
            switchTab('welcome');
        }

        // Format status for display
        function formatStatus(status) {
            const statusMap = {
                'pending': 'Pending',
                'in-progress': 'In Progress',
                'completed': 'Completed',
                'cancelled': 'Cancelled'
            };
            return statusMap[status] || status;
        }

        // Format date for display
        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'short', day: 'numeric' };
            return new Date(dateString).toLocaleDateString(undefined, options);
        }
    </script>
</body>
</html> 
