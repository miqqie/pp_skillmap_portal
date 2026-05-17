# 🚀 The Comprehensive Beginner's Guide to JavaScript
### Deep-Dive: Learning Through the SkillMap Portal

---

JavaScript is the engine that makes web pages interactive. While HTML provides the **structure** and CSS provides the **style**, JavaScript provides the **behavior** — everything that happens when you click a button, filter a dropdown, or export a PDF.

In this guide, JavaScript is explained using a consistent mental model:

> **Data** = Items inside jars  
> **Variables** = Labels attached to jars  
> **Code** = Rules that move, modify, or read jars

Every example in this guide comes directly from `index.html` in the SkillMap Portal — so you can see real, working code alongside the explanation.

---

## 📋 Table of Contents

1. [The Building Blocks of JavaScript](#-the-building-blocks-of-javascript)
2. [The Naming Confusion: Java vs JavaScript](#-the-naming-confusion-java-vs-javascript)
3. [JavaScript vs Python: Syntax & Element Management](#-javascript-vs-python-syntax--element-management)
4. [Variables: Jars and Labels](#-variables-jars-and-labels)
5. [Functions: Reusable Rules](#-functions-reusable-rules)
6. [DOM Interaction: Reading and Updating the Page](#-dom-interaction-reading-and-updating-the-page)
7. [Arrays & Array Methods: Working with Lists](#-arrays--array-methods-working-with-lists)
8. [Objects: Named Jars with Multiple Compartments](#-objects-named-jars-with-multiple-compartments)
9. [Loops: Repeating Rules Across Jars](#-loops-repeating-rules-across-jars)
10. [Conditionals: Decision Making](#-conditionals-decision-making)
11. [Asynchronous JavaScript: Fetching & Loading Data](#-asynchronous-javascript-fetching--loading-data)
12. [Template Literals: Building HTML Strings](#-template-literals-building-html-strings)
13. [Events: Listening for User Actions](#-events-listening-for-user-actions)
14. [Data Transformation & Regular Expressions](#-data-transformation--regular-expressions)
15. [Quick Reference: Key Commands](#-quick-reference-key-commands)
16. [Extending the SkillMap Portal: Future Possibilities](#-extending-the-skillmap-portal-future-possibilities)

---

## 🧱 The Building Blocks of JavaScript

Before diving into any specific topic, it helps to understand what JavaScript is actually made of. Every JavaScript program — no matter how big or small — is built from just a handful of core ingredients. Once you recognise these, reading code starts to feel a lot less like a foreign language.

Think of it like cooking. You don't need to know every recipe in the world. You just need to understand what an ingredient *is* and what it *does* — then you can follow any recipe.

Here are the core building blocks:

---

### 📦 Values — The Raw Ingredients

A **value** is simply a piece of information. It could be a number, a word, a true/false switch, or nothing at all.

```javascript
42              // a number
"Hello"         // a piece of text (called a "string")
true            // a yes/no switch (called a "boolean")
null            // deliberately empty — "there is nothing here"
undefined       // hasn't been given a value yet
```

You'll see these everywhere. For example, when the portal checks whether a dropdown has been filled in:

```javascript
// If sVal is empty (""), null, or undefined — all of these are "falsy"
if (!sVal || !rVal) return;
```

Values are the foundation everything else is built on. Every variable holds a value, every array is a list of values, every function works with values.

---

### 🏷️ Variables — Labels on Jars

A **variable** is a named container that holds a value. You create one with `const` or `let`, give it a name, and assign a value to it. From then on, you can use that name anywhere instead of writing the raw value out every time.

```javascript
const roleName = "Software Engineer";   // a label stuck to a text value
let pageNumber = 1;                      // a label that will move as pages increase
```

Variables make your code readable and reusable. Instead of writing `"Software Engineer"` twenty times, you write `roleName` — and if it ever changes, you only update it in one place.

→ *Deep dive: [Variables: Jars and Labels](#-variables-jars-and-labels)*

---

### 📋 Data Structures — Jars That Hold Many Things

Sometimes one value isn't enough. JavaScript gives you two ways to group values together:

**Arrays** — an ordered list (like a numbered shelf of jars):
```javascript
const sectors = ["Healthcare", "Finance", "Technology"];
sectors[0]; // "Healthcare" — counting starts at zero
```

**Objects** — a collection of named values (like a jar with labelled compartments):
```javascript
const skill = {
    name: "Data Analysis",
    level: 3,
    required: true
};
skill.name; // "Data Analysis"
```

In the SkillMap Portal, the entire dataset is one giant object with arrays inside it — sectors, roles, skills, and work functions all stored as named lists.

→ *Deep dive: [Arrays & Array Methods](#-arrays--array-methods-working-with-lists) · [Objects](#-objects-named-jars-with-multiple-compartments)*

---

### ⚙️ Functions — Reusable Instructions

A **function** is a named set of steps that you can run whenever you need them. You write the instructions once, give them a name, and then call that name to run them.

```javascript
function showWelcome() {
    document.getElementById('welcome-msg').style.display = 'flex';
}

showWelcome(); // runs those steps right now
```

Functions are how JavaScript avoids repeating itself. The SkillMap Portal has functions for rendering the table, opening modals, toggling panels, exporting PDFs — each one is a self-contained set of instructions with a clear name.

→ *Deep dive: [Functions: Reusable Rules](#-functions-reusable-rules)*

---

### 🔀 Control Flow — Decision Making and Repetition

Code doesn't always run top to bottom. **Control flow** lets you make decisions and repeat steps.

**Conditionals** let the code choose a path:
```javascript
if (isLargeText) {
    fontSize = "18px";  // take this path
} else {
    fontSize = "12px";  // or take this one
}
```

**Loops** let the code repeat a step multiple times:
```javascript
// Run this once for every page in the PDF
for (let i = 1; i <= totalPages; i++) {
    doc.setPage(i);
    doc.text(`Page ${i}`, 100, 290);
}
```

→ *Deep dive: [Conditionals: Decision Making](#-conditionals-decision-making) · [Loops: Repeating Rules Across Jars](#-loops-repeating-rules-across-jars)*

---

### 🌐 The DOM — The Live Page You Can Touch

The **DOM (Document Object Model)** is the browser's internal map of your webpage. Every button, dropdown, heading, and table is a node in this map — and JavaScript can read or change any of it at any time.

```javascript
// Find the welcome message on the page and hide it
document.getElementById('welcome-msg').style.display = 'none';

// Write new text into the role pill
document.getElementById('final-role').innerText = "Software Engineer";
```

The DOM is what makes JavaScript visual. Without it, JavaScript would just crunch numbers silently in the background. With it, every change you make shows up instantly on screen.

→ *Deep dive: [DOM Interaction: Reading and Updating the Page](#-dom-interaction-reading-and-updating-the-page)*

---

### 🎧 Events — Listening for the User

An **event** is something the user does — clicking, typing, selecting from a dropdown, resizing the window. JavaScript can listen for these and respond with a function.

```javascript
// When the sector dropdown changes, run updateRoles()
<select onchange="updateRoles()">

// When the column header is clicked, collapse that column
th.onclick = () => toggleColumn(idx);
```

Events are the bridge between the user and the code. Without events, nothing would ever happen — the page would just sit there.

→ *Deep dive: [Events: Listening for User Actions](#-events-listening-for-user-actions)*

---

### 🔄 How They All Fit Together

Here's the big picture: **values** are the raw data. **Variables** give them names. **Data structures** group them. **Functions** do things with them. **Control flow** decides when and how many times. **The DOM** puts the results on screen. **Events** make it respond to the user.

In the SkillMap Portal, every single interaction follows this same chain:

> **User clicks a dropdown** *(event)* → **`render()` fires** *(function)* → **reads the selected values** *(variables)* → **filters through thousands of rows** *(data structures + control flow)* → **updates the table on screen** *(DOM)*

Once you see that chain, the rest of the guide is just filling in the details of each step.

---

### 📋 Summary Table

| Building Block | What It Is | Real-World Analogy | Go Deeper |
|---|---|---|---|
| **Value** | A raw piece of data — a number, word, yes/no, or nothing | An ingredient in a recipe | [Variables](#-variables-jars-and-labels) |
| **Variable** | A named label attached to a value | A sticky note on a jar | [Variables](#-variables-jars-and-labels) |
| **Array** | An ordered list of values | A numbered shelf of jars | [Arrays & Array Methods](#-arrays--array-methods-working-with-lists) |
| **Object** | A collection of named values grouped together | A jar with labelled compartments | [Objects](#-objects-named-jars-with-multiple-compartments) |
| **Function** | A named set of reusable instructions | A named recipe you can follow any time | [Functions](#-functions-reusable-rules) |
| **Conditional** | A decision — do this *or* do that depending on the situation | A fork in the road | [Conditionals](#-conditionals-decision-making) |
| **Loop** | A repeated instruction — do this *for every item* or *until done* | An assembly line | [Loops](#-loops-repeating-rules-across-jars) |
| **DOM** | The live map of everything visible on the page | The stage that the audience sees | [DOM Interaction](#-dom-interaction-reading-and-updating-the-page) |
| **Event** | Something the user does that triggers a response | Pressing a doorbell — the chime is the function | [Events](#-events-listening-for-user-actions) |

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🛑 The "Naming Confusion": Java vs JavaScript

One of the most frequent points of confusion for beginners is the nomenclature. Despite the similar branding, **Java and JavaScript are entirely different languages** with distinct architectures and purposes.

### The Origins of the Name

In 1995, Java was the most prominent programming language globally. JavaScript was originally developed as "LiveScript," but was renamed to "JavaScript" as a marketing strategy to capitalize on Java's enormous mindshare at the time.

> A common industry analogy: **"Java is to JavaScript as Car is to Carpet."** They share a prefix but serve completely unrelated functions.

### Key Technical Differences

| Feature | JavaScript *(Used in this Portal)* | Java *(The "Other" Language)* |
|---|---|---|
| **Primary Goal** | Interactivity — controls what happens on screen | Structure — handles backend systems and heavy processing |
| **Execution** | Runs directly inside web browsers | Runs inside a Virtual Machine (JVM) |
| **Flexibility** | Dynamic — easier to change and adapt quickly | Strict — requires precise type definitions for stability |
| **Where You Write It** | Inside `<script>` tags in an HTML file | In separate `.java` files, compiled before running |

In the SkillMap Portal, JavaScript handles **everything the user can interact with**: loading data, building the table, opening modals, filtering dropdowns, and generating PDFs — all without a page refresh.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🐍 JavaScript vs Python: Syntax & Element Management

### 1. The Grammar (Syntax) Gap

Different languages organize instructions differently.

- **JavaScript** uses curly braces `{ }` to group blocks of code, and semicolons `;` to end statements.
- **Python** uses indentation (whitespace) to define blocks, and no semicolons.

```javascript
// JavaScript: curly braces + semicolons
function greet(name) {
    return "Hello, " + name + "!";
}
```

```python
# Python: indentation, no braces
def greet(name):
    return "Hello, " + name + "!"
```

Both do the same thing — the syntax is just different grammar for the same idea.

### 2. Element Management: Internal vs External Access

This is one of the most practically important differences for web development.

**JavaScript** operates *inside* the browser. The page is already loaded around it, so it has **direct, native access** to every element on screen via the **DOM** (Document Object Model).

**Python**, when used for browser automation (e.g., with Selenium), operates *externally* — it has to act as a remote controller reaching into the browser from the outside.

#### Finding Elements (The "Hook")

Think of the webpage as a collection of labeled jars already arranged on a shelf. Finding an element is reaching for a specific jar.

| Feature | JavaScript | Python (Selenium) |
|---|---|---|
| **Command** | `document.getElementById('sel-sector')` | `driver.find_element(By.ID, 'sel-sector')` |
| **Access type** | Direct (already inside the system) | Indirect (must reach in from outside) |
| **Speed** | Immediate | Slight overhead per call |

In the SkillMap Portal, JavaScript grabs elements constantly:

```javascript
// From render() in index.html — grabbing the sector dropdown directly
const sVal = document.getElementById('sel-sector').value;
const rVal = document.getElementById('sel-role').value;

// If either is empty, stop immediately — no point building a table
if (!sVal || !rVal) return;
```

No external tool required — the code is *already on the page*, so access is instant.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 📦 Variables: Jars and Labels

Variables define how labels attach to jars, and whether those labels can be moved to different jars later.

### 🔒 `const` — Fixed Label

The label **cannot be reassigned** to a different jar after creation. If the jar is an Object or Array, the *contents* can still change — but the label stays attached to the same jar.

```javascript
// A primitive: the label '5' is stuck to the number jar
const count = 5;

// An object: the label is stuck to the PDF engine jar,
// but the engine itself can still have pages added to it
const doc = new jsPDF('l', 'mm', 'a4');
```

**From the SkillMap Portal:**

```javascript
// From downloadPDF() — these references never need to change,
// so const is the right choice
const { jsPDF } = window.jspdf;
const doc = new jsPDF('l', 'mm', 'a4');
const pageWidth  = doc.internal.pageSize.getWidth();
const pageHeight = doc.internal.pageSize.getHeight();
const primaryEmerald = [16, 185, 129]; // RGB color — fixed config value
```

### 🔄 `let` — Movable Label

The label **can be reassigned** to a different jar over time. Use `let` when a value is expected to change: a counter, a running total, a cursor position.

```javascript
// From downloadPDF() — y tracks the current vertical pen position on the PDF
// and moves down as content is drawn
let y = 32;

// After drawing the description block:
y += descHeight + 10; // label moves to the new position jar

// After drawing another section:
y += 8;               // moves again
```

Another example — a running text string that grows:

```javascript
// From cleanText() — filtered starts empty and characters are appended one by one
let filtered = "";
for (let i = 0; i < str.length; i++) {
    let code = str.charCodeAt(i);
    if (code === 32 || (code >= 33 && code <= 126)) {
        filtered += str[i]; // label reassigned to a longer string jar each time
    }
}
```

### 🧭 When to Use `const` vs `let`

Think of it this way: **if you're going to stick a label on a jar and never move it, use `const`. If the label might need to move to a different jar later, use `let`.**

> **Rule of thumb:** Start with `const` for everything. Only switch to `let` when JavaScript complains — or when you already know the value will change (like a score that goes up, or a position that moves).

Here are some everyday examples to make it click:

**Use `const` when the thing stays the same:**
- A button on the page — it's always *that* button, you're just clicking it
- A colour like `[16, 185, 129]` — it doesn't change mid-way through
- The data you loaded from a file — the contents can update, but the container stays the same

**Use `let` when the thing needs to change:**
- A page counter that goes `1, 2, 3...` as you loop through PDF pages
- A running Y position on the PDF that moves down as you draw each section
- A piece of HTML text you're building up piece by piece

In short: `const` is a label **glued** to the jar. `let` is a label on a **sticky note** — easy to peel off and move.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🔧 Functions: Reusable Rules

A function is a **named block of logic** that groups multiple steps into a single callable unit. Rather than repeating the same 10 lines of code in five places, you write them once inside a function and call it by name.

```javascript
// Basic shape of a function
function doSomething(input) {
    // steps here
    return result;
}
```

### From the Portal: `toggleCWF()`

```javascript
// Toggles the Critical Work Functions panel open/closed
function toggleCWF() {
    const c = document.getElementById('cwf-container');
    const i = document.getElementById('cwf-icon');
    c.classList.toggle('expanded');
    // Ternary: if expanded show ▲, otherwise show ▼
    i.innerText = c.classList.contains('expanded') ? '▲' : '▼';
}
```

One button click calls `toggleCWF()`. Without the function, you'd have to duplicate all four lines everywhere the toggle appears.

### From the Portal: `toggleColumn(colIdx)`

```javascript
// Collapses or expands a specific table column by its index
function toggleColumn(colIdx) {
    const isNowCollapsed = !window._collapsedCols[colIdx]; // flip the boolean
    window._collapsedCols[colIdx] = isNowCollapsed;         // remember the new state
    const table = document.getElementById('grid');
    applyCollapsed(colIdx, isNowCollapsed, table);           // delegate the visual work
}

function applyCollapsed(colIdx, collapse, table) {
    if (!table) return;
    // Update the header cell
    const th = table.querySelectorAll('thead th')[colIdx];
    if (th) th.classList.toggle('col-collapsed', collapse);
    // Update every body cell in that column
    table.querySelectorAll('tbody tr').forEach(row => {
        const cell = row.querySelectorAll('td')[colIdx];
        if (cell) cell.classList.toggle('col-collapsed-cell', collapse);
    });
}
```

Notice how `toggleColumn` doesn't do the visual work itself — it delegates to `applyCollapsed`. This **separation of concerns** is good practice: one function decides *what* to do, another decides *how*.

### Arrow Functions: The Shorthand Form

Arrow functions (`=>`) are a shorter syntax for writing functions, commonly used for small, one-purpose operations.

```javascript
// Traditional function
function double(n) { return n * 2; }

// Equivalent arrow function
const double = (n) => n * 2;
```

From the Portal, arrow functions appear constantly inside array methods:

```javascript
// Each d is a row of job data — find the one matching the selected role
const roleData = jobData.find(d => d[rKey] === rVal && d[sKey] === sVal);

// Get a friendly label for a column header
const getFriendlyLabel = (label) => {
    const l = label ? label.trim() : "";
    if (l.toUpperCase().startsWith("TSC")) return "Competencies";
    if (l.toUpperCase().startsWith("PROFICIENCY")) return "Proficiency";
    return "K&A";
};
```

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🌐 DOM Interaction: Reading and Updating the Page

The **DOM (Document Object Model)** is the browser's internal, live representation of the page. Every visible element — text, buttons, containers, tables — exists as a jar inside the DOM tree. JavaScript can reach in and read or change any of it at any time.

### Step 1 — Locating a Jar

```javascript
document.getElementById('welcome-msg');
```

This searches the DOM shelf for the jar with the ID `welcome-msg`. It does not create a new one; it retrieves an existing one.

### Step 2 — Attaching a Label

```javascript
const welcome = document.getElementById('welcome-msg');
```

Attaching a `const` label gives you a direct, high-speed handle to that jar. You can now use `welcome` instead of calling `getElementById` repeatedly.

### Step 3 — Modifying the Jar

```javascript
welcome.style.display = 'none'; // hide the welcome message
```

The jar still exists in memory — it's just invisible. Toggle it back with `'flex'` or `'block'`.

### Types of DOM Interaction

| Type | Example | Purpose |
|---|---|---|
| **Read** | `inputBox.value` | Observe current contents |
| **Write** | `element.innerText = "New Title"` | Replace visible text |
| **Style** | `element.style.color = "red"` | Change appearance |
| **Control** | `element.style.display = "none"` | Include or exclude from render |
| **Class** | `element.classList.toggle('expanded')` | Switch CSS classes on/off |
| **HTML** | `element.innerHTML = "<b>Bold</b>"` | Replace with rich HTML content |

### From the Portal: The `render()` Function

`render()` is the heart of the portal. Every time a dropdown changes, `render()` fires and repaints the entire interface. Here is a slice of what it does using DOM interaction:

```javascript
function render() {
    const sVal = document.getElementById('sel-sector').value;  // READ the sector
    const rVal = document.getElementById('sel-role').value;    // READ the role
    if (!sVal || !rVal) return;                                 // Guard clause — exit early if incomplete

    // CONTROL: hide the welcome screen, show the data area
    document.getElementById('welcome-msg').style.display = 'none';
    document.getElementById('app-content').style.display = 'flex';

    // CONTROL: unlock the Export PDF button
    document.getElementById('btn-pdf').disabled = false;

    // WRITE: update the breadcrumb pill text
    document.getElementById('final-role').innerText = rVal;

    // WRITE + STYLE: update the description text
    const descRow = jobDescData.find(d => d[dR] === rVal);
    document.getElementById('final-desc').innerText = descRow ? descRow[dD] : "";
}
```

> **Key Idea:** The DOM is a **live system**. Updates appear instantly without a page refresh because the browser immediately recalculates the layout after each change.

### From the Portal: Dynamically Building the CWF Panel

Rather than hardcoding HTML, JavaScript creates DOM elements programmatically and appends them to the page:

```javascript
// For each Critical Work Function group, build and attach a DOM node
for (const [fn, ts] of Object.entries(groups)) {
    const g = document.createElement('div');   // create a new <div> jar
    g.className = "cwf-group";                 // assign a CSS class
    g.innerHTML = `<div class="cwf-header">${fn}</div><ul class="task-list"></ul>`;

    // For each task in this function, create a list item and append it
    ts.forEach(t => {
        const li = document.createElement('li');
        li.className = "task-item";
        li.innerText = t;
        g.querySelector('ul').appendChild(li); // attach <li> to the <ul> inside g
    });

    cont.appendChild(g); // attach the whole group to the page container
}
```

This pattern — `createElement` → set content → `appendChild` — is a core DOM building block.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 📋 Arrays & Array Methods: Working with Lists

An array is an **ordered list of jars**. Arrays are one of JavaScript's most-used data structures, and they come with powerful built-in methods that can filter, transform, and reduce lists in one readable line.

```javascript
const fruits = ["apple", "banana", "cherry"];
fruits[0]; // "apple" — zero-indexed
```

### The "Big Four" Array Methods

#### `.filter()` — Keep only matching jars

```javascript
// From render() — keep only the skill rows that belong to this role and sector
const filtered = skillData.filter(d =>
    d[ss] === sVal &&
    pairs.has(`${(d[st] || "").trim()}|${(d[sl] || "").trim()}`)
);
```

`.filter()` returns a **new array** of every element where the test returns `true`. The original array is untouched.

#### `.map()` — Transform every jar into a new shape

```javascript
// From showSectorAnalytics() — convert the skill map object into an array of
// {name, count} objects that are easier to sort and display
const allSkills = Object.entries(skillToRolesMap)
    .map(([name, roleSet]) => ({ name: name, count: roleSet.size }))
    .filter(s => s.count > 0)
    .sort((a, b) => b.count - a.count);
```

`.map()` returns a **new array** of the same length, with each element replaced by the return value of your function.

#### `.find()` — Get the first matching jar

```javascript
// From updateRoles() — find the header column whose name contains "sector"
const sKey = jobHeaders.find(h => h.toLowerCase().includes('sector'));

// From render() — find the description row matching the selected role
const descRow = jobDescData.find(d => d[dR] === rVal);
```

`.find()` returns the **first element** that matches, or `undefined` if none do. Notice how the portal uses `.find()` constantly to locate the right column key by name rather than by hardcoded index — making the code resilient to column reordering.

#### `.forEach()` — Run a rule for every jar (no return value)

```javascript
// From updateRoles() — add each role as an <option> in the dropdown
roles.forEach(r => rSelect.add(new Option(r, r)));

// From showPeerRoles() — build the HTML for each sector's roles
sortedSectorNames.forEach(secName => {
    const roles = Array.from(diffSectorGroups[secName]).sort();
    diffSectorsHtml += `<div>...</div>`;
});
```

`.forEach()` is for **side effects** (updating the DOM, building strings) — it does not return a new array.

### Chaining Methods

Because these methods return arrays, you can **chain them** — the output of one becomes the input of the next:

```javascript
// From updateRoles() — one readable pipeline:
// 1. Filter job data to the selected sector
// 2. Extract the role name from each row (.map)
// 3. Remove duplicates ([...new Set(...)])
// 4. Remove empty strings (.filter(Boolean))
// 5. Sort alphabetically (.sort)
const roles = [...new Set(
    jobData
        .filter(d => d[sKey] === sVal)
        .map(d => d[rKey])
)].filter(Boolean).sort();
```

Each step is a separate, readable concern. This is far cleaner than writing a nested loop manually.

### Removing Duplicates with `Set`

A `Set` is a collection that **automatically rejects duplicates**. Wrapping an array in `new Set(...)` and spreading it back with `[...]` is the idiomatic JavaScript way to deduplicate:

```javascript
// Get all unique sector names from thousands of job rows
const sectors = [...new Set(jobData.map(d => d[sKey]))].filter(Boolean).sort();

// Get the unique content items in a table cell
const uniqueItems = [...new Set(filtered.map(d => d[v]).filter(val => val && val !== '-'))];
```

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🗃️ Objects: Named Jars with Multiple Compartments

An object groups **related data under named keys**, like a jar with labeled sections inside.

```javascript
const skill = {
    name: "Data Analysis",
    level: 3,
    sector: "Infocomm Technology"
};

skill.name;      // "Data Analysis"
skill["level"];  // 3
```

### From the Portal: JSON Data Structure

The entire portal's data arrives as a single JSON object with four named sections:

```javascript
// After fetch and decompression:
const data = JSON.parse(decompressed);

// Each key is a named compartment in the data jar
skillData    = data.job_roles.records;    // the skills matrix rows
skillHeaders = data.job_roles.columns;    // the column names
jobData      = data.skills_map.records;   // role-to-sector mapping
cwfData      = data.cwf.records;          // Critical Work Functions
```

### Building Objects Dynamically

Objects can also be built on-the-fly as data is processed:

```javascript
// From showSectorAnalytics() — build a map of skill → set of roles that need it
const skillToRolesMap = {};

jobData.forEach(d => {
    if (d[js] === sectorName) {
        const baseSkillName = d[jt].replace(/\s*level\s*\d+/gi, "").trim();

        // Create the key if it doesn't exist yet, then add the role
        if (!skillToRolesMap[baseSkillName]) skillToRolesMap[baseSkillName] = new Set();
        skillToRolesMap[baseSkillName].add(d[jr]);
    }
});
```

After this loop, `skillToRolesMap["Data Analysis"]` would be a `Set` of every role requiring that skill — ready to be counted and sorted.

### Destructuring Objects

Rather than writing `const name = obj.name; const count = obj.count;`, JavaScript lets you **destructure** in one line:

```javascript
// From the PDF engine — pull jsPDF out of the global window.jspdf object
const { jsPDF } = window.jspdf;

// Equivalent to:
// const jsPDF = window.jspdf.jsPDF;
```

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🔄 Loops: Repeating Rules Across Jars

Loops automate a rule across a sequence of jars, replacing repetitive manual code.

### `for` Loop — Classic Counter

```javascript
// From downloadPDF() — add page numbers to every page
const totalPages = doc.internal.getNumberOfPages();

for (let i = 1; i <= totalPages; i++) {
    doc.setPage(i);
    const footerText = `Page ${i} of ${totalPages}`;
    const textWidth = doc.getTextWidth(footerText);
    doc.text(footerText, (pageWidth / 2) - (textWidth / 2), pageHeight - 10);
}
```

`i` starts at 1, increments by 1 each loop, and stops when it exceeds `totalPages`. Every page gets a centered footer automatically.

### `for...of` Loop — Iterate Over Values

```javascript
// From render() — populate every filter dropdown with the same headers
for (const id of ['row1', 'row2', 'row3', 'col1', 'col2', 'val']) {
    const s = document.getElementById(id);
    filteredHeaders.forEach(h => s.add(new Option(h, h)));
}
```

### `for...in` / `Object.entries()` — Iterate Over Object Keys

```javascript
// From render() — loop through CWF groups (an object keyed by function name)
for (const [fn, ts] of Object.entries(groups)) {
    // fn = function name (e.g. "Manage Data")
    // ts = Set of tasks under that function
    const g = document.createElement('div');
    g.innerHTML = `<div class="cwf-header">${fn}</div>`;
    // ... append task items ...
    cont.appendChild(g);
}
```

`Object.entries()` converts an object into an array of `[key, value]` pairs, which you can then loop over cleanly.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🔀 Conditionals: Decision Making

Conditionals allow the program to choose between outcomes based on the current state of a jar.

### `if / else`

```javascript
// From render() — show or hide the Track pill based on whether data exists
if (roleData && roleData[tKey]) {
    const trackPill = document.getElementById('final-track');
    trackPill.innerText = roleData[tKey];
    trackPill.style.display = 'inline-block';
} else {
    document.getElementById('final-track').style.display = 'none';
}
```

### Ternary Operator `? :`

A compact one-line `if/else` for simple decisions:

```javascript
// condition ? valueIfTrue : valueIfFalse

// From toggleCWF() — update the icon based on current state
i.innerText = c.classList.contains('expanded') ? '▲' : '▼';

// From showPeerRoles() — choose font size based on accessibility mode
const sectorHeaderSize = isLargeText ? "18px" : "12px";

// From downloadPDF() — label continuation pages
const label = (data.pageNumber === tableStartPage)
    ? "SKILLS MATRIX"
    : "SKILLS MATRIX (CONTINUED)";
```

### Guard Clauses (Early Return)

Rather than deeply nesting `if` blocks, the portal uses **guard clauses** to exit early if a precondition isn't met:

```javascript
// From render() — don't do anything unless both dropdowns have values
function render() {
    const sVal = document.getElementById('sel-sector').value;
    const rVal = document.getElementById('sel-role').value;
    if (!sVal || !rVal) return; // 🛑 stop here if incomplete

    // ... all the real work happens below, without nesting ...
}

// From applyCollapsed() — don't crash if the table doesn't exist yet
function applyCollapsed(colIdx, collapse, table) {
    if (!table) return;
    // ...
}
```

Guard clauses keep functions flat and readable — a good habit to develop early.

### Compact View Lock: A Real Conditional Example

```javascript
// From render() — lock the Compact View checkbox when Cols 2 is active
const col2Val   = document.getElementById('col2').value;
const isCol2Active = col2Val && col2Val !== 'none' && col2Val !== '';
const viewToggle   = document.getElementById('view-toggle');
const lockIcon     = document.getElementById('compact-lock-icon');

if (isCol2Active) {
    viewToggle.checked    = true;
    viewToggle.disabled   = true;
    viewToggle.style.opacity = '0.5';
    viewToggle.style.cursor  = 'not-allowed';
    if (lockIcon) lockIcon.style.display = 'inline';
} else {
    viewToggle.disabled      = false;
    viewToggle.style.opacity = '1';
    viewToggle.style.cursor  = 'pointer';
    if (lockIcon) lockIcon.style.display = 'none';
}
```

One `if/else` block manages six DOM property changes simultaneously. This is what makes JavaScript powerful — a single conditional can reshape a visible section of the UI.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## ⏳ Asynchronous JavaScript: Fetching & Loading Data

Web apps often need to **wait** for something — a network request, a file load — without freezing the page. JavaScript handles this with asynchronous patterns.

### The Problem: Waiting Without Freezing

If loading a 3MB file took 2 seconds and JavaScript stopped everything while waiting, the browser would hang. Instead, JavaScript says "go fetch this, and when it's done, run *this* function."

### Promises and `.then()` Chaining

```javascript
// From index.html — the full data loading pipeline
fetch("skillmap_data.json.gz")           // 1. Request the compressed file
    .then(response => response.arrayBuffer())  // 2. When it arrives, read the raw bytes
    .then(buffer => {
        // 3. Decompress the gzip bytes into a string (using the Pako library)
        const decompressed = pako.inflate(new Uint8Array(buffer), { to: "string" });

        // 4. Parse the JSON string into a usable JavaScript object
        const data = JSON.parse(decompressed);

        // 5. Distribute the data into module-level variables
        skillData    = data.job_roles.records;
        skillHeaders = data.job_roles.columns;
        jobData      = data.skills_map.records;
        cwfData      = data.cwf.records;

        // 6. Populate the Sector dropdown with unique sector names
        const sectors = [...new Set(jobData.map(d => d[sKey]))].filter(Boolean).sort();
        sectors.forEach(s => sSelect.add(new Option(s, s)));
    })
    .catch(error => console.error("Error loading skillmap data:", error));
```

Each `.then()` receives the output of the previous step. The `.catch()` at the end handles any error in the entire chain — one safety net for all steps.

### Header Reordering After Load

Once the data is parsed, the portal swaps specific column pairs into a better display order — without touching the underlying data:

```javascript
// From the data loading block
const swapHeaders = (headers, name1, name2) => {
    const idx1 = headers.indexOf(name1);
    const idx2 = headers.indexOf(name2);
    if (idx1 !== -1 && idx2 !== -1) {
        // Destructuring swap — no temporary variable needed
        [headers[idx1], headers[idx2]] = [headers[idx2], headers[idx1]];
    }
};

// Classification should appear before Items
swapHeaders(skillHeaders, "Knowledge / Ability Items", "Knowledge / Ability Classification");
// Code should appear before Category
swapHeaders(skillHeaders, "TSC_CCS Category", "TSC_CCS Code");
```

The `[a, b] = [b, a]` pattern is a clean JavaScript trick for swapping two values without a temporary holding variable.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 📝 Template Literals: Building HTML Strings

Template literals (backtick strings) allow you to **embed variables and expressions directly inside strings**, making dynamic HTML generation far more readable than string concatenation.

```javascript
// Old way (concatenation — hard to read)
const html = "<div class='" + myClass + "'>" + myText + "</div>";

// New way (template literal — clear and clean)
const html = `<div class='${myClass}'>${myText}</div>`;
```

### From the Portal: Building the Skill Search URL

```javascript
// From searchSkill() — builds and opens a live search URL
function searchSkill(skillName) {
    navigator.clipboard.writeText(skillName).then(() => {
        const toast = document.getElementById("toast");
        toast.innerText = `Searching portal for: ${skillName}`;  // template literal
        toast.className = "show";

        const searchUrl = `https://courses.myskillsfuture.gov.sg/search?q=${encodeURIComponent(skillName)}&termOrigin=ORGANIC`;

        setTimeout(() => {
            toast.className = "";
            window.open(searchUrl, "_blank"); // open in a new tab
        }, 500);
    });
}
```

### From the Portal: Building the Peer Roles Modal

Template literals shine when building large HTML blocks:

```javascript
// From showPeerRoles() — the entire modal is built as one template literal
const modalHtml = `
    <div id="peer-overlay" onclick="closeModal()" style="position:fixed; ..."></div>
    <div id="peer-modal" class="${accessibilityClass}" style="...">
        <h3 class="modal-title">
            Skill Portability: ${title} (L${level})
        </h3>
        <div>
            <h4>Within ${currentSector}</h4>
            ${renderSimpleList(sameSector)}
        </div>
        <button onclick="closeModal()">Close</button>
    </div>`;

const div = document.createElement('div');
div.id = "modal-wrapper";
div.innerHTML = modalHtml;        // inject the built HTML into the page
document.body.appendChild(div);  // attach to the live DOM
```

The `${}` placeholders are evaluated at runtime — `accessibilityClass`, `title`, `level`, `currentSector` are all live JavaScript values embedded directly into the HTML string.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🖱️ Events: Listening for User Actions

Events connect user actions (clicks, changes, key presses) to JavaScript functions.

### Inline Event Handlers

The simplest approach — write the handler directly in the HTML attribute:

```html
<!-- From index.html — the sector dropdown calls updateRoles() on change -->
<select id="sel-sector" onchange="updateRoles()"></select>

<!-- The role dropdown triggers a full render -->
<select id="sel-role" onchange="render()"></select>

<!-- The CWF expand/collapse button -->
<div id="cwf-toggle" onclick="toggleCWF()">Critical Work Functions</div>
```

### Assigning Handlers in JavaScript

You can also assign event handlers from the script side, which keeps HTML cleaner and allows dynamic targeting:

```javascript
// From initCollapsibleColumns() — clicking a column header collapses it
th.onclick = () => toggleColumn(idx);

// From render() — clicking the sector pill opens analytics for that sector
const finalSectorEl = document.getElementById('final-sector');
finalSectorEl.onclick = () => showSectorAnalytics(sVal);
```

### `DOMContentLoaded` — Run Code After the Page Loads

```javascript
// From index.html — set up defaults only after the DOM is fully parsed
document.addEventListener('DOMContentLoaded', () => {
    initMobileDefaults();

    window.addEventListener('resize', () => {
        // reserved for future use
    });
});
```

This prevents errors from trying to access DOM elements before they exist.

### `MutationObserver` — Watch for DOM Changes

For more advanced scenarios, the portal watches for newly added elements:

```javascript
// Watches for modal elements being added to the body
// and adds the 'active' class for mobile animation
const observer = new MutationObserver((mutations) => {
    mutations.forEach((mutation) => {
        mutation.addedNodes.forEach(node => {
            if (node.id === 'modal-wrapper') {
                const modal = document.getElementById('peer-modal');
                if (modal && window.innerWidth < 900) {
                    setTimeout(() => modal.classList.add('active'), 10);
                }
            }
        });
    });
});
observer.observe(document.body, { childList: true });
```

This is an advanced pattern — a `MutationObserver` fires a callback whenever child nodes are added or removed from the watched element.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 🔤 Data Transformation & Regular Expressions

Raw data is rarely in the exact shape needed for display. JavaScript provides string and regex tools to clean and reshape it.

### `String` Methods

```javascript
// Normalize column names to find them by partial match
h.toLowerCase().includes('sector')   // true if header contains "sector"
h.toLowerCase().includes('level')    // true if header contains "level"

str.trim()        // removes leading and trailing whitespace
str.replace(x, y) // replace occurrences of x with y
str.split('.')    // split a string into an array by delimiter
```

### Regular Expressions (Regex)

Regex is a pattern-matching language embedded in JavaScript. It looks intimidating at first, but each piece has a specific meaning.

```javascript
// From showSectorAnalytics() — strip " Level 3" or " (Advanced)" from a skill title
// to get just the base name
const baseSkillName = rawTitle
    .replace(/\s*level\s*\d+/gi, "")   // remove " Level 3", " level 12", etc.
    .replace(/\s*\(.*?\)\s*/g, "")     // remove anything in parentheses
    .trim();

// From cleanText() inside downloadPDF() — sanitize strings for PDF output
return decoded
    .replace(/\u00a0/g, ' ')           // replace non-breaking spaces with regular spaces
    .replace(/—/g, '--')               // em-dash → double hyphen (Helvetica-safe)
    .replace(/–/g, '-')                // en-dash → single hyphen
    .replace(/[^\x20-\x7E]/g, '')     // strip every character outside printable ASCII
    .replace(/\s+/g, ' ')             // collapse multiple spaces into one
    .trim();
```

**Reading the patterns:**

| Pattern | Meaning |
|---|---|
| `\s*` | Zero or more whitespace characters |
| `\d+` | One or more digits |
| `g` flag | Apply globally (all matches, not just the first) |
| `i` flag | Case-insensitive |
| `.*?` | Any characters, as few as possible (lazy match) |
| `[^\x20-\x7E]` | Any character *not* in the printable ASCII range |

### `JSON.parse()` and `JSON.stringify()`

```javascript
// Unpack a compressed JSON string into a usable object
const data = JSON.parse(decompressed);

// Encode an object as a string key (used to group rows by their row+column values)
const groupKey = JSON.stringify({ r: [d[r1], d[r2], d[r3]], c: [d[c1], d[c2]] });

// Later — decode it back
const key = JSON.parse(groupKey);
```

`JSON.stringify` is an elegant trick for using a complex object as a Map key — since Map keys are compared by reference, not value, turning an object into a string makes it safely comparable.

[⬆ Back to Table of Contents](#-table-of-contents)

---

## 📚 Quick Reference: Key Commands

| Command | Purpose | SkillMap Portal Example |
|---|---|---|
| `document.getElementById(id)` | Find a DOM element by its ID | `document.getElementById('sel-sector')` |
| `element.value` | Read the current value of an input or select | `document.getElementById('sel-role').value` |
| `element.innerText = "..."` | Write plain text into an element | `document.getElementById('final-role').innerText = rVal` |
| `element.innerHTML = "..."` | Write HTML markup into an element | `cont.innerHTML = ""` (clear the CWF panel) |
| `element.style.display = "..."` | Show or hide an element | `welcome.style.display = 'none'` |
| `element.classList.toggle(cls)` | Add a class if absent, remove if present | `c.classList.toggle('expanded')` |
| `element.disabled = true/false` | Enable or disable a button or input | `document.getElementById('btn-pdf').disabled = false` |
| `document.createElement(tag)` | Create a new DOM element | `document.createElement('div')` |
| `parent.appendChild(child)` | Attach an element to the DOM | `cont.appendChild(g)` |
| `fetch(url)` | Request a remote file | `fetch("skillmap_data.json.gz")` |
| `JSON.parse(str)` | Convert a JSON string to an object | `JSON.parse(decompressed)` |
| `JSON.stringify(obj)` | Convert an object to a string | `JSON.stringify({ r: [...], c: [...] })` |
| `array.filter(fn)` | Keep elements that pass a test | `skillData.filter(d => d[ss] === sVal)` |
| `array.map(fn)` | Transform every element | `jobData.map(d => d[rKey])` |
| `array.find(fn)` | Get the first matching element | `jobHeaders.find(h => h.includes('sector'))` |
| `array.forEach(fn)` | Run a function on every element | `roles.forEach(r => select.add(new Option(r, r)))` |
| `array.sort()` | Sort an array (modifies in place) | `.sort((a, b) => b.count - a.count)` |
| `[...new Set(array)]` | Remove duplicates from an array | `[...new Set(jobData.map(d => d[sKey]))]` |
| `str.includes(x)` | Check if a string contains a substring | `h.toLowerCase().includes('level')` |
| `str.replace(regex, x)` | Replace pattern matches in a string | `.replace(/\s*level\s*\d+/gi, "")` |
| `str.trim()` | Remove leading/trailing whitespace | `d[jt].trim()` |
| `setTimeout(fn, ms)` | Run a function after a delay | `setTimeout(() => toast.className = "", 500)` |
| `window.open(url, "_blank")` | Open a URL in a new tab | `window.open(searchUrl, "_blank")` |
| `navigator.clipboard.writeText(str)` | Copy text to the clipboard | `navigator.clipboard.writeText(skillName)` |
| `encodeURIComponent(str)` | Make a string safe for use in a URL | `encodeURIComponent(skillName)` |
| `doc.save(filename)` | Export and download the PDF | `doc.save("Map_SoftwareEngineer.pdf")` |

---

## 🌍 Extending the SkillMap Portal: Future Possibilities

The SkillMap Portal is built entirely in **Vanilla JavaScript** — pure JS, no frameworks, no build tools. For a single-developer project loaded from a single HTML file, this is the right call. It's lean, fast, and has zero setup overhead.

But as a product grows — more data, more users, more features, more collaborators — the tools you reach for change. This section imagines what the SkillMap Portal could become, and which technologies would make each future version possible.

---

### ⚛️ React.js — If the Portal Became a Multi-View App

**The limitation today:** Every time a user changes a dropdown, the entire `render()` function fires and repaints the whole table from scratch. This works fine for a single view, but as soon as you want multiple panels open at once — say, a sidebar comparison, a live search, and an analytics chart all updating simultaneously — manually wiring up DOM updates becomes a tangled mess.

**What React would change:** React lets you break the UI into self-contained **components** — a `RoleCard`, a `SkillGrid`, a `CompareModal` — each managing its own state. When data changes, only the affected component rerenders, not the whole page. The portal's entire `render()` function could be replaced by a component tree that updates itself intelligently.

```javascript
// Today — one big function repaints everything
function render() {
    document.getElementById('welcome-msg').style.display = 'none';
    document.getElementById('final-role').innerText = rVal;
    // ... 200 more lines ...
}

// With React — each piece updates itself when its data changes
function RoleBadge({ role }) {
    return <span className="role-pill">{role}</span>;
}
function SkillGrid({ sector, role }) {
    const data = useSkillData(sector, role); // automatically rerenders when this changes
    return <table>...</table>;
}
```

**Why it would matter for the Portal:** If future versions added user accounts, saved comparisons, or real-time collaboration — features where different users see different states simultaneously — React's component model would make that manageable. It's also the most widely known framework, meaning it's easier to find collaborators.

📖 Resources:
- [Official React Docs (react.dev)](https://react.dev) — the best starting point, with interactive examples
- [React in 100 Seconds — Fireship (YouTube)](https://www.youtube.com/watch?v=Tn6-PIqc4UM) — a fast visual overview
- [Full React Tutorial — The Net Ninja (YouTube)](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gZD-Tvwfod2gaISzfRiP9d) — beginner-friendly, step by step

---

### 🟢 Node.js — If the Data Pipeline Moved to a Server

**The limitation today:** The data pipeline is entirely manual. When the competency framework Excel files are updated, someone has to re-export the CSVs, run the conversion script, recompress the `.gz` file, and redeploy. The portal has no way to update its own data — it just loads whatever file is sitting on the server.

**What Node.js would change:** Node.js would let you write a **server-side script** that watches for new Excel uploads, converts them to JSON automatically, and serves the freshest data to the portal without any manual steps. You could also expose an API — so instead of fetching one monolithic `.gz` file, the portal fetches only the sector or role it needs on demand.

```javascript
// A Node.js script that auto-converts Excel → JSON when a new file appears
const chokidar = require('chokidar');
const { convertExcelToJson } = require('./pipeline');

chokidar.watch('./uploads/*.xlsx').on('add', (filePath) => {
    console.log(`New file detected: ${filePath}`);
    convertExcelToJson(filePath); // run the same pipeline logic, now automated
});
```

**Why it would matter for the Portal:** The current `.gz` file loads the entire dataset on every visit. As the competency framework grows, that payload grows too. A Node.js API would let the portal fetch only what it needs — a specific sector, a specific role — making it faster and far more scalable for larger institutions managing hundreds of job roles.

📖 Resources:
- [Node.js Official Site (nodejs.org)](https://nodejs.org) — download and getting started guides
- [Node.js Crash Course — Traversy Media (YouTube)](https://www.youtube.com/watch?v=fBNz5xF-Kx4) — practical intro, no fluff
- [The Odin Project: NodeJS Path](https://www.theodinproject.com/paths/full-stack-javascript) — free, structured full curriculum

---

### 🔷 TypeScript — If the Portal Grew to a Team Project

**The limitation today:** The portal currently uses a lot of dynamic column-key lookups — finding the right header by calling `.find(h => h.toLowerCase().includes('sector'))` and storing it in a variable like `sKey`. This works, but there's nothing stopping you from accidentally passing `sKey` where `rKey` was expected. The error only surfaces at runtime, when the table silently renders wrong.

**What TypeScript would change:** TypeScript would let you define exactly what shape each piece of data is allowed to take. A `SkillRow` type would declare which fields exist and what type each is. If you tried to pass a string where a number was expected, TypeScript would flag it in your editor before you even ran the code.

```typescript
// Without TypeScript — silent runtime bugs possible
function buildRow(data, key) {
    return data[key]; // no idea if key is valid
}

// With TypeScript — errors caught immediately
type SkillRow = {
    sector: string;
    role: string;
    proficiencyLevel: number;
};

function buildRow(data: SkillRow, key: keyof SkillRow) {
    return data[key]; // ✅ TypeScript ensures key is a valid field name
}
```

**Why it would matter for the Portal:** Right now one person wrote all the code and holds the context in their head. The moment a second developer joins, or you return to the code six months later, that implicit knowledge is gone. TypeScript acts as self-documenting code — the types tell you exactly what each function expects, making the codebase safer to extend and easier to hand off.

📖 Resources:
- [TypeScript Official Docs (typescriptlang.org)](https://www.typescriptlang.org/docs/) — includes a live playground in the browser
- [TypeScript in 100 Seconds — Fireship (YouTube)](https://www.youtube.com/watch?v=zQnBQ4tB3ZA)
- [Total TypeScript (totaltypescript.com)](https://www.totaltypescript.com/tutorials) — free interactive tutorials

---

### 🟨 Vue.js — A Lighter Path to a Framework

**The limitation today:** The same as with React — as the portal's interactivity grows, manually orchestrating DOM updates becomes harder to maintain. But React has a steeper learning curve and requires a build tool setup.

**What Vue.js would change:** Vue is designed to be adopted **incrementally**. You can drop a single `<script>` tag into the existing HTML — no build tool needed — and start making individual parts of the page reactive. The portal's sidebar filters, for example, could be converted to a Vue component without touching the rest of the code.

```html
<!-- Vue can be dropped into an existing HTML file — no build step needed -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="filter-panel">
    <!-- Vue handles the dropdown binding and re-render automatically -->
    <select v-model="selectedSector" @change="updateRoles">
        <option v-for="s in sectors" :value="s">{{ s }}</option>
    </select>
</div>
```

**Why it would matter for the Portal:** Vue's `@change` and `v-model` directly replace the portal's `onchange="render()"` and `document.getElementById(...).value` patterns — but with automatic two-way data binding. The transition would feel natural, and the portal could migrate one section at a time rather than doing a full rewrite.

📖 Resources:
- [Official Vue Docs (vuejs.org)](https://vuejs.org/guide/introduction) — widely praised as one of the clearest framework docs available
- [Vue.js Crash Course — Traversy Media (YouTube)](https://www.youtube.com/watch?v=qZXt1Aom3Cs)

---

### 📦 npm & ⚡ Vite — If the Portal Split Into Multiple Files

**The limitation today:** All 3,000+ lines of the portal live in a single `index.html`. That's manageable now, but as features are added — a user preferences module, a charting library, a data export engine — the file becomes unwieldy. Finding and editing a specific function starts to feel like searching a very long book with no chapters.

**What npm and Vite would change:** npm would let you install libraries properly (`npm install jspdf`) instead of relying on CDN script tags that could change or go offline. Vite would let you split the code across logical files — `render.js`, `pdf.js`, `analytics.js`, `dom.js` — and import them cleanly.

```javascript
// Instead of one enormous index.html, the code lives in focused files:

// pdf.js — all PDF export logic lives here
export function downloadPDF(data) { ... }

// analytics.js — sector and track analysis lives here
export function showSectorAnalytics(sector) { ... }

// main.js — the entry point just imports what it needs
import { downloadPDF } from './pdf.js';
import { showSectorAnalytics } from './analytics.js';
```

**Why it would matter for the Portal:** The current structure means any change to the PDF export risks accidentally breaking the render logic — they're inches apart in the same file. Splitting into modules creates clear boundaries. It also makes it far easier to test individual pieces in isolation, and to onboard a new contributor who only needs to understand one module at a time.

📖 Resources:
- [npmjs.com](https://www.npmjs.com) — search for any package and see its docs and download stats
- [Vite Official Docs (vitejs.dev)](https://vitejs.dev/guide/) — get a project running in under a minute
- [npm Crash Course — Traversy Media (YouTube)](https://www.youtube.com/watch?v=jHDhaSSKmB0)
- [Vite Crash Course — Traversy Media (YouTube)](https://www.youtube.com/watch?v=89NJdbYTgJ8)

---

### 🗺️ A Possible Roadmap for the Portal

If the SkillMap Portal were to evolve into a full-scale institutional platform, the technology upgrades might look something like this:

| Version | What's New | Technology Added |
|---|---|---|
| **v1 (Today)** | Single HTML file, static data, Vanilla JS | — |
| **v2** | Auto-updating data pipeline, on-demand API | Node.js backend |
| **v3** | Codebase split into modules, npm packages | npm + Vite |
| **v4** | Multi-view UI, saved comparisons, live filters | React or Vue |
| **v5** | Multi-developer team, large codebase | TypeScript |

Each step is an evolution, not a replacement. The Vanilla JavaScript you've learned in this guide is the foundation that every one of those versions is still built on.

📖 General Learning Resources:
- [MDN Web Docs (developer.mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/JavaScript) — the authoritative JavaScript reference, free and maintained by Mozilla
- [javascript.info](https://javascript.info) — the best free written tutorial for JavaScript, from absolute basics to advanced
- [The Odin Project (theodinproject.com)](https://www.theodinproject.com) — a completely free, project-based full-stack curriculum
- [freeCodeCamp (freecodecamp.org)](https://www.freecodecamp.org) — free structured courses with certifications
- [Fireship (YouTube)](https://www.youtube.com/@Fireship) — fast, high-quality videos on every modern JS tool and concept

[⬆ Back to Table of Contents](#-table-of-contents)

---

*Built with ❤️ using the SkillMap Portal as a living, real-world example. Every code snippet in this guide runs in production — open `index.html` and search for the function names to see the full context.*
