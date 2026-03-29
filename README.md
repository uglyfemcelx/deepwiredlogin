<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>deep_wired_access</title>

<style>

body{
    background:black;
    color:#00ff88;
    font-family:"Courier New", monospace;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
    flex-direction:column;
    overflow:hidden;
    position:relative;
}
input{
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:10px;
    margin:5px;
    font-family:inherit;
    width:200px;
}
button{
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:10px;
    cursor:pointer;
}
#error{
    color:red;
    margin-top:10px;
    min-height:20px;
}
#title{
    margin-bottom:10px;
}
#bgText{
    position:absolute;
    color:#003322;
    font-size:12px;
    white-space:pre;
    opacity:0.2;
    pointer-events:none;
    animation:scroll 20s linear infinite;
}
@keyframes scroll{
    from{transform:translateY(100%);}
    to{transform:translateY(-100%);}
}
.glitch{
    animation:glitch 0.2s infinite;
    color:red;
}
@keyframes glitch{
    0%{transform:translate(0);}
    25%{transform:translate(2px,-2px);}
    50%{transform:translate(-2px,2px);}
    75%{transform:translate(2px,2px);}
    100%{transform:translate(0);}
}
</style>

</head>

<body>

<div id="bgText">
010101010101010101010101010101010101
i see you
you shouldn't be here
who gave you access
lain lain lain
remember me remember me

</div>

<div id="title">> deep_wired authentication required</div><input id="user" placeholder="username">
<input id="pass" type="password" placeholder="password">
<button onclick="login()">enter</button><div id="error">

</div>

<script>
let attempts = 0;

function login(){
    const u = document.getElementById("user").value.toLowerCase();
    const p = document.getElementById("pass").value.toLowerCase();

    attempts++; 

    const correct =
        (u === "lain" && p === "alice") ||
        (u === "i exist" && p === "only in the wired") ||
        (u === "who am i" && p === "unknown");

    if(correct){ 
        document.body.innerHTML = "> verifying identity...\n> syncing memory...\n> do you remember?\n\n> access granted.";

        setTimeout(()=>{
            window.location.href = "deep_wired_node.html";
        }, 3000);

    } else {

        const error = document.getElementById("error");

        if(attempts === 1){
            error.textContent = "> access denied.";
        }
        else if(attempts === 2){
            error.textContent = "> incorrect... dont try again.";
        }
        else if(attempts === 3){
            error.textContent = "> stop guessing.";
            document.getElementById("title").classList.add("glitch")
        }
        else if(attempts === 4){
            document.body.innerHTML = "> too many attempts. \n> someone is watching you"
            
        }
        else if(attempts >= 5){
            document.body.innerHTML = "> connection terminated.\n> do not come back";
        }
    }
}

// random glitch text
setInterval(()=>{
    if(Math.random() < 0.2){
        const glitch = document.createElement("div");
        glitch.classList.add("glitch");
        glitch.textContent = "> ...who are you?";
        glitch.style.position = "absolute";
        glitch.style.top = Math.random()*100 + "%";
        glitch.style.left = Math.random()*100 + "%";

        document.body.appendChild(glitch);

        setTimeout(()=>{
            glitch.remove();
        }, 1000);
    }
}, 2000);
</script>

</body>
</html>
