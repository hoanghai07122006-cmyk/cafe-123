<%@ Page Language="C#" AutoEventWireup="true" %>

<!DOCTYPE html>
<html lang="vi">

<head runat="server">

<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>

<title>CHILL COFFEE</title>

<script src="https://cdn.tailwindcss.com"></script>

<style>

body{
    font-family:Arial,sans-serif;
    background:#a97857;
    overflow-x:hidden;
}

.hidden{
    display:none;
}
#bankSection img{
width:300px;
height:300px;
object-fit:contain;
background:white;
padding:10px;
}
.slide{
    position:absolute;
    inset:0;
    opacity:0;
    transition:1s;
}

.slide.active{
    opacity:1;
}

.slide-image{
    width:100%;
    height:100%;
    object-fit:cover;
    animation:zoom 8s linear infinite;
}

@keyframes zoom{

from{
transform:scale(1);
}

to{
transform:scale(1.1);
}

}

.overlay{
    position:absolute;
    inset:0;
    background:rgba(0,0,0,0.5);
}

.slide-content{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    text-align:center;
    color:white;
    z-index:5;
}

.slider-btn{
    position:absolute;
    top:50%;
    transform:translateY(-50%);
    width:60px;
    height:60px;
    border:none;
    border-radius:50%;
    background:rgba(255,255,255,0.3);
    color:white;
    font-size:30px;
    cursor:pointer;
    z-index:10;
}

.left-btn{
left:20px;
}

.right-btn{
right:20px;
}

.product-card img{
transition:0.5s;
}

.product-card:hover img{
transform:scale(1.05);
}
.product-card{
    position:relative;
}

.delete-btn{
    position:absolute;
    top:10px;
    right:10px;
    width:35px;
    height:35px;
    border:none;
    border-radius:50%;
    background:red;
    color:white;
    font-size:18px;
    font-weight:bold;
    cursor:pointer;
    z-index:20;
}

.delete-btn:hover{
    background:darkred;
}

.image-list{
    display:flex;
    gap:8px;
    justify-content:center;
    margin-top:10px;
}

.image-list img{
    width:55px;
    height:55px;
    object-fit:cover;
    border-radius:10px;
    cursor:pointer;
    border:2px solid white;
    transition:0.3s;
}

.image-list img:hover{
    transform:scale(1.1);
    border:2px solid #ffcc99;
}

.remove-cart-btn{
    background:red;
    color:white;
    border:none;
    width:35px;
    height:35px;
    border-radius:50%;
    cursor:pointer;
    font-weight:bold;
}

.remove-cart-btn:hover{
    background:darkred;
}
</style>

</head>

<body>

<form id="form1" runat="server">

<!-- LOGIN -->

<section
id="loginPage"
class="min-h-screen flex items-center justify-center relative overflow-hidden"
>

<img
src="https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?q=80&w=2070&auto=format&fit=crop"
class="absolute inset-0 w-full h-full object-cover"
>

<div class="absolute inset-0 bg-black bg-opacity-60"></div>

<div class="relative z-10 bg-white/10 backdrop-blur-lg border border-white/20 p-10 rounded-[40px] shadow-2xl w-[430px]">

<div class="text-center mb-8">
    <h1 class="text-5xl font-bold text-white mb-3">

CHILL COFFEE

</h1>

<p class="text-gray-200 text-lg">

Coffee & Chill Space

</p>

</div>

<input
id="username"
type="text"
placeholder="Tên đăng nhập"
class="w-full bg-white/20 border border-white/30 text-white placeholder-gray-200 p-4 rounded-2xl outline-none mb-5"
/>

<input
id="password"
type="password"
placeholder="Mật khẩu"
class="w-full bg-white/20 border border-white/30 text-white placeholder-gray-200 p-4 rounded-2xl outline-none mb-5"
/>

<select
id="role"
class="w-full bg-white/20 border border-white/30 text-white p-4 rounded-2xl outline-none mb-6"
>

<option value="Khách Hàng" class="text-black">
Khách Hàng
</option>

