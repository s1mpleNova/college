# Web Application Development — Step-by-Step Practical Guide
**Subject Code: BE05000281 | 14 Practicals | HTML/CSS → JavaScript → Node.js/Express → React.js**

**Tools needed:** Visual Studio Code (or any text editor), a modern web browser, Node.js runtime, and Postman (for API testing).

---

## Practical 1: Static HTML Page

**Objective:** Build a static page using headings, paragraphs, lists, and links.

1. Create a project folder, e.g. `practical1`, and open it in VS Code.
2. Create a file named `index.html`.
3. Add the basic HTML5 boilerplate:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>My First Page</title>
   </head>
   <body>
   </body>
   </html>
   ```
4. Inside `<body>`, add a main heading `<h1>`, a subheading `<h2>`, and 2–3 paragraphs `<p>` about a topic of your choice.
5. Add an unordered list `<ul>` with 3–4 `<li>` items, and an ordered list `<ol>` with steps for something.
6. Add a hyperlink using `<a href="https://example.com">Visit Example</a>`.
7. Save the file, right-click it in VS Code → **Open with Live Server** (or just double-click to open in browser).
8. Verify all elements render correctly.

---

## Practical 2: HTML Tables, Forms, and Media Elements

**Objective:** Build a page combining tables, a form, and media.

1. In the same or a new folder, create `index.html`.
2. Add a `<table>` with a `<thead>` (header row) and `<tbody>` (2–3 data rows), including `<th>` and `<td>` tags.
3. Below it, add a `<form>` with:
   - A text input: `<input type="text" name="name" placeholder="Your Name">`
   - An email input: `<input type="email" name="email">`
   - A radio button group: `<input type="radio" name="gender" value="male">`
   - A checkbox: `<input type="checkbox" name="subscribe">`
   - A submit button: `<button type="submit">Submit</button>`
4. Add an `<img>` tag pointing to any local or online image, with an `alt` attribute.
5. Add a `<video>` tag with `controls` attribute pointing to a sample video file (or embed a YouTube iframe).
6. Open in browser and test filling the form and submitting (it will reload the page by default — that's expected at this stage).

---

## Practical 3: CSS Styling

**Objective:** Style a webpage using selectors, colors, fonts, and box model properties.

1. Reuse the HTML from Practical 1 or create a new `index.html`.
2. Create a `style.css` file in the same folder.
3. Link it in the `<head>`:
   ```html
   <link rel="stylesheet" href="style.css">
   ```
4. In `style.css`, practice different selectors:
   ```css
   body { font-family: Arial, sans-serif; background-color: #f4f4f4; }
   h1 { color: #2c3e50; text-align: center; }
   p { color: #333; line-height: 1.6; }
   .highlight { background-color: yellow; }
   #main-title { font-size: 2rem; }
   ```
5. Add a `class="highlight"` to one paragraph and an `id="main-title"` to your `<h1>` to see class/ID selectors work.
6. Experiment with `margin`, `padding`, and `border` on a `<div>` wrapping some content.
7. Refresh the browser and observe the styling changes.

---

## Practical 4: Responsive Layout with Flexbox

**Objective:** Build a layout using Flexbox and positioning.

1. Create `index.html` with a `<div class="container">` containing 3 `<div class="box">` child elements (each with some text).
2. In `style.css`:
   ```css
   .container {
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     align-items: center;
     gap: 10px;
   }
   .box {
     background-color: #3498db;
     color: white;
     padding: 20px;
     flex: 1;
   }
   ```
3. Change `flex-direction` to `column` and observe the layout change.
4. Experiment with `justify-content` values: `center`, `space-around`, `flex-end`.
5. Add a `position: relative` container with one `position: absolute` child to see absolute positioning in action.
6. Resize the browser window to see how Flexbox items adjust.

---

## Practical 5: Responsive Personal Portfolio Webpage (Mini-Project)

**Objective:** Build a complete, responsive personal portfolio page.

1. Create a new folder `portfolio` with `index.html` and `style.css`.
2. Structure the page with semantic sections: `<header>` (name + nav), `<section id="about">`, `<section id="skills">`, `<section id="projects">`, `<footer>`.
3. In the header, add your name and a simple nav bar linking to each section (`<a href="#about">About</a>` etc.).
4. In "About," add a short bio paragraph and a photo (`<img>`).
5. In "Skills," list your skills using a `<ul>` or a Flexbox row of skill "cards."
6. In "Projects," add 2–3 project cards, each with a title, short description, and a link.
7. Style everything using CSS Flexbox for layout.
8. Add a **media query** at the bottom of `style.css` for responsiveness:
   ```css
   @media (max-width: 600px) {
     .container { flex-direction: column; }
     nav a { display: block; margin: 5px 0; }
   }
   ```
9. Resize your browser (or use DevTools' device toolbar) to confirm the layout adapts on smaller screens.

---

## Practical 6: Landing Page with Bootstrap

**Objective:** Build a landing page using the Bootstrap framework.

1. Create a new `index.html` and include Bootstrap via CDN in the `<head>`:
   ```html
   <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
   ```
   and before `</body>`:
   ```html
   <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
   ```
2. Add a Bootstrap **navbar** (copy the "Navbar" example from Bootstrap's documentation) with your site name and 2–3 links.
3. Add a Bootstrap **jumbotron/hero section** with a heading, a short paragraph, and a call-to-action button (`class="btn btn-primary"`).
4. Add a **grid row of cards** (`class="row"` with 3 `class="col-md-4"` columns, each containing a `class="card"`) to showcase features or products.
5. Preview in the browser and check that the navbar and grid respond correctly when resizing the window.

---

## Practical 7: Basic JavaScript — Variables, Datatypes, Operators, Conditionals

**Objective:** Write foundational JavaScript programs.

1. Create `index.html` with a `<script src="script.js"></script>` before `</body>`.
2. Create `script.js` and declare variables of different types:
   ```javascript
   let name = "Alice";
   let age = 20;
   let isStudent = true;
   console.log(typeof name, typeof age, typeof isStudent);
   ```
3. Practice operators:
   ```javascript
   let a = 10, b = 3;
   console.log(a + b, a - b, a * b, a / b, a % b);
   console.log(a > b, a === 10, a !== b);
   ```
4. Write a simple grade-checker using if-else:
   ```javascript
   let marks = 78;
   if (marks >= 90) console.log("Grade A");
   else if (marks >= 75) console.log("Grade B");
   else if (marks >= 50) console.log("Grade C");
   else console.log("Fail");
   ```
5. Open the HTML file in browser, open DevTools (F12) → Console tab, and confirm the outputs appear.

---

## Practical 8: DOM Manipulation & Event Handling — To-Do List

**Objective:** Build a working to-do list using the DOM.

1. In `index.html`, add:
   ```html
   <input type="text" id="taskInput" placeholder="Enter a task">
   <button id="addBtn">Add</button>
   <ul id="taskList"></ul>
   ```
2. In `script.js`, select the elements:
   ```javascript
   const input = document.getElementById("taskInput");
   const btn = document.getElementById("addBtn");
   const list = document.getElementById("taskList");
   ```
3. Add a click event listener to create new list items:
   ```javascript
   btn.addEventListener("click", () => {
     if (input.value.trim() === "") return;
     const li = document.createElement("li");
     li.textContent = input.value;
     li.addEventListener("click", () => li.remove());
     list.appendChild(li);
     input.value = "";
   });
   ```
4. Open in browser, add a few tasks, and click on a task to remove it (demonstrates DOM creation, event handling, and removal).

---

## Practical 9: Browser Local Storage

**Objective:** Persist to-do list data across page refreshes.

1. Extend the to-do list from Practical 8.
2. After adding a task, save the full list to Local Storage:
   ```javascript
   function saveTasks() {
     const tasks = Array.from(list.children).map(li => li.textContent);
     localStorage.setItem("tasks", JSON.stringify(tasks));
   }
   ```
3. Call `saveTasks()` inside both the "add" and "remove" event handlers.
4. On page load, restore saved tasks:
   ```javascript
   window.addEventListener("DOMContentLoaded", () => {
     const saved = JSON.parse(localStorage.getItem("tasks")) || [];
     saved.forEach(task => {
       const li = document.createElement("li");
       li.textContent = task;
       li.addEventListener("click", () => { li.remove(); saveTasks(); });
       list.appendChild(li);
     });
   });
   ```
5. Add some tasks, refresh the page, and confirm they persist.
6. Open DevTools → Application tab → Local Storage to inspect the stored data directly.

---

## Practical 10: Fetch API — Consuming a Public API

**Objective:** Fetch and display data from a public API.

1. Create `index.html` with a `<div id="result"></div>`.
2. In `script.js`, use the Fetch API to call a free public API (e.g. a joke API):
   ```javascript
   fetch("https://official-joke-api.appspot.com/random_joke")
     .then(response => response.json())
     .then(data => {
       document.getElementById("result").innerHTML =
         `<p>${data.setup}</p><p><strong>${data.punchline}</strong></p>`;
     })
     .catch(error => console.error("Error fetching data:", error));
   ```
3. Open in browser and confirm the joke loads and displays.
4. Add a "New Joke" button that re-runs the fetch call on click.
5. Try the `async/await` syntax as an alternative:
   ```javascript
   async function getJoke() {
     const response = await fetch("https://official-joke-api.appspot.com/random_joke");
     const data = await response.json();
     console.log(data);
   }
   ```

---

## Practical 11: Simple REST API with Node.js & Express.js

**Objective:** Build a basic backend API with GET/POST routes.

1. Create a new folder `practical11-api`, open a terminal in it.
2. Initialize the project:
   ```
   npm init -y
   npm install express
   ```
3. Create `server.js`:
   ```javascript
   const express = require("express");
   const app = express();
   app.use(express.json());

   let items = [{ id: 1, name: "Sample Item" }];

   app.get("/items", (req, res) => {
     res.json(items);
   });

   app.post("/items", (req, res) => {
     const newItem = { id: items.length + 1, name: req.body.name };
     items.push(newItem);
     res.status(201).json(newItem);
   });

   app.listen(3000, () => console.log("Server running on http://localhost:3000"));
   ```
4. Run the server:
   ```
   node server.js
   ```
5. Open a browser to `http://localhost:3000/items` to see the GET response.
6. Use Postman (or `curl`) to send a POST request to `http://localhost:3000/items` with a JSON body `{ "name": "New Item" }`, then GET again to confirm it was added.

---

## Practical 12: Connect Express to a Database (CRUD with Postman)

**Objective:** Perform full CRUD operations against a database.

1. Ensure MongoDB (or MySQL) is running locally, or use a free MongoDB Atlas cloud cluster.
2. In your project from Practical 11, install the driver:
   ```
   npm install mongoose
   ```
3. In `server.js`, connect to MongoDB and define a schema:
   ```javascript
   const mongoose = require("mongoose");
   mongoose.connect("mongodb://localhost:27017/practicalDB");

   const Item = mongoose.model("Item", { name: String });
   ```
4. Replace the in-memory routes with database-backed ones:
   ```javascript
   app.get("/items", async (req, res) => res.json(await Item.find()));
   app.post("/items", async (req, res) => res.status(201).json(await Item.create(req.body)));
   app.put("/items/:id", async (req, res) => res.json(await Item.findByIdAndUpdate(req.params.id, req.body, { new: true })));
   app.delete("/items/:id", async (req, res) => { await Item.findByIdAndDelete(req.params.id); res.status(204).end(); });
   ```
5. Restart the server (`node server.js`).
6. In Postman, test all 4 operations in order: **POST** (create), **GET** (read all), **PUT** (update by ID), **DELETE** (remove by ID).
7. Confirm each operation reflects correctly in the database (use `GET` after each step to verify).

---

## Practical 13: Basic React.js App with Components, Props, and useState

**Objective:** Build a small interactive React app.

1. Create a new React app:
   ```
   npx create-react-app practical13
   cd practical13
   npm start
   ```
2. In `src/App.js`, create a `Counter` component:
   ```jsx
   import { useState } from "react";

   function Counter({ label }) {
     const [count, setCount] = useState(0);
     return (
       <div>
         <h3>{label}: {count}</h3>
         <button onClick={() => setCount(count + 1)}>Increment</button>
         <button onClick={() => setCount(count - 1)}>Decrement</button>
       </div>
     );
   }

   function App() {
     return (
       <div>
         <Counter label="Counter A" />
         <Counter label="Counter B" />
       </div>
     );
   }

   export default App;
   ```
3. Save and check the browser (auto-reloads at `http://localhost:3000`).
4. Click Increment/Decrement on both counters and confirm they update **independently** (demonstrating component state + props).

---

## Practical 14: Full-Stack Integration — React Frontend + Node/Express Backend

**Objective:** Connect a React frontend to the backend API built in Practicals 11–12.

1. Ensure your Express API from Practical 12 is running on `http://localhost:3000`.
2. Create a new React app for the frontend (run it on a different port, e.g. 3001, since 3000 is taken by the API — Create React App will prompt to use another port automatically):
   ```
   npx create-react-app practical14-frontend
   cd practical14-frontend
   npm install axios
   npm start
   ```
3. In `src/App.js`, fetch and display items from the API, and add a form to create new ones:
   ```jsx
   import { useState, useEffect } from "react";
   import axios from "axios";

   function App() {
     const [items, setItems] = useState([]);
     const [name, setName] = useState("");

     useEffect(() => {
       axios.get("http://localhost:3000/items").then(res => setItems(res.data));
     }, []);

     const addItem = async () => {
       const res = await axios.post("http://localhost:3000/items", { name });
       setItems([...items, res.data]);
       setName("");
     };

     return (
       <div>
         <h2>Items</h2>
         <ul>{items.map(item => <li key={item._id || item.id}>{item.name}</li>)}</ul>
         <input value={name} onChange={e => setName(e.target.value)} placeholder="New item" />
         <button onClick={addItem}>Add</button>
       </div>
     );
   }

   export default App;
   ```
4. If you get a **CORS error** in the browser console, install and enable CORS on the Express server:
   ```
   npm install cors
   ```
   and in `server.js`:
   ```javascript
   const cors = require("cors");
   app.use(cors());
   ```
5. Restart the Express server, refresh the React app, and confirm items load from the database and new items can be added through the form — completing the full-stack loop (React ↔ Express ↔ Database).

---

### General Notes
- Practicals 1–10 only need a browser and a text editor — no installation required.
- Practicals 11–14 need Node.js installed (`node -v` to check) and, for 12 & 14, a running MongoDB instance.
- Use Postman to test API endpoints independently before connecting them to the frontend — it isolates backend bugs from frontend bugs.
