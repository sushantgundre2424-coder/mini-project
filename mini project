# mini-project
<!DOCTYPE html>
<html>
<head>
<title>STICKUS PRO</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
body {
  margin:0;
  font-family: Arial;
  background: lightgray;
}

/* Header */
header {
  background: purple;
  color: white;
  padding: 10px;
  position: sticky;
  top: 0;
}

nav {
  display:flex;
  justify-content: space-between;
  align-items: center;
}

.logo { font-size:22px; font-weight:bold; }

.cart {
  background:white;
  color:black;
  padding:5px 10px;
  border-radius:20px;
  cursor:pointer;
}

/* Search */
.search {
  width:100%;
  padding:8px;
  margin-top:10px;
  border:none;
  border-radius:5px;
}

/* Categories */
.categories {
  text-align:center;
  margin:10px;
}

.categories button {
  margin:5px;
  padding:8px 12px;
  border:none;
  background: purple;
  color:white;
  cursor:pointer;
}

.categories button:hover {
  opacity:0.8;
}

/* Products */
.products {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:15px;
  padding:15px;
}

.card {
  background:white;
  padding:10px;
  border-radius:10px;
  text-align:center;
}

.card img {
  width:100%;
  height:140px;
  object-fit:contain;
}

button {
  background: deeppink;
  color:white;
  border:none;
  padding:6px;
  cursor:pointer;
  margin-top:5px;
}

/* Cart */
.cart-box {
  position:fixed;
  right:10px;
  top:70px;
  background:white;
  width:260px;
  padding:10px;
  border-radius:10px;
  display:none;
}

.checkout {
  background:green;
  width:100%;
  margin-top:10px;
}

.rating { color:gold; }

/* Footer */
footer {
  background:black;
  color:white;
  text-align:center;
  padding:10px;
}
</style>
</head>

<body>

<header>
  <nav>
    <div class="logo">STICKUS</div>
    <div class="cart" onclick="toggleCart()">Cart (<span id="count">0</span>)</div>
  </nav>

  <input type="text" class="search" placeholder="Search stickers..." onkeyup="searchProducts(this.value)">
</header>

<!-- Categories -->
<div class="categories">
  <button onclick="filterCategory('all')">All</button>
  <button onclick="filterCategory('gaming')">Gaming</button>
  <button onclick="filterCategory('music')">Music</button>
  <button onclick="filterCategory('nature')">Nature</button>
  <button onclick="filterCategory('vehicle')">Vehicle</button>
  <button onclick="filterCategory('emoji')">Emoji</button>
</div>

<!-- Products -->
<div class="products" id="products"></div>

<!-- Cart -->
<div class="cart-box" id="cartBox">
  <h3>Your Cart</h3>
  <ul id="cartItems"></ul>
  <p>Total: ₹<span id="total">0</span></p>
  <button class="checkout" onclick="checkout()">Checkout</button>
</div>

<footer>
  <p>©️ 2026 STICKUS PRO</p>
</footer>

<script>

// 🧠 EASY TO EDIT PRODUCTS HERE
const products = [
  {name:"Gamer Sticker", price:249, category:"gaming", img:"https://cdn-icons-png.flaticon.com/512/686/686589.png", rating:5},
  {name:"Controller Sticker", price:199, category:"gaming", img:"https://cdn-icons-png.flaticon.com/512/1055/1055687.png", rating:4},
  {name:"Music Sticker", price:169, category:"music", img:"https://cdn-icons-png.flaticon.com/512/727/727269.png", rating:4},
  {name:"Headphone Sticker", price:179, category:"music", img:"https://cdn-icons-png.flaticon.com/512/727/727245.png", rating:5},
  {name:"Nature Sticker", price:209, category:"nature", img:"https://cdn-icons-png.flaticon.com/512/2909/2909765.png", rating:4},
  {name:"Mountain Sticker", price:219, category:"nature", img:"https://cdn-icons-png.flaticon.com/512/414/414927.png", rating:5},
  {name:"Car Sticker", price:199, category:"vehicle", img:"https://cdn-icons-png.flaticon.com/512/744/744465.png", rating:5},
  {name:"Bike Sticker", price:179, category:"vehicle", img:"https://cdn-icons-png.flaticon.com/512/2972/2972185.png", rating:4},
  {name:"Emoji Sticker", price:99, category:"emoji", img:"https://cdn-icons-png.flaticon.com/512/742/742751.png", rating:4},
  {name:"Cool Emoji", price:119, category:"emoji", img:"https://cdn-icons-png.flaticon.com/512/742/742940.png", rating:5}
];

// 🔧 STATE
let cart = JSON.parse(localStorage.getItem("cart")) || [];
let currentCategory = "all";
let searchText = "";

// ⭐ Rating
function stars(n){
  return "★".repeat(n) + "☆".repeat(5-n);
}

// 🛍️ Display
function display(list){
  let box = document.getElementById("products");
  box.innerHTML = "";

  list.forEach((p,i)=>{
    box.innerHTML += `
      <div class="card">
        <img src="${p.img}">
        <h3>${p.name}</h3>
        <div class="rating">${stars(p.rating)}</div>
        <p>₹${p.price}</p>
        <button onclick="add(${i})">Add</button>
      </div>
    `;
  });
}

// 🛒 Cart functions
function add(i){
  cart.push(products[i]);
  saveCart();
}

function saveCart(){
  localStorage.setItem("cart", JSON.stringify(cart));
  updateCart();
}

function updateCart(){
  document.getElementById("count").innerText = cart.length;

  let list = document.getElementById("cartItems");
  let total = 0;
  list.innerHTML = "";

  cart.forEach((item,i)=>{
    total += item.price;
    list.innerHTML += `
      <li>
        ${item.name} ₹${item.price}
        <button onclick="removeItem(${i})">X</button>
      </li>
    `;
  });

  document.getElementById("total").innerText = total;
}

function removeItem(i){
  cart.splice(i,1);
  saveCart();
}

function toggleCart(){
  let box = document.getElementById("cartBox");
  box.style.display = box.style.display==="block" ? "none":"block";
}

function checkout(){
  alert("Order placed successfully!");
  cart=[];
  saveCart();
}

// 🔍 Filters
function filterCategory(cat){
  currentCategory = cat;
  applyFilters();
}

function searchProducts(text){
  searchText = text.toLowerCase();
  applyFilters();
}

function applyFilters(){
  let filtered = products.filter(p=>{
    let matchCategory = currentCategory==="all" || p.category===currentCategory;
    let matchSearch = p.name.toLowerCase().includes(searchText);
    return matchCategory && matchSearch;
  });

  display(filtered);
}

// 🚀 Init
applyFilters();
updateCart();

</script>

</body>
</html>
