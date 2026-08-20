# Learn Knowledge Base

> A structured, AI-usable knowledge base built from the 11 image files in the `Learn` folder.
> **The images are the primary source of truth.** Every section below names the image file it came from.

---

## 1. Knowledge Base Information

| Item | Detail |
|---|---|
| **Knowledge base name** | `Learn_Knowledge_Base.md` |
| **Date created** | 13–14 July 2026 |
| **Source folder** | `/Users/winter/Desktop/Web_App/Learn/` |
| **Source files** | 11 image files: `1.jpg`, `2.jpg`, `3.jpg`, `4.jpg`, `5.jpg`, `6.jpg`, `7.jpg`, `8.jpg`, `9.jpg`, `10.jpg`, `11.jpg` |
| **Expected count** | 11 — **confirmed: exactly 11 image files found**, no sub-folders, no other file types |
| **Subject of the images** | Team work-breakdown and system architecture for a 4-person AI image-generation **Web App** project (distributed across 3 PCs) |
| **Language of the images** | Mixed Thai + English (technical terms in English, explanations in Thai) |
| **Readability** | All 11 images were readable. A small number of elements are partially obscured or overlapping — every one of them is listed in **Section 15** |
| **Purpose** | Primary AI reference for future tasks about this Web App project: role assignment, API design, database design, deployment, testing, and system architecture |

### How source and AI content are separated

Throughout this document:

* **Bold "From the image"** blocks, quoted text, and all tables reproduce **exactly what is printed in the image**. Thai text is reproduced verbatim, with an English translation in brackets.
* Blocks marked **"AI explanation"** are written by AI to make the source easier to understand. They are **not** printed in the images.
* Anything unclear, unreadable, cut off, or missing is marked **`Needs further verification`** and collected in **Section 15**.

---

## 2. Overview of All 11 Source Images

