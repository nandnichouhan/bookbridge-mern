# BookBridge – Credit-Based Community Book Exchange (MERN)

BookBridge is a **credit-based, community book exchange platform** built with **MongoDB, Express.js, React.js, and Node.js**.  
Users list books, earn credits when others request them, and spend those credits to request new books. No money involved.

The UI is a modern, card-based dashboard with soft gradients, clear credit pill indicators, and smooth navigation between browsing, exchanges, giveaways, and profile.

---

## 1. Tech stack

- **Frontend**: React + Vite
- **Backend**: Node.js + Express
- **Database**: MongoDB
- **Auth**: Email + password (JWT)

---

## 2. Project structure

```text
Call/
  backend/        # Node/Express/MongoDB API
  frontend/       # React/Vite single-page app
```

You run backend and frontend separately.

---

## 3. Prerequisites

- **Node.js** (LTS)
- **npm**
- **MongoDB Community Server**
  - Running locally on `mongodb://127.0.0.1:27017`

> On Windows, install MongoDB as a **service**, then ensure the **MongoDB** service is running from `services.msc`.

---

## 4. Backend setup (`backend/`)

### 4.1 Install dependencies

```bash
cd backend
npm install
```

### 4.2 Environment variables

A sample file is provided:

```text
backend/.env.example
```

Create `.env` next to it (or copy/rename):

```bash
cd backend
cp .env.example .env   # on Windows PowerShell: copy .env.example .env
```

Default `.env` values:

```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017
MONGO_DB_NAME=bookbridge
JWT_SECRET=supersecret-jwt-key-change-me
JWT_EXPIRES_IN=7d
```

### 4.3 Start MongoDB

Make sure MongoDB is running locally (Windows service or `mongod`).

### 4.4 Seed sample data (optional but recommended)

```bash
cd backend
npm run seed
```

This creates:

- A couple of **demo users** with credits.
- A few **sample books**, including a free giveaway.

### 4.5 Run backend server

```bash
cd backend
npm run dev
```

Backend will start at:

- `http://localhost:5000`
- Health check: `http://localhost:5000/api/health`

---

## 5. Frontend setup (`frontend/`)

### 5.1 Install dependencies

```bash
cd frontend
npm install
```

### 5.2 API URL (optional)

By default the frontend talks to:

```text
http://localhost:5000/api
```

You can override with a `.env` file:

```env
VITE_API_URL=http://localhost:5000/api
```

### 5.3 Run frontend dev server

```bash
cd frontend
npm run dev
```

Vite will print a URL like:

```text
http://localhost:5173  (or 5174, etc.)
```

Open that in the browser.

---

## 6. Auth flow (email + password)

BookBridge uses a straightforward **email + password** flow with JWT:

- **Register** (`POST /api/auth/register`)
  - Body: `{ "name", "email", "password" }`
  - On success: returns `{ token, user }`.
- **Login** (`POST /api/auth/login`)
  - Body: `{ "email", "password" }`
  - On success: returns `{ token, user }`.
- Frontend stores the token in `localStorage` (`bb_token`) and sends it as `Authorization: Bearer <token>`.

**From the UI:**

- **Register page**: enter Name, Email, Password → you are logged in and taken to the **Dashboard**.
- **Login page**: email + password → redirects to **Dashboard**.

---

## 7. Main features

- **Dashboard**
  - Credit balance pill
  - Recent books grid
  - Quick explanation of the credit system

- **Browse books**
  - Search by title/author
  - Responsive book cards with cover, genre, and credit cost or “Free giveaway”.

- **Book details & request**
  - Full book description, condition, owner info, pickup location.
  - Request panel:
    - Optional message to owner.
    - If it’s a normal listing, credits move from requester to owner.
    - If it’s a giveaway, credits are not used.

- **Exchanges**
  - See all exchange requests involving you.
  - Owners can approve/reject pending requests.

- **My listings**
  - Create new listings with title, author, genre, and credit cost.
  - View your own books and whether they are giveaways or credit-based.

- **Giveaways**
  - Filter view of all books marked as free giveaways.

- **Profile**
  - Update display name, bio, and avatar color.
  - View email and current credits.

---

## 8. Running everything together

1. Start MongoDB (service or `mongod`).
2. Start backend:

   ```bash
   cd backend
   npm run dev
   ```

3. Start frontend:

   ```bash
   cd frontend
   npm run dev
   ```

4. Open the Vite URL (e.g. `http://localhost:5173`) in your browser.
5. Register a new account and explore:
   - List a book in **My listings**.
   - Browse and request books.
   - Check **Exchanges** to see your requests.

---

## 9. Notes for GitHub submission

- Root contains this `README.md`, `.gitignore`, `backend/`, and `frontend/`.
- Sensitive data like `.env` is **ignored** by git – reviewers can create their own `.env` from `.env.example`.
- Screenshots or a short demo GIF can be added later at the top of this README.

