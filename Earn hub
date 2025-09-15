<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Earn Hub</title>
<style>
body { font-family: Arial, sans-serif; margin:0; padding:0; background:#f5f5f5; }
nav { position: fixed; bottom:0; width:100%; display:flex; justify-content:space-around; background:#fff; border-top:1px solid #ccc; }
nav button { flex:1; padding:15px; font-size:16px; cursor:pointer; border:none; background:none; }
.tab { display:none; padding:20px; margin-bottom:60px; }
#balanceDisplay { text-align:center; font-size:22px; font-weight:bold; margin-bottom:20px; background:#4CAF50; color:#fff; padding:10px 0; border-radius:10px; }
input, button { padding:10px; margin:5px 0; border-radius:5px; border:1px solid #ccc; }
button { background:#4CAF50; color:#fff; cursor:pointer; }
button:hover { background:#45a049; }
.card { background:#fff; padding:15px; margin:10px 0; border-radius:10px; box-shadow:0 2px 5px rgba(0,0,0,0.1); display:flex; justify-content:space-between; align-items:center; }
.card a { background:#2196F3; color:#fff; padding:5px 10px; border-radius:5px; text-decoration:none; }
.card a:hover { background:#0b7dda; }
table { width:100%; border-collapse: collapse; margin-bottom:10px; }
th, td { border:1px solid #000; padding:5px; text-align:center; }
#adminNav button { padding:10px; margin:2px; background:#2196F3; color:#fff; border-radius:5px; border:none; cursor:pointer; }
#adminNav button:hover { background:#0b7dda; }
</style>
<script src="https://js.paystack.co/v2/inline.js"></script>
</head>
<body><div id="signupSection">
  <h2>Welcome to Earn Hub</h2>
  <p>Pay ₦200 to access the app</p>
  <input type="email" id="userEmail" placeholder="Enter your email">
  <input type="text" id="referralInput" placeholder="Referral code (optional)">
  <button onclick="payUser()">Pay ₦200</button>
</div><div id="mainApp" style="display:none;">
  <div id="balanceDisplay">Balance: ₦0</div>  <div id="dashboardTab" class="tab">
    <h3>Tasks & Ads</h3>
    <div id="tasksList"></div>
    <div id="adsList"></div>
  </div>  <div id="referTab" class="tab">
    <h3>Refer & Earn</h3>
    <p>Your Referral Code: <span id="refCode"></span></p>
  </div>  <div id="profileTab" class="tab">
    <h3>Profile</h3>
    <p>Username: <span id="usernameDisplay"></span></p>
    <p>Email: <span id="emailDisplay"></span></p>
    <button onclick="requestDeposit()">Deposit</button>
    <button onclick="requestWithdraw()">Withdraw</button>
    <button onclick="logout()">Logout</button>
  </div>  <nav>
    <button onclick="showTab('dashboardTab')">Dashboard</button>
    <button onclick="showTab('referTab')">Refer & Earn</button>
    <button onclick="showTab('profileTab')">Profile</button>
  </nav>
</div><div id="adminPanel" style="display:none;">
  <h2>Admin Control Panel</h2>
  <div>
    <input type="text" id="adminUser" placeholder="Admin Username">
    <input type="password" id="adminPass" placeholder="Admin Password">
    <button onclick="adminLogin()">Login</button>
  </div>
  <div id="adminControls" style="display:none;">
    <div id="adminNav">
      <button onclick="showAdminTab('adminDashboard')">Dashboard</button>
      <button onclick="showAdminTab('adminUsers')">User Management</button>
      <button onclick="showAdminTab('adminTasks')">Tasks & Ads</button>
      <button onclick="showAdminTab('adminDeposits')">Deposit Requests</button>
      <button onclick="showAdminTab('adminWithdraws')">Withdraw Requests</button>
    </div><div id="adminDashboard" class="tab">
  <h3>Dashboard Overview</h3>
  <p>Total Users: <span id="totalUsers">0</span></p>
  <p>Total Balance: ₦<span id="totalBalance">0</span></p>
</div>

<div id="adminUsers" class="tab">
  <h3>User Management</h3>
  <table>
    <thead><tr><th>Username</th><th>Email</th><th>Balance</th><th>Referral</th><th>Action</th></tr></thead>
    <tbody id="usersTable"></tbody>
  </table>
</div>

<div id="adminTasks" class="tab">
  <h3>Manage Tasks</h3>
  <input type="text" id="taskName" placeholder="Task Name">
  <input type="text" id="taskLink" placeholder="Task Link/URL">
  <input type="number" id="taskAmount" placeholder="Amount ₦">
  <button onclick="addTask()">Add Task</button>
  <div id="adminTaskList"></div>
  <h3>Manage Ads</h3>
  <input type="text" id="adVideo" placeholder="Video URL">
  <input type="text" id="adLink" placeholder="Ad Link">
  <input type="number" id="adAmount" placeholder="Amount ₦">
  <button onclick="addAd()">Add Ad</button>
  <div id="adminAdList"></div>
</div>

<div id="adminDeposits" class="tab">
  <h3>Deposit Requests</h3>
  <ul id="depositRequestsList"></ul>
</div>

<div id="adminWithdraws" class="tab">
  <h3>Withdraw Requests</h3>
  <ul id="withdrawRequestsList"></ul>
</div>

  </div>
</div><script>
const ADMINS = [
  { username:"chiboi001", password:"Chiboy@2011" },
  { username:"Giftedness furniture", password:"Talented@47" }
];

if(!localStorage.getItem('users')) localStorage.setItem('users', JSON.stringify({}));
if(!localStorage.getItem('tasks')) localStorage.setItem('tasks', JSON.stringify([]));
if(!localStorage.getItem('ads')) localStorage.setItem('ads', JSON.stringify([]));
if(!localStorage.getItem('deposits')) localStorage.setItem('deposits', JSON.stringify([]));
if(!localStorage.getItem('withdraws')) localStorage.setItem('withdraws', JSON.stringify([]));

function payUser(){
  const email = document.getElementById('userEmail').value;
  const ref = document.getElementById('referralInput').value.trim();
  if(!email){ alert("Enter your email"); return; }
  window.open('https://paystack.shop/pay/eraanjyry-', '_blank');
  const deposits = JSON.parse(localStorage.getItem('deposits'));
  deposits.push({ email: email, referral: ref, amount: 200, approved:false });
  localStorage.setItem('deposits', JSON.stringify(deposits));
  alert('Deposit request sent for admin approval after payment.');
  document.getElementById('signupSection').style.display='none';
  document.getElementById('mainApp').style.display='block';
  localStorage.setItem('currentUser', email.split('@')[0]);
  initUserApp();
}

function initUserApp(){
  const currentUser = localStorage.getItem('currentUser');
  const users = JSON.parse(localStorage.getItem('users'));
  if
