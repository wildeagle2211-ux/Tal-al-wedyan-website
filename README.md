<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Car Transfer System Pro</title>

<style>
body{
    font-family:Arial;
    margin:0;
    padding:20px;
    background:#0f172a;
    color:white;
    transition:0.3s;
}

.container{
    max-width:1000px;
    margin:auto;
}

.card{
    background:#111827;
    padding:20px;
    border-radius:12px;
}

input, select{
    width:100%;
    padding:10px;
    margin:5px 0;
    border-radius:8px;
    border:none;
}

button{
    padding:10px;
    background:#38bdf8;
    border:none;
    border-radius:8px;
    font-weight:bold;
    cursor:pointer;
    margin:5px;
}

.lang{
    background:#22c55e;
}

table{
    width:100%;
    margin-top:20px;
    border-collapse:collapse;
}

th, td{
    border:1px solid #333;
    padding:10px;
    text-align:center;
}

th{
    background:#1f2937;
}

/* RTL SUPPORT */
.rtl{
    direction:rtl;
    text-align:right;
}

.rtl input, .rtl select{
    text-align:right;
}
</style>

</head>

<body>

<div class="container">

<div class="card">

<h2 id="title">🚗 Car Transfer System Pro</h2>

<button class="lang" onclick="setLang('en')">English</button>
<button class="lang" onclick="setLang('ar')">العربية</button>

<input type="text" id="car" placeholder="Car Name / اسم السيارة">
<input type="text" id="customer" placeholder="Customer Name / اسم العميل">
<input type="text" id="phone" placeholder="Phone Number / رقم الهاتف">
<input type="number" id="fee" placeholder="Transfer Fee / رسوم النقل">

<select id="status">
    <option value="Completed">Completed / تم النقل</option>
    <option value="Pending">Pending / لم يتم النقل</option>
</select>

<input type="file" id="file">

<button onclick="addData()">Add Record</button>
<button onclick="window.print()">Print / طباعة</button>

<table>
<thead>
<tr>
<th>Car / سيارة</th>
<th>Customer / عميل</th>
<th>Phone / هاتف</th>
<th>Fee / رسوم</th>
<th>Status / حالة</th>
<th>File / ملف</th>
</tr>
</thead>

<tbody id="tableData"></tbody>

</table>

</div>

</div>

<script>

let data = JSON.parse(localStorage.getItem("cars")) || [];
render();

// ADD DATA
function addData(){

    let car = document.getElementById("car").value;
    let customer = document.getElementById("customer").value;
    let phone = document.getElementById("phone").value;
    let fee = document.getElementById("fee").value;
    let status = document.getElementById("status").value;

    let fileInput = document.getElementById("file");
    let fileName = fileInput.files.length > 0 ? fileInput.files[0].name : "";

    if(car=="" || customer=="" || phone=="" || fee==""){
        alert("Fill all fields");
        return;
    }

    data.push({
        car,
        customer,
        phone,
        fee,
        status,
        file:fileName
    });

    localStorage.setItem("cars", JSON.stringify(data));

    render();

    document.getElementById("car").value="";
    document.getElementById("customer").value="";
    document.getElementById("phone").value="";
    document.getElementById("fee").value="";
    document.getElementById("file").value="";
}

// RENDER
function render(){
    let table = document.getElementById("tableData");
    table.innerHTML="";

    data.forEach(item=>{
        table.innerHTML += `
        <tr>
            <td>${item.car}</td>
            <td>${item.customer}</td>
            <td>${item.phone}</td>
            <td>${item.fee}</td>
            <td>${item.status}</td>
            <td>${item.file || "-"}</td>
        </tr>
        `;
    });
}

// LANGUAGE SWITCH
function setLang(lang){

    if(lang === "ar"){
        document.body.classList.add("rtl");
        document.getElementById("title").innerText = "🚗 نظام نقل السيارات الاحترافي";
    }else{
        document.body.classList.remove("rtl");
        document.getElementById("title").innerText = "🚗 Car Transfer System Pro";
    }
}

</script>

</body>
</html>
