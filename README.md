<!doctype html>
<html lang="en">

<head>

<meta charset="utf-8">

<meta
 name="viewport"
 content="width=device-width,initial-scale=1"
>

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
 background:#16a34a;
 color:white;
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
.field textarea{
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

.primary{
 background:#111827;
 color:#fff
}

.secondary{
 background:#e5e7eb
}

.cartrow{
 display:flex;
 justify-content:space-between;
 padding:12px 0;
 border-bottom:1px solid #eee
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
 class="btn"
 onclick="openCart()"
>
Cart (<span id="count">0</span>)
</button>

<button
 class="btn"
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


<!-- ACCOUNT -->

<div
 id="accountModal"
 class="modal"
>

<div class="panel">

<h2>
Customer Account
</h2>

<div class="field">

<label>
Email
</label>

<input
 id="email"
 type="email"
>

</div>


<div class="field">

<label>
Password
</label>

<input
 id="password"
 type="password"
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
 class="btn secondary"
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

<p id="accountMsg"></p>

</div>

</div>


<!-- CART -->

<div
 id="cartModal"
 class="modal"
>

<div class="panel">

<h2>
Your Cart
</h2>

<div id="cartItems"></div>

<h3 id="total"></h3>

<div class="actions">

<button
 class="btn primary"
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
 createUserWithEmailAndPassword
}
from
"https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";


const firebaseConfig={

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


const app=
initializeApp(firebaseConfig);


const db=
getDatabase(app);


const auth=
getAuth(app);


let products={};

let cart=
JSON.parse(
 localStorage.getItem("novaCart")||"[]"
);

let user=null;


const money=n=>
"₦"+Number(n||0)
.toLocaleString("en-NG");


const safe=s=>
String(s??"")
.replace(
 /[&<>"']/g,
 c=>({
  "&":"&amp;",
  "<":"&lt;",
  ">":"&gt;",
  '"':"&quot;",
  "'":"&#039;"
 }[c])
);


onValue(
 ref(db,"products"),
 snapshot=>{

  products=
  snapshot.val()||{};

  renderCats();

  render();

 }
);


onAuthStateChanged(
 auth,
 u=>{

  user=u;

  account.textContent=
  u?"Account":"Login";

 }
);


function renderCats(){

 let old=
 category.value;

 let categories=
 [
  ...new Set(
   Object.values(products)
   .map(p=>p.category)
   .filter(Boolean)
  )
 ];


 category.innerHTML=
 '<option value="all">All categories</option>'+
 categories
 .map(
  x=>`<option>${safe(x)}</option>`
 )
 .join("");


 category.value=
 categories.includes(old)
 ?old
 :"all";

}


function render(){

 let q=
 search.value.toLowerCase();

 let c=
 category.value;


 let list=
 Object.entries(products)
 .filter(
  ([id,p])=>
  (p.name||"")
  .toLowerCase()
  .includes(q)
  &&
  (c==="all"||p.category===c)
  &&
  p.available!==false
 );


 productsBox.innerHTML=
 list.length

 ?

 list.map(
 ([id,p])=>`

 <article class="card">

 <div class="pic">

 ${
  p.image

  ?

  `<img
  src="${safe(p.image)}"
  onerror="this.style.display='none'"
  >`

  :

  "🛍️"
 }

 </div>


 <div class="info">

 <div class="cat">

 ${safe(p.category||"General")}

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
  p.description||
  "Available now"
 )}

 </small>


 <button
 class="btn add"
 onclick="add('${id}')"
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


const productsBox=
document.getElementById("products");


search.oninput=
render;


category.onchange=
render;


window.add=id=>{

 let item=
 cart.find(x=>x.id===id);


 if(item){

  item.qty++;

 }else{

  cart.push({
   id:id,
   qty:1
  });

 }


 save();

 alert("Added to cart");

};


function save(){

 localStorage.setItem(
  "novaCart",
  JSON.stringify(cart)
 );


 count.textContent=
 cart.reduce(
  (a,x)=>a+x.qty,
  0
 );

}


window.openCart=()=>{

 cartItems.innerHTML=
 cart.length

 ?

 cart.map(
 x=>{

  let p=
  products[x.id];

  if(!p)return"";


  return `

  <div class="cartrow">

  <span>

  ${safe(p.name)}

  <br>

  ${money(p.price)}
  × ${x.qty}

  </span>


  <span>

  <button
  class="btn secondary"
  onclick="qty('${x.id}',-1)"
  >
  −
  </button>

  <button
  class="btn secondary"
  onclick="qty('${x.id}',1)"
  >
  +
  </button>

  </span>

  </div>

  `;

 }).join("")

 :

 "<p>Your cart is empty.</p>";


 let totalAmount=
 cart.reduce(
  (a,x)=>
  a+
  (products[x.id]?.price||0)*
  x.qty,
  0
 );


 total.textContent=
 "Total: "+
 money(totalAmount);


 cartMsg.textContent="";


 cartModal.classList.add("show");

};


window.qty=(id,n)=>{

 let item=
 cart.find(x=>x.id===id);


 if(item){

  item.qty+=n;


  if(item.qty<1){

   cart=
   cart.filter(
    y=>y.id!==id
   );

  }

 }


 save();

 openCart();

};


window.checkout=async()=>{

 if(!cart.length){

  cartMsg.textContent=
  "Your cart is empty.";

  return;

 }


 if(!user){

  cartMsg.textContent=
  "Please login first.";

  return;

 }


 let items=
 cart.map(
 x=>({

  productId:x.id,

  name:
  products[x.id]?.name||"",

  price:
  Number(
   products[x.id]?.price||0
  ),

  quantity:x.qty

 })
 );


 let totalAmount=
 items.reduce(
  (a,x)=>
  a+
  x.price*x.quantity,
  0
 );


 let orderRef=
 push(ref(db,"orders"));


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

   status:
   "pending",

   createdAt:
   Date.now()

  }
 );


 cart=[];

 save();


 cartMsg.textContent=
 "Order placed successfully.";

};


window.openAccount=()=>{

 accountModal.classList.add("show");

};


window.closeM=id=>{

 document
 .getElementById(id)
 .classList.remove("show");

};


window.login=async()=>{

 try{

  await signInWithEmailAndPassword(
   auth,
   email.value,
   password.value
  );


  accountMsg.textContent=
  "Login successful.";


  setTimeout(
   ()=>closeM("accountModal"),
   600
  );


 }catch(e){

  accountMsg.textContent=
  e.message;

 }

};


window.register=async()=>{

 try{

  let r=
  await createUserWithEmailAndPassword(
   auth,
   email.value,
   password.value
  );


  await set(
   ref(db,"users/"+r.user.uid),
   {

    email:
    r.user.email,

    createdAt:
    Date.now()

   }
  );


  accountMsg.textContent=
  "Account created successfully.";


  setTimeout(
   ()=>closeM("accountModal"),
   600
  );


 }catch(e){

  accountMsg.textContent=
  e.message;

 }

};


save();

</script>

</body>
</html>
