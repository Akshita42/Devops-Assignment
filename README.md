# ✅ Tasks – To-Do List Web App
### AWS Cloud Deployment Assignment

---

## 🌐 Live Website

> **🔗 Live URL:** [http://todoapp-akshita-20260519.s3-website.ap-south-1.amazonaws.com](http://todoapp-akshita-20260519.s3-website.ap-south-1.amazonaws.com)

---

## 📌 Project Overview

A simple, interactive **To-Do List** web application developed using HTML, CSS, and vanilla JavaScript, hosted as a static website on **Amazon S3**.

This project was built as part of a cloud computing assignment to demonstrate:
- Static website development using frontend web technologies
- Cloud hosting and deployment on AWS
- Public accessibility via a live URL

---

## 🎯 Features

### Core Features
| Feature | Details |
|---|---|
| ➕ Add tasks | Input field + **Add** button |
| ✅ Complete tasks | Custom animated checkbox |
| 🗑️ Delete tasks | Per-task delete button with animation |
| 💾 Persistence | Tasks saved to **localStorage** — survive page refresh |
| 📊 Live statistics | Total / Active / Completed counters |
| 🔍 Filter system | **All · Active · Completed** tab filters |
| 🧹 Clear Completed | Remove all done tasks in one click |
| ⌨️ Keyboard support | Press **Enter** to add a task |

### Bonus Features
| Feature | Details |
|---|---|
| ✏️ Inline editing | **Double-click** any task to edit it |
| 🎨 Animations | Slide-in on add, slide-out on delete, shake on empty submit |
| 📱 Responsive | Works on mobile and desktop |
| 🔒 XSS-safe | User input is HTML-escaped before DOM insertion |

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| **HTML5** | Semantic page structure |
| **CSS3** | Styling, Flexbox layout, animations, responsive design |
| **JavaScript (ES6+)** | DOM manipulation, localStorage, event handling |
| **Font Awesome 6** | Icons via CDN |
| **Google Fonts – Inter** | Modern typography via CDN |
| **Amazon S3** | Static website hosting on AWS |

---

## 🏗️ Architecture

```
index.html                  ← single deployable file
├── <style>                 ← CSS (design tokens, layout, animations)
├── <body>                  ← semantic HTML (header, stats, input, list)
└── <script>                ← JavaScript
    ├── State               (tasks[], filter)
    ├── Persistence         (localStorage load/save)
    ├── CRUD operations     (add, toggle, delete, edit, clearCompleted)
    ├── Render functions    (renderList, updateStats)
    └── Event listeners     (click, keydown, dblclick)
```

---

## 📁 Project Structure

```
PEP-assignment/
├── index.html    ← complete web application (HTML + CSS + JS)
└── README.md     ← this file
```

---

## 🚀 AWS S3 Deployment Steps

### Step 1 — Create an S3 Bucket
```
AWS Console → S3 → Create bucket
Bucket name: todoapp-akshita-20260519  (globally unique)
Region: ap-south-1 (Mumbai)
Block all public access: UNCHECK ✓
```

### Step 2 — Enable Static Website Hosting
```
Bucket → Properties → Static website hosting → Enable
Index document: index.html
Error document: index.html
```

### Step 3 — Set Public Bucket Policy
Go to **Permissions → Bucket Policy** and add:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::todoapp-akshita-20260519/*"
    }
  ]
}
```

### Step 4 — Upload Website File
```
Bucket → Objects → Upload → Add files → select index.html → Upload
```

### Step 5 — Access the Live Website
```
Bucket → Properties → Static website hosting → Bucket website endpoint
```
Live URL:
```
http://todoapp-akshita-20260519.s3-website.ap-south-1.amazonaws.com
```

---

## 🖥️ Run Locally (for testing before deployment)

```bash
# Option 1 — open directly in browser (Windows)
start index.html

# Option 2 — serve with Python
python -m http.server 8080
# Visit: http://localhost:8080
```

---

## 📸 Deployment Screenshots

> Screenshots of the deployment process are submitted separately as part of the assignment report.

Steps captured:
1. S3 bucket creation
2. Static website hosting configuration
3. Bucket policy setup
4. File upload
5. Live website access via public URL

---

## 📄 License

MIT — free to use, modify, and deploy.
