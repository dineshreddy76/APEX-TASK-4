<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Full Project</title>
  <link rel="stylesheet" href="style.css" />
 <style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, sans-serif;
  background-color:gray;
  line-height: 1.6;
  padding-bottom: 4rem;
}
header {
  background: skyblue;
  color: #fff;
  padding: 1rem;
  text-align: center;
}
nav a {
  color:#fff;
  margin: 0 10px;
  text-decoration: none;
}
section {
  padding: 2rem;
}
.project-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
.project-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  flex: 1 1 45%;
  box-shadow: 0 0 5px rgba(0,0,0,0.1);
}
input, textarea, select {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
}
button {
  padding: 10px;
  background: #333;
  color: white;
  border: none;
  cursor: pointer;
  margin-top: 10px;
}
ul {
  list-style: none;
  margin-top: 1rem;
}
li {
  background: #fff;
  margin-bottom: 10px;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}
.controls {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 1rem;
}
.product {
  background: white;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}
.product img {
  width: 100%;
  height: 120px;
  object-fit: cover;
  border-radius: 5px;
  margin-bottom: 8px;
}
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background: #222;
  color: #fff;
  text-align: center;
  padding: 1rem;
}
</style>
</head>
<body>

  <header>
    <h1>My Portfolio</h1>
    <nav>
      <a href="#about">About</a>
      <a href="#projects">Projects</a>
      <a href="#todo">To-Do</a>
      <a href="#products">Products</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <section id="about">
    <h2>About Me</h2>
    <p>I'm a web developer skilled in HTML, CSS, JavaScript, and building interactive applications.</p>
  </section>

  <section id="projects">
    <h2>Projects</h2>
    <div class="project-list">
      <div class="project-card">
        <h3>To-Do App</h3>
        <p>Organize your daily tasks with persistence using local storage.</p>
      </div>
      <div class="project-card">
        <h3>Product Page</h3>
        <p>Dynamic product listing with filtering and sorting.</p>
      </div>
    </div>
  </section>

  <section id="todo">
    <h2>To-Do List</h2>
    <input type="text" id="taskInput" placeholder="Add a new task" />
    <button onclick="addTask()">Add Task</button>
    <ul id="taskList"></ul>
  </section>

  <section id="products">
    <h2>Product Listing</h2>
    <div class="controls">
      <select id="categoryFilter">
        <option value="all">All Categories</option>
        <option value="electronics">Electronics</option>
        <option value="clothing">Clothing</option>
      </select>

      <select id="sortPrice">
        <option value="low">Price: Low to High</option>
        <option value="high">Price: High to Low</option>
      </select>
    </div>
    <div id="productList" class="product-grid"></div>
  </section>

  <section id="contact">
    <h2>Contact Me</h2>
    <form id="contactForm">
      <input type="text" placeholder="Your Name" required />
      <input type="email" placeholder="Your Email" required />
      <textarea placeholder="Your Message" required></textarea>
      <button type="submit">Send</button>
    </form>
  </section>

  <footer>
    <p>&copy; 2025 Your Name</p>
  </footer>

  <script>
// Contact Form
document.getElementById("contactForm").addEventListener("submit", function(e) {
  e.preventDefault();
  alert("Thank you for contacting me!");
});

// To-Do List
const taskInput = document.getElementById('taskInput');
const taskList = document.getElementById('taskList');

function addTask() {
  const task = taskInput.value.trim();
  if (task === "") return;

  const li = document.createElement("li");
  li.textContent = task;

  const delBtn = document.createElement("button");
  delBtn.textContent = "X";
  delBtn.onclick = () => {
    li.remove();
    saveTasks();
  };

  li.appendChild(delBtn);
  taskList.appendChild(li);
  taskInput.value = "";
  saveTasks();
}

