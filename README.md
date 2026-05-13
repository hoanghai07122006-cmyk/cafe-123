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
