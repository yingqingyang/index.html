# index.html
新版网格计算器
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>合约网格计算器</title>
<style>
body{
font-family:Arial;
padding:20px;
background:#f5f5f5;
}
input{
width:100%;
padding:8px;
margin:5px 0;
}
button{
padding:10px;
width:100%;
background:#2c7be5;
color:white;
border:none;
font-size:16px;
}
.result{
margin-top:20px;
background:white;
padding:15px;
}
</style>
</head>

<body>

<h2>ETH合约做多网格计算器</h2>

当前价格
<input id="price">

网格下限
<input id="low">

网格上限
<input id="high">

网格数量
<input id="grid">

投入资金(U)
<input id="capital">

杠杆倍数
<input id="leverage">

资金费率(每8小时 %)
<input id="funding">

持仓天数
<input id="days">

<button onclick="calc()">计算</button>

<div class="result" id="result"></div>

<script>

function calc(){

let price=parseFloat(document.getElementById("price").value);
let low=parseFloat(document.getElementById("low").value);
let high=parseFloat(document.getElementById("high").value);
let grid=parseFloat(document.getElementById("grid").value);
let capital=parseFloat(document.getElementById("capital").value);
let leverage=parseFloat(document.getElementById("leverage").value);
let funding=parseFloat(document.getElementById("funding").value);
let days=parseFloat(document.getElementById("days").value);

let position=capital*leverage;

let gridGap=(high-low)/grid;

let singleProfit=(gridGap/price)*(position/grid);

let liq=price*(1-1/leverage);

let fundingCost=position*(funding/100)*3*days;

let safe=((price-liq)/price)*100;

document.getElementById("result").innerHTML=

"仓位规模: "+position.toFixed(2)+" U<br>"+
"每格价格差: "+gridGap.toFixed(2)+"<br>"+
"单格收益: "+singleProfit.toFixed(2)+" U<br>"+
"预估强平价: "+liq.toFixed(2)+"<br>"+
"强平安全距离: "+safe.toFixed(2)+" %<br>"+
"资金费成本: "+fundingCost.toFixed(2)+" U";

}

</script>

</body>
</html>
