<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>NovaStore</title>

<style>
*{
 box-sizing:border-box;
 font-family:Arial,sans-serif
}

body{
 margin:0;
 background:#f5f6f8;
 color:#172033
}

header{
 background:#111827;
 color:#fff;
 position:sticky;
 top:0;
 z-index:5
}

.top{
 max-width:1100px;
 margin:auto;
 padding:14px;
 display:flex;
 gap:10px;
 align-items:center
}

.logo{
 font-size:22px;
 font-weight:800;
 flex:1
}

.search{
 flex:2;
 padding:11px;
 border-radius:8px;
 border:0
}

.btn{
 padding:10px 13px;
 border:0;
 border-radius:8px;
 cursor:pointer
}

.primary{
 background:#111827;
 color:#fff
}

.green{
 background:#16a34a;
 color:#fff
}

.red{
 background:#dc2626;
 color:#fff
}

.secondary{
 background:#e5e7eb
}

.hero{
 max-width:1100px;
 margin:18px auto;
 padding:25px
}

.hero div{
 background:#111827;
 color:#fff;
 padding:30px;
 border-radius:18px
}

.filters,
.products{
 max-width:1100px;
 margin:auto;
 padding:0 15px
}

.filters{
 margin-bottom:15px
}

.filters select{
 padding:10px;
 border:1px solid #ddd;
 border-radius:8px
}

.products{
 display:grid;
 grid-template-columns:
 repeat(auto-fill,minmax(210px,1fr));
 gap:15px;
 padding-bottom:40px
}

.card{
 background:#fff;
 border-radius:13px;
 overflow:hidden;
 box-shadow:0 2px 9px #0001
}

.pic{
 height:175px;
 background:#eee;
 display:flex;
 align-items:center;
 justify-content:center
}

.pic img{
 width:100%;
 height:100%;
 object-fit:cover
}

.info{
 padding:14px
}

.cat{
 font-size:12px;
 color:#687386
}

.name{
 font-weight:bold;
 margin:7px 0
}

.old{
 text-decoration:line-through;
 color:#888;
 font-size:13px
}

.price{
 font-size:19px;
 font-weight:bold;
 margin:6px 0
}

.add{
 width:100%;
 margin-top:10px
}

.modal{
 display:none;
 position:fixed;
 inset:0;
 background:#0008;
 z-index:10;
 padding:15px;
 overflow:auto
}

.modal.show{
 display:block
}

.panel{
 background:white;
 max-width:600px;
 margin:30px auto;
 padding:20px;
 border-radius:14px
}

.field{
 margin:10px 0
}

.field label{
 display:block;
 font-size:13px;
 font-weight:bold;
 margin-bottom:5px
}

.field input,
.field textarea,
.field select{
 width:100%;
 padding:11px;
 border:1px solid #ddd;
 border-radius:8px
}

.actions{
 display:flex;
 gap:8px;
 margin-top:15px;
 flex-wrap:wrap
}

.cartrow{
 display:flex;
 justify-content:space-between;
 gap:10px;
 padding:12px 0;
 border-bottom:1px solid #eee
}

.message{
 margin-top:12px;
 padding:10px;
 border-radius:8px;
 background:#f3f4f6
}

.accountInfo{
 background:#f3f4f6;
 padding:12px;
 border-radius:8px;
 margin:10px 0
}

@media(max-width:650px){

 .top{
  flex-wrap:wrap
 }

 .search{
  order:3;
  flex-basis:100%
 }

 .hero{
  padding:10px
 }

 .products{
  grid-template-columns:repeat(2,1fr);
  gap:10px;
  padding:0 10px 30px
 }

 .pic{
  height:140px
 }

 .cartrow{
  flex-direction:column
 }

}
</style>

</head>

<body>

<header>

<div class="top">

<div class="logo">
NovaStore
</div>

<input
 id="search"
 class="search"
 placeholder="Search products"
>

<button
 class="btn secondary"
 onclick="openCart()"
>
Cart (<span id="count">0</span>)
</button>

<button
 class="btn secondary"
 id="account"
 onclick="openAccount()"
>
Login
</button>

</div>

</header>


<section class="hero">

<div>

<h1>
Welcome to NovaStore
</h1>

<p>
Quality products at great prices.
</p>

</div>

</section>


<div class="filters">

<select id="category">

<option value="all">
All categories
</option>

</select>

</div>


<main
 id="products"
 class="products"
>

<p>
Loading products...
</p>

</main>


<footer
 style="text-align:center;padding:30px;color:#687386"
>

© 2026 NovaStore

</footer>


<!-- ACCOUNT MODAL -->

<div
 id="accountModal"
 class="modal"
>

<div class="panel">

