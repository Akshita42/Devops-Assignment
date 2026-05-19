# ✅ Akshiip – To-Do List

A clean, modern, fully-featured **To-Do List** web application built with pure HTML, CSS, and vanilla JavaScript. No frameworks, no build tools, no dependencies — just one self-contained `index.html` file ready to deploy anywhere.

> **Live URL (after S3 deploy):** `http://<your-bucket-name>.s3-website-<region>.amazonaws.com`

---

## 🎯 Features

### Core
| Feature | Details |
|---|---|
| ➕ Add tasks | Input field + **Add** button |
| ✅ Complete tasks | Custom animated checkbox |
| 🗑️ Delete tasks | Per-task delete button with slide-out animation |
| 💾 Persistence | Tasks saved to **localStorage** — survive page refresh |
| 📊 Live statistics | Total / Active / Completed counters update in real time |
| 🔍 Filter system | **All · Active · Completed** tab filters |
| 🧹 Clear Completed | Remove all done tasks in one click |
| ⌨️ Keyboard support | Press **Enter** to add a task |

### Bonus
| Feature | Details |
|---|---|
| ✏️ Inline editing | **Double-click** any task text to edit; **Enter** saves, **Esc** cancels |
| 🎨 Animations | Slide-in on add, slide-out on delete, shake on empty submit |
| 📱 Responsive | Single-column layout on mobile, wider card on desktop |
| 🔒 XSS-safe | All user text is HTML-escaped before DOM insertion |

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **HTML5** | Semantic structure (`<main>`, `<nav>`, `<header>`, `<ul>`) |
| **CSS3** | Custom properties, Flexbox, animations, responsive design |
| **JavaScript ES6+** | DOM manipulation, localStorage, event delegation |
| **Font Awesome 6** | Icons (CDN) |
| **Google Fonts – Inter** | Modern typography (CDN) |
| **AWS S3** | Static website hosting |

---

## 🏗️ Architecture

```
index.html          ← single deployable file
├── <style>         ← all CSS (design tokens, components, animations)
├── <body>          ← semantic HTML structure
│   ├── Stats bar
│   ├── Input card
│   ├── Filter toolbar
│   └── Task list (dynamically rendered)
└── <script>        ← all JavaScript
    ├── State        (tasks[], filter)
    ├── Persistence  (load / save to localStorage)
    ├── CRUD         (addTask, toggleTask, removeTask, updateText, clearCompleted)
    ├── Render       (render, renderList, updateStats)
    └── Event wiring (click, keydown, dblclick)
```

---

## 🚀 AWS S3 Deployment Guide

### Prerequisites
- AWS account with S3 access
- AWS CLI installed (optional)

### Step-by-step

**1. Create an S3 bucket**
```
AWS Console → S3 → Create bucket
Bucket name: akshiip-todo  (must be globally unique)
Region: choose nearest (e.g. ap-south-1 for Mumbai)
Block all public access: UNCHECK (required for static hosting)
```

**2. Enable Static Website Hosting**
```
Bucket → Properties → Static website hosting → Enable
Index document: index.html
Error document: index.html
```

**3. Add a Public Bucket Policy**

Go to **Permissions → Bucket Policy** and paste:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```
Replace `YOUR-BUCKET-NAME` with your actual bucket name.

**4. Upload the file**

Via Console: **Objects → Upload → Add files → index.html → Upload**

Via AWS CLI:
```bash
aws s3 cp index.html s3://YOUR-BUCKET-NAME/index.html --acl public-read
```

**5. Access your app**

Your URL will be:
```
http://YOUR-BUCKET-NAME.s3-website-REGION.amazonaws.com
```
Example: `http://akshiip-todo.s3-website-ap-south-1.amazonaws.com`

---

### Optional: Add HTTPS with CloudFront

1. **CloudFront → Create Distribution**
2. Origin domain: your S3 website endpoint
3. Viewer Protocol Policy: **Redirect HTTP to HTTPS**
4. Default root object: `index.html`
5. Your app will be served over HTTPS at a `*.cloudfront.net` URL

---

## 🖥️ Run Locally

No build step needed. Just open the file:

```bash
# Option 1 – open directly in browser
start index.html          # Windows
open index.html           # macOS

# Option 2 – serve with Python (avoids some CORS quirks)
python -m http.server 8080
# then visit http://localhost:8080
```

---

## 📁 Project Structure

```
Akshiip/
├── index.html    ← entire application (HTML + CSS + JS)
└── README.md     ← this file
```

---

## 🧩 Key Code Concepts

### localStorage persistence
```js
function save() {
  localStorage.setItem('akshiip_tasks', JSON.stringify(tasks));
}
function load() {
  tasks = JSON.parse(localStorage.getItem('akshiip_tasks')) || [];
}
```

### Inline editing (double-click)
```js
span.addEventListener('dblclick', () => startEdit(span, id));
// Sets contentEditable="true", commits on blur or Enter
```

### XSS protection
```js
function escapeHtml(str) {
  return str.replace(/&/g,'&amp;').replace(/</g,'&lt;') /* ... */;
}
```

---

## 📸 UI Overview

- **Dark glassmorphism** theme with purple accent
- **Stats bar** — live task counts at a glance
- **Animated checkbox** — green fill on completion
- **Shake animation** — red border shake on empty submit
- **Slide animations** — tasks animate in/out of the list

---

## 📄 License

MIT — free to use, modify, and deploy.
