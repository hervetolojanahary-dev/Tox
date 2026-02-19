<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Pr��diction Heure</title>

<style>
body{
font-family: Arial;
background:#0f172a;
color:white;
text-align:center;
padding:20px;
}

input{
padding:10px;
width:80%;
margin:10px;
border-radius:8px;
border:none;
}

button{
padding:12px 20px;
background:#22c55e;
color:white;
border:none;
border-radius:10px;
font-size:18px;
}

.result{
margin-top:20px;
font-size:24px;
color:#facc15;
}
</style>
</head>

<body>

<h2>Radar Heure Pr��dictive</h2>

<input type="time" id="heure" step="1"><br>
<input type="text" id="hex" placeholder="Entrer Hex"><br>
<input type="text" id="dec" placeholder="Entrer Dec"><br>

<button onclick="calcul()">Calculer</button>

<div class="result" id="result"></div>

<script>
function sommeChiffres(text){
let chiffres = text.replace(/[^0-9]/g,'');
let somme = 0;
for(let i=0;i<chiffres.length;i++){
somme += parseInt(chiffres[i]);
}
return somme;
}

function racineUnique(n){
while(n > 9){
n = n.toString().split('').reduce((a,b)=>a+parseInt(b),0);
}
return n;
}

function calcul(){

let h = document.getElementById("heure").value;
let hex = document.getElementById("hex").value;
let dec = document.getElementById("dec").value;

if(!h){
alert("Entrer heure");
return;
}

let [HH,MM,SS] = h.split(':').map(Number);

/// HEX
let sommeHex = sommeChiffres(hex);
let minAdd = racineUnique(sommeHex);

MM += minAdd;

/// DEC
let sommeDec = sommeChiffres(dec);

let minDec = Math.floor(sommeDec / 60);
let secDec = sommeDec % 60;

MM += minDec;
SS += secDec;

/// correction temps
if(SS >= 60){
MM += Math.floor(SS/60);
SS = SS % 60;
}

if(MM >= 60){
HH += Math.floor(MM/60);
MM = MM % 60;
}

if(HH >= 24){
HH = HH % 24;
}

/// affichage
let res = 
String(HH).padStart(2,'0') + ":" +
String(MM).padStart(2,'0') + ":" +
String(SS).padStart(2,'0');

document.getElementById("result").innerHTML =
"Pr��diction finale : " + res;

}
</script>

</body>
</html>
# Tox
