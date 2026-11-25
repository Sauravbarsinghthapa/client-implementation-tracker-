# Deploying Client Implementation Tracker (CIT) for Free

This guide explains how to host **Client Implementation Tracker (CIT)** 100% for free on **Render** with a persistent **Turso** cloud SQLite database.

---

## Step 1: Create a Free Turso Database (Persistent SQLite)
1. Sign up for a free account at **https://turso.tech** (no credit card required).
2. Create a new database (e.g., `cit-production`).
3. Click **Connect / Create Token** and copy:
   - `TURSO_DATABASE_URL` (looks like `libsql://cit-production-yourname.turso.io`)
   - `TURSO_AUTH_TOKEN` (the generated token string)

---

## Step 2: Deploy on Render (Free Web Hosting)
1. Sign up for a free account at **https://render.com** using your GitHub account.
2. Click **New +** → **Web Service** (or **Blueprint** to auto-detect `render.yaml`).
3. Select this GitHub repository.
4. Use these settings (auto-filled if using `render.yaml`):
   - **Runtime:** `Node`
   - **Build Command:** `npm install && npm run build`
   - **Start Command:** `npm start`
   - **Instance Type:** `Free`
5. Add these **Environment Variables**:
   - `TURSO_DATABASE_URL` = *(paste your Turso URL)*
   - `TURSO_AUTH_TOKEN` = *(paste your Turso token)*
   - `JWT_SECRET` = *(any long random string, or auto-generated)*
6. Click **Create Web Service**.

Render will build the app and give you a live URL like `https://client-implementation-tracker.onrender.com`.
On first startup, the app automatically creates all database tables and seeds the initial demo data.

---

## Step 3: Initial Login
- **Super Administrator:** `admin@cit.local` / `password123`
- Other demo roles (`management@cit.local`, `pm@cit.local`, `coordinator@cit.local`, `qa@cit.local`, `dev@cit.local`, `support@cit.local`, `viewer@cit.local`) also use `password123`.

> **Note on Render Free Tier:** Free web services spin down after 15 minutes of inactivity and take ~30 seconds to wake up on the first request. Your Turso database remains 100% persistent.
