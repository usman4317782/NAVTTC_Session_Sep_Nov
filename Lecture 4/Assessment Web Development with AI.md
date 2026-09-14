# Web Development Assessment — Vibe Coding Project
### Full-Stack Frontend System (Client-Side Only) + Free Deployment

**Total Marks: 100**
**Submission Type:** Individual / Group (as instructed by teacher)
**Deployment Requirement:** Mandatory — Live link must be submitted

---

## 1. Project Overview

Students are required to design and develop a **complete, functional web application** using the **"Vibe Coding"** approach (AI-assisted coding using tools like ChatGPT, Claude, Cursor, Copilot, etc., combined with the student's own understanding and customization).

The project must be a **fully working system** — not just static pages — meaning it should include:

- Multiple interconnected pages/screens
- Functional logic (CRUD-like operations: Create, Read, Update, Delete)
- Data persistence using **Browser Local Storage / IndexedDB only**
- A clean, responsive, and professional UI

The system must then be **deployed live for free** so it can be accessed via a public URL.

---

## 2. Project Idea Suggestions (Choose One or Propose Your Own)

Students may choose any real-world mini-system idea, such as:

- Student Management System
- To-Do / Task Manager with Categories
- Expense Tracker
- Library Book Management System
- Inventory / Stock Management
- Simple E-commerce Product Catalog (Cart using Local Storage)
- Employee Attendance Tracker
- Recipe / Blog Management App
- Personal Notes App with Search & Tags
- Quiz / MCQ Practice App with Score Tracking

> Any other idea is acceptable **only if approved by the instructor** before development.

---

## 3. Mandatory Technical Requirements

### 3.1 Allowed Technologies (Strictly Frontend Only)

| Category | Allowed |
|---|---|
| Structure | HTML5 |
| Styling | CSS3, Bootstrap 5 (via CDN) |
| Logic | Vanilla JavaScript (ES6+) |
| Data Storage | Browser **Local Storage** or **IndexedDB** only |
| Icons/Fonts | Font Awesome / Google Fonts / Bootstrap Icons (via CDN) |
| Charts (optional) | Chart.js (via CDN) |

### 3.2 Strictly NOT Allowed

- ❌ Any **paid tool, API key, or subscription-based service**
- ❌ Any **real-time / cloud database** (Firebase Realtime DB, MongoDB Atlas, Supabase, MySQL server, etc.)
- ❌ Any backend server / Node.js / PHP / Python backend
- ❌ Any framework requiring build tools (React, Angular, Vue with npm build) — **unless CDN-based (e.g., React via CDN)** is explicitly approved
- ❌ Paid hosting or hosting requiring credit card verification

### 3.3 File Structure Requirement

Project **must** follow this clean structure (or a logical equivalent):

```
project-name/
│
├── index.html
├── pages/
│   ├── page2.html
│   ├── page3.html
│   └── ...
├── css/
│   └── style.css
├── js/
│   └── script.js
├── assets/
│   ├── images/
│   └── icons/
└── README.md
```

- All CSS/JS **must be in separate files** (no large inline `<style>` or `<script>` blocks except minor inline event handling if justified).
- Code must be **properly commented** and **indented**.

---

## 4. Deployment Requirement (Mandatory)

Students must deploy their project live using **free hosting platforms**, such as:

- **Netlify** (Drag & Drop or GitHub linked)
- **Vercel**
- **GitHub Pages**
- **InfinityFree** (as mentioned) or similar free static hosting
- **Render (Static Site - Free Tier)**

### Deployment Checklist

- [ ] Project is uploaded and accessible via a **public live URL**
- [ ] Live link works on **both desktop and mobile browsers**
- [ ] No broken links, missing files, or console errors on live site
- [ ] `index.html` loads correctly as the homepage
- [ ] All CDN links (Bootstrap, icons, fonts, Chart.js) load properly online

**Submission must include:**
1. Live deployed link
2. GitHub repository link (if used)
3. ZIP file of complete project (as backup)

---

## 5. Assessment Rubrics (Total: 100 Marks)

### Rubric 1: Project Planning & Idea (10 Marks)

| Criteria | Marks |
|---|---|
| Clear problem statement / purpose of the system | 3 |
| Well-defined features list (planned before coding) | 3 |
| Realistic scope suitable for frontend-only system | 4 |

---

### Rubric 2: HTML Structure & Semantic Markup (10 Marks)

| Criteria | Marks |
|---|---|
| Proper use of semantic HTML5 tags (header, nav, main, footer, section) | 4 |
| Multiple pages/views properly linked and organized | 3 |
| Clean, valid, and well-indented HTML code | 3 |

---

### Rubric 3: CSS Styling & Responsiveness (15 Marks)

| Criteria | Marks |
|---|---|
| Proper use of Bootstrap grid system & components | 5 |
| Custom CSS for unique branding/design (not default Bootstrap look) | 5 |
| Fully responsive on mobile, tablet, and desktop | 5 |

---

### Rubric 4: JavaScript Functionality & Logic (20 Marks)

| Criteria | Marks |
|---|---|
| CRUD operations working correctly (Add/View/Edit/Delete) | 8 |
| Form validation (required fields, correct data types, error messages) | 4 |
| Search / filter / sort functionality (if applicable to project) | 4 |
| Clean, modular, and well-commented JavaScript code | 4 |

---

### Rubric 5: Data Persistence (Local Storage / IndexedDB) (15 Marks)

| Criteria | Marks |
|---|---|
| Data correctly saved to Local Storage / IndexedDB | 6 |
| Data correctly retrieved and displayed after page reload | 5 |
| Update and Delete operations correctly reflected in storage | 4 |

---

### Rubric 6: UI/UX Design Quality (10 Marks)

| Criteria | Marks |
|---|---|
| Visual consistency (colors, fonts, spacing) | 3 |
| User-friendly navigation and layout | 3 |
| Use of icons, feedback messages (alerts/toasts), and empty states | 4 |

---

### Rubric 7: Vibe Coding Understanding & Customization (10 Marks)

*(To ensure the student understands the AI-assisted code, not just copy-pasted it)*

| Criteria | Marks |
|---|---|
| Student can explain the logic/flow of their code when asked | 4 |
| Evidence of manual customization beyond AI's default output (naming, structure, extra features) | 3 |
| Student can identify and fix a bug live if asked during viva | 3 |

---

### Rubric 8: Deployment (5 Marks)

| Criteria | Marks |
|---|---|
| Successfully deployed live on a free hosting platform | 3 |
| Live link fully functional with no errors | 2 |

---

### Rubric 9: Documentation (README.md) (5 Marks)

| Criteria | Marks |
|---|---|
| Project title, description, and features list | 2 |
| Technologies used and setup/usage instructions | 2 |
| Live link and screenshots included | 1 |

---

## 6. Marks Distribution Summary

| # | Rubric | Marks |
|---|---|---|
| 1 | Project Planning & Idea | 10 |
| 2 | HTML Structure & Semantic Markup | 10 |
| 3 | CSS Styling & Responsiveness | 15 |
| 4 | JavaScript Functionality & Logic | 20 |
| 5 | Data Persistence (Local Storage/IndexedDB) | 15 |
| 6 | UI/UX Design Quality | 10 |
| 7 | Vibe Coding Understanding & Customization | 10 |
| 8 | Deployment | 5 |
| 9 | Documentation (README.md) | 5 |
| **Total** | | **100** |

---

## 7. Submission Guidelines

1. Submit before the deadline via the specified portal/email/LMS.
2. Include the following in your submission:
   - ✅ Live Deployed Link
   - ✅ GitHub Repository Link (recommended)
   - ✅ ZIP file of project folder
   - ✅ README.md file
3. Be prepared for a **short viva/demo** (5–10 minutes) where you will:
   - Walk through your code
   - Explain how Local Storage/IndexedDB is used
   - Make a small live code change if requested

---

## 8. Academic Integrity Note

- Use of AI tools (ChatGPT, Claude, Copilot, Cursor, etc.) is **allowed and encouraged** as part of "Vibe Coding."
- However, **blind copy-pasting without understanding** will result in marks deduction under Rubric 7.
- Plagiarism between students (identical projects) will result in **zero marks for both parties**.

---

*Good luck! Build something you would actually be proud to show in your portfolio.*