<option value="Nhân Viên" class="text-black">
Nhân Viên
</option>

<option value="Chủ Cửa Hàng" class="text-black">
Chủ Cửa Hàng
</option>

</select>

<button
type="button"
onclick="login()"
class="w-full bg-[#4d2416] hover:bg-[#2e130b] text-white py-4 rounded-2xl text-xl font-bold"
>

Đăng Nhập

</button>

<button
type="button"
onclick="openRegister()"
class="w-full mt-4 bg-white/20 hover:bg-white/30 text-white py-4 rounded-2xl border border-white/30"
>

Đăng Ký Tài Khoản

</button>

</div>

</section>

<!-- REGISTER -->

<div
id="registerModal"
class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
>

<div class="bg-white p-10 rounded-3xl w-[450px]">

<h2 class="text-3xl font-bold text-[#4d2416] mb-6">

Đăng Ký Tài Khoản

</h2>

<input
id="registerUsername"
type="text"
placeholder="Tên đăng nhập"
class="w-full border border-[#a97857] p-4 rounded-xl mb-5"
/>

<input
id="registerPassword"
type="password"
placeholder="Mật khẩu"
class="w-full border border-[#a97857] p-4 rounded-xl mb-5"
/>

<button
type="button"
onclick="registerAccount()"
class="w-full bg-[#4d2416] text-white py-4 rounded-xl mb-4"
>

Đăng Ký

</button>

<button
type="button"
onclick="closeRegister()"
class="w-full bg-red-500 text-white py-4 rounded-xl"
>

Hủy

</button>

</div>

</div>

<!-- WEBSITE -->

<div id="shopPage" class="hidden">

<header class="fixed top-0 left-0 w-full bg-[#a97857] z-50">

<div class="max-w-7xl mx-auto px-6 py-5 flex justify-between items-center">

<div class="flex items-center gap-4">

<img
src="https://cdn-icons-png.flaticon.com/512/924/924514.png"
class="w-16 h-16"
/>

<h1 class="text-3xl text-white font-bold tracking-[4px]">

CHILL COFFEE

</h1>

</div>

<div class="flex gap-8 text-white text-lg font-medium">

<button type="button" onclick="showSection('homeSection')">
Home
</button>

<button type="button" onclick="showSection('productSection')">
Menu
</button>

<button type="button" onclick="showSection('warehouseSection')">
Kho
</button>

<button type="button" onclick="showSection('ingredientSection')">
Nguyên Liệu
</button>

<button type="button" onclick="showSection('billSection')">
Bills
</button>
    <button type="button" onclick="showSection('revenueSection')">
Doanh Thu
</button>
</div>
    <button
type="button"
onclick="logout()"
class="bg-red-500 text-white px-5 py-3 rounded-xl"
>

Đăng Xuất

</button>

</div>

</header>

<!-- HOME -->

<section id="homeSection" class="pt-32 min-h-screen">

<div class="relative w-[95%] mx-auto h-[550px] overflow-hidden rounded-[30px] shadow-2xl">

<div class="slide active">

<img
src="https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?q=80&w=2070&auto=format&fit=crop"
class="slide-image"
/>

<div class="overlay"></div>

<div class="slide-content">

<p class="text-4xl tracking-[10px] mb-5">
Freshly Roasted
</p>

<h1 class="text-8xl tracking-[20px] mb-10">
COFFEE
</h1>

<button
type="button"
onclick="showSection('productSection')"
class="bg-[#4d2416] px-10 py-4 rounded-full text-white border border-white"
>

Shop Now

</button>

</div>

</div>

<button
type="button"
class="slider-btn left-btn"
onclick="prevSlide()"
>

❮

</button>

<button
type="button"
class="slider-btn right-btn"
onclick="nextSlide()"
>

❯

</button>

</div>

</section>

<!-- MENU -->

<section
id="productSection"
class="hidden pt-32 py-20 min-h-screen"
>

<div class="max-w-7xl mx-auto px-6">