<h2>
Customer Account
</h2>

<div
 id="loggedInBox"
 style="display:none"
>

<div class="accountInfo">

You are logged in as:

<strong id="loggedEmail"></strong>

</div>

<div class="actions">

<button
 class="btn red"
 onclick="logoutCustomer()"
>
Logout
</button>

<button
 class="btn secondary"
 onclick="closeM('accountModal')"
>
Close
</button>

</div>

</div>


<div
 id="loginBox"
>

<div class="field">

<label>
Email
</label>

<input
 id="email"
 type="email"
 autocomplete="email"
>

</div>


<div class="field">

<label>
Password
</label>

<input
 id="password"
 type="password"
 autocomplete="current-password"
>

</div>


<div class="actions">

<button
 class="btn primary"
 onclick="login()"
>
Login
</button>

<button
 class="btn green"
 onclick="register()"
>
Create account
</button>

<button
 class="btn secondary"
 onclick="closeM('accountModal')"
>
Close
</button>

</div>

</div>

<p
 id="accountMsg"
></p>

</div>

</div>


<!-- CART MODAL -->

<div
 id="cartModal"
 class="modal"
>

<div class="panel">

<h2>
Your Cart
</h2>

<div id="cartItems"></div>

<h3 id="total">
Total: ₦0
</h3>

<div class="field">

<label>
Payment method
</label>

<select id="paymentMethod">

<option value="bank_transfer">
Bank Transfer
</option>

<option value="cash_on_delivery">
Cash on Delivery
</option>

</select>

</div>


<div
 id="bankInfo"
 class="message"
>

<strong>Bank Transfer</strong>

<p>
After placing your order, contact NovaStore for the current bank-transfer details.
</p>

<p>
Do not send money to an unverified account.
</p>

</div>


<div class="actions">

<button
 class="btn green"
 onclick="checkout()"
>
Place Order
</button>

<button
 class="btn secondary"
 onclick="closeM('cartModal')"
>
Close
</button>

</div>

<p id="cartMsg"></p>

</div>

</div>


<script type="module">

import {
 initializeApp
}
from
"https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";


import {
 getDatabase,
 ref,
 onValue,
 push,
 set
}
from
"https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js";


import {
 getAuth,
 onAuthStateChanged,
 signInWithEmailAndPassword,
 createUserWithEmailAndPassword,
 signOut
}
from
"https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";


/* FIREBASE */

