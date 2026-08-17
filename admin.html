<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NovaStore Admin</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    body {
      background: #f4f6f8;
      min-height: 100vh;
    }

    #loginPage {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .login-box {
      width: 100%;
      max-width: 400px;
      background: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 5px 25px rgba(0,0,0,.1);
    }

    h1 {
      text-align: center;
      margin-bottom: 8px;
    }

    .subtitle {
      text-align: center;
      color: #777;
      margin-bottom: 25px;
    }

    label {
      display: block;
      font-weight: bold;
      margin-bottom: 7px;
    }

    input {
      width: 100%;
      padding: 13px;
      border: 1px solid #ddd;
      border-radius: 8px;
      margin-bottom: 16px;
      font-size: 16px;
    }

    button {
      cursor: pointer;
    }

    #loginButton {
      width: 100%;
      padding: 14px;
      border: 0;
      border-radius: 8px;
      background: #111;
      color: white;
      font-size: 16px;
      font-weight: bold;
    }

    #message {
      text-align: center;
      margin-top: 15px;
      color: #c00;
    }

    #adminPage {
      display: none;
    }

    header {
      background: #111;
      color: white;
      padding: 18px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    header h2 {
      margin: 0;
    }

    #logoutButton {
      background: white;
      color: #111;
      border: 0;
      padding: 10px 16px;
      border-radius: 7px;
      font-weight: bold;
    }

    .container {
      max-width: 1100px;
      margin: 25px auto;
      padding: 0 20px;
    }

    .welcome,
    .card,
    .section {
      background: white;
      border-radius: 12px;
      padding: 25px;
      box-shadow: 0 2px 10px rgba(0,0,0,.05);
    }

    .welcome {
      margin-bottom: 20px;
    }

    .welcome p {
      color: #666;
      margin-top: 8px;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 18px;
    }

    .card h3 {
      color: #777;
      font-size: 15px;
      margin-bottom: 10px;
    }

    .card strong {
      font-size: 28px;
    }

    .section {
      margin-top: 20px;
    }

    .section p {
      color: #666;
      line-height: 1.6;
      margin-top: 10px;
    }

    .store-link {
      display: inline-block;
      margin-top: 18px;
      padding: 12px 18px;
      background: #111;
      color: white;
      text-decoration: none;
      border-radius: 8px;
    }
  </style>
</head>

<body>

  <!-- LOGIN -->
  <section id="loginPage">

    <div class="login-box">

      <h1>NovaStore</h1>

      <p class="subtitle">Admin Panel</p>

      <form id="loginForm">

        <label for="email">Email</label>

        <input
          id="email"
          type="email"
          placeholder="Admin email"
          required
        >

        <label for="password">Password</label>

        <input
          id="password"
          type="password"
          placeholder="Password"
          required
        >

        <button id="loginButton" type="submit">
          Login
        </button>

      </form>

      <div id="message"></div>

    </div>

  </section>


  <!-- ADMIN DASHBOARD -->
  <section id="adminPage">

    <header>

      <h2>NovaStore Admin</h2>

      <button id="logoutButton">
        Logout
      </button>

    </header>

    <main class="container">

      <div class="welcome">

        <h2>Welcome, Admin 👋</h2>

        <p>You are logged into the NovaStore admin panel.</p>

        <p>
          Account:
          <strong id="adminEmail"></strong>
        </p>

        <a class="store-link" href="index.html">
          View Store
        </a>

      </div>

      <div class="cards">

        <div class="card">
          <h3>Products</h3>
          <strong>0</strong>
        </div>

        <div class="card">
          <h3>Orders</h3>
          <strong>0</strong>
        </div>

        <div class="card">
          <h3>Customers</h3>
          <strong>0</strong>
        </div>

      </div>

      <div class="section">

        <h2>Dashboard</h2>

        <p>
          Firebase authentication is connected. We can now connect
          your products, orders and customers to your database.
        </p>

      </div>

    </main>

  </section>


  <script type="module">

    import { initializeApp }
      from "https://www.gstatic.com/firebasejs/12.1.0/firebase-app.js";

    import {
      getAuth,
      signInWithEmailAndPassword,
      onAuthStateChanged,
      signOut
    } from "https://www.gstatic.com/firebasejs/12.1.0/firebase-auth.js";


    const firebaseConfig = {

      apiKey: "AIzaSyCNrU3igTkkcQ0Z6Zq1dluKw_s_3yHovjE",

      authDomain:
        "novastore-6fd18.firebaseapp.com",

      databaseURL:
        "https://novastore-6fd18-default-rtdb.asia-southeast1.firebasedatabase.app",

      projectId:
        "novastore-6fd18",

      storageBucket:
        "novastore-6fd18.firebasestorage.app",

      messagingSenderId:
        "783420364153",

      appId:
        "1:783420364153:web:1b56b655e3e804726d8ba8",

      measurementId:
        "G-Q760SBLPLT"
    };


    try {

      const app = initializeApp(firebaseConfig);

      const auth = getAuth(app);

      const loginPage =
        document.getElementById("loginPage");

      const adminPage =
        document.getElementById("adminPage");

      const loginForm =
        document.getElementById("loginForm");

      const message =
        document.getElementById("message");

      const loginButton =
        document.getElementById("loginButton");

      const logoutButton =
        document.getElementById("logoutButton");

      const adminEmail =
        document.getElementById("adminEmail");


      loginForm.addEventListener("submit", async function(e) {

        e.preventDefault();

        const email =
          document.getElementById("email").value.trim();

        const password =
          document.getElementById("password").value;

        message.textContent = "";

        loginButton.disabled = true;

        loginButton.textContent = "Logging in...";


        try {

          await signInWithEmailAndPassword(
            auth,
            email,
            password
          );

        } catch (error) {

          console.error(error);

          message.textContent =
            "Login failed. Check your email and password.";

        } finally {

          loginButton.disabled = false;

          loginButton.textContent = "Login";

        }

      });


      onAuthStateChanged(auth, function(user) {

        if (user) {

          loginPage.style.display = "none";

          adminPage.style.display = "block";

          adminEmail.textContent =
            user.email || "";

        } else {

          loginPage.style.display = "flex";

          adminPage.style.display = "none";

        }

      });


      logoutButton.addEventListener("click", async function() {

        await signOut(auth);

      });


    } catch (error) {

      console.error(error);

      document.getElementById("message").textContent =
        "Firebase could not load. Please refresh the page.";

    }

  </script>

</body>
</html>
