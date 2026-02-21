# CodeNotes 📝

A fullstack programming notes app for **Java**, **Python**, and **C** — built with **Next.js** and **MongoDB Atlas**, deployable on **Vercel** in minutes.

---

## 🚀 Tech Stack

| Layer     | Technology          |
|-----------|---------------------|
| Frontend  | Next.js (React)     |
| Backend   | Next.js API Routes  |
| Database  | MongoDB Atlas       |
| Hosting   | Vercel              |

---

## ✨ Features

- Add, edit, delete, and view notes
- Filter by language (Java / Python / C)
- Live search across title + content
- Notes stored in MongoDB (persistent, shared)
- Responsive dark UI with smooth animations
- Keyboard shortcut: `Ctrl/Cmd+N` to add, `Esc` to close

---

## 🛠 Local Development

### 1. Clone & install

```bash
git clone https://github.com/YOUR_USERNAME/codenotes.git
cd codenotes
npm install
```

### 2. Set up MongoDB Atlas

1. Go to [https://cloud.mongodb.com](https://cloud.mongodb.com) and create a free account
2. Create a **new project** → **Build a Database** → choose the **Free (M0)** tier
3. Set a username + password for your database user
4. Under **Network Access**, add `0.0.0.0/0` (allow from anywhere) — required for Vercel
5. Click **Connect** → **Drivers** → copy your connection string

It looks like:
```
mongodb+srv://myuser:mypassword@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
```

### 3. Create `.env.local`

```bash
cp .env.local.example .env.local
```

Edit `.env.local` and paste your connection string:

```
MONGODB_URI=mongodb+srv://myuser:mypassword@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
```

### 4. Run the dev server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) 🎉

---

## ☁️ Deploy to Vercel

### Option A — Via GitHub (recommended)

1. Push this project to a GitHub repo
2. Go to [https://vercel.com](https://vercel.com) → **New Project**
3. Import your GitHub repo
4. Under **Environment Variables**, add:
   - Key: `MONGODB_URI`
   - Value: your MongoDB Atlas connection string
5. Click **Deploy** ✅

### Option B — Via Vercel CLI

```bash
npm i -g vercel
vercel
# Follow prompts, then add env variable:
vercel env add MONGODB_URI
vercel --prod
```

---

## 📁 Project Structure

```
codenotes/
├── lib/
│   └── mongodb.js          # MongoDB connection helper
├── pages/
│   ├── index.js            # Main UI page
│   └── api/
│       └── notes/
│           ├── index.js    # GET all, POST new
│           └── [id].js     # GET one, PUT, DELETE
├── .env.local.example      # Env variable template
├── .gitignore
├── next.config.js
├── package.json
└── README.md
```

---

## 🔌 API Endpoints

| Method | Endpoint              | Description                        |
|--------|-----------------------|------------------------------------|
| GET    | `/api/notes`          | Get all notes (supports `?lang=java&search=...`) |
| POST   | `/api/notes`          | Create a note `{title, content, lang}` |
| GET    | `/api/notes/:id`      | Get a single note                  |
| PUT    | `/api/notes/:id`      | Update a note                      |
| DELETE | `/api/notes/:id`      | Delete a note                      |

---

## ⚠️ Important Notes

- Never commit `.env.local` — it's in `.gitignore`
- MongoDB Atlas free tier (M0) supports up to 512MB — plenty for notes
- Make sure to whitelist `0.0.0.0/0` in Atlas Network Access for Vercel deploys
