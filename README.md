<h1 align="center">📚 Developer Handbook</h1>

<p align="center">
  <strong>Cheat sheet for modern web development.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Work%20in%20Progress-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Updated-Daily-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/PRs-Welcome-blue?style=for-the-badge" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Frontend-E34F26?style=flat-square&logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/Backend-339933?style=flat-square&logo=nodedotjs&logoColor=white" />
  <img src="https://img.shields.io/badge/Databases-4169E1?style=flat-square&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/DevOps-2496ED?style=flat-square&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/Cloud-FF9900?style=flat-square&logo=amazonwebservices&logoColor=white" />
</p>

---

## 📖 About

**Developer Handbook** is a living, personal documentation of everything I learn as a developer. It is organized into four areas, and each area has a technology checklist, quick comparisons and a place for the best resources I find.

I update it a little every day, so it keeps growing as I do.

> **Legend:** `[ ]` not started · `[x]` learned and documented

---

## 🧭 Table of Contents

| # | Section | What's inside |
|---|---|---|
| 1 | [🎨 Frontend](#frontend) | HTML, CSS, JavaScript, frameworks, tooling |
| 2 | [⚙️ Backend](#backend) | Languages, frameworks, APIs, authentication |
| 3 | [🗄️ Databases](#databases) | SQL, NoSQL, caching, ORMs |
| 4 | [☁️ DevOps & Cloud Services](#devops) | Git, Docker, CI/CD, hosting, cloud |
| 5 | [🗺️ Roadmap](#roadmap) | What's coming next |
| 6 | [🤝 Contributing](#contributing) | How to suggest changes |

---

<a id="frontend"></a>

## 🎨 Frontend

Everything that runs in the browser and shapes what users see and touch.

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=html,css,js,ts,react,vue,tailwind,bootstrap,sass,vite&perline=10" />
  </a>
</p>

### ✅ Technology Checklist

**Core**
- [x] **HTML5**: page structure and semantic markup · [Docs](https://github.com/PrashUpdates/techstack-handbook/blob/main/Frontend/Core/HTML5/docs.md) · [Cheat Sheet](https://github.com/PrashUpdates/techstack-handbook/blob/main/Frontend/Core/HTML5/cheat-sheet.md) · [Notes](https://github.com/PrashUpdates/techstack-handbook/blob/main/Frontend/Core/HTML5/notes.md)
- [ ] **CSS3**: styling, Flexbox, Grid, responsive design · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **JavaScript (ES6+)**: logic, DOM manipulation, async code · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **TypeScript**: typed JavaScript for safer, larger projects · [Docs](#) · [Cheat Sheet](#) · [Notes](#)

**Frameworks & Libraries**
- [ ] **React.js**: component-based UIs · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Vue.js**: progressive framework for interactive UIs · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Next.js**: React framework with routing and server rendering · [Docs](#) · [Cheat Sheet](#) · [Notes](#)

**Styling**
- [ ] **Tailwind CSS**: utility-first styling · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Bootstrap**: ready-made responsive components · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Sass / SCSS**: CSS with variables, nesting and mixins · [Docs](#) · [Cheat Sheet](#) · [Notes](#)

**Tooling**
- [ ] **Vite**: fast dev server and build tool · [Docs](#) · [Notes](#)
- [ ] **npm**: package management · [Docs](#) · [Notes](#)
- [ ] **Browser DevTools**: debugging, network and performance · [Docs](#) · [Notes](#)

### ⚖️ Quick Comparison: UI Frameworks

| | React | Vue | Angular |
|---|---|---|---|
| **Type** | Library | Framework | Full framework |
| **Language** | JavaScript / JSX | JavaScript / SFC | TypeScript |
| **Learning curve** | Medium | Easy | Steep |
| **Best for** | Flexible apps, large ecosystem | Quick start, small to medium apps | Large enterprise apps |

### 🔗 Essential Resources

| Resource | Link |
|---|---|
| MDN Web Docs | [click here](https://developer.mozilla.org/en-US/) |
| Official React Docs | [click here](https://react.dev/learn) |
| CSS Reference / Tricks | [click here](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) |
| Practice Projects | [click here](https://www.frontendmentor.io/challenges) |

---

<a id="backend"></a>

## ⚙️ Backend

The server side: business logic, APIs and everything users never see.

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=python,flask,django,fastapi,nodejs,express,java,spring,php,go&perline=10" />
  </a>
</p>

### ✅ Technology Checklist

**Languages**
- [ ] **Python**: readable, versatile, great for APIs and automation · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Node.js**: JavaScript on the server · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Java**: strongly typed, common in enterprise systems · [Docs](#) · [Notes](#)
- [ ] **Go**: fast, simple, good for scalable services · [Docs](#) · [Notes](#)

**Frameworks**
- [ ] **Flask**: lightweight Python micro-framework for REST APIs · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Django**: batteries-included Python framework · [Docs](#) · [Notes](#)
- [ ] **FastAPI**: modern, fast Python APIs with automatic docs · [Docs](#) · [Notes](#)
- [ ] **Express.js**: minimal Node.js web framework · [Docs](#) · [Cheat Sheet](#) · [Notes](#)

**Core Concepts**
- [ ] **REST APIs**: endpoints, HTTP methods, status codes · [Guide](#) · [Notes](#)
- [ ] **Authentication**: sessions, JWT, OAuth · [Guide](#) · [Notes](#)
- [ ] **Environment Variables**: keeping secrets and config out of code · [Guide](#) · [Notes](#)
- [ ] **CORS**: letting a frontend talk to a backend safely · [Guide](#) · [Notes](#)
- [ ] **Testing APIs**: Postman, unit and integration tests · [Guide](#) · [Notes](#)

### ⚖️ Quick Comparison: Backend Frameworks

| | Flask | Django | FastAPI | Express |
|---|---|---|---|---|
| **Language** | Python | Python | Python | JavaScript |
| **Style** | Minimal | Batteries included | Modern, async | Minimal |
| **Learning curve** | Easy | Medium | Easy to medium | Easy |
| **Best for** | Small APIs, prototypes | Full web apps, admin panels | High-performance APIs | JS-based APIs |

### 🔗 Essential Resources

| Resource | Link |
|---|---|
| Python Docs | [Add link](#) |
| Flask / Django Docs | [Add link](#) |
| HTTP Status Codes | [Add link](#) |
| REST API Design Guide | [Add link](#) |

---

<a id="databases"></a>

## 🗄️ Databases

Where data lives: storing, querying and caching it efficiently.

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=mysql,postgres,sqlite,mongodb,redis,firebase,supabase,prisma&perline=8" />
  </a>
</p>

### ✅ Technology Checklist

**Relational (SQL)**
- [ ] **SQL Basics**: SELECT, JOIN, GROUP BY, indexes · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **SQLite**: file-based database, ideal for small projects and learning · [Docs](#) · [Notes](#)
- [ ] **MySQL**: popular open-source relational database · [Docs](#) · [Notes](#)
- [ ] **PostgreSQL**: powerful, feature-rich relational database · [Docs](#) · [Notes](#)

**NoSQL**
- [ ] **MongoDB**: document database that stores JSON-like data · [Docs](#) · [Notes](#)
- [ ] **Redis**: in-memory store for caching and fast lookups · [Docs](#) · [Notes](#)

**Backend-as-a-Service & Tools**
- [ ] **Firebase**: hosted database, auth and storage · [Docs](#) · [Notes](#)
- [ ] **Supabase**: open-source Postgres-based backend platform · [Docs](#) · [Notes](#)
- [ ] **ORMs (Prisma, SQLAlchemy)**: working with databases through code · [Docs](#) · [Notes](#)

**Core Concepts**
- [ ] **Database Design**: tables, keys, relationships, normalization · [Guide](#) · [Notes](#)
- [ ] **CRUD Operations**: create, read, update, delete · [Guide](#) · [Notes](#)
- [ ] **Backups & Migrations**: changing schemas without losing data · [Guide](#) · [Notes](#)

### ⚖️ Quick Comparison: SQL vs NoSQL

| | SQL (relational) | NoSQL |
|---|---|---|
| **Data model** | Tables with rows and columns | Documents, key-value, graphs |
| **Schema** | Fixed and structured | Flexible |
| **Examples** | SQLite, MySQL, PostgreSQL | MongoDB, Redis |
| **Best for** | Structured data, relationships | Flexible or fast-changing data, caching |

### ⚖️ Quick Comparison: Popular Databases

| | SQLite | MySQL | PostgreSQL | MongoDB | Redis |
|---|---|---|---|---|---|
| **Type** | SQL | SQL | SQL | NoSQL (document) | NoSQL (key-value) |
| **Setup** | None, just a file | Needs a server | Needs a server | Needs a server | Needs a server |
| **Best for** | Learning, small apps | General web apps | Complex queries | Flexible data | Caching |

### 🔗 Essential Resources

| Resource | Link |
|---|---|
| SQL Practice Platform | [Add link](#) |
| SQLite Docs | [Add link](#) |
| MongoDB University | [Add link](#) |
| Database Design Guide | [Add link](#) |

---

<a id="devops"></a>

## ☁️ DevOps & Cloud Services

Version control, containers, deployment and the platforms that run your code.

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=git,github,githubactions,docker,kubernetes,linux,nginx,aws,gcp,azure,vercel,netlify,cloudflare&perline=13" />
  </a>
</p>

### ✅ Technology Checklist

**Version Control**
- [ ] **Git**: tracking changes, branching, merging · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **GitHub**: code hosting, pull requests, collaboration · [Docs](#) · [Notes](#)

**Automation & Containers**
- [ ] **GitHub Actions**: automated testing and deployment (CI/CD) · [Docs](#) · [Notes](#)
- [ ] **Docker**: packaging apps into containers · [Docs](#) · [Cheat Sheet](#) · [Notes](#)
- [ ] **Kubernetes**: running and scaling containers · [Docs](#) · [Notes](#)

**Servers**
- [ ] **Linux & Terminal**: essential commands, permissions, shell basics · [Cheat Sheet](#) · [Notes](#)
- [ ] **Nginx**: web server and reverse proxy · [Docs](#) · [Notes](#)

**Hosting & Cloud**
- [ ] **Cloudflare Pages**: frontend hosting · [Docs](#) · [Notes](#)
- [ ] **Render**: backend and web service hosting · [Docs](#) · [Notes](#)
- [ ] **Vercel / Netlify**: frontend hosting with easy deploys · [Docs](#) · [Notes](#)
- [ ] **AWS**: broad cloud platform (compute, storage, databases) · [Docs](#) · [Notes](#)
- [ ] **Google Cloud / Azure**: other major cloud platforms · [Docs](#) · [Notes](#)

**Core Concepts**
- [ ] **CI/CD**: automating build, test and deploy · [Guide](#) · [Notes](#)
- [ ] **Environment Management**: dev, staging and production · [Guide](#) · [Notes](#)
- [ ] **Domains, DNS & HTTPS**: how a site gets its address and security · [Guide](#) · [Notes](#)

### ⚖️ Quick Comparison: Hosting Platforms

| | Cloudflare Pages | Vercel | Netlify | Render | AWS |
|---|---|---|---|---|---|
| **Good for** | Static frontends | Frontends, Next.js | Static frontends | Backends, full apps | Everything, at scale |
| **Backend support** | Limited | Serverless functions | Serverless functions | Yes | Yes |
| **Difficulty** | Easy | Easy | Easy | Easy | Hard |

### ⚖️ Quick Comparison: Git vs GitHub

| | Git | GitHub |
|---|---|---|
| **What it is** | Version control tool | Online platform to host Git repositories |
| **Works** | On your computer | On the web |
| **Used for** | Tracking changes | Sharing, collaborating, pull requests |

### 🔗 Essential Resources

| Resource | Link |
|---|---|
| Git Cheat Sheet | [Add link](#) |
| Docker Getting Started | [Add link](#) |
| GitHub Actions Docs | [Add link](#) |
| Cloud Provider Docs | [Add link](#) |

---

<a id="roadmap"></a>

## 🗺️ Roadmap

- [ ] Add inner pages for every technology in the checklists
- [ ] Add cheat sheets for HTML, CSS, JavaScript, Git and SQL
- [ ] Add small project examples for each section
- [ ] Add a "Common Errors & Fixes" page
- [ ] Add a "Tools & Extensions" page

---

<a id="contributing"></a>

## 🤝 Contributing

Found a mistake or a great resource? Open an issue or send a pull request.

1. Fork the repository
2. Create a branch: `git checkout -b add-resource`
3. Commit your changes: `git commit -m "Add resource"`
4. Push and open a Pull Request

---

## 👨‍💻 Author

**Prashant** · [@PrashUpdates](https://github.com/PrashUpdates)

---

<p align="center">
  <strong>📚 Developer Handbook</strong>
  <br/>
  Learn a little every day. ⭐ Star the repo if it helps you.
</p>