# test-5
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Browser IDE</title>

<style>
body{
    font-family:Arial,sans-serif;
    background:#f4f4f4;
    margin:20px;
}
.container{
    max-width:900px;
    margin:auto;
}
select,button{
    padding:10px;
    margin:10px 0;
}
textarea{
    width:100%;
    border:1px solid #ccc;
    border-radius:5px;
    padding:10px;
    font-family:monospace;
}
#code{
    height:300px;
}
#input{
    height:80px;
}
#output{
    background:#222;
    color:#0f0;
    height:150px;
}
</style>

</head>
<body>

<div class="container">

<h2>Browser IDE</h2>

<select id="language">
<option value="c">C</option>
<option value="cpp">C++</option>
<option value="java">Java</option>
<option value="python">Python</option>
<option value="javascript">JavaScript</option>
</select>

<h3>Code</h3>
<textarea id="code">// Write your code here</textarea>

<h3>Input</h3>
<textarea id="input"></textarea>

<br>
<button onclick="runCode()">Run Code</button>

<h3>Output</h3>
<textarea id="output" readonly></textarea>

</div>

<script>
async function runCode(){

const language=document.getElementById("language").value;
const code=document.getElementById("code").value;
const input=document.getElementById("input").value;

try{

const response=await fetch("http://localhost:3000/run",{
method:"POST",
headers:{
"Content-Type":"application/json"
},
body:JSON.stringify({
language,
code,
input
})
});

const data=await response.json();

document.getElementById("output").value=data.output;

}catch(e){
document.getElementById("output").value=
"Backend server not running.";
}

}
</script>

</body>
</html>
