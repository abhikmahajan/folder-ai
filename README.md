<!--
 ┌──────────────────────────────────────────────────────────────┐
 │            FOLDER.AI · A FULL-STACK AI PLATFORM             │
 │           Copyright © 2024-2025  Abhik Mahajan              │
 └──────────────────────────────────────────────────────────────┘
-->

<!-- Badges -->
![GitHub last commit](https://img.shields.io/github/last-commit/abhikmahajan/folder-ai?color=brightgreen)
![Issues](https://img.shields.io/github/issues/abhikmahajan/folder-ai)
![License](https://img.shields.io/github/license/abhikmahajan/folder-ai)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-blue)

# **Folder.AI**

Folder.AI is a modern full-stack platform that bundles powerful AI services—text generation, image manipulation, résumé review, and more—into one streamlined web application. Built with **React 19**, **Vite**, **TailwindCSS 4**, and an **Express 5** server, the project showcases best-practice architecture, type-safe APIs, and secure Clerk authentication.

> **Live demo:** <https://folder-ai-server.vercel.app>  
> **Repository:** <https://github.com/abhikmahajan/folder-ai>

---

## **Table of Contents**

- [Features](#features)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Running Locally](#running-locally)
- [API Reference](#api-reference)
- [Deployment Guide](#deployment-guide)
- [Performance Optimizations](#performance-optimizations)
- [Security Notes](#security-notes)
- [Troubleshooting & FAQ](#troubleshooting--faq)
- [Contributing](#contributing)
- [License](#license)

---

## **Features**

| Category             | Description                                                                                                               |
|----------------------|---------------------------------------------------------------------------------------------------------------------------|
| **AI Services**      | Article & blog-title generation, AI image creation, background/object removal, PDF résumé review, community sharing.      |
| **Authentication**   | Production-grade auth via **Clerk** with JWT sessions, role-based route protection, and React hooks for instant UX.       |
| **Scalable Backend** | **Express 5** with typed routes, secure environment configs, and **NeonDB** serverless PostgreSQL for effortless scaling. |
| **Cloud Storage**    | **Cloudinary** handles all uploads (images & PDFs), on-the-fly transformations, and global CDN caching.                    |
| **CI/CD**            | Zero-config GitHub→Vercel pipeline: push to `main` deploys both client & server automatically.                            |
| **Developer DX**     | Vite HMR <50 ms, Tailwind JIT, ESLint + Prettier, absolute imports, and conventional commits.                             |

---

## **Screenshots**

| Home Page | Dashboard | AI Image Generator |
|-----------|-----------|--------------------|
| ![Home](./docs/screens/home.png) | ![Dashboard](./docs/screens/dashboard.png) | ![Image](./docs/screens/image-gen.png) |

*(Add your own screenshots in `docs/screens/` to display them here.)*

---

## **Tech Stack**

### **Frontend**

| Package                        | Purpose                                |
|--------------------------------|----------------------------------------|
| React 19 + Vite                | Lightning-fast SPA development         |
| TailwindCSS 4 (Oxide engine)   | Utility-first CSS, 10× faster builds   |
| React Router DOM 7             | Nested routing & code-splitting        |
| React Hot Toast 2              | Beautiful async notifications          |
| Lucide React 0.525             | Tree-shakable icon set                 |
| React Markdown 10              | Safe markdown rendering                |

### **Backend**

| Package                          | Purpose                                     |
|----------------------------------|---------------------------------------------|
| Express 5                        | Robust routing & middleware                 |
| @clerk/express                   | Auth guard & session handling               |
| OpenAI SDK 5                     | GPT-4/3.5 text & DALL·E image endpoints     |
| Cloudinary 2                     | Media uploads, transforms, CDN cache        |
| @neondatabase/serverless 1       | Serverless PostgreSQL with pooling          |
| Multer 2                         | File uploads & validation                   |
| PDF-Parse 1                      | Extract text for résumé analysis            |
| CORS 2.8                         | Fine-grained API sharing rules              |

---

## **Project Structure**

folder-ai/
├── client/ # React + Vite SPA
│ ├── public/ # Static assets
│ ├── src/
│ │ ├── assets/ # Images, logos
│ │ ├── components/ # Reusable UI
│ │ ├── pages/ # Route components
│ │ ├── hooks/ # Custom React hooks
│ │ └── main.jsx # Entry point
│ └── vite.config.js
├── server/ # Node + Express API
│ ├── configs/ # Cloudinary, Multer
│ ├── controllers/ # Request handlers
│ ├── routes/ # API routes
│ ├── middlewares/ # Auth, errors
│ ├── server.js # App bootstrap
│ └── vercel.json # Vercel functions cfg
├── docs/ # Extra docs & assets
└── README.md # ← you are here


---

## **Getting Started**

### **Prerequisites**

- Node.js ≥ 18.17.0  
- npm or pnpm or yarn  
- Git CLI

### **Quick Start**

1 · Clone
git clone https://github.com/abhikmahajan/folder-ai.git
cd folder-ai

2 · Install backend deps
cd server && npm i

3 · Install frontend deps
cd ../client && npm i

4 · Add .env files (see next section)
5 · Run dev servers (two terminals)
Terminal A
cd server && npm run server

Terminal B
cd client && npm run dev



Open <http://localhost:5173> (Vite) and <http://localhost:3000> (API).

---

## **Environment Variables**

Create a `.env` file in **/server**:


Clerk
CLERK_PUBLISHABLE_KEY=pk_******
CLERK_SECRET_KEY=sk_******

OpenAI
OPENAI_API_KEY=sk-******

Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud
CLOUDINARY_API_KEY=123456
CLOUDINARY_API_SECRET=abc123

NeonDB
DATABASE_URL=postgresql://user:pass@host:5432/db

Server
PORT=3000


_For the frontend, Clerk keys can also live in `.env` or Vite’s `import.meta.env`._

---

## **Running Locally**

| Task               | Command                          |
|--------------------|----------------------------------|
| **Backend (dev)**  | `npm run server` (nodemon)       |
| **Frontend (dev)** | `npm run dev` (Vite)             |
| **Unit Tests**     | `npm test` (coming soon)         |
| **Lint**           | `npm run lint` (eslint + prettier) |
| **Build**          | `npm run build` (Vite + Terser)  |

---

## **API Reference**

> All endpoints are prefixed with `/api` and protected via `requireAuth()`.

| Method | Endpoint                       | Body Params                          | Description                        |
|--------|--------------------------------|--------------------------------------|------------------------------------|
| POST   | `/ai/generate-article`         | `{ topic, length }`                  | GPT article drafting               |
| POST   | `/ai/generate-blog-title`      | `{ topic }`                          | Catchy headline generation         |
| POST   | `/ai/generate-image`           | `{ prompt }`                         | DALL·E image synthesis             |
| POST   | `/ai/remove-image-background`  | `form-data: image`                   | AI background removal              |
| POST   | `/ai/remove-image-object`      | `form-data: image, objectName`       | Target object removal              |
| POST   | `/ai/resume-review`            | `form-data: pdf`                     | Résumé feedback & scoring          |

**Auth payload** is handled automatically by Clerk’s JWT, no extra tokens needed.

---

## **Deployment Guide**

### **Vercel Monorepo**

Both the `client` and `server` directories are treated as separate Vercel “projects”:


vercel/
├── client → Framework: Vite, Output: dist/
└── server → “@vercel/node” λ function


1. Push to `main`.  
2. Vercel detects `client` and runs `npm run build` → static assets.  
3. Vercel builds **server** as a serverless function via `vercel.json`.  
4. Custom rewrites in `client/vercel.json` ensure SPA routing.

### **Custom Domains**

vercel domains add folder.ai
vercel certs add folder.ai


---

## **Performance Optimizations**

- **Oxide JIT**: Tailwind 4’s Rust engine cuts CSS build time by ≈90 %.  
- **React 19** automatic batching and `use()` API for async data.  
- **Tree-shaking**: Lucide icons include only what’s imported.  
- **Serverless PG pooling**: NeonDB uses pg-bouncer automatically.  
- **HTTP/2 & gzip** out-of-the-box on Vercel’s Edge Network.

---

## **Security Notes**

| Layer       | Measure                                                               |
|-------------|-----------------------------------------------------------------------|
| **Auth**    | Clerk JWTs, rotating sessions, social login, webhook secrets.         |
| **Uploads** | Multer whitelist (`image/*, application/pdf`), 10 MB file limit.      |
| **Transport**| Enforced HTTPS, HSTS, same-site cookies, CORS allow-list.            |
| **Storage** | NeonDB encrypted at rest, Cloudinary signed URLs, least-privilege IAM.|

---

## **Troubleshooting & FAQ**

> **Q1:** _Env vars not loading?_  
> **A:** Confirm `.env` is sibling to `server.js`; restart `nodemon`.

> **Q2:** _OpenAI quota exceeded?_  
> **A:** Check usage dashboard; upgrade plan or throttle requests client-side.

> **Q3:** _Images not transforming?_  
> **A:** Verify Cloudinary “Transformations” is enabled and API key has signed URL access.

See `/docs/FAQ.md` for an extended list.

---

## **Contributing**

1. **Fork** → **Clone** → `git checkout -b feature/awesome-feature`  
2. Commit with **conventional commits** (`feat: add X, fix: Y`).  
3. **Test** and **Lint** (`npm test && npm run lint`).  
4. Push and open a **Pull Request** describing _what_ and _why_.  

All contributors must sign the CLA in the PR template.

---

## **License**

Distributed under the MIT License.  
© 2024-2025 Abhik Mahajan & contributors.

---

> _Made with ☕️, ❤️._
