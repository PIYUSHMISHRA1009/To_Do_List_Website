<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <link rel="stylesheet" href="style.css">

  <title>To do List</title>
</head>
<body>
  <div class = "container">
    <div class="todo-app">
      <h2>To-Do List <img src="images/icon.png"></h2>
      <div class="row">
        <input type="text" id="input-box" placeholder="List your Tasks here:">
        <button onclick="addTask()">Add</button>
      </div>
      <ul id="list-container">
        <!---<li class="checked">Task 1</li>
        <li>Task 2</li>
        <li>Task 3</li>---->
      </ul>
    </div>
  </div>
<script src="script.js">

</script>
</body>
</html>


/* Base Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  width: 100%;
  min-height: 100vh;
  background: linear-gradient(135deg, #153677, #4e085f);
  padding: 10px;
}

.todo-app {
  width: 100%;
  max-width: 540px;
  background: #fff;
  margin: 100px auto 20px;
  padding: 40px 30px 70px;
  border-radius: 10px;
}

.todo-app h2 {
  color: #002765;
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.todo-app h2 img {
  width: 30px;
  margin-left: 10px;
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #edeef0;
  border-radius: 30px;
  padding-left: 20px;
  margin-bottom: 25px;
}

input {
  flex: 1;
  border: none;
  outline: none;
  background: transparent;
  padding: 10px;
  font-size: 14px;
}

button {
  border: none;
  outline: none;
  padding: 16px 50px;
  background: #ff5945;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  border-radius: 40px;
}

ul li {
  list-style: none;
  font-size: 17px;
  padding: 12px 8px 12px 50px;
  user-select: none;
  cursor: pointer;
  position: relative;
}

ul li::before {
  content: '';
  position: absolute;
  height: 28px;
  width: 28px;
  border-radius: 50%;
  background-image: url(images/unchecked.png);
  background-size: cover;
  background-position: center;
  top: 12px;
  left: 8px;
}

ul li.checked {
  color: #555;
  text-decoration: line-through;
}

ul li.checked::before {
  background-image: url(images/checked.png);
}

ul li span {
  position: absolute;
  right: 0;
  top: 5px;
  width: 40px;
  height: 40px;
  font-size: 22px;
  color: #555;
  line-height: 40px;
  text-align: center;
  border-radius: 50%;
}

ul li span:hover {
  background: #edeef0;
}

/* Media Queries for Responsiveness */
@media (max-width: 768px) {
  .todo-app {
    padding: 30px 20px 60px;
    margin: 80px auto 20px;
  }

  .todo-app h2 {
    font-size: 20px;
    margin-bottom: 15px;
  }

  .todo-app h2 img {
    width: 25px;
  }

  .row {
    flex-direction: column;
    align-items: stretch;
    padding: 10px;
  }

  input {
    padding: 8px;
    font-size: 14px;
  }

  button {
    padding: 12px 30px;
    font-size: 14px;
    border-radius: 30px;
    margin-top: 10px;
  }

  ul li {
    font-size: 16px;
    padding: 10px 8px 10px 40px;
  }

  ul li::before {
    height: 24px;
    width: 24px;
    top: 8px;
    left: 4px;
  }

  ul li span {
    width: 30px;
    height: 30px;
    font-size: 18px;
    line-height: 30px;
  }
}

@media (max-width: 480px) {
  .todo-app {
    padding: 20px 15px 50px;
    margin: 60px auto 10px;
  }

  .todo-app h2 {
    font-size: 18px;
    margin-bottom: 10px;
  }

  .todo-app h2 img {
    width: 20px;
  }

  .row {
    padding: 8px;
  }

  input {
    padding: 6px;
    font-size: 13px;
  }

  button {
    padding: 10px 20px;
    font-size: 13px;
    border-radius: 20px;
    margin-top: 8px;
  }

  ul li {
    font-size: 15px;
    padding: 8px 6px 8px 30px;
  }

  ul li::before {
    height: 20px;
    width: 20px;
    top: 6px;
    left: 2px;
  }

  ul li span {
    width: 25px;
    height: 25px;
    font-size: 16px;
    line-height: 25px;
  }
}

const inputBox = document.getElementById("input-box");
const listContainer = document.getElementById("list-container");
function addTask(){
  if(inputBox.value === ''){
    alert("You must write something!");

  }
  else{
    let li = document.createElement("li");
    li.innerHTML = inputBox.value;
    listContainer.appendChild(li);
    let span = document.createElement("span");
    span.innerHTML = "\u00d7";
    li.appendChild(span);
  }
  inputBox.value="";
  saveData();

}

listContainer.addEventListener("click" , function(e){
  if(e.target.tagName === "LI"){
    e.target.classList.toggle("checked");
    saveData();
  }
  else if(e.target.tagName === "SPAN"){
    e.target.parentElement.remove();
    saveData();
  }
} ,false);

function saveData(){
  localStorage.setItem("data",listContainer.innerHTML);
}
function showTask(){
  listContainer.innerHTML = localStorage.getItem("data");
}
showTask();

