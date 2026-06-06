# Personal Task Manager

A full-stack task manager app built with **React + Vite** for the frontend and **Express + TypeScript** for the backend.

Users can create, view, update, delete, and filter tasks with JSON file persistence on the server.

## Features

- Add tasks with title, optional description, and optional due date
- Edit tasks and toggle completion
- Delete tasks with confirmation
- Filter tasks by All / Active / Completed
- Search tasks by title
- Overdue tasks highlighted visually
- Persist tasks in `server/data/tasks.json`
- Backend API tests with Vitest + Supertest

## Tech Stack

- Frontend: React 18, Vite, TypeScript, Tailwind CSS
- Backend: Node.js, Express, TypeScript
- Storage: JSON file persistence
- Testing: Vitest, Supertest

## Getting Started

### Prerequisites

- Node.js 18 or newer
- npm

### Install dependencies

```powershell
cd personal-task-manager-main
npm install
npm run install:all
```

### Run locally

```powershell
npm run dev
```

This starts:
- Frontend on `http://localhost:5173`
- Backend on `http://localhost:3001`

### Run backend only

```powershell
cd server
npm install
npm run dev
```

### Run frontend only

```powershell
cd client
npm install
npm run dev
```

### Run tests

```powershell
cd server
npm test
```

## API Reference

Base URL: `http://localhost:3001/api`

### GET /tasks

Return all tasks with optional filters.

Query parameters:

- `status` — `all`, `active`, or `completed` (default: `all`)
- `search` — case-insensitive title search

### GET /tasks/:id

Return a single task by id.

### POST /tasks

Create a new task.

Request body:

```json
{
  "title": "Buy groceries",
  "description": "Optional",
  "dueDate": "2026-06-15"
}
```

### PUT /tasks/:id

Update a task.

Request body example:

```json
{
  "title": "Buy groceries",
  "description": "Eggs and milk",
  "dueDate": "2026-06-16",
  "completed": true
}
```

### PATCH /tasks/:id/toggle

Toggle completion status for a task.

### DELETE /tasks/:id

Delete a task.

### GET /health

Health check endpoint.

## Project Structure

```
personal-task-manager-main/
├─ client/                # React frontend
├─ server/                # Express backend
├─ README.md
├─ package.json
└─ package-lock.json
```

## Deployment

This project is deployment-ready with the following environment variables:

- Backend:
  - `PORT` — port for the Express server (default `5000`)
  - `CORS_ORIGIN` — allowed frontend origin(s), comma-separated
  - `DATA_FILE` — optional path to the JSON persistence file
  - `HOST` — optional listen host, default `0.0.0.0` for cloud deployment
- Frontend:
  - `VITE_API_URL` — deployed backend API base URL, for example `https://my-backend.example.com/api`

Deployment flow:

1. Build and deploy the backend from `server/`.
2. Build and deploy the frontend from `client/`.
3. Set the frontend `VITE_API_URL` to your backend API URL.
4. Set the backend `CORS_ORIGIN` to your frontend URL.

Recommended hosts:

- Backend: Render, Railway, Heroku, Fly.io, or similar
- Frontend: Vercel, Netlify, or static hosting

### Render deployment

To deploy both services on Render, use the repo root `render.yaml` configuration and set these environment variables:

- Backend service:
  - `CORS_ORIGIN=https://<frontend-service>.onrender.com`
  - `HOST=0.0.0.0`
- Frontend service:
  - `VITE_API_URL=https://<backend-service>.onrender.com/api`

If you want to deploy only one service on Render, create a Web Service for the backend and a Static Site for the frontend.

## Notes

- Designed for a personal single-user setup without authentication.
- Data is persisted in a local JSON file for simplicity.