<div class="bg-white p-6 rounded-3xl shadow-lg mb-10">

<div class="flex justify-between items-center">

<h3 class="text-3xl font-bold text-[#4d2416]">
Đơn Nước
</h3>

<button
type="button"
onclick="checkout(); return false;"
class="bg-[#4d2416] text-white px-8 py-3 rounded-xl"
>

Thanh Toán

</button>

</div>

<input
id="searchCart"
type="text"
placeholder="Tìm kiếm sản phẩm..."
onkeyup="searchCart()"
class="w-full border border-[#a97857] p-4 rounded-xl mt-5"
/>

<div id="cartList" class="mt-6 space-y-4"></div>
    <div class="mt-6">

<select
id="paymentMethod"
onchange="changePaymentMethod()"
class="w-full border border-[#a97857] p-4 rounded-xl"
>

<option value="cash">
Thanh toán tiền mặt
</option>

<option value="bank">
Chuyển khoản ngân hàng
</option>

</select>

</div>

<div
id="bankSection"
class="hidden mt-6 bg-[#f8ede5] p-6 rounded-2xl"
>

<h3 class="text-2xl font-bold text-[#4d2416] mb-5">

Thông Tin Chuyển Khoản
   
</h3>

    <img
id="qrImage"
class="w-72 mx-auto mb-5 rounded-2xl border-4 border-white shadow-xl bg-white p-2"
style="display:block;width:300px;height:300px;"
alt="QR Chuyển Khoản"
/>
    <p class="text-green-600 font-bold text-center text-xl mt-4">
Quét mã QR để thanh toán
</p>
<p class="text-xl mb-2">
Ngân hàng: MB BANK
</p>

<p class="text-xl mb-2">
Số tài khoản: 2206200677777
</p>

<p class="text-xl">
Chủ tài khoản: TRAN DUY HIEU
</p>

</div>
</div>

<div
id="productContainer"
class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8"
>

</div>

</div>

</section>

<!-- KHO -->

<section
id="warehouseSection"
class="hidden pt-32 py-20 min-h-screen"
>

<div class="max-w-7xl mx-auto px-6">

<div class="bg-white p-8 rounded-3xl shadow-xl mb-10">

<h2 class="text-5xl font-bold text-[#4d2416] mb-10">

Kho Sản Phẩm

</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10">

<input
id="newProductName"
type="text"
placeholder="Tên sản phẩm"
class="border p-4 rounded-xl"
/>

<input
id="newProductPrice"
type="number"
placeholder="Giá sản phẩm"
class="border p-4 rounded-xl"
/>

<input
id="newProductImage"
type="file"
accept="image/*"
class="border p-4 rounded-xl"
/>

<button
type="button"
onclick="addNewProduct()"
class="bg-[#4d2416] text-white p-4 rounded-xl"
>

Thêm Sản Phẩm

</button>

</div>

<div
id="warehouseList"
class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
>

</div>

</div>

</div>

</section>

<!-- NGUYÊN LIỆU -->

<section
id="ingredientSection"
class="hidden pt-32 py-20 min-h-screen"
>

<div class="max-w-6xl mx-auto bg-white p-10 rounded-3xl shadow-xl">

<h2 class="text-5xl font-bold text-[#4d2416] mb-10">

Nguyên Liệu

</h2>

<div class="flex gap-4 mb-10">

<input
id="ingredientName"
type="text"
placeholder="Tên nguyên liệu"
class="flex-1 border p-4 rounded-xl"
/>

<input
id="ingredientQty"
type="number"
placeholder="Số lượng"
class="flex-1 border p-4 rounded-xl"
/>

<button
type="button"
onclick="addIngredient()"
class="bg-[#4d2416] text-white px-8 rounded-xl"
>

Thêm

</button>

</div>

<div id="ingredientList" class="space-y-5"></div>

</div>

</section>

<!-- HÓA ĐƠN -->

<section
id="billSection"
class="hidden pt-32 py-20 min-h-screen"
>

