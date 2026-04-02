
# 🗺️ SkillMap Portal

[](https://www.google.com/search?q=https://opensource.org/licenses/MIT)
[](https://www.google.com/search?q=https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[](https://www.google.com/search?q=https://github.com/parallax/jsPDF)

An interactive, data-driven web application designed to visualize and compare professional competency frameworks. The **SkillMap Portal** allows users to traverse complex skill ecosystems, identify "Skill Portability" across industry sectors, and generate professional, customized career reports.

Live Demo:  https://huggingface.co/spaces/Miqqie/skillsmap
-----

## 📋 Table of Contents

1.  [The Motivation](https://www.google.com/search?q=%23-the-motivation)
2.  [Objective](https://www.google.com/search?q=%23-objective)
3.  [Data Architecture & Pipeline](https://www.google.com/search?q=%23-data-architecture--pipeline)
4.  [Technical Stack](https://www.google.com/search?q=%23-technical-stack)
5.  [Special Features](https://www.google.com/search?q=%23-special-features)
6.  [Customizable User Experience](https://www.google.com/search?q=%23-customizable-user-experience)
7.  [Automated PDF Report Engine](https://www.google.com/search?q=%23-automated-pdf-report-engine)
8.  [VS Code Setup & Extensions](https://www.google.com/search?q=%23-vs-code-setup--extensions)
9.  [How to Use](https://www.google.com/search?q=%23-how-to-use)

-----

## 💡 The Motivation

The genesis of this project was a real-world data accessibility challenge. The original competency frameworks were stored in an **Excel workbook spread across several different worksheets**.

While the data was comprehensive, the format created a "Silo Effect":

  * **Disconnected Data**: Information was fragmented. A user interested in a specific role would have to manually toggle between several tabs to find the corresponding skills, descriptions, and work functions.
  * **No Unified View**: There was no single interface that could aggregate this data into a cohesive "Career Profile."
  * **Barriers to Analysis**: Identifying skill overlaps between **different job roles** required significant manual effort and cross-tab referencing, making the data difficult for non-technical users to leverage for career planning.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 🎯 Objective
 
The SkillMap Portal bridges the gap between static competency documentation and dynamic career planning. By providing a multi-dimensional view of skills and job roles, the application helps:

  * **Employees** identify their next career move by comparing skill overlaps.
  * **HR Professionals** analyze the density of specific competencies across an entire sector.
  * **Job Seekers** discover "hidden" portability between different job roles and industry sectors.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 🗂️ Data Architecture & Pipeline

To move from fragmented Excel sheets to a high-performance web portal, the data undergoes a specific transformation pipeline: **Excel/CSV → Hierarchical JSON → Gzip Compression**.

### The Conversion Process:

1.  **Normalization**: Raw CSV exports from various worksheets are cleaned and normalized to ensure consistent Skill IDs and Role names.
2.  **Hierarchical Mapping**: Unlike flat CSV rows, the data is structured into a nested JSON format. This allows a single "Job Role" object to contain its associated skills, work functions, and proficiency levels as sub-arrays.
3.  **Compression**: The resulting JSON is compressed into a `.gz` (Gzip) file before being hosted on the server.

### Why Convert & Compress?

  * **Relational Efficiency**: JSON allows for complex "Many-to-Many" relationships (e.g., one skill appearing in many roles) that are cumbersome to navigate in flat CSV worksheets.
  * **Payload Reduction**: Large competency datasets can exceed 5MB+ in plain text. Gzip compression reduces this footprint by **70–80%**, ensuring the app loads instantly even on mobile networks.
  * **Client-Side Speed**: Browsers can parse JSON into JavaScript objects natively. By delivering pre-structured JSON, the application avoids the performance "tax" of parsing raw CSV strings every time a user filters a role.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 🛠️ Technical Stack

The SkillMap Portal utilizes a "Modern Vanilla" architecture.

### 1\. The Engine: Vanilla JavaScript (ES6+)

JavaScript provides the **behavior** of the portal. "Vanilla" refers to using the language in its purest form without external frameworks like React or Angular.

  * **Why Vanilla?** It eliminates "framework overhead," ensuring the app remains lightweight and loads nearly instantly.
  * **Asynchronous Logic:** Uses `async/await` patterns to decompress and process data in the background.

### 2\. Performance: Pako (zlib)

To handle the large-scale data, the portal uses **Pako**. It fetches the compressed `.gz` data and decompresses it instantly in the browser's memory.

### 3\. Document Logic: jsPDF & jspdf-autotable

Used for professional documentation, manually calculating coordinates to place headers, footers, and intersection highlights.

### 4\. UI Architecture: Custom CSS & Responsive Design

  * **Custom CSS Variables:** Allows **Larger Text Mode** and **Compact View** to work by swapping single values that update the entire UI instantly.
  * **Flexbox & CSS Grid:** Ensures alignment regardless of screen size.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## ✨ Special Features

### 1\. Advanced Multi-Pivot Grid

The core engine allows users to pivot data dynamically. You can set Rows, Columns, and Content values to create a custom matrix view of any role's requirements, allowing for a 360-degree view of competency levels.

### 2\. Sector & Track Analytics

The interface features interactive **Sector and Track pills**. Clicking these triggers an automated analysis across all roles within that category to identify and display the **most in-demand skills**.

### 3\. "Skill Portability" Discovery

The **Peer Discovery** algorithm scans the entire database to find other roles—even those in completely different sectors—that require that exact skill at the same level.

### 4\. Integrated Training Discovery

Every skill displayed in the grid table is **dynamically hyperlinked**. Clicking a skill name triggers a direct search on the `myskillsfuture.gov.sg` portal, connecting theoretical competencies to real-world training courses.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 🎛️ Customizable User Experience

The interface acts as a flexible workspace, allowing users to shape exactly what data they see:

  * **Information Filtering**: Toggle specific data layers
  * **Compact Mode**: Designed for power users, this mode strips away decorative padding for high-density side-by-side comparisons.
  * **Larger Text Mode**: Re-scales the entire UI for accessibility or group presentations.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 📄 Automated PDF Report Engine

The application features a sophisticated PDF generation engine powered by **jsPDF** and **autoTable**, employing two distinct rendering logic paths:

### 1\. The Dynamic Matrix Export (Pivot Grid)

  * **Matrix Logic:** Preserves the complex row/column relationships established in the web UI.
  * **Contextual Headers:** Automatically applies "(CONTINUED)" labels on subsequent pages for data continuity.

### 2\. The Comprehensive Job Comparison Report

  * **Dual-Profile Synthesis:** Creates a side-by-side competency map, intelligently grouping **shared competencies**.
  * **Intersection Analysis:** Visually quantifies "transferable experience" where a user's current skills meet the requirements of a target role.

### Aesthetic & Functional Highlights:

  * **Executive Branding:** Styled with a clean, modern color palette (**Slate & Emerald**) and professional headers/footers.
  * **Visual Scannability:** Uses color-coded pills for proficiency levels and zebra-striping to prevent eye fatigue.
  * **Intelligent Layout:** Includes **Smart Page-Break Logic** to ensure multi-line descriptions are never split across pages.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 💻 VS Code Setup & Extensions

To run the SkillMap Portal locally, you must use a local development server to bypass **CORS** security restrictions when fetching the data files.

### Required Extension: Live Server

To enable the **"Go Live"** functionality, install the following in VS Code:

  * **Live Server (by Ritwick Dey):**
      * **How to Install:** Search for "Live Server" in the Extensions tab (`Ctrl+Shift+X`) and click **Install**.
      * **How to Use:** Right-click `index.html` and select **"Open with Live Server"**, or click the **"Go Live"** button in the bottom status bar.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)

-----

## 🚀 How to Use

1.  **Filter**: Select a **Sector** and **Job Role** from the sidebar.
2.  **Analyze Demand**: Click on **Sector or Track pills** to identify the most in-demand skills in that area.
3.  **Explore**: Click on any **hyperlinked skill** to find relevant courses on MySkillsFuture.
4.  **Compare**: Click the Role pill to open the Comparison Modal and see skill transferability.
5.  **Export**: Use the **Export PDF** button to save your view as a professional, shareable report.

[⬆ Back to Table of Contents](https://www.google.com/search?q=%23-table-of-contents)