const firebaseConfig = {

 apiKey:
 "AIzaSyCNrU3igTkkcQ0Z6Zq1dluKw_s_3yHovE",

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


const app =
 initializeApp(firebaseConfig);

const db =
 getDatabase(app);

const auth =
 getAuth(app);


/* VARIABLES */

let products = {};

let cart =
 JSON.parse(
  localStorage.getItem("novaCart") || "[]"
 );

let user = null;


/* ELEMENTS */

const productsBox =
 document.getElementById("products");

const searchInput =
 document.getElementById("search");

const categoryInput =
 document.getElementById("category");

const accountButton =
 document.getElementById("account");

const accountModal =
 document.getElementById("accountModal");

const cartModal =
 document.getElementById("cartModal");

const count =
 document.getElementById("count");

const cartItems =
 document.getElementById("cartItems");

const total =
 document.getElementById("total");

const cartMsg =
 document.getElementById("cartMsg");

const accountMsg =
 document.getElementById("accountMsg");

const loginBox =
 document.getElementById("loginBox");

const loggedInBox =
 document.getElementById("loggedInBox");

const loggedEmail =
 document.getElementById("loggedEmail");

const emailInput =
 document.getElementById("email");

const passwordInput =
 document.getElementById("password");

const paymentMethod =
 document.getElementById("paymentMethod");

const bankInfo =
 document.getElementById("bankInfo");


/* MONEY */

const money = n =>
 "₦" +
 Number(n || 0)
 .toLocaleString("en-NG");


/* SAFE TEXT */

const safe = s =>
 String(s ?? "")
 .replace(
  /[&<>"']/g,
  c => ({
   "&":"&amp;",
   "<":"&lt;",
   ">":"&gt;",
   '"':"&quot;",
   "'":"&#039;"
  }[c])
 );


/* LOAD PRODUCTS */

onValue(
 ref(db,"products"),
 snapshot => {

  products =
  snapshot.val() || {};

  renderCats();

  render();

 },
 error => {

  console.error(
   "Products error:",
   error
  );

  productsBox.innerHTML =
  "<p>Unable to load products.</p>";

 }
);


/* AUTH STATE */

onAuthStateChanged(
 auth,
 currentUser => {

  user =
  currentUser;

  if(user){

   accountButton.textContent =
   "Account";

   loggedEmail.textContent =
   user.email || "";

  }else{

   accountButton.textContent =
   "Login";

  }

 }
);


/* CATEGORIES */

function renderCats(){

 const old =
 categoryInput.value;

 const categories =
 [
  ...new Set(
   Object.values(products)
   .map(
    p => p.category
   )
   .filter(Boolean)
  )
 ];

 categoryInput.innerHTML =
 '<option value="all">All categories</option>' +

 categories
 .map(
  x =>
  `<option value="${safe(x)}">
   ${safe(x)}
  </option>`
 )
 .join("");

 categoryInput.value =
 categories.includes(old)
 ? old
 : "all";

}


/* PRODUCTS */

function render(){

 const q =
 searchInput.value
 .toLowerCase()
 .trim();

 const c =
 categoryInput.value;

 const list =
 Object.entries(products)
 .filter(
  ([id,p]) =>

  (p.name || "")
  .toLowerCase()
  .includes(q)

  &&

  (
   c === "all" ||
   p.category === c
  )

  &&

  p.available !== false
 );


 productsBox.innerHTML =
 list.length

 ?

 list.map(
  ([id,p]) => `

  <article class="card">

  <div class="pic">

  ${
   p.image

   ?

   `<img
    src="${safe(p.image)}"
    alt="${safe(p.name)}"
    onerror="
     this.style.display='none'
    "
   >`

   :

   "🛍️"
  }

  </div>


  <div class="info">

  <div class="cat">

  ${safe(
   p.category ||
   "General"
  )}

  </div>


  <div class="name">

  ${safe(p.name)}

  </div>


  ${
   p.oldPrice

   ?

   `<div class="old">
   ${money(p.oldPrice)}
   </div>`

   :

   ""
  }


  <div class="price">

  ${money(p.price)}

  </div>


  <small>

  ${safe(
   p.description ||
   "Available now"
  )}

  </small>


  <button
   class="btn green add"
   onclick="addToCart('${id}')"
  >

  Add to Cart

  </button>

  </div>

  </article>

  `
 ).join("")

 :

 "<p>No products found.</p>";

}


searchInput.oninput =
 render;

categoryInput.onchange =
 render;


/* ADD TO CART */

window.addToCart =
 function(id){

  const product =
  products[id];

  if(!product){

   alert(
    "Product is no longer available."
   );

   return;

  }

  const existing =
  cart.find(
   x => x.id === id
  );

  if(existing){

   existing.qty++;

  }else{

   cart.push({
    id:id,
    qty:1
   });

  }

  saveCart();

  alert(
   "Added to cart."
  );

 };


/* SAVE CART */

function saveCart(){

 localStorage.setItem(
  "novaCart",
  JSON.stringify(cart)
 );

 count.textContent =
 cart.reduce(
  (sum,item) =>
  sum + item.qty,
  0
 );

}


/* OPEN CART */

window.openCart =
 function(){

  renderCart();

  cartModal.classList.add(
   "show"
  );

 };


/* RENDER CART */

function renderCart(){

 const validCart =
 cart.filter(
  item =>
  products[item.id]
 );

 if(
  validCart.length !==
  cart.length
 ){

  cart =
  validCart;

  saveCart();

 }


 if(!cart.length){

  cartItems.innerHTML =
  "<p>Your cart is empty.</p>";

 }else{

  cartItems.innerHTML =
  cart.map(
   item => {

    const p =
    products[item.id];

    return `

    <div class="cartrow">

    <div>

    <strong>
    ${safe(p.name)}
    </strong>

    <br>

    ${money(p.price)}
    × ${item.qty}

    </div>


    <div>

    <button
     class="btn secondary"
     onclick="
      changeQty(
       '${item.id}',
       -1
      )
     "
    >
    −
    </button>

    <button
     class="btn secondary"
     onclick="
      changeQty(
       '${item.id}',
       1
      )
     "
    >
    +
    </button>

    </div>

    </div>

    `;

   }
  ).join("");

 }


 const totalAmount =
 cart.reduce(
  (sum,item) =>
  sum +
  (
   Number(
    products[item.id]?.price || 0
   )
   *
   item.qty
  ),
  0
 );


 total.textContent =
 "Total: " +
 money(totalAmount);

 cartMsg.textContent =
 "";

 updatePaymentInfo();

 }


/* CHANGE QUANTITY */

window.changeQty =
 function(id,change){

  const item =
  cart.find(
   x => x.id === id
  );

  if(!item)return;

  item.qty += change;

  if(item.qty < 1){

   cart =
   cart.filter(
    x => x.id !== id
   );

  }

  saveCart();

  renderCart();

 };


/* PAYMENT INFO */

function updatePaymentInfo(){

 if(
  paymentMethod.value ===
  "bank_transfer"
 ){

  bankInfo.style.display =
  "block";

 }else{

  bankInfo.style.display =
  "none";

 }

}


paymentMethod.onchange =
 updatePaymentInfo;


/* CHECKOUT */

window.checkout =
 async function(){

  cartMsg.textContent =
  "";

  if(!cart.length){

   cartMsg.textContent =
   "Your cart is empty.";

   return;

  }


  if(!user){

   cartMsg.textContent =
   "Please create an account or login before placing an order.";

   return;

  }


  const items =
  cart.map(
   item => ({

    productId:
    item.id,

    name:
    products[item.id]?.name || "",

    price:
    Number(
     products[item.id]?.price || 0
    ),

    quantity:
    item.qty

   })
  );


  const totalAmount =
  items.reduce(
   (sum,item) =>
   sum +
   item.price *
   item.quantity,
   0
  );


  const selectedPayment =
  paymentMethod.value;


  try{

   const orderRef =
   push(
    ref(db,"orders")
   );


   await set(
    orderRef,
    {

     userId:
     user.uid,

     email:
     user.email,

     items:
     items,

     total:
     totalAmount,

     paymentMethod:
     selectedPayment,

     status:
     "pending",

     createdAt:
     Date.now()

    }
   );


   cart = [];

   saveCart();

   renderCart();


   cartMsg.textContent =
   "Order placed successfully.";

  }catch(error){

   console.error(error);

   cartMsg.textContent =
   "Unable to place order: " +
   error.message;

  }

 };


/* ACCOUNT */

window.openAccount =
 function(){

  accountMsg.textContent =
  "";

  if(user){

   loginBox.style.display =
   "none";

   loggedInBox.style.display =
   "block";

   loggedEmail.textContent =
   user.email || "";

  }else{

   loginBox.style.display =
   "block";

   loggedInBox.style.display =
   "none";

  }

  accountModal.classList.add(
   "show"
  );

 };


/* LOGIN */

window.login =
 async function(){

  const email =
  emailInput.value.trim();

  const password =
  passwordInput.value;


  if(!email || !password){

   accountMsg.textContent =
   "Enter your email and password.";

   return;

  }


  accountMsg.textContent =
  "Signing in...";


  try{

   await signInWithEmailAndPassword(
    auth,
    email,
    password
   );


   accountMsg.textContent =
   "Login successful.";

  }catch(error){

   console.error(error);

   if(
    error.code ===
    "auth/invalid-credential"
   ){

    accountMsg.textContent =
    "Incorrect email or password. You must create an account first.";

   }else if(
    error.code ===
    "auth/invalid-email"
   ){

    accountMsg.textContent =
    "Please enter a valid email.";

   }else if(
    error.code ===
    "auth/too-many-requests"
   ){

    accountMsg.textContent =
    "Too many attempts. Please wait and try again.";

   }else{

    accountMsg.textContent =
    error.message;

   }

  }

 };


/* REGISTER */

window.register =
 async function(){

  const email =
  emailInput.value.trim();

  const password =
  passwordInput.value;


  if(!email || !password){

   accountMsg.textContent =
   "Enter an email and password.";

   return;

  }


  if(password.length < 6){

   accountMsg.textContent =
   "Password must be at least 6 characters.";

   return;

  }


  accountMsg.textContent =
  "Creating account...";


  try{

   const result =
   await createUserWithEmailAndPassword(
    auth,
    email,
    password
   );


   await set(
    ref(
     db,
     "users/" +
     result.user.uid
    ),
    {

     email:
     result.user.email,

     createdAt:
     Date.now()

    }
   );


   accountMsg.textContent =
   "Account created successfully.";

  }catch(error){

   console.error(error);

   if(
    error.code ===
    "auth/email-already-in-use"
   ){

    accountMsg.textContent =
    "This email already has an account. Please login.";

   }else if(
    error.code ===
    "auth/invalid-email"
   ){

    accountMsg.textContent =
    "Please enter a valid email.";

   }else{

    accountMsg.textContent =
    error.message;

   }

  }

 };


/* LOGOUT */

window.logoutCustomer =
 async function(){

  try{

   await signOut(auth);

   accountMsg.textContent =
   "You have been logged out.";

   loginBox.style.display =
   "block";

   loggedInBox.style.display =
   "none";

  }catch(error){

   accountMsg.textContent =
   error.message;

  }

 };


/* CLOSE MODALS */

window.closeM =
 function(id){

  document
  .getElementById(id)
  .classList.remove(
   "show"
  );

 };


/* INITIAL CART COUNT */

saveCart();

</script>

</body>
</html>