<div class="max-w-5xl mx-auto bg-white p-10 rounded-3xl shadow-xl">

<h2 class="text-5xl font-bold text-[#4d2416] mb-10">

Hóa Đơn

</h2>

<div id="billContent"></div>

</div>

</section>
    <!-- DOANH THU -->

<section
id="revenueSection"
class="hidden pt-32 py-20 min-h-screen"
>

<div class="max-w-6xl mx-auto">

<div class="bg-white p-10 rounded-3xl shadow-xl">

<h2 class="text-5xl font-bold text-[#4d2416] mb-10">

Doanh Thu Quán Cafe

</h2>

<div class="grid grid-cols-1 md:grid-cols-3 gap-8">

<div class="bg-[#f8ede5] p-8 rounded-3xl text-center">

<p class="text-2xl text-[#4d2416] mb-4">
Tổng Doanh Thu
</p>

<h1
id="totalRevenue"
class="text-5xl font-bold text-green-600"
>
0đ
</h1>

</div>

<div class="bg-[#f8ede5] p-8 rounded-3xl text-center">

<p class="text-2xl text-[#4d2416] mb-4">
Tổng Hóa Đơn
</p>

<h1
id="totalBills"
class="text-5xl font-bold text-blue-600"
>
0
</h1>

</div>

<div class="bg-[#f8ede5] p-8 rounded-3xl text-center">

<p class="text-2xl text-[#4d2416] mb-4">
Sản Phẩm
</p>

<h1
id="totalProducts"
class="text-5xl font-bold text-red-500"
>
0
</h1>

</div>

</div>

</div>

</div>

</section>
</div>

</form>

