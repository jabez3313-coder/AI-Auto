<!DOCTYPE html>
<html lang="ko">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>eBook Library</title>

<style>

body{
font-family:"Noto Serif KR", serif;
background:#f5f3ef;
margin:0;
padding:20px;
}

.title{
text-align:center;
font-size:28px;
margin-bottom:30px;
font-weight:600;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
gap:20px;
max-width:1000px;
margin:auto;
}

.book{
background:white;
border-radius:10px;
overflow:hidden;
cursor:pointer;
box-shadow:0 5px 15px rgba(0,0,0,0.05);
transition:0.3s;
}

.book:hover{
transform:translateY(-5px);
box-shadow:0 10px 20px rgba(0,0,0,0.1);
}

.book img{
width:100%;
height:240px;
object-fit:cover;
}

.book-title{
padding:12px;
font-size:16px;
text-align:center;
line-height:1.4;
}

</style>

</head>

<body>

<div class="title">
📚 스토리북 라이브러리
</div>

<div id="books" class="grid"></div>

<script>

fetch("../data/stories/stories.json")
.then(res=>res.json())
.then(data=>{

let html=""

data.forEach(book=>{

html+=`
<div class="book" onclick="openBook('${book.id}')">
<img src="../public${book.coverImage}">
<div class="book-title">
${book.title}
</div>
</div>
`

})

document.getElementById("books").innerHTML=html

})

function openBook(id){
window.location.href=`viewer.html?book=${id}`
}

</script>

</body>

</html>