function saveTasks() {
  const tasks = [];
  taskList.querySelectorAll("li").forEach(li => {
    tasks.push(li.childNodes[0].textContent);
  });
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function loadTasks() {
  const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  tasks.forEach(task => {
    taskInput.value = task;
    addTask();
  });
}
window.onload = () => {
  loadTasks();
  displayProducts(products);
};

// Product List with Images
const products = [
  {
    name: "Laptop",
    price: 100000,
    category: "electronics",
    image: "https://th.bing.com/th/id/OIP.jtS23CrdNk0SdkIahKlOqwHaEo?w=316&h=197&c=8&rs=1&qlt=90&o=6&dpr=1.3&pid=3.1&rm=2"
  },
  {
    name: "Smartphone",
    price: 2000,
    category: "electronics",
    image: "https://th.bing.com/th/id/OIP.-Tps1udTX4qMwmPKsajJowHaHa?r=0&pid=ImgDet&w=185&h=185&c=7&dpr=1.3"
  },
  {
    name: "Headphones",
    price: 2500,
    category: "electronics",
    image: " https://th.bing.com/th/id/OIP.4rMdbVaV1IPcRgaVkixHigHaF7?w=279&h=223&c=8&rs=1&qlt=90&o=6&dpr=1.3&pid=3.1&rm=2"
  },
  {
    name: "Smartwatch",
    price: 3000,
    category: "electronics",
    image: "https://m.media-amazon.com/images/I/613qFCwaEnL.SL1500.jpg"
  },
  {
    name: "Shirt",
    price: 1000,
    category: "clothing",
    image: "https://th.bing.com/th/id/OPAC.o9wIAWeKXyPxDg474C474?o=5&pid=21.1&w=185&h=277&c=7&dpr=1.3"
  },
  {
    name: "Jeans",
    price: 1500,
    category: "clothing",
    image: "https://plus.unsplash.com/premium_photo-1674828601362-afb73c907ebe?q=80&w=1953&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
  },
  {
    name: "Jacket",
    price: 2000,
    category: "clothing",
    image: "https://th.bing.com/th/id/OIP.z4VY-LkxBTLagzSWQ4VFswHaIy?r=0&pid=ImgDet&w=185&h=219&c=7&dpr=1.3"
  },
  {
    name: "Shoes",
    price: 2500,
    category: "clothing",
    image: "https://th.bing.com/th/id/OIP.poQli54lcHQLwHHMcwgTWwHaNL?r=0&pid=ImgDet&w=185&h=329&c=7&dpr=1.3"
  },
  {
    name: "Lehanga",
    price: 4000,
    category: "clothing",
    image: "https://th.bing.com/th/id/OIP.RtljN456xZC6jodiLU-YoQHaMV?w=182&h=304&c=7&r=0&o=5&dpr=1.3&pid=1.7"
  },
  {
    name: "College Bags",
    price: 4000,
    category: "clothing",
    image: "https://th.bing.com/th/id/OIP.ATwgZEmNIGf7x0uzBzW7EgHaIX?r=0&pid=ImgDet&w=185&h=209&c=7&dpr=1.3"
  },
  {
    name: "saree",
    price: 2000,
    category: "clothing",
    image: "https://th.bing.com/th/id/OIP.IfCusDhNjIMjolf2-yzD8AHaJ4?r=0&pid=ImgDet&w=185&h=246&c=7&dpr=1.3"
  },
  {
    name: "Juice jar mixture",
    price: 500,
    category: "electronics",
    category: "",
    image: "https://i5.walmartimages.com/seo/Cotsoco-400ml-Portable-Blender-USB-Rechargeable-Smoothie-Blender-Personal-Juicer-Cup-Fruit-Mixer-High-Borosilicate-Glass-Cup-Pink_824b09de-b774-458f-b3e2-29aa5d1e0c02.efc3d3f49cdd1ee658731619586fa15c.jpeg?odnHeight=580&odnWidth=580&odnBg=FFFFFF"
  },
  {
    name: "Multipurpose cooker",
    price: 3000,
    category: "electronics",
    image: " https://th.bing.com/th/id/OIP.Pbhp3Tv1XCFq0Y99YHfdKwHaHb?w=206&h=207&c=7&r=0&o=5&dpr=1.3&pid=1.7"
  },
{
    name: "shervani",
    price: 5000,
    category: "clothing",
    image: "https://th.bing.com/th/id/OIP.AcnKOjj9zAslvcko1EVJcQHaJQ?r=0&pid=ImgDet&w=185&h=231&c=7&dpr=1.3"
  },
  
];

const productList = document.getElementById('productList');
const categoryFilter = document.getElementById('categoryFilter');
const sortPrice = document.getElementById('sortPrice');

function displayProducts(list) {
  productList.innerHTML = '';
  list.forEach(p => {
    const div = document.createElement('div');
    div.className = 'product';
    div.innerHTML = `
      <img src="${p.image}" alt="${p.name}">
      <h3>${p.name}</h3>
      <p>$${p.price}</p>
    `;
    productList.appendChild(div);
  });
}

function filterAndSort() {
  let filtered = [...products];
  const cat = categoryFilter.value;
  const sort = sortPrice.value;

  if (cat !== 'all') filtered = filtered.filter(p => p.category === cat);
  if (sort === 'low') filtered.sort((a, b) => a.price - b.price);
  else filtered.sort((a, b) => b.price - a.price);

  displayProducts(filtered);
}

categoryFilter.addEventListener('change', filterAndSort);
sortPrice.addEventListener('change', filterAndSort);
</script>
</body>
</html>