<script>

    let currentRole = "";
    let currentUser = "";

    let accounts =
        JSON.parse(localStorage.getItem("accounts")) || [

            {
                username: "admin",
                password: "999",
                role: "Chủ Cửa Hàng"
            },

            {
                username: "nhanvien",
                password: "123",
                role: "Nhân Viên"
            }

        ];

    let products =
        JSON.parse(localStorage.getItem("products")) || [

            {
                name: "Espresso Coffee",
                price: 55000,
                image: "https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?q=80&w=1200&auto=format&fit=crop"
            },

            {
                name: "Mocha Coffee",
                price: 65000,
                image: "https://images.unsplash.com/photo-1517701550927-30cf4ba1f864?q=80&w=1200&auto=format&fit=crop"
            }

        ];

    let ingredients =
        JSON.parse(localStorage.getItem("ingredients")) || [

            { name: "Cafe", qty: 100 },
            { name: "Sữa", qty: 50 },
            { name: "Nước Ngọt", qty: 70 }

        ];

    let cart = [];

    function saveProducts() {

        localStorage.setItem(
            "products",
            JSON.stringify(products)
        );

    }

    function saveIngredients() {

        localStorage.setItem(
            "ingredients",
            JSON.stringify(ingredients)
        );

    }

    function login() {

        const username =
            document.getElementById("username").value;

        const password =
            document.getElementById("password").value;

        const role =
            document.getElementById("role").value;

        const user = accounts.find(acc =>

            acc.username == username &&
            acc.password == password &&
            acc.role == role

        );

        if (user) {

            currentRole = role;
            currentUser = username;
            sessionStorage.setItem("loggedIn", "true");
            sessionStorage.setItem("currentUser", username);
            sessionStorage.setItem("currentRole", role);
            document
                .getElementById("loginPage")
                .classList.add("hidden");

            document
                .getElementById("shopPage")
                .classList.remove("hidden");

            showSection("homeSection");

            renderProducts();
            renderWarehouse();
            renderIngredients();
            renderBills();

        }
        else {

            alert("Sai tài khoản!");

        }

    }

    function openRegister() {

        document
            .getElementById("registerModal")
            .classList.remove("hidden");

    }

    function closeRegister() {

        document
            .getElementById("registerModal")
            .classList.add("hidden");

    }

    function registerAccount() {

        const username =
            document.getElementById("registerUsername").value;

        const password =
            document.getElementById("registerPassword").value;

        accounts.push({

            username,
            password,
            role: "Khách Hàng"

        });

        localStorage.setItem(
            "accounts",
            JSON.stringify(accounts)
        );

        alert("Đăng ký thành công!");

        closeRegister();

    }

    function logout() {

        sessionStorage.clear();

        location.reload();

    }


    function showSection(id) {

        if (
            id == "warehouseSection" ||
            id == "ingredientSection" ||
            id == "revenueSection"
        ) {

            if (
                currentRole == "Khách Hàng" &&
                id != "revenueSection"
            ) {
                if (
                    id == "revenueSection" &&
                    currentRole != "Chủ Cửa Hàng"
                ) {

                    alert("Chỉ chủ cửa hàng được xem doanh thu!");

                    return;

                }
                alert("Bạn không có quyền truy cập!");

                return;

            }

        }

        document
            .querySelectorAll("#shopPage section")
            .forEach(section => {

                section.classList.add("hidden");

            });

        document
            .getElementById(id)
            .classList.remove("hidden");

    }

    function renderProducts() {

        let html = "";

        products.forEach((product, index) => {

            html += `

<div class="product-card bg-[#4d2416] rounded-[30px] overflow-hidden shadow-2xl text-white">

${currentRole != "Khách Hàng" ? `
<button
class="delete-btn"
onclick="deleteProduct(${index})"
>
X
</button>
` : ""}

<div class="p-3">

<img
id="mainImage-${index}"
src="${product.image}"
class="w-full h-[350px] object-cover rounded-2xl"
>
<div class="image-list">

<img
src="${product.image}"
onclick="changeImage('mainImage-${index}',this.src)"
>

<img
src="https://images.unsplash.com/photo-1509042239860-f550ce710b93?q=80&w=1200&auto=format&fit=crop"
onclick="changeImage('mainImage-${index}',this.src)"
>

<img
src="https://images.unsplash.com/photo-1517701550927-30cf4ba1f864?q=80&w=1200&auto=format&fit=crop"
onclick="changeImage('mainImage-${index}',this.src)"
>

</div>

</div>

<div class="p-6">

<input
value="${product.name}"
onchange="changeProductName(${index},this.value)"
class="w-full text-black p-3 rounded-xl mb-3"
${currentRole == "Khách Hàng" ? "readonly" : ""}
>

<input
value="${product.price}"
type="number"
onchange="changeProductPrice(${index},this.value)"
class="w-full text-black p-3 rounded-xl mb-3"
${currentRole == "Khách Hàng" ? "readonly" : ""}
>

<div class="flex gap-3 mb-3">

<input
id="qty-${index}"
type="number"
min="1"
value="1"
class="w-24 text-black p-3 rounded-xl"
/>

<button
type="button"
onclick="addToCart(${index}); return false;"
class="flex-1 bg-white text-[#4d2416] py-3 rounded-full font-bold"
>
Buy Now
</button>

</div>

</div>

</div>

`;

        });

        document
            .getElementById("productContainer")
            .innerHTML = html;

    }

    function addNewProduct() {

        const name =
            document.getElementById("newProductName").value;

        const price =
            document.getElementById("newProductPrice").value;

        const file =
            document.getElementById("newProductImage").files[0];

        if (!file) {

            alert("Chọn ảnh!");

            return;

        }

        const reader = new FileReader();

        reader.onload = function (e) {

            products.push({

                name: name,
                price: Number(price),
                image: e.target.result

            });

            saveProducts();

            renderProducts();
            renderWarehouse();

        };

        reader.readAsDataURL(file);

    }

    function renderWarehouse() {

        let html = "";

        products.forEach(product => {

            html += `

<div class="bg-[#f8ede5] rounded-3xl overflow-hidden shadow-xl p-5">

<img
src="${product.image}"
class="w-full h-[250px] object-cover rounded-2xl mb-5"
>

<h3 class="text-3xl font-bold text-[#4d2416] mb-3">

${product.name}

</h3>

<p class="text-2xl font-bold">

${product.price.toLocaleString()}đ

</p>

</div>

`;

        });

        document
            .getElementById("warehouseList")
            .innerHTML = html;

    }

    function changeProductName(index, value) {

        products[index].name = value;

        saveProducts();

        renderWarehouse();

    }

    function changeProductPrice(index, value) {

        products[index].price = Number(value);

        saveProducts();

        renderWarehouse();

    }

    function deleteProduct(index) {

        if (currentRole == "Khách Hàng") {

            alert("Bạn không có quyền xóa!");

            return;

        }

        products.splice(index, 1);

        saveProducts();

        renderProducts();
        renderWarehouse();

    }

    function addIngredient() {

        const name =
            document.getElementById("ingredientName").value;

        const qty =
            document.getElementById("ingredientQty").value;

        ingredients.push({

            name,
            qty: Number(qty)

        });

        saveIngredients();

        renderIngredients();

    }

    function renderIngredients() {

        let html = "";

        ingredients.forEach((item, index) => {

            html += `
            <div class="bg-[#f8ede5] p-6 rounded-2xl flex justify-between items-center">

<div>

<h3 class="text-3xl font-bold text-[#4d2416]">

${item.name}

</h3>

<p class="text-xl mt-2">

Số lượng: ${item.qty}

</p>

</div>

<div class="flex gap-4">

<button
type="button"
onclick="increaseIngredient(${index}); return false;"
class="bg-green-500 text-white px-6 py-3 rounded-xl"
>

+

</button>

<button
type="button"
onclick="decreaseIngredient(${index}); return false;"
class="bg-red-500 text-white px-6 py-3 rounded-xl"
>

-

</button>

</div>

</div>

`;

        });

        document
            .getElementById("ingredientList")
            .innerHTML = html;

    }

    function increaseIngredient(index) {

        ingredients[index].qty++;

        saveIngredients();

        renderIngredients();

    }

    function decreaseIngredient(index) {

        if (ingredients[index].qty > 0) {

            ingredients[index].qty--;

        }

        saveIngredients();

        renderIngredients();

    }

    function addToCart(index) {

        const qty = Number(
            document.getElementById(`qty-${index}`).value
        );

        if (qty <= 0) {

            alert("Số lượng không hợp lệ!");
            return;

        }

        let product = {

            name: products[index].name,
            price: products[index].price,
            image: products[index].image,
            qty: qty

        };

        cart.push(product);

        updateCart();

    }
    function removeCartItem(index) {

        cart.splice(index, 1);

        updateCart();

    }

    function updateCart() {
        let html = "";
        let total = 0;

        cart.forEach((item, index) => {

            total += item.price * item.qty;

            html += `

<div class="cart-item bg-[#f8ede5] p-5 rounded-2xl">

<div class="flex justify-between items-center">

<div>

<h3 class="text-2xl font-bold text-[#4d2416]">
${item.name}
</h3>

<p class="text-xl font-bold">
${item.price.toLocaleString()}đ x ${item.qty}
</p>

</div>

<button
class="remove-cart-btn"
onclick="removeCartItem(${index})"
>
X
</button>

</div>

</div>

`;

        });

        html += `

<div class="text-3xl font-bold text-[#4d2416] mt-6">

Tổng:
${total.toLocaleString()}đ

</div>

`;

        document
            .getElementById("cartList")
            .innerHTML = html;

    }

    function searchCart() {

        const keyword =
            document.getElementById("searchCart")
                .value
                .toLowerCase();

        const cartItems =
            document.querySelectorAll(".cart-item");

        cartItems.forEach(item => {

            const text =
                item.innerText.toLowerCase();

            if (text.includes(keyword)) {

                item.style.display = "block";

            }
            else {

                item.style.display = "none";

            }

        });

    }

    function checkout() {

        if (cart.length == 0) {

            alert("Chưa có món!");

            return;

        }

        let total = 0;
        let items = "";

        cart.forEach(item => {

            total += item.price * item.qty;

            items += `
<p>
${item.name}
- ${item.price.toLocaleString()}đ
x ${item.qty}
</p>
`;

        });
        const paymentMethod =
            document.getElementById("paymentMethod").value;
        let billHtml = `

<div class="bg-[#f8ede5] p-8 rounded-3xl shadow-lg mb-8">

<h3 class="text-3xl font-bold text-[#4d2416] mb-6">

Hóa Đơn Cafe

</h3>

<p><b>Khách hàng:</b> ${currentUser}</p>

<p>
<b>Thanh toán:</b>
${paymentMethod == "cash"
                ? "Tiền Mặt"
                : "Chuyển Khoản"}
</p>

<div class="mt-5">

${items}

</div>
<div class="text-3xl font-bold text-[#4d2416] mt-6">

Tổng:
${total.toLocaleString()}đ

</div>

</div>

`;

        let bills =
            JSON.parse(localStorage.getItem("bills")) || [];

        bills.push({

            username: currentUser,
            html: billHtml

        });

        localStorage.setItem(
            "bills",
            JSON.stringify(bills)
        );

        renderBills();

        cart = [];

        updateCart();

        alert("Thanh toán thành công!");

    }
    function updateRevenue() {

        let bills =
            JSON.parse(localStorage.getItem("bills")) || [];

        let revenue = 0;

        bills.forEach(bill => {

            const match =
                bill.html.match(/Tổng:\s*([\d\.]+)/);

            if (match) {

                revenue += Number(
                    match[1].replace(/\./g, '')
                );

            }

        });

        document
            .getElementById("totalRevenue")
            .innerText =
            revenue.toLocaleString() + "đ";

        document
            .getElementById("totalBills")
            .innerText =
            bills.length;

        document
            .getElementById("totalProducts")
            .innerText =
            products.length;

    }
    function renderBills() {

        let bills =
            JSON.parse(localStorage.getItem("bills")) || [];

        let html = "";

        bills.forEach(bill => {

            if (bill.username == currentUser) {

                html += bill.html;

            }

        });

        document
            .getElementById("billContent")
            .innerHTML = html;
        updateRevenue();
    }

    let slides =
        document.querySelectorAll(".slide");

    let currentSlide = 0;

    function showSlide(index) {

        slides.forEach(slide => {

            slide.classList.remove("active");

        });

        slides[index].classList.add("active");

    }

    function nextSlide() {

        currentSlide++;

        if (currentSlide >= slides.length) {

            currentSlide = 0;

        }

        showSlide(currentSlide);

    }

    function prevSlide() {

        currentSlide--;

        if (currentSlide < 0) {

            currentSlide = slides.length - 1;

        }

        showSlide(currentSlide);

    }

    function changeImage(id, src) {

        document.getElementById(id).src = src;

    }

    setInterval(() => {

        nextSlide();

    }, 5000);
    window.onload = function () {

        if (sessionStorage.getItem("loggedIn") == "true") {

            currentUser =
                sessionStorage.getItem("currentUser");

            currentRole =
                sessionStorage.getItem("currentRole");

            document
                .getElementById("loginPage")
                .classList.add("hidden");

            document
                .getElementById("shopPage")
                .classList.remove("hidden");

            showSection("homeSection");

            renderProducts();
            renderWarehouse();
            renderIngredients();
            renderBills();

        }

    }
</script>
<script>

    function changePaymentMethod() {

        const method =
            document.getElementById("paymentMethod").value;

        const bankSection =
            document.getElementById("bankSection");

        if (method == "bank") {

            bankSection.classList.remove("hidden");

            document.getElementById("qrImage").src =
                "https://img.vietqr.io/image/MB-2206209677777-compact2.png?amount=0&addInfo=ThanhToanCafe&accountName=TRAN%20DUY%20HIEU";

        }
        else {

            bankSection.classList.add("hidden");

        }

    }

</script>
</body>
</html>
