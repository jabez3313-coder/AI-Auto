<!DOCTYPE html>
<html lang="ko">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>eBook Viewer</title>

<style>

body{
font-family: "Noto Serif KR", serif;
background:#f5f3ef;
margin:0;
padding:0;
display:flex;
justify-content:center;
}

.container{
max-width:700px;
background:white;
min-height:100vh;
padding:30px 20px;
box-shadow:0 0 20px rgba(0,0,0,0.05);
}

.title{
text-align:center;
font-size:26px;
margin-bottom:20px;
font-weight:600;
}

.image{
width:100%;
border-radius:8px;
margin-bottom:25px;
}

.text{
font-size:18px;
line-height:1.8;
text-align:left;
white-space:pre-line;
margin-bottom:30px;
color:#333;
}

.navigation{
display:flex;
justify-content:space-between;
margin-top:20px;
}

button{
padding:12px 20px;
border:none;
background:#8c7a5b;
color:white;
border-radius:6px;
cursor:pointer;
font-size:16px;
}

button:hover{
background:#6f5f46;
}

.page{
text-align:center;
margin-top:15px;
color:#999;
}

</style>

</head>

<body>

<div class="container">

<div class="title" id="title"></div>

<img id="image" class="image"/>

<div id="text" class="text"></div>

<div class="navigation">
<button onclick="prev()">← 이전</button>
<button onclick="next()">다음 →</button>
</div>

<div id="page" class="page"></div>

</div>

<script>

let page = 0
let data

const params = new URLSearchParams(location.search)
const book = params.get("book") || "story-01"

fetch(`../data/stories/${book}.json`)
.then(res => res.json())
.then(json=>{
data=json
document.getElementById("title").innerText=data.title
show()
})

function show(){

let p=data.pages[page]

document.getElementById("text").innerText=p.text || ""

if(p.image){
document.getElementById("image").src=`../public${p.image}`
document.getElementById("image").style.display="block"
}else{
document.getElementById("image").style.display="none"
}

document.getElementById("page").innerText =
(page+1) + " / " + data.pages.length

}

function next(){
if(page < data.pages.length-1){
page++
show()
}
}

function prev(){
if(page > 0){
page--
show()
}
}

</script>

</body>

</html>
