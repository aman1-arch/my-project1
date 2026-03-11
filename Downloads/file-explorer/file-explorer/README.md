# 🗂️ Recursive Tree File Explorer

> Full-Stack Engineering Assignment — MEVN Stack (MongoDB, Express.js, Vue 3, Node.js)

A nested file/folder navigator with **recursive data structures** and **lazy loading** via REST API.

---

## ✨ Features

- 📁 **Recursive Tree View** — Unlimited nesting depth using a self-referencing MongoDB schema
- ⚡ **Lazy Loading** — Children are only fetched from the API when a folder is first expanded
- ➕ **Create** files and folders at root level
- 🗑️ **Delete** a node and all its descendants recursively
- 🎨 **File-type icons** — Different icons for `.vue`, `.js`, `.json`, `.md`, etc.

---

## 🏗️ Project Structure

```
file-explorer/
├── backend/
│   ├── models/
│   │   └── Node.js          # Self-referencing Mongoose schema
│   ├── routes/
│   │   └── nodes.js         # REST API endpoints
│   ├── seed/
│   │   └── seed.js          # Sample data seeder
│   ├── server.js            # Express app entry point
│   ├── .env.example
│   └── package.json
│
└── frontend/
    ├── src/
    │   ├── api/
    │   │   └── nodes.js     # Axios API calls
    │   ├── components/
    │   │   ├── Sidebar.vue  # Root container + create modal
    │   │   └── TreeNode.vue # Recursive node component
    │   ├── App.vue
    │   ├── main.js
    │   └── style.css
    ├── index.html
    ├── vite.config.js
    └── package.json
```

---

## 🚀 Setup & Run

### Prerequisites
- Node.js v18+
- MongoDB running locally on port 27017

### 1. Backend

```bash
cd backend
npm install
cp .env.example .env   # Edit MONGO_URI if needed
npm run seed           # (Optional) seed sample data
npm run dev            # Starts on http://localhost:5000
```

### 2. Frontend

```bash
cd frontend
npm install
npm run dev            # Starts on http://localhost:3000
```

Open **http://localhost:3000** in your browser.

---

## 🔌 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/nodes` | Get all root-level nodes |
| `GET` | `/api/nodes/:parentId/children` | Get children of a folder (lazy load) |
| `POST` | `/api/nodes` | Create a file or folder |
| `DELETE` | `/api/nodes/:id` | Delete a node + all descendants |

### POST `/api/nodes` Body
```json
{
  "name": "index.js",
  "type": "file",
  "parentId": null
}
```

---

## 🗄️ Database Schema

```js
{
  name: String,        // Display name
  type: String,        // "file" | "folder"
  parentId: ObjectId,  // null for root, ref to parent Node
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🧠 Key Design Decisions

- **Self-referencing schema**: Each node stores only its `parentId`, enabling unlimited nesting without deeply nested arrays in MongoDB.
- **Lazy loading**: `loaded` flag on each `TreeNode` prevents redundant API calls — children are fetched only once on first expand.
- **Recursive component**: `TreeNode.vue` renders itself for children, making depth infinite with no extra code.
- **Cascade delete**: The backend `deleteRecursive` function traverses all descendants before deleting, ensuring no orphaned documents.

---

## 📦 Tech Stack

| Layer | Technology |
|-------|-----------|
| Database | MongoDB + Mongoose |
| Backend | Node.js + Express.js |
| Frontend | Vue 3 (Composition API) + Vite |
| HTTP | Axios |
## ⚙️ Setup Instructions

### 1. Clone the Repository

git clone https://github.com/YOUR_USERNAME/file-explorer.git

cd file-explorer

---

### 2. Run Backend

cd backend

npm install

npm start

Server runs on:
http://localhost:5000

---

### 3. Run Frontend

cd frontend

npm install

npm run dev

Frontend runs on:
http://localhost:5173

---

### 4. Seed Database

cd backend

node seed.js
## 🔄 Data Flow

1. Vue frontend sends API requests using Axios.
2. Requests are sent to the Node.js Express backend.
3. Express routes process the request and interact with MongoDB Atlas through Mongoose models.
4. MongoDB returns data to the backend.
5. Backend sends JSON responses back to the Vue frontend.
6. Vue components update the UI based on the received data.
## 🚀 Live Deployment

Frontend (Vercel):
https://your-vercel-app-link.vercel.app

Backend (Render):
https://file-explorer-backend-0ws9.onrender.com