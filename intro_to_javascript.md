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

1. [The Naming Confusion: Java vs JavaScript](#-the-naming-confusion-java-vs-javascript)
2. [JavaScript vs Python: Syntax & Element Management](#-javascript-vs-python-syntax--element-management)
3. [Variables: Jars and Labels](#-variables-jars-and-labels)
4. [Functions: Reusable Rules](#-functions-reusable-rules)
5. [DOM Interaction: Reading and Updating the Page](#-dom-interaction-reading-and-updating-the-page)
6. [Arrays & Array Methods: Working with Lists](#-arrays--array-methods-working-with-lists)
7. [Objects: Named Jars with Multiple Compartments](#-objects-named-jars-with-multiple-compartments)
8. [Loops: Repeating Rules Across Jars](#-loops-repeating-rules-across-jars)
9. [Conditionals: Decision Making](#-conditionals-decision-making)
10. [Asynchronous JavaScript: Fetching & Loading Data](#-asynchronous-javascript-fetching--loading-data)
11. [Template Literals: Building HTML Strings](#-template-literals-building-html-strings)
12. [Events: Listening for User Actions](#-events-listening-for-user-actions)
13. [Data Transformation & Regular Expressions](#-data-transformation--regular-expressions)
14. [Quick Reference: Key Commands](#-quick-reference-key-commands)

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

> **Rule of thumb:** Use `const` by default. Switch to `let` only when you *know* the value needs to change.

| Use `const` for | Use `let` for |
|---|---|
| DOM element references | Counters and loop indices |
| Configuration values and colors | Cursor/position trackers |
| Data arrays loaded from a file | Accumulated HTML strings |
| Function references | Flags that flip between true/false |

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

*Built with ❤️ using the SkillMap Portal as a living, real-world example. Every code snippet in this guide runs in production — open `index.html` and search for the function names to see the full context.*