| # | File name | Main topic (as printed) | Content type | Readable? |
|---|---|---|---|---|
| 1 | `1.jpg` | 📊 สรุปการแบ่งงาน 4 คน *(Summary of the work division among 4 people)* | Table | ✅ Fully readable |
| 2 | `2.jpg` | 👤 คนที่ 1 — UX/UI Frontend Developer → 📊 Workflow Diagram | Flow diagram (3 phases) | ✅ Readable (phase tab buttons overlap — see §15) |
| 3 | `3.jpg` | 🛠 Tools ที่ต้องใช้ *(Tools required)* — for Person 1, Frontend | Table (9 rows) | ✅ Fully readable |
| 4 | `4.jpg` | 👤 คนที่ 2 — Flask Backend Developer → 📊 Workflow Diagram | Flow diagram (3 phases) | ✅ Readable (phase tab buttons overlap — see §15) |
| 5 | `5.jpg` | 🛠 Tools ที่ต้องใช้ — for Person 2, Backend | Table (13 rows) | ✅ Fully readable |
| 6 | `6.jpg` | 🔌 การเชื่อมต่อ P2P ของคนที่ 2 *(Person 2's peer-to-peer connections)* + 📊 Database Schema (ER Diagram) | Sequence diagram + ER diagram | ✅ Readable |
| 7 | `7.jpg` | 👤 คนที่ 3 — AI Engineer → 📊 Workflow Diagram | Flow diagram (3 phases) | ✅ Readable (phase tab buttons overlap — see §15) |
| 8 | `8.jpg` | 🛠 Tools ที่ต้องใช้ — for Person 3, AI Engineer | Table (12 rows) | ✅ Fully readable |
| 9 | `9.jpg` | 👤 คนที่ 4 — QA / DevOps + Nginx Reverse Proxy → 📊 Workflow Diagram | Callout note + flow diagram (4 phases) | ✅ Readable (phase tab buttons overlap — see §15) |
| 10 | `10.jpg` | 🛠 Tools ที่ต้องใช้ — for Person 4, QA/DevOps | Table (14 rows) | ✅ Fully readable |
| 11 | `11.jpg` | 🔌 การเชื่อมต่อ P2P ของคนที่ 4 (DevOps View) | Network / deployment diagram | ⚠️ Readable, but one PC label is partially covered and connection lines overlap — see §15 |

**Observation (AI):** the folder's numbering is already a logical learning order — an overview first (`1.jpg`), then each team member in turn, each with *Workflow diagram → Tools table* (→ *P2P connection diagram*, where one is provided).

---

## 3. Overall Picture — What This Image Set Is About

**Source: all 11 images, primarily `1.jpg`, `6.jpg`, `9.jpg`, `11.jpg`.**

The 11 images document **one project**: a web application where a user logs in, types a text prompt, and an AI generates or edits an image. The work is split among **4 team members**, each owning one **layer** of the system and one **physical PC**:

```
                    ┌─────────────────────────────────────────────┐
                    │  Person 4 — QA / DevOps + Nginx (all PCs)   │
                    │  Testing · Deployment · Monitoring · Backup │
                    └─────────────────────────────────────────────┘
                            ▲            ▲            ▲
                            │            │            │
  Browser                   │            │            │
     │                      │            │            │
     ▼                      │            │            │
┌──────────────────┐   ┌──────────────────┐   ┌──────────────────┐
│  PC1 192.168.1.10│   │  PC2 192.168.1.20│   │  PC3 192.168.1.30│
│  Nginx :80       │──▶│  Flask :5000     │──▶│  FastAPI :7860   │
│  Frontend        │◀──│  SQLite DB       │◀──│  GPU / Stable    │
│  (Person 1)      │   │  (Person 2)      │   │  Diffusion       │
└──────────────────┘   └──────────────────┘   │  (Person 3)      │
                                              └──────────────────┘
```
*(Diagram drawn by AI to summarise `1.jpg`, `6.jpg`, `9.jpg` and `11.jpg`. It is not itself an image in the folder.)*

**Cross-reference (AI, from another source — not printed in these images):** the three IP addresses `192.168.1.10 / .20 / .30`, the Nginx reverse proxy and the Flask + Stable Diffusion stack are the same distributed system described in the course lecture slides for the **LUMA class project** (`Lecture/Lecture 4 - Point Operation.pdf`). The `Learn` images appear to be the **per-member work-breakdown documentation** for that project. The images themselves never use the name "LUMA".

---

## 4. Detailed Summary of Each Image

### 4.1 `1.jpg` — 📊 สรุปการแบ่งงาน 4 คน (Summary of the 4-person work division)

**Source: `1.jpg`**

**From the image** — one table, columns: `สมาชิก` (Member) | `หน้าที่หลัก` (Main duty) | `สิ่งที่ส่งมอบ` (Deliverables) | `PC`:

| สมาชิก (Member) | หน้าที่หลัก (Main duty) | สิ่งที่ส่งมอบ (Deliverables) | PC |
|---|---|---|---|
| **คนที่ 1** (Person 1) | UX/UI Frontend | หน้าเว็บ *(web pages)*, Bootstrap, JavaScript, API Integration | 192.168.1.10 |
| **คนที่ 2** (Person 2) | Flask Backend | Authentication, REST API, Database, Queue, Logging | 192.168.1.20 |
| **คนที่ 3** (Person 3) | AI Engineer | Image Generation, Image Editing, Model/LoRA, AI API | 192.168.1.30 |
| **คนที่ 4** (Person 4) | QA / DevOps + **Nginx** | Testing, **Nginx/Reverse Proxy**, Deployment, Dashboard, Backup, Docs | 192.168.1.10 (Nginx) + ทุก PC *(all PCs)* |

**AI explanation:** this is the master index for the whole image set. Each of the other 10 images expands one row of this table. Note that Person 4 is the only member without a PC of their own — they work **across** all three machines, and they install Nginx onto Person 1's PC.

---

### 4.2 `2.jpg` — 👤 คนที่ 1 — UX/UI Frontend Developer (Workflow Diagram)

**Source: `2.jpg`**

**From the image** — diagram title bar: `คนที่ 1 - UX/UI Frontend | PC: 192.168.1.10`. Three phases, each a left-to-right chain of boxes:

**Phase 1: Design**
1. `Wireframe / Mockup` — ออกแบบ UI ทุกหน้า *(design the UI for every page)*
2. → `Design System` — สี, Font, Component *(colours, fonts, components)*
3. → `Responsive Layout` — Desktop + Mobile

**Phase 2: Development**
1. `หน้า Login / Register` *(Login / Register page)*
2. → `หน้า Dashboard` *(Dashboard page)*
3. → `หน้า Image Generation` — Form + Preview
4. → `หน้า Image Editing` — Canvas + Tools
5. → `หน้า Gallery` — แสดงรูปทั้งหมด *(show all images)*
6. → `หน้า History / Profile`

**Phase 3: API Integration**
1. `เชื่อม Login API` → `/api/login` *(connect the Login API)*
2. → `เชื่อม Generate API` → `/api/generate`
3. → `เชื่อม Edit API` → `/api/edit`
4. → `Polling / WebSocket` — รับ Progress Update *(receive progress updates)*

**AI explanation:** the frontend is built in three stages — first design it (no code), then build the pages as static screens, then wire those screens to the real backend. The last box exists because image generation is slow: the browser cannot simply wait for the HTTP response, so it must either **poll** (ask "is it done yet?" repeatedly) or hold a **WebSocket** open to receive progress pushed from the server.

---

### 4.3 `3.jpg` — 🛠 Tools ที่ต้องใช้ (Tools required) — Person 1, Frontend

**Source: `3.jpg`**

**From the image** — table, columns: `หมวด` (Category) | `Tool` | `วัตถุประสงค์` (Purpose):

| หมวด (Category) | Tool | วัตถุประสงค์ (Purpose) |
|---|---|---|
| Editor | VS Code | เขียน HTML/CSS/JS *(write HTML/CSS/JS)* |
| Design | Figma / Canva | ออกแบบ UI Mockup *(design the UI mockup)* |
| CSS Framework | Bootstrap 5 | Responsive Layout + Components |
| JavaScript | Vanilla JS / jQuery | DOM Manipulation, Event Handling |
| API Client | Fetch API / Axios | เรียก REST API จาก Backend *(call the backend's REST API)* |
| WebSocket | Socket.IO Client | รับ real-time progress update *(receive real-time progress updates)* |
| Image Preview | Canvas API | แสดงผลภาพ, crop, rotate *(display the image, crop, rotate)* |
| Version Control | Git + GitHub | จัดการ Source Code *(manage source code)* |
| Browser Dev | Chrome DevTools | Debug, Network Monitor |

**AI explanation:** each tool maps directly onto a box in `2.jpg` — Figma/Canva serves Phase 1, Bootstrap 5 + Vanilla JS serves Phase 2, and Fetch/Axios + Socket.IO Client serves Phase 3. The Canvas API is what makes the "Image Editing — Canvas + Tools" page possible.

---

### 4.4 `4.jpg` — 👤 คนที่ 2 — Flask Backend Developer (Workflow Diagram)

**Source: `4.jpg`**

**From the image** — diagram title bar: `คนที่ 2 - Flask Backend | PC: 192.168.1.20`. Three phases:

**Phase 1: Setup**
1. `ติดตั้ง Python + Flask` *(install Python + Flask)*
2. → `สร้าง Virtual Environment` *(create a virtual environment)*
3. → `ออกแบบ Database Schema` *(design the database schema)*
4. → `สร้าง SQLite Database` *(create the SQLite database)*

**Phase 2: API Development** — four API groups, each printed as one box:

| Box | Endpoints (exactly as printed) |
|---|---|
| **Auth API** | `POST /api/register` · `POST /api/login` · `POST /api/logout` |
| **Image API** | `POST /api/generate` · `POST /api/edit` · `GET /api/images` |
| **User API** | `GET /api/profile` · `PUT /api/profile` · `GET /api/history` |
| **Task API** | `GET /api/task/:id` · `POST /api/callback` |

**Phase 3: Security & Logging**
1. `JWT Authentication`
2. → `Input Validation` — ป้องกัน SQL Injection *(prevent SQL injection)*
3. → `Rate Limiting`
4. → `Logging System` — บันทึกทุก Request *(log every request)*

**AI explanation:** the backend is the hub of the system — it is the only component that talks to both the browser and the AI server. `POST /api/callback` is unusual and important: it is **not** called by the browser, it is called **by the AI server** when a picture is finished (see `6.jpg`). `GET /api/task/:id` is the endpoint the browser polls while it waits.

---

### 4.5 `5.jpg` — 🛠 Tools ที่ต้องใช้ — Person 2, Backend

**Source: `5.jpg`**

**From the image:**

| หมวด (Category) | Tool | วัตถุประสงค์ (Purpose) |
|---|---|---|
| Language | Python 3.10+ | ภาษาหลัก *(main language)* |
| Framework | Flask 3.x | Web Framework |
| Database | SQLite3 | เก็บข้อมูล User, Image, Task *(store User, Image, Task data)* |
| ORM | Flask-SQLAlchemy | จัดการ Database ผ่าน Python Object *(manage the DB through Python objects)* |
| Auth | Flask-JWT-Extended | JWT Token Authentication |
| Validation | Marshmallow / Flask-WTF | Input Validation |
| CORS | Flask-CORS | อนุญาต Cross-Origin จาก Frontend *(allow cross-origin requests from the frontend)* |
| HTTP Client | requests (Python) | ส่ง Request ไป AI Server *(send requests to the AI server)* |
| Logging | Python logging module | บันทึก Log ระบบ *(record system logs)* |
| API Testing | Postman / Thunder Client | ทดสอบ API ระหว่างพัฒนา *(test the API during development)* |
| Editor | VS Code + Python Extension | เขียนโค้ด *(write code)* |
| Version Control | Git + GitHub | จัดการ Source Code |
| Process Manager | Waitress (Windows) / Gunicorn (Linux) | Production Server |

**AI explanation:** the last row matters in practice — Flask's built-in development server (`app.run()`) is not meant for production, so a WSGI server (Waitress on Windows, Gunicorn on Linux) is used instead when the app is deployed. `requests` appears here because the backend acts as an **HTTP client** to the AI server, not only as a server to the browser.

---

### 4.6 `6.jpg` — 🔌 การเชื่อมต่อ P2P ของคนที่ 2 + 📊 Database Schema (ER Diagram)

**Source: `6.jpg`** — this image contains **two** diagrams.

#### (a) Sequence diagram — "การเชื่อมต่อ P2P ของคนที่ 2" *(Person 2's peer-to-peer connections)*

**From the image** — four participants across the top:

| Participant | Address as printed |
|---|---|
| ❎ **Nginx** | `192.168.1.10:80` |
| ⚙ **Flask Backend** | `192.168.1.20:5000` |
| 🗄 **SQLite** | `192.168.1.20 (local file)` |
| 🤖 **AI Server** | `192.168.1.30:7860` |

**From the image** — the message sequence, in order (solid arrow = request, dashed arrow = response):

| # | From → To | Message (exactly as printed) |
|---|---|---|
| 1 | Nginx → Flask Backend | `POST /api/generate {"prompt": "a cute cat"}` |
| 2 | Flask Backend → SQLite | `INSERT INTO tasks (status='pending')` |
| 3 | Flask Backend → AI Server | `POST http://192.168.1.30:7860/ai/generate` `{"prompt": "a cute cat", "task_id": "abc123"}` |
| 4 | AI Server ⇢ Flask Backend | `{"status": "accepted", "task_id": "abc123"}` |
| 5 | Flask Backend ⇢ Nginx | `{"task_id": "abc123", "status": "queued"}` |
| 6 | *(note over AI Server)* | `🤖 AI กำลังสร้างรูป (30-60 วินาที)...` *(AI is generating the image (30–60 seconds)…)* |
| 7 | AI Server → Flask Backend | `POST http://192.168.1.20:5000/api/callback` `{"task_id": "abc123", "image_base64": "...", "status": "done"}` |
| 8 | Flask Backend → SQLite | `UPDATE tasks SET status='completed'` `INSERT INTO images (filepath, prompt, ...)` |
| 9 | Nginx → Flask Backend | `GET /api/task/abc123 (Frontend polling)` |
| 10 | Flask Backend → SQLite | `SELECT * FROM tasks WHERE id='abc123'` |
| 11 | SQLite ⇢ Flask Backend | `{status: 'completed', image_url: '/uploads/abc123.png'}` |
| 12 | Flask Backend ⇢ Nginx | `{"status": "completed", "image_url": "/uploads/abc123.png"}` |

> The `"image_base64": "..."` ellipsis in step 7 is printed in the image itself — the real value is a long base64 string that the diagram abbreviates.

**AI explanation — why the flow is shaped like this:** generating an image takes 30–60 seconds, which is far too long for one HTTP request to stay open. So the backend **accepts the job and returns immediately** (`status: "queued"`, steps 4–5). The AI server works in the background, then *calls the backend back* (`/api/callback`, step 7) when it's finished. Meanwhile the browser keeps asking `GET /api/task/abc123` (step 9) until the status flips to `completed`. This pattern is called an **asynchronous job queue with a callback**.

#### (b) Database Schema (ER Diagram)

**From the image** — three tables:

**`USERS`**

| Key | Type | Field |
|---|---|---|
| PK | int | `id` |
| UK | string | `username` |
| UK | string | `email` |
|  | string | `password_hash` |
|  | string | `avatar_url` |
|  | datetime | `created_at` |
|  | datetime | `updated_at` |

**`IMAGES`**

| Key | Type | Field |
|---|---|---|
| PK | int | `id` |
| FK | int | `user_id` |
|  | string | `filename` |
|  | string | `filepath` |
|  | string | `prompt` |
|  | string | `model_used` |
|  | string | `status` |
|  | datetime | `created_at` |

**`TASKS`**

| Key | Type | Field |
|---|---|---|
| PK | int | `id` |
| UK | string | `task_id` |
| FK | int | `user_id` |
| FK | int | `image_id` |
|  | string | `task_type` |
|  | string | `status` |
|  | text | `params_json` |
|  | datetime | `created_at` |
|  | datetime | `completed_at` |

**From the image** — the three relationship labels drawn between the tables:

| Relationship | Label printed on the line |
|---|---|
| `USERS` → `IMAGES` | `creates` |
| `IMAGES` → `TASKS` | `generated_by` |
| `USERS` → `TASKS` | `submits` |

All three are drawn one-to-many (a single "one" bar on the `USERS` / `IMAGES` side, a crow's foot on the many side).

**AI explanation:** `USERS.id` is the owner of everything. `IMAGES` stores the finished picture (its `filepath` is what gets returned as `image_url`). `TASKS` is the job ticket: it holds the public `task_id` (e.g. `"abc123"` from the sequence diagram), the `status` the browser polls, `params_json` for the generation settings, and `image_id` which is filled in once the image exists. Note that `password_hash` — not a plain password — is what is stored, and that `task_id` is a separate **UK** (unique key) string, distinct from the integer primary key, so it can be exposed publicly in URLs without leaking row counts.

---

### 4.7 `7.jpg` — 👤 คนที่ 3 — AI Engineer (Workflow Diagram)

**Source: `7.jpg`**

**From the image** — diagram title bar: `คนที่ 3 - AI Engineer | PC: 192.168.1.30`. Three phases:

**Phase 1: Model Setup**
1. `ติดตั้ง CUDA + cuDNN` *(install CUDA + cuDNN)*
2. → `ติดตั้ง PyTorch` *(install PyTorch)*
3. → `Download Base Model` — Stable Diffusion (Forge)
4. → `Download LoRA Models` — สำหรับ Style ต่างๆ *(for various styles)*
5. → `ทดสอบ Inference` — สร้างรูปทดสอบ *(test inference — generate a test image)*

**Phase 2: AI API Service**

| Box | As printed |
|---|---|
| `สร้าง API Server` | FastAPI on port 7860 *(create the API server)* |
| `POST /ai/generate` | txt2img - สร้างรูปจาก Prompt *(generate an image from a prompt)* |
| `POST /ai/edit` | img2img - แก้ไขรูป *(edit an image)* |
| `POST /ai/inpaint` | Inpaint - ลบ/เพิ่มส่วนของรูป *(remove/add parts of an image)* |
| `GET /ai/models` | ดูรายชื่อ Model ทั้งหมด *(list all models)* |

**Phase 3: Queue & Optimization**
1. `Request Queue` — จัดคิวงานไม่ให้ GPU ล่ม *(queue the jobs so the GPU doesn't crash)*
2. → `VRAM Management` — จัดการหน่วยความจำ GPU *(manage GPU memory)*
3. → `Callback to Backend` — ส่งผลลัพธ์กลับ 192.168.1.20 *(send the result back to 192.168.1.20)*
4. → `Error Handling` — Retry + Fallback

**AI explanation:** the AI PC is the only machine with a GPU, and a GPU can only render one image at a time. That is why Phase 3 exists: the **request queue** serialises incoming jobs so that two simultaneous requests don't try to allocate VRAM at once and crash the process. The `Callback to Backend` box is the *other end* of step 7 in `6.jpg` — the same message, drawn from the AI engineer's point of view.

---

### 4.8 `8.jpg` — 🛠 Tools ที่ต้องใช้ — Person 3, AI Engineer

**Source: `8.jpg`**

**From the image:**

| หมวด (Category) | Tool | วัตถุประสงค์ (Purpose) |
|---|---|---|
| Language | Python 3.10+ | ภาษาหลัก *(main language)* |
| AI Framework | PyTorch 2.x | Deep Learning Framework |
| GPU Driver | CUDA 11.8+ / cuDNN | GPU Acceleration |
| Image Gen | Stable Diffusion WebUI Forge | Image Generation Engine |
| Model Format | Safetensors | Model Weight Files |
| LoRA | LoRA / LoHa adapters | Fine-tuned Style (anime, realistic, etc.) |
| API Server | FastAPI + Uvicorn | Serve AI เป็น REST API *(serve the AI as a REST API)* |
| Image Processing | Pillow (PIL) | Resize, Crop, Format Convert |
| HTTP Client | requests / httpx | Callback กลับ Backend *(callback to the backend)* |
| GPU Monitor | nvidia-smi / GPUtil | Monitor VRAM Usage |
| Editor | VS Code + Jupyter Notebook | เขียนโค้ด + ทดลอง Model *(write code + experiment with models)* |
| Version Control | Git + Git LFS | จัดการ Source + Model Files ขนาดใหญ่ *(manage source + large model files)* |

**AI explanation:** two entries here are easy to miss but are the reason this role is separate from the backend role. **Git LFS** (Large File Storage) is listed instead of plain Git because model weight files are hundreds of megabytes to several gigabytes — ordinary Git cannot handle them well. And **`requests` / `httpx`** appear again (as in `5.jpg`), because the AI server must itself act as an HTTP *client* in order to fire the callback.

---

### 4.9 `9.jpg` — 👤 คนที่ 4 — QA / DevOps + Nginx Reverse Proxy (Workflow Diagram)

**Source: `9.jpg`**

**From the image** — a callout box at the top, labelled **IMPORTANT**:

> คนที่ 4 รับงาน **Nginx / Reverse Proxy** จากคนที่ 5 เพิ่มเติม เพราะเป็นงาน Infrastructure ที่เกี่ยวข้องกับ Deployment โดยตรง
>
> *(Person 4 additionally takes over the **Nginx / Reverse Proxy** work from Person 5, because it is infrastructure work directly related to deployment.)*

**From the image** — diagram title bar: `คนที่ 4 - QA/DevOps + Nginx | ทุก PC` *(all PCs)*. **Four** phases (this is the only role with four):

**Phase 1: Nginx + Network (งานจากคนที่ 5)** *(work from Person 5)*
1. `ติดตั้ง Nginx` — บน PC1 (192.168.1.10) *(install Nginx on PC1)*
2. → `Config Reverse Proxy` — `/api/*` → `192.168.1.20:5000` and `/ai/*` → `192.168.1.30:7860`
3. → `ตั้งค่า Firewall` — เปิด Port ที่จำเป็น *(configure the firewall — open the necessary ports)*
4. → `Gzip + Caching Optimization`

**Phase 2: Testing**
1. `เขียน Test Cases` — ครอบคลุมทุก API *(write test cases covering every API)*
2. → `Unit Test - Backend API`
3. → `Integration Test` — Frontend ↔ Backend ↔ AI
4. → `Load Test` — ทดสอบ Performance *(test performance)*

**Phase 3: Deployment**
1. `เขียน Deploy Script` — สำหรับแต่ละ PC *(write a deploy script for each PC)*
2. → `Deploy Frontend → PC1`
3. → `Deploy Backend → PC2`
4. → `Deploy AI Server → PC3`

**Phase 4: Monitor + Docs**
1. `Monitoring Dashboard` — Health Check ทุก PC *(health-check every PC)*
2. → `Backup Strategy` — Database + รูปภาพ *(database + images)*
3. → `คู่มือผู้ใช้งาน` — User Manual *(user manual)*
4. → `คู่มือ Deploy` — Admin Manual *(deployment manual)*

**AI explanation — the reverse-proxy mapping is the single most important line in this image.** Because Nginx maps `/api/*` to the Flask PC and `/ai/*` to the AI PC, the browser only ever needs to know **one** address (`192.168.1.10:80`). It never contacts `192.168.1.20` or `192.168.1.30` directly. This is exactly why, in the sequence diagram of `6.jpg`, the first arrow comes *from Nginx* rather than from the browser.

---

### 4.10 `10.jpg` — 🛠 Tools ที่ต้องใช้ — Person 4, QA/DevOps

**Source: `10.jpg`**

**From the image:**

| หมวด (Category) | Tool | วัตถุประสงค์ (Purpose) |
|---|---|---|
| Web Server | Nginx | Reverse Proxy + Static File Serving |
| SSL | OpenSSL | สร้าง Self-signed Certificate (optional) *(create a self-signed certificate)* |
| Testing | pytest | Unit/Integration Test สำหรับ Python |
| API Testing | Postman / Newman (CLI) | ทดสอบ API ทุก Endpoint *(test every API endpoint)* |
| Load Testing | Locust | ทดสอบ Performance / Concurrent Users |
| Browser Test | Selenium / Playwright | UI Automation Test (optional) |
| SSH Client | OpenSSH / PuTTY | Remote Access ทุก PC *(remote access to every PC)* |
| Deploy | Shell Scripts (Bash/PowerShell) | Automate Deployment |
| Backup | rsync / robocopy | Backup Database + Images |
| Monitoring | Custom HTML Dashboard + cron | Monitor Health ทุก Service *(monitor the health of every service)* |
| Network | curl / ping / netstat | ทดสอบ Connection ระหว่าง PC *(test connections between PCs)* |
| Docs | Markdown | เขียนคู่มือ *(write manuals)* |
| Diagrams | draw.io / Mermaid | System Architecture Diagrams |
| Version Control | Git + GitHub | จัดการ Source Code |

**AI explanation:** this is the longest tool list of the four because Person 4's job spans every machine. Note the pairing of cross-platform alternatives (`rsync`/`robocopy`, `Bash`/`PowerShell`, `Gunicorn`/`Waitress` in `5.jpg`) — the images assume the team may be running a mix of Linux and Windows PCs.

---

### 4.11 `11.jpg` — 🔌 การเชื่อมต่อ P2P ของคนที่ 4 (DevOps View)

**Source: `11.jpg`**

**From the image** — a box labelled `คนที่ 4 - QA/DevOps` at the top, containing five tool nodes:

| Node | Icon |
|---|---|
| `Nginx Config` | ❎ |
| `Deploy Scripts` | 🚀 |
| `Test Runner` | 🧪 |
| `Health Monitor` | 📊 |
| `Backup` | 💾 |

**From the image** — three target PC boxes at the bottom:

| PC box (as printed) | Contains |
|---|---|
| `PC1 - Frontend + Nginx (192...` *(IP text partially covered — see §15)* | `Static Files`, `Nginx :80` |
| `PC2 - Backend + DB (192.168.1.20)` | `Flask :5000`, `SQLite DB` |
| `PC3 - AI Server (192.168.1.30)` | `FastAPI :7860`, `GPU` |

**From the image** — the connection labels printed on the lines between them:

| Connection label (as printed) | Meaning of the Thai text |
|---|---|
| `SSH :22` — ติดตั้ง + config Nginx | install + configure Nginx |
| `SSH :22 + SCP` — อัพ HTML/CSS/JS | upload HTML/CSS/JS |
| `SSH :22 + SCP` — อัพ Python code + pip install | upload Python code + pip install |
| `SSH :22 + SCP` — อัพ AI code + models | upload AI code + models |
| `HTTP :80` — UI Test | — |
| `HTTP :5000` — API Test | — |
| `HTTP :7860` — AI API Test | — |
| `GET /health` | — |
| `GET /api/health` | — |
| `GET /ai/health` | — |
| `SSH + rsync` | — |

**AI explanation (inferred — the lines in the image overlap, so the exact node-to-line routing is `Needs further verification`):** reading the labels together with the five tool nodes, the intended mapping is almost certainly:

* **Nginx Config** → PC1 over `SSH :22` (install and configure Nginx).
* **Deploy Scripts** → all three PCs over `SSH :22 + SCP` (upload HTML/CSS/JS to PC1, Python code to PC2, AI code + models to PC3).
* **Test Runner** → all three PCs over HTTP (`:80` UI test, `:5000` API test, `:7860` AI API test).
* **Health Monitor** → all three PCs via `GET /health`, `GET /api/health`, `GET /ai/health`.
* **Backup** → PC2 via `SSH + rsync` (that is the PC holding the SQLite DB and the saved images).

The key insight of this image: **Person 4 reaches every machine two different ways** — over **SSH/SCP** to *push files and configuration in*, and over **HTTP** to *check from the outside that the service is alive and correct*. Those are the two halves of DevOps: deployment and observation.

---

## 5. Important Concepts and Terminology

**Sources are named in the right-hand column. All terms below appear in the images; the "plain-language meaning" column is AI-written explanation.**

| Term | Plain-language meaning (AI) | Appears in |
|---|---|---|
| **Reverse Proxy** | One public front door. Nginx receives every request and forwards it to the right internal PC, so the browser only knows one address. | `1.jpg`, `9.jpg`, `10.jpg`, `11.jpg` |
| **Nginx** | The web server used as that front door; also serves the static files (HTML/CSS/JS). | `1.jpg`, `6.jpg`, `9.jpg`, `10.jpg`, `11.jpg` |
| **REST API** | The set of HTTP endpoints (`POST /api/generate`, …) the frontend calls. | `1.jpg`, `3.jpg`, `4.jpg`, `8.jpg` |
| **Endpoint** | One specific URL + HTTP method pair, e.g. `POST /api/login`. | `2.jpg`, `4.jpg`, `7.jpg`, `10.jpg` |
| **JWT (JSON Web Token)** | A signed token the server issues at login; the browser sends it back on every later request to prove who it is. | `4.jpg`, `5.jpg` |
| **Authentication** | Checking *who* the user is (login/register/logout). | `1.jpg`, `4.jpg`, `5.jpg` |
| **Input Validation** | Checking incoming data before using it — here specifically to stop **SQL Injection**. | `4.jpg`, `5.jpg` |
| **SQL Injection** | An attack where hostile text in a form field is executed as database commands. | `4.jpg` |
| **Rate Limiting** | Capping how many requests one client may send, so nobody can flood the server. | `4.jpg` |
| **CORS** | The browser rule that blocks a page from calling a different origin; `Flask-CORS` opts in to allow it. | `5.jpg` |
| **ORM** | A layer (Flask-SQLAlchemy) that lets you treat database rows as Python objects instead of writing raw SQL. | `5.jpg` |
| **Queue** | A waiting line for jobs, so the single GPU only handles one at a time. | `1.jpg`, `7.jpg` |
| **Polling** | The browser repeatedly asking `GET /api/task/:id` "is it done yet?". | `2.jpg`, `6.jpg` |
| **WebSocket / Socket.IO** | A connection held open so the server can *push* progress to the browser instead of being asked. | `2.jpg`, `3.jpg` |
| **Callback** | The AI server calling the backend back (`POST /api/callback`) when the slow job finishes. | `4.jpg`, `6.jpg`, `7.jpg` |
| **txt2img** | Generating a new image from a text prompt. | `7.jpg` |
| **img2img** | Producing a new image from an existing image (editing). | `7.jpg` |
| **Inpaint** | Removing or adding *part* of an image while keeping the rest. | `7.jpg` |
| **LoRA / LoHa** | Small add-on files that adapt the base model to a particular style, without retraining the whole model. | `1.jpg`, `7.jpg`, `8.jpg` |
| **Base Model / Checkpoint** | The large pre-trained Stable Diffusion model (here served through **Forge**). | `7.jpg`, `8.jpg` |
| **Safetensors** | The file format used for model weights. | `8.jpg` |
| **VRAM** | The GPU's own memory — the scarce resource that Phase 3 of `7.jpg` exists to protect. | `7.jpg`, `8.jpg` |
| **CUDA / cuDNN** | NVIDIA's libraries that let PyTorch run on the GPU. | `7.jpg`, `8.jpg` |
| **Unit Test / Integration Test / Load Test** | Test one function · test the whole chain Frontend↔Backend↔AI · test the system under many concurrent users. | `9.jpg`, `10.jpg` |
| **Virtual Environment** | An isolated Python installation per project, so dependencies don't collide. | `4.jpg` |
| **Git LFS** | Git extension for very large files (the model weights). | `8.jpg` |
| **SSH / SCP / rsync** | Remote login · copy files to a remote PC · efficiently sync/back up files. | `10.jpg`, `11.jpg` |
| **Health Check** | A cheap endpoint (`/health`) that answers "am I alive?" for the monitoring dashboard. | `9.jpg`, `11.jpg` |

---

## 6. Formulas and Calculation Methods

**Source: all 11 images.**

**There are no mathematical formulas, equations, or calculations in any of the 11 images.** These images are architecture and planning documents, not technical/theoretical slides. Nothing in this section is invented — inventing a formula here would be a fabrication.

What the images *do* contain is a set of **fixed numeric values** that must be memorised exactly, because the whole system is wired around them:

| Value | What it is | Source image(s) |
|---|---|---|
| `192.168.1.10` | PC1 — Frontend + Nginx | `1.jpg`, `6.jpg`, `9.jpg`, `11.jpg` |
| `192.168.1.20` | PC2 — Flask Backend + SQLite DB | `1.jpg`, `6.jpg`, `7.jpg`, `9.jpg`, `11.jpg` |
| `192.168.1.30` | PC3 — AI Server (GPU) | `1.jpg`, `6.jpg`, `9.jpg`, `11.jpg` |
| Port `80` | Nginx (HTTP) | `6.jpg`, `11.jpg` |
| Port `5000` | Flask backend | `6.jpg`, `9.jpg`, `11.jpg` |
| Port `7860` | AI server (FastAPI) | `6.jpg`, `7.jpg`, `9.jpg`, `11.jpg` |
| Port `22` | SSH (used by DevOps for deployment) | `11.jpg` |
| **30–60 seconds** | How long the AI takes to generate one image | `6.jpg` |
| Python `3.10+` | Required Python version (backend and AI) | `5.jpg`, `8.jpg` |
| Flask `3.x`, PyTorch `2.x`, CUDA `11.8+`, Bootstrap `5` | Required tool versions | `3.jpg`, `5.jpg`, `8.jpg` |

**AI explanation of the one "calculation" that matters:** the 30–60 second figure in `6.jpg` is what *forces* the entire asynchronous design. A normal HTTP request is expected to answer in well under a second; anything holding a connection open for a minute risks a proxy or browser timeout. That single number is the reason the system needs a task queue, a callback and polling instead of one simple request/response.

---

## 7. Code Explanations

**Source: `4.jpg`, `6.jpg`, `7.jpg`, `9.jpg`, `11.jpg`.**

**No program source code (no Python, JavaScript, or HTML listings) appears in any of the 11 images.** What *does* appear is **code-like content**: API signatures, JSON messages, SQL statements and a proxy configuration mapping. Every item below is transcribed exactly as printed, then explained.

### 7.1 API endpoints — the backend (`4.jpg`)

```
Auth API      POST /api/register     POST /api/login     POST /api/logout
Image API     POST /api/generate     POST /api/edit      GET  /api/images
User API      GET  /api/profile      PUT  /api/profile   GET  /api/history
Task API      GET  /api/task/:id     POST /api/callback
```

**AI explanation:** `:id` is a **route parameter** — a placeholder filled in at call time, e.g. `GET /api/task/abc123`. The HTTP verbs follow REST convention: `POST` = create/do something, `GET` = read, `PUT` = update.

### 7.2 API endpoints — the AI server (`7.jpg`)

```
FastAPI on port 7860
POST /ai/generate     txt2img  - สร้างรูปจาก Prompt
POST /ai/edit         img2img  - แก้ไขรูป
POST /ai/inpaint      Inpaint  - ลบ/เพิ่มส่วนของรูป
GET  /ai/models                - ดูรายชื่อ Model ทั้งหมด
```

**AI explanation:** note the deliberate `/ai/*` prefix. It exists so that Nginx can route on the path alone (see 7.4) without inspecting the request body.

### 7.3 JSON messages (`6.jpg`)

```jsonc
// 1. Browser → Backend, via Nginx
POST /api/generate      {"prompt": "a cute cat"}

// 2. Backend → AI server
POST http://192.168.1.30:7860/ai/generate
                        {"prompt": "a cute cat", "task_id": "abc123"}

// 3. AI server accepts the job immediately
                        {"status": "accepted", "task_id": "abc123"}

// 4. Backend answers the browser immediately — the picture is NOT ready yet
                        {"task_id": "abc123", "status": "queued"}

// 5. 30–60 s later: AI server calls the backend BACK
POST http://192.168.1.20:5000/api/callback
                        {"task_id": "abc123", "image_base64": "...", "status": "done"}

// 6. Browser polls; once ready the backend answers
GET /api/task/abc123    {"status": "completed", "image_url": "/uploads/abc123.png"}
```

**AI explanation:** `task_id` (`"abc123"`) is the thread that ties all six messages together. The image travels back from the GPU as **base64** text inside JSON (`image_base64`), and the backend saves it to disk and hands the browser a plain **URL** (`image_url`) instead — a much cheaper thing for the browser to fetch and cache.

### 7.4 Nginx reverse-proxy configuration (`9.jpg`)

```
/api/*  →  192.168.1.20:5000
/ai/*   →  192.168.1.30:7860
```

**AI explanation:** a path-prefix rule. Any URL starting `/api/` is forwarded to the Flask PC; anything starting `/ai/` goes to the AI PC. Everything else is served by Nginx itself as static files (`Static Files` node in `11.jpg`).

### 7.5 SQL statements (`6.jpg`)

```sql
INSERT INTO tasks (status='pending')                  -- when the job arrives
UPDATE tasks SET status='completed'                   -- when the callback arrives
INSERT INTO images (filepath, prompt, ...)            -- save the finished picture
SELECT * FROM tasks WHERE id='abc123'                 -- when the browser polls
```

> Transcribed exactly as printed in `6.jpg`. **Note (AI, flagged — not a correction to the source):** `INSERT INTO tasks (status='pending')` is not valid SQL syntax as written (valid SQL would be `INSERT INTO tasks (status) VALUES ('pending')`), and `SELECT * FROM tasks WHERE id='abc123'` compares the *integer* `id` column against a string, whereas the schema in the same image stores `'abc123'` in the `task_id` column. These are almost certainly shorthand for a diagram rather than real errors in the design. Recorded here as a concern only — see §15. `Needs further verification`

### 7.6 Health-check endpoints (`11.jpg`)

```
GET /health          → PC1 (Nginx)
GET /api/health      → PC2 (Flask)
GET /ai/health       → PC3 (FastAPI)
```

**AI explanation:** these three are used by the monitoring dashboard, not by the app. Note they do **not** appear in the API lists of `4.jpg` or `7.jpg` — see §15.

---

## 8. Important Tables and Diagrams

| Diagram / Table | What it is | Source |
|---|---|---|
| **Work-division table** | The 4 members, their duties, deliverables and PCs — the index to the whole set | `1.jpg` |
| **Frontend workflow** | 3 phases: Design → Development → API Integration | `2.jpg` |
| **Frontend tools table** | 9 rows | `3.jpg` |
| **Backend workflow** | 3 phases: Setup → API Development → Security & Logging | `4.jpg` |
| **Backend tools table** | 13 rows | `5.jpg` |
| **P2P sequence diagram** | The complete 12-step life of one image-generation request | `6.jpg` |
| **ER diagram** | `USERS`, `IMAGES`, `TASKS` and their relationships | `6.jpg` |
| **AI workflow** | 3 phases: Model Setup → AI API Service → Queue & Optimization | `7.jpg` |
| **AI tools table** | 12 rows | `8.jpg` |
| **QA/DevOps workflow** | 4 phases: Nginx+Network → Testing → Deployment → Monitor+Docs | `9.jpg` |
| **QA/DevOps tools table** | 14 rows | `10.jpg` |
| **DevOps network view** | 5 DevOps tools × 3 PCs, over SSH/SCP and HTTP | `11.jpg` |

**The two most important diagrams to know by heart** *(AI judgement)*: the **sequence diagram in `6.jpg`** (it explains *how the system works*) and the **reverse-proxy mapping in `9.jpg`** (it explains *how the three PCs become one website*).

---

## 9. Step-by-Step Procedures

Each procedure below is transcribed from the phase chain of one workflow image. The order is the order the arrows point in.

### 9.1 Frontend — Person 1 · Source: `2.jpg`

1. **Design** — Wireframe/Mockup for every page → build a Design System (colours, fonts, components) → make the layout responsive (Desktop + Mobile).
2. **Development** — build the pages in this order: Login/Register → Dashboard → Image Generation (Form + Preview) → Image Editing (Canvas + Tools) → Gallery → History/Profile.
3. **API Integration** — connect the Login API (`/api/login`) → the Generate API (`/api/generate`) → the Edit API (`/api/edit`) → add Polling/WebSocket for progress updates.

### 9.2 Backend — Person 2 · Source: `4.jpg`

1. **Setup** — install Python + Flask → create a virtual environment → design the database schema → create the SQLite database.
2. **API Development** — build the Auth API → the Image API → the User API → the Task API *(endpoints listed in §4.4)*.
3. **Security & Logging** — JWT authentication → input validation (prevent SQL injection) → rate limiting → a logging system that records every request.

### 9.3 AI Engineer — Person 3 · Source: `7.jpg`

1. **Model Setup** — install CUDA + cuDNN → install PyTorch → download the base model (Stable Diffusion / Forge) → download LoRA models for the styles you need → test inference by generating a test image.
2. **AI API Service** — stand up a FastAPI server on port 7860 → expose `POST /ai/generate` (txt2img) → `POST /ai/edit` (img2img) → `POST /ai/inpaint` → `GET /ai/models`.
3. **Queue & Optimization** — add a request queue so the GPU doesn't crash → manage VRAM → send results back to the backend at `192.168.1.20` via callback → handle errors with retry + fallback.

### 9.4 QA / DevOps — Person 4 · Source: `9.jpg`

1. **Nginx + Network** *(work inherited from Person 5)* — install Nginx on PC1 (192.168.1.10) → configure the reverse proxy (`/api/*` → `192.168.1.20:5000`, `/ai/*` → `192.168.1.30:7860`) → configure the firewall, opening only the necessary ports → enable Gzip + caching.
2. **Testing** — write test cases covering every API → unit-test the backend API → integration-test the whole chain Frontend ↔ Backend ↔ AI → load-test for performance.
3. **Deployment** — write a deploy script for each PC → deploy Frontend to PC1 → Backend to PC2 → AI Server to PC3.
4. **Monitor + Docs** — build a monitoring dashboard that health-checks every PC → define a backup strategy (database + images) → write the User Manual → write the Admin/Deploy Manual.

### 9.5 The end-to-end request procedure · Source: `6.jpg`

The single most important sequence in the whole image set — what happens when a user clicks "Generate":

1. Browser sends `POST /api/generate {"prompt": "a cute cat"}`; **Nginx** forwards it to Flask.
2. Flask writes a row: `INSERT INTO tasks (status='pending')`.
3. Flask forwards the job to the AI server: `POST http://192.168.1.30:7860/ai/generate {"prompt": ..., "task_id": "abc123"}`.
4. AI server replies immediately: `{"status": "accepted", "task_id": "abc123"}`.
5. Flask replies immediately to the browser: `{"task_id": "abc123", "status": "queued"}`. **The user now has a task ID, but no picture.**
6. The AI works for **30–60 seconds**.
7. AI server calls back: `POST http://192.168.1.20:5000/api/callback {"task_id": "abc123", "image_base64": "...", "status": "done"}`.
8. Flask saves it: `UPDATE tasks SET status='completed'` and `INSERT INTO images (filepath, prompt, ...)`.
9. Meanwhile the browser has been polling: `GET /api/task/abc123`.
10. Flask looks it up: `SELECT * FROM tasks WHERE id='abc123'`.
11. SQLite returns `{status: 'completed', image_url: '/uploads/abc123.png'}`.
12. Flask returns `{"status": "completed", "image_url": "/uploads/abc123.png"}` — the browser now displays the picture.

---

## 10. Important Examples

**Source: `6.jpg`** — the images contain exactly **one** fully worked example, and it runs through the whole sequence diagram:

| Element | Value in the example |
|---|---|
| The prompt | `"a cute cat"` |
| The task ID | `"abc123"` |
| Time to generate | 30–60 seconds |
| Intermediate status values | `pending` → `queued` → `accepted` → `done` → `completed` |
| The final image path | `/uploads/abc123.png` |
| The final response | `{"status": "completed", "image_url": "/uploads/abc123.png"}` |

**AI explanation — read the status values carefully, they are the example's real lesson:** the *same job* is described by different words at different points because different components own it. `pending` is what the **database** row says the moment it is created; `accepted` is what the **AI server** says when it takes the job; `queued` is what the **browser** is told; `done` is what the **AI server** reports on the callback; `completed` is the final **database** state the browser eventually sees. When implementing this, these strings must be defined once and used consistently, or the frontend will poll forever waiting for a status that never comes.

Other concrete examples printed in the images:

* **Reverse-proxy example** (`9.jpg`): a request to `/api/anything` goes to `192.168.1.20:5000`; a request to `/ai/anything` goes to `192.168.1.30:7860`.
* **Deployment example** (`11.jpg`): HTML/CSS/JS is pushed to PC1 by `SCP`; Python code + `pip install` to PC2; AI code + models to PC3.
* **LoRA example** (`8.jpg`): LoRA/LoHa adapters supply fine-tuned styles — "anime, realistic, etc.".

---

## 11. Connections Between All 11 Images

### 11.1 The logical learning order

The file numbering is already the right order to study them in:

```
1.jpg   OVERVIEW ─ the 4 roles and their 3 PCs
  │
  ├── Person 1 · Frontend   →  2.jpg (workflow)  →  3.jpg (tools)
  ├── Person 2 · Backend    →  4.jpg (workflow)  →  5.jpg (tools)  →  6.jpg (P2P + database)
  ├── Person 3 · AI         →  7.jpg (workflow)  →  8.jpg (tools)
  └── Person 4 · QA/DevOps  →  9.jpg (workflow)  → 10.jpg (tools)  → 11.jpg (P2P / DevOps view)
```

Every member follows the same documentation pattern — **Workflow → Tools** — and the two members whose work crosses machine boundaries (Backend and DevOps) get an extra **P2P connection diagram**.

### 11.2 How the images depend on each other (traceable links)

| Link | From | To | Why they connect |
|---|---|---|---|
| **Endpoints match** | `2.jpg` (frontend calls `/api/login`, `/api/generate`, `/api/edit`) | `4.jpg` (backend defines those exact endpoints in the Auth API and Image API) | The frontend's Phase 3 is consuming the backend's Phase 2 |
| **Polling matches** | `2.jpg` ("Polling / WebSocket — รับ Progress Update") | `6.jpg` (`GET /api/task/abc123 (Frontend polling)`) and `4.jpg` (`GET /api/task/:id`) | The same mechanism drawn from three points of view |
| **Callback matches** | `7.jpg` ("Callback to Backend — ส่งผลลัพธ์กลับ 192.168.1.20") | `6.jpg` (step 7: `POST http://192.168.1.20:5000/api/callback`) and `4.jpg` (`POST /api/callback`) | The AI engineer's Phase 3 box **is** the backend's Task API |
| **AI endpoints match** | `7.jpg` (`POST /ai/generate`, FastAPI on port 7860) | `6.jpg` (`POST http://192.168.1.30:7860/ai/generate`) | Same endpoint, same port, drawn from two sides |
| **Proxy explains the sequence** | `9.jpg` (`/api/*` → `192.168.1.20:5000`, `/ai/*` → `192.168.1.30:7860`) | `6.jpg` (the sequence starts at the **Nginx** participant, not at the browser) | Nginx is why the browser only knows one address |
| **Database matches the tools** | `6.jpg` (ER diagram: `USERS`, `IMAGES`, `TASKS`) | `5.jpg` (`SQLite3` — "เก็บข้อมูล User, Image, Task"; `Flask-SQLAlchemy` as the ORM) | The tools row names exactly the three tables in the diagram |
| **Deployment targets match** | `11.jpg` (PC1 `Nginx :80` + `Static Files`; PC2 `Flask :5000` + `SQLite DB`; PC3 `FastAPI :7860` + `GPU`) | `1.jpg` (the `PC` column) and `9.jpg` (Phase 3 Deployment) | The DevOps view is the physical realisation of the work-division table |
| **Backup matches** | `10.jpg` (`rsync / robocopy` — "Backup Database + Images") | `11.jpg` (`SSH + rsync` line) and `6.jpg` (the DB and images both live on PC2) | Backup targets PC2 because that's where the data is |
| **JWT matches** | `4.jpg` (Phase 3 "JWT Authentication") | `5.jpg` (`Flask-JWT-Extended` — "JWT Token Authentication") | The tool that implements the workflow box |
| **Tool tables are parallel** | `3.jpg`, `5.jpg`, `8.jpg`, `10.jpg` | each other | All four use the identical `หมวด / Tool / วัตถุประสงค์` format, one per member |

### 11.3 The one-sentence summary of the whole set

> **`1.jpg`** splits the project into four roles; **`2–3.jpg`** build the face, **`4–6.jpg`** build the brain and the memory, **`7–8.jpg`** build the imagination, and **`9–11.jpg`** wire all three machines together, test them, deploy them and watch them.

---

## 12. Common Mistakes and Warnings

**Warnings printed in the images (source facts):**

| Warning | Source |
|---|---|
| **`ป้องกัน SQL Injection`** — validate all input to prevent SQL injection | `4.jpg` |
| **`Rate Limiting`** — cap request rates | `4.jpg` |
| **`จัดคิวงานไม่ให้ GPU ล่ม`** — queue the jobs *so the GPU doesn't crash* | `7.jpg` |
| **`VRAM Management`** — manage GPU memory | `7.jpg` |
| **`Error Handling — Retry + Fallback`** | `7.jpg` |
| **`ตั้งค่า Firewall — เปิด Port ที่จำเป็น`** — open only the ports you actually need | `9.jpg` |
| **IMPORTANT callout** — Person 4 absorbs the Nginx/Reverse-Proxy work from Person 5 because it is infrastructure work tied directly to deployment | `9.jpg` |
| **`password_hash`** stored in the `USERS` table — never a plain password | `6.jpg` |

**Common mistakes (AI-written, derived from the images — not printed in them):**

1. **Waiting synchronously for the image.** The single biggest design error would be to have `POST /api/generate` block until the picture is ready. `6.jpg` shows why: the AI takes 30–60 seconds. The endpoint must return `queued` immediately.
2. **Forgetting that the callback comes *from* the AI server.** `POST /api/callback` (`4.jpg`) is an *inbound* endpoint on the backend, called by PC3. It is easy to mistake it for something the browser calls.
3. **Letting the browser talk to `:5000` or `:7860` directly.** Per `9.jpg`, everything must go through Nginx on PC1. Bypassing the proxy will work on a developer's laptop and break in the deployed system.
4. **Confusing `TASKS.id` (integer PK) with `TASKS.task_id` (string UK).** `6.jpg` defines both. `"abc123"` is the *task_id*.
5. **Running two generations at once.** Without the request queue from `7.jpg`, concurrent jobs will exhaust VRAM and crash the GPU process.
6. **Committing model files with plain Git.** `8.jpg` specifies **Git LFS** for exactly this reason.
7. **Deploying with Flask's development server.** `5.jpg` specifies Waitress (Windows) / Gunicorn (Linux) as the production process manager.
8. **Forgetting CORS during development.** `5.jpg` lists `Flask-CORS`; while the frontend is served from a different origin than the API, the browser will silently block the calls.
9. **Inconsistent status strings.** See §10 — `pending` / `queued` / `accepted` / `done` / `completed` all appear in one flow.

---

## 13. Problem-Solving Guidelines

**AI-written guidance, grounded in the images. Use these when answering questions or debugging this project.**

### 13.1 "Where does this task belong?" — routing any question to the right role

| If the question is about… | It belongs to | Check image |
|---|---|---|
| A page, a button, a layout, Bootstrap, the Canvas editor | Person 1 — Frontend | `2.jpg`, `3.jpg` |
| An endpoint, login, the database, a task record, logging | Person 2 — Backend | `4.jpg`, `5.jpg`, `6.jpg` |
| The model, LoRA, VRAM, txt2img/img2img/inpaint, the GPU | Person 3 — AI | `7.jpg`, `8.jpg` |
| Nginx, ports, deployment, tests, backups, monitoring | Person 4 — QA/DevOps | `9.jpg`, `10.jpg`, `11.jpg` |

### 13.2 Debugging by layer — follow the request path from `6.jpg`

When something is broken, walk the path in order and find the first hop that fails:

1. **Browser → Nginx (PC1 :80)** — is Nginx running? Is the static file served? *(`11.jpg`: `HTTP :80` UI Test, `GET /health`)*
2. **Nginx → Flask (PC2 :5000)** — is the `/api/*` proxy rule correct? *(`9.jpg`)* Is Flask up? *(`11.jpg`: `GET /api/health`)*
3. **Flask → SQLite** — did the task row get inserted? *(`6.jpg` step 2)*
4. **Flask → AI (PC3 :7860)** — did the AI server accept? *(`6.jpg` steps 3–4; `11.jpg`: `GET /ai/health`)*
5. **AI → Flask callback** — did `POST /api/callback` arrive? *(this is the most commonly missed hop, because it is the only request that flows "backwards")*
6. **Browser polling** — is `GET /api/task/:id` returning `completed`? *(`6.jpg` steps 9–12)*

**Rule of thumb (AI):** if the user sees a spinner forever, the failure is almost always at hop 5 or 6 — the picture was probably generated, but the callback never landed or the status string never changed.

### 13.3 When designing something new for this project

1. Start from `1.jpg` — confirm which PC/role owns it.
2. If it crosses a machine boundary, it needs an **endpoint** (add it to the right list in `4.jpg` or `7.jpg`) **and** an Nginx rule (`9.jpg`).
3. If it takes longer than a second, it needs the **queue + callback + polling** pattern from `6.jpg`, not a plain request/response.
4. If it stores anything, it needs a column in `USERS` / `IMAGES` / `TASKS` (`6.jpg`).
5. If it can be reached from the browser, it needs input validation, rate limiting and a log line (`4.jpg`).

---

## 14. Quick Revision Summary

**Memorise these — they are the backbone of all 11 images:**

* **4 people, 3 PCs.** Person 1 Frontend (PC1 `.10`), Person 2 Backend (PC2 `.20`), Person 3 AI (PC3 `.30`), Person 4 QA/DevOps + Nginx (all PCs). — `1.jpg`
* **3 ports.** Nginx `:80` · Flask `:5000` · FastAPI/AI `:7860`. SSH is `:22`. — `6.jpg`, `9.jpg`, `11.jpg`
* **One front door.** Nginx on PC1 proxies `/api/*` → `.20:5000` and `/ai/*` → `.30:7860`. — `9.jpg`
* **3 tables.** `USERS` (who) · `IMAGES` (the picture) · `TASKS` (the job ticket). — `6.jpg`
* **The generate flow.** `POST /api/generate` → insert task (`pending`) → call the AI → return `queued` immediately → **AI works 30–60 s** → AI calls `POST /api/callback` → update to `completed` → browser's `GET /api/task/:id` finally returns `image_url`. — `6.jpg`
* **4 AI endpoints.** `/ai/generate` (txt2img) · `/ai/edit` (img2img) · `/ai/inpaint` · `/ai/models`. — `7.jpg`
* **Security trio.** JWT auth · input validation (anti-SQL-injection) · rate limiting — plus log every request. — `4.jpg`
* **Why a queue exists.** One GPU, 30–60 s per image, limited VRAM. — `7.jpg`
* **DevOps has two channels.** SSH/SCP *in* (deploy), HTTP *from outside* (test + health check). — `11.jpg`

---

## 15. Unclear or Unreadable Information — `Needs further verification`

Everything below is either partially obscured in the source image, internally inconsistent across images, or absent where it might be expected. **None of it has been guessed at or filled in.**

| # | Item | Image(s) | Status |
|---|---|---|---|
| 1 | The small **phase "tab" buttons** at the top of each workflow diagram render with **overlapping text** and are individually illegible (e.g. in `4.jpg` they read as `Phase 2: API,DeP̶h̶a̶s̶e̶ 1̶: S̶e̶t̶` overlapping). The phase *names* are still fully recoverable from the section headers immediately below them, which are clear. | `2.jpg`, `4.jpg`, `7.jpg`, `9.jpg` | `Needs further verification` (cosmetic only — no information lost) |
| 2 | In `11.jpg`, the **PC1 box label** reads `PC1 - Frontend + Nginx (192...` — the rest of the IP is **covered by the overlapping PC3 box**. The address is `192.168.1.10` according to `1.jpg`, `6.jpg` and `9.jpg`, but that specific text is not legible *in this image*. | `11.jpg` | `Needs further verification` (resolved by other images) |
| 3 | In `11.jpg`, the **connection lines cross and overlap**, so the exact line-to-node routing cannot be traced with certainty. The mapping given in §4.11 is **AI inference from the connection labels**, not a direct reading. | `11.jpg` | `Needs further verification` |
| 4 | The **IMPORTANT note in `9.jpg` refers to "คนที่ 5" (Person 5)** — but `1.jpg` describes a **4-person** team. Who Person 5 was is **never explained anywhere in the 11 images**. **Resolved by cross-reference (AI, from a different source — not from the images):** the course lecture `Lecture/Lecture 4 - Point Operation.pdf`, slide 55, gives an example team split of **five** roles, the fifth being *"**คนที่ 5 (ถ้ามี) — Reverse Proxy, Routing**"* — literally "Person 5 (**if there is one**)", noted as having a light workload. So Person 5 is an **optional** role defined by the lecture, and `9.jpg` documents this team's decision to fold that optional role into Person 4. | `9.jpg` vs `1.jpg`; resolved via `Lecture 4` s.55 | Resolved by cross-reference (outside the images) |
| 5 | **WebSocket has no backend tool.** `2.jpg` (Phase 3) and `3.jpg` both specify Socket.IO / WebSocket for progress updates, but the backend tool list in `5.jpg` contains **no** WebSocket library (no Flask-SocketIO), and the sequence in `6.jpg` shows **polling**, not WebSocket. Whether WebSocket is actually implemented is unclear. | `2.jpg`, `3.jpg`, `5.jpg`, `6.jpg` | `Needs further verification` |
| 6 | **Health-check endpoints are undocumented.** `11.jpg` shows `GET /health`, `GET /api/health` and `GET /ai/health`, but none of these appear in the backend API list (`4.jpg`) or the AI API list (`7.jpg`). | `11.jpg` vs `4.jpg`, `7.jpg` | `Needs further verification` |
| 7 | **The SQL in `6.jpg` is shorthand, not valid SQL.** `INSERT INTO tasks (status='pending')` is not syntactically valid, and `SELECT * FROM tasks WHERE id='abc123'` queries the integer `id` column with a string value, while the ER diagram in the same image puts `'abc123'` in the `task_id` column. Recorded exactly as printed; **not silently corrected**. | `6.jpg` | `Needs further verification` |
| 8 | **Port 7860 is assigned to FastAPI.** `7.jpg` and `8.jpg` say the AI service is `FastAPI + Uvicorn` on port `7860`, while `8.jpg` also lists `Stable Diffusion WebUI Forge` as the generation engine — and 7860 is conventionally Forge/A1111's own WebUI port. Whether FastAPI *wraps*, *replaces* or *proxies* Forge on that port is not stated. | `7.jpg`, `8.jpg` | `Needs further verification` |
| 9 | **No P2P connection diagram exists for Person 1 or Person 3.** Only Person 2 (`6.jpg`) and Person 4 (`11.jpg`) have one. | folder-level | Noted — not an error, just absent |
| 10 | The frontend integrates only **3** APIs in `2.jpg` (`/api/login`, `/api/generate`, `/api/edit`), whereas the backend defines **11** endpoints in `4.jpg`. The workflow box is presumably not exhaustive, but the images do not say so. | `2.jpg` vs `4.jpg` | `Needs further verification` |
| 11 | Deadlines, dates, grading weights, team member names and any deliverable due dates are **not present** anywhere in the 11 images. | folder-level | Absent from source |

---

## 16. Instructions for AI — How to Use This Knowledge Base

**When working on any future task about this Web App project, follow these rules:**

1. **Treat the 11 images in `/Users/winter/Desktop/Web_App/Learn/` as the source of truth.** This document is a faithful transcription plus clearly-marked explanation. If this file and an image ever disagree, **the image wins**.
2. **Always cite the image.** When you state a fact from this project, name the file it came from (e.g. "per `6.jpg`, the AI takes 30–60 seconds"). Every section above is traceable to a specific `N.jpg`.
3. **Never invent an endpoint, a port, an IP address, a table column, or a tool.** The complete authoritative lists are: endpoints in §7.1 / §7.2, ports and IPs in §6, database columns in §4.6, tools in §4.3 / §4.5 / §4.8 / §4.10. If something is not in those lists, say it is not specified — do not fill the gap.
4. **Respect the `Needs further verification` items in §15.** Do not resolve them silently. If a task depends on one (e.g. "is WebSocket implemented?"), state the ambiguity and ask, rather than picking an answer.
5. **Route the task to the right role first** (§13.1). Code for a page → Person 1's stack (Bootstrap 5, Vanilla JS/jQuery, Fetch/Axios, Canvas API). Code for an endpoint → Person 2's stack (Flask 3.x, Flask-SQLAlchemy, SQLite3, Flask-JWT-Extended). Code for the model → Person 3's stack (PyTorch 2.x, FastAPI, Forge, LoRA). Config/tests/deployment → Person 4's stack (Nginx, pytest, Locust, shell scripts).
6. **Use the tools the images specify — not your own favourites.** If asked for a backend endpoint, write Flask, not FastAPI. If asked for the AI service, write FastAPI, not Flask. That split is deliberate (`5.jpg` vs `8.jpg`).
7. **Preserve the asynchronous pattern.** Any code you generate for image generation must follow `6.jpg`: accept → return a `task_id` immediately → work in the background → callback → poll. Never write a blocking generate endpoint.
8. **Keep the naming from the images.** `task_id`, `image_base64`, `image_url`, `params_json`, `password_hash`, `/api/callback`, `/ai/generate` — use these exact names so generated code matches the design.
9. **Separate source from inference in your answers**, the way this document does. Say "the image shows…" versus "I would suggest…".
10. **Do not modify the original images.** They are read-only source material.
11. **Cross-reference the lecture material where relevant.** The course lectures (`Lecture/` and `Lecture_Knowledge_Base.md`) cover the *theory* behind this project — Flask, Jinja, the distributed architecture, Stable Diffusion, LoRA, ControlNet, img2img/inpaint. The `Learn` images cover the *team's implementation plan*. Use the lectures for "why/how does this technique work", and the `Learn` images for "what exactly are we building and who builds it". Flag clearly when you are drawing on the lectures rather than on the images.
12. **When asked for something the images do not cover** (a deadline, a member's real name, a UI colour scheme, actual source code), say so plainly — the images are planning documents, and §15 lists what they leave out.

---

## 17. Verification Checklist

| Check | Result |
|---|---|
| All 11 images inspected | ✅ `1.jpg`, `2.jpg`, `3.jpg`, `4.jpg`, `5.jpg`, `6.jpg`, `7.jpg`, `8.jpg`, `9.jpg`, `10.jpg`, `11.jpg` |
| Exactly 11 image files found in `Learn/` | ✅ Confirmed — 11 files, no more, no fewer |
| No image skipped | ✅ Every image has its own subsection in §4 |
| Both text **and** visual information analysed | ✅ Tables transcribed row-by-row; diagrams read box-by-box and arrow-by-arrow |
| Content matches the source images | ✅ All tables, endpoints, IPs, ports, JSON, SQL and field names transcribed as printed |
| No unsupported information added | ✅ AI explanation is labelled as such throughout; §6 explicitly records that **no formulas exist** rather than inventing any |
| Unclear content marked | ✅ 11 items marked `Needs further verification` in §15 |
| Every section names its source image | ✅ |
| Organised and AI-usable | ✅ §16 gives explicit usage rules |
| Original images unmodified | ✅ Read-only access; nothing renamed, moved or deleted |

---

*End of `Learn_Knowledge_Base.md`. Source of truth: the 11 images in `/Users/winter/Desktop/Web_App/Learn/`.*
