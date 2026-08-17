<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>NovaStore Admin</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Arial,sans-serif;
}

body{
    background:#f5f6f8;
    color:#222;
}

header{
    background:#111827;
    color:white;
    padding:18px 20px;
}

header h1{
    max-width:1100px;
    margin:auto;
}

.container{
    max-width:1100px;
    margin:auto;
    padding:25px 15px;
}

.box{
    background:white;
    padding:20px;
    border-radius:12px;
    margin-bottom:20px;
    box-shadow:0 2px 10px #00000012;
}

input,select{
    width:100%;
    padding:12px;
    border:1px solid #ccc;
    border-radius:7px;
    margin:6px 0 12px;
}

button{
    border:0;
    border-radius:7px;
    padding:11px 15px;
    cursor:pointer;
}

.primary{
    background:#22c55e;
    color:white;
    width:100%;
    font-weight:bold;
}

.dark{
    background:#111827;
    color:white;
}

.danger{
    background:#ef4444;
    color:white;
}

.hidden{
    display:none;
}

.product{
    border:1px solid #ddd;
    border-radius:10px;
    padding:15px;
    margin-top:12px;
    display:flex;
    justify-content:space-between;
    gap:15px;
    align-items:center;
}

.product-info{
    flex:1;
}

.product-info h3{
    margin-bottom:6px;
}

.product-info p{
    color:#666;
    font-size:14px;
}

.actions{
    display:flex;
    gap:7px;
}

.status{
    padding:12px;
    border-radius:7px;
    margin-bottom:15px;
    background:#eef2ff;
}

@media(max-width:650px){
    .product{
        flex-direction:column;
        align-items:stretch;
    }

    .actions{
        width:100%;
    }

    .actions button{
        flex:1;
    }
}
</style>
</head>

<body>

<header>
<h1>NovaStore Admin</h1>
</header>

<div class="container">

<!-- LOGIN -->

<div id="loginBox" class="box">

<h2>Admin Login</h2>

<br>

<input
id="email"
type="email"
placeholder="Admin email"
>

<input
id="password"
type="password"
placeholder="Password"
>

<button
class="primary"
onclick="login()"
>
Login
</button>

<p id="loginStatus" style="margin-top:12px;color:#ef4444"></p>

</div>


<!-- DASHBOARD -->

<div id="dashboard" class="hidden">

<div class="box">

<h2>Admin Dashboard</h2>

<p id="adminEmail" style="margin:8px 0;color:#666"></p>

<button
class="dark"
onclick="logout()"
>
Logout
</button>

</div>


<!-- ADD PRODUCT -->

<div class="box">

<h2 id="formTitle">
Add Product
</h2>

<br>

<input
id="productName"
type="text"
placeholder="Product name"
>

<input
id="productPrice"
type="number"
placeholder="Price"
>

<input
id="productOld"
type="number"
placeholder="Old price"
>

<select id="productCategory">

<option value="Electronics">
Electronics
</option>

<option value="Fashion">
Fashion
</option>

<option value="Home">
Home
</option>

<option value="Accessories">
Accessories
</option>

</select>

<input
id="productIcon"
type="text"
placeholder="Product icon e.g. 🎧"
>

<input
id="productDescription"
type="text"
placeholder="Product description"
>

<button
class="primary"
onclick="saveProduct()"
id="saveButton"
>
Add Product
</button>

<br><br>

<button
class="dark hidden"
onclick="cancelEdit()"
id="cancelButton"
>
Cancel Edit
</button>

<p id="productStatus" style="margin-top:12px"></p>

</div>


<!-- PRODUCTS -->

<div class="box">

<h2>Products</h2>

<div id="productsList">
Loading products...
</div>

</div>

</div>

</div>


<script type="module">

import { initializeApp }
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
    getAuth,
    signInWithEmailAndPassword,
    onAuthStateChanged,
    signOut
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

