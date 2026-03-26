<!DOCTYPE html>
<html>

<head>
<title>eBook Viewer</title>

<style>
body{
font-family: sans-serif;
text-align:center;
padding:20px;
}

img{
max-width:90%;
}

button{
padding:10px;
margin:10px;
}
</style>

</head>

<body>

<h2 id="title"></h2>

<img id="image">

<p id="text"></p>

<button onclick="prev()">이전</button>
<button onclick="next()">다음</button>

<script>

let page=0
let data

fetch("../data/stories/peter-01.json")
.then(res=>res.json())
.then(json=>{
data=json
document.getElementById("title").innerText=data.title
show()
})

function show(){

let p=data.pages[page]

document.getElementById("text").innerText=p.text || ""

if(p.image){
document.getElementById("image").src="../public"+p.image
}else{
document.getElementById("image").style.display="none"
}

}

function next(){
if(page < data.pages.length-1){
page++
show()
}
}

function prev(){
if(page>0){
page--
show()
}
}

</script>

</body>

</html>
