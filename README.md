# Lost and Founds

A full-stack web application for reporting, browsing, and reclaiming lost or found items on a campus/community, with built-in real-time chat between users and an admin dashboard for moderation.

## Features

- **User accounts** — register, log in, and update your profile (name, email, password) with JWT-based authentication
- **Post items** — report a lost or found item with a title, status, location, description, contact info, and photo
- **Browse & search** — view all active items posted by the community
- **Real-time chat** — message other users directly about an item using Socket.IO, with chat history saved per room
- **Inbox** — see all your active conversations at a glance
- **Admin dashboard** — admins can view/manage users and items, and archive or restore either one
- **Notifications** — in-app notification center for updates

## Tech Stack

**Frontend**
- React 19 + Vite
- Tailwind CSS + Bootstrap
- Socket.IO client

**Backend**
- Node.js + Express
- MongoDB + Mongoose
- Socket.IO (real-time messaging)
- JWT (`jsonwebtoken`) for auth, `bcrypt` for password hashing
- `multer` for image uploads

## Project Structure

```
Lost-and-Founds/
├── lost-and-found-backend/
│   ├── controllers/       # Admin logic (restore users/items)
│   ├── middleware/         # JWT auth middleware
│   ├── models/             # Mongoose schemas: User, Item, Message
│   ├── routes/              # Express routes: auth, items, chat, admin
│   ├── uploads/              # Uploaded item images
│   └── server.js               # App entry point (Express + Socket.IO + MongoDB)
└── lost-and-found-frontend/
    ├── src/
    │   ├── components/        # Navbar, Dashboard, ChatBox, AdminDashboard, etc.
    │   ├── App.jsx
    │   └── config.js
    └── vite.config.js
```

## Getting Started

### Prerequisites
- Node.js (v18+ recommended)
- A MongoDB database (local or MongoDB Atlas)

### 1. Clone the repo
```bash
git clone https://github.com/AbdulrahmanKiwan/Lost-and-Founds.git
cd Lost-and-Founds
```

### 2. Set up the backend
```bash
cd lost-and-found-backend
npm install
```

Create a `.env` file in `lost-and-found-backend/` with the following variables:
```
MONGODB_URI=your_mongodb_connection_string
PORT=5000
JWT_SECRET=your_jwt_secret
FRONTEND_URL=http://localhost:5173
```

Start the backend (with auto-reload):
```bash
npm run dev
```

### 3. Set up the frontend
In a separate terminal:
```bash
cd lost-and-found-frontend
npm install
npm run dev
```

The frontend will run on `http://localhost:5173` and the backend on `http://localhost:5000` by default.

## API Overview

| Route | Description |
|---|---|
| `POST /api/auth/register` | Create a new account |
| `POST /api/auth/login` | Log in and receive a JWT |
| `POST /api/auth/forgot-password` | Reset password with current password |
| `PUT /api/auth/update` | Update profile (authenticated) |
| `GET /api/items` | List all active items |
| `POST /api/items` | Create a new item (with image upload) |
| `PUT /api/items/:id` | Update an item |
| `DELETE /api/items/:id` | Archive an item |
| `PUT /api/items/:id/restore` | Restore an archived item |
| `GET /api/messages/:roomId` | Get chat history for a room |
| `GET /api/chat-rooms/:userId` | Get a user's chat rooms |
| `GET /api/admin/users` | List users (admin only) |
| `PUT /api/admin/items/:id` | Edit an item (admin only) |

Real-time chat events (`send_message`, `receive_message`, `join_room`) are handled over Socket.IO.