import {
    getDatabase,
    ref,
    push,
    set,
    get,
    remove
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js";


/* FIREBASE */

const firebaseConfig = {

    apiKey:
    "AIzaSyCNrU3igTkkcQ0Z6Zq1dluKw_s_3yHovjE",

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


const app = initializeApp(firebaseConfig);

const auth = getAuth(app);

const db = getDatabase(app);


/* ADMIN EMAIL */

const ADMIN_EMAIL =
"Sbgodstime@gmail.com";


/* EDITING */

let editingId = null;


/* LOGIN */

window.login = async function(){

    const email =
    document.getElementById("email").value.trim();

    const password =
    document.getElementById("password").value;

    const status =
    document.getElementById("loginStatus");

    status.textContent = "";

    if(!email || !password){

        status.textContent =
        "Enter your email and password.";

        return;
    }

    try{

        const result =
        await signInWithEmailAndPassword(
            auth,
            email,
            password
        );

        if(
            result.user.email.toLowerCase() !==
            ADMIN_EMAIL.toLowerCase()
        ){

            await signOut(auth);

            status.textContent =
            "This account is not authorized as an admin.";

            return;
        }

    }catch(error){

        console.error(error);

        status.textContent =
        "Login failed. Check your email and password.";

    }

};


/* AUTH STATE */

onAuthStateChanged(auth,user => {

    if(
        user &&
        user.email &&
        user.email.toLowerCase() ===
        ADMIN_EMAIL.toLowerCase()
    ){

        document
        .getElementById("loginBox")
        .classList.add("hidden");

        document
        .getElementById("dashboard")
        .classList.remove("hidden");

        document
        .getElementById("adminEmail")
        .textContent =
        "Logged in as: " + user.email;

        loadProducts();

    }else{

        document
        .getElementById("loginBox")
        .classList.remove("hidden");

        document
        .getElementById("dashboard")
        .classList.add("hidden");

    }

});


/* LOGOUT */

window.logout = async function(){

    await signOut(auth);

};


/* LOAD PRODUCTS */

async function loadProducts(){

    const list =
    document.getElementById("productsList");

    list.innerHTML =
    "Loading products...";

    try{

        const snapshot =
        await get(ref(db,"products"));

        if(!snapshot.exists()){

            list.innerHTML =
            "<p>No products yet.</p>";

            return;
        }

        const data =
        snapshot.val();

        list.innerHTML = "";

        Object.entries(data).forEach(
            ([id,p]) => {

                const div =
                document.createElement("div");

                div.className =
                "product";

                div.innerHTML = `

                    <div class="product-info">

                        <h3>
                            ${escapeHtml(p.icon || "📦")}
                            ${escapeHtml(p.name || "")}
                        </h3>

                        <p>
                            Category:
                            ${escapeHtml(p.cat || "")}
                        </p>

                        <p>
                            Price:
                            ₦${Number(p.price || 0).toLocaleString("en-NG")}
                        </p>

                    </div>

                    <div class="actions">

                        <button
                            class="dark"
                            onclick="editProduct('${id}')"
                        >
                            Edit
                        </button>

                        <button
                            class="danger"
                            onclick="deleteProduct('${id}')"
                        >
                            Delete
                        </button>

                    </div>
                `;

                list.appendChild(div);

            }
        );

    }catch(error){

        console.error(error);

        list.innerHTML =
        "<p style='color:red'>Could not load products.</p>";

    }

}


/* SAVE PRODUCT */

window.saveProduct = async function(){

    const name =
    document.getElementById("productName")
    .value.trim();

    const price =
    Number(
        document.getElementById("productPrice")
        .value
    );

    const old =
    Number(
        document.getElementById("productOld")
        .value
    );

    const cat =
    document.getElementById("productCategory")
    .value;

    const icon =
    document.getElementById("productIcon")
    .value.trim() || "📦";

    const desc =
    document.getElementById("productDescription")
    .value.trim();

    const status =
    document.getElementById("productStatus");

    if(!name || !price){

        status.style.color =
        "#ef4444";

        status.textContent =
        "Enter a product name and price.";

        return;
    }

    const product = {

        name:name,

        price:price,

        old:old || price,

        cat:cat,

        icon:icon,

        desc:desc

    };

    try{

        if(editingId){

            await set(
                ref(db,"products/" + editingId),
                product
            );

            status.style.color =
            "#15803d";

            status.textContent =
            "Product updated successfully.";

        }else{

            const newProduct =
            push(ref(db,"products"));

            await set(
                newProduct,
                product
            );

            status.style.color =
            "#15803d";

            status.textContent =
            "Product added successfully.";

        }

        clearForm();

        loadProducts();

    }catch(error){

        console.error(error);

        status.style.color =
        "#ef4444";

        status.textContent =
        "Could not save product. Check Firebase rules.";

    }

};


/* EDIT PRODUCT */

window.editProduct = async function(id){

    try{

        const snapshot =
        await get(
            ref(db,"products/" + id)
        );

        if(!snapshot.exists()){

            alert("Product not found.");

            return;
        }

        const p =
        snapshot.val();

        editingId = id;

        document.getElementById("productName")
        .value = p.name || "";

        document.getElementById("productPrice")
        .value = p.price || "";

        document.getElementById("productOld")
        .value = p.old || "";

        document.getElementById("productCategory")
        .value = p.cat || "Electronics";

        document.getElementById("productIcon")
        .value = p.icon || "";

        document.getElementById("productDescription")
        .value = p.desc || "";

        document.getElementById("formTitle")
        .textContent =
        "Edit Product";

        document.getElementById("saveButton")
        .textContent =
        "Update Product";

        document.getElementById("cancelButton")
        .classList.remove("hidden");

        window.scrollTo({
            top:0,
            behavior:"smooth"
        });

    }catch(error){

        console.error(error);

        alert("Could not load product.");

    }

};


/* DELETE PRODUCT */

window.deleteProduct = async function(id){

    if(
        !confirm(
            "Are you sure you want to delete this product?"
        )
    ){

        return;

    }

    try{

        await remove(
            ref(db,"products/" + id)
        );

        loadProducts();

    }catch(error){

        console.error(error);

        alert(
            "Could not delete product."
        );

    }

};


/* CANCEL EDIT */

window.cancelEdit = function(){

    clearForm();

};


/* CLEAR FORM */

function clearForm(){

    editingId = null;

    document.getElementById("productName")
    .value = "";

    document.getElementById("productPrice")
    .value = "";

    document.getElementById("productOld")
    .value = "";

    document.getElementById("productIcon")
    .value = "";

    document.getElementById("productDescription")
    .value = "";

    document.getElementById("formTitle")
    .textContent =
    "Add Product";

    document.getElementById("saveButton")
    .textContent =
    "Add Product";

    document.getElementById("cancelButton")
    .classList.add("hidden");

}


/* ESCAPE HTML */

function escapeHtml(value){

    return String(value)

    .replace(/&/g,"&amp;")
    .replace(/</g,"&lt;")
    .replace(/>/g,"&gt;")
    .replace(/"/g,"&quot;")
    .replace(/'/g,"&#039;");

}

</script>

</body>
</html>
