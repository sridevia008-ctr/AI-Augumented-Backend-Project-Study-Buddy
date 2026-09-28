Absolutely — here is a **clean copy-paste version** of your README in Markdown, formatted to look like the GitHub README shown in your image.

````markdown
# AI StudyBuddy API

An AI-powered educational backend built with **Node.js, Express, MongoDB, and Gemini 2.5 Flash.**

## Features

- JWT auth stored in **HTTP-only cookies** (access + refresh tokens)
- Role-Based Access Control (student / admin)
- Upload study materials (`.txt`, `.md`, `.pdf`)
- AI-powered: summarize, flashcards, quiz, study plan via Gemini 2.5 Flash

---

## Setup

### 1. Install dependencies

```bash
npm install
````

### 2. Create `.env` file

```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/ai-studybuddy
JWT_ACCESS_SECRET=your_access_secret_here
JWT_REFRESH_SECRET=your_refresh_secret_here
GEMINI_API_KEY=your_gemini_api_key_here
NODE_ENV=development
```

### 3. Run the server

```bash
node index.js
```

---

## Project Structure

```text
ai-studybuddy/
├── index.js                     # Entry point
├── uploads/                     # Temp file storage
└── src/
    ├── controllers/
    │   ├── authController.js    # register, login, refresh, logout
    │   ├── materialController.js# upload + all AI features
    │   └── adminController.js   # admin-only routes
    ├── middleware/
    │   ├── auth.js              # protect + adminOnly
    │   └── upload.js            # multer config
    ├── models/
    │   ├── User.js
    │   └── Material.js
    ├── routes/
    │   ├── auth.js
    │   ├── materials.js
    │   └── admin.js
    └── utils/
        ├── db.js                # MongoDB connection
        ├── gemini.js            # Gemini AI helper
        └── tokens.js            # JWT + cookie helpers
```

---

## API Reference

### Auth Routes — `/api/auth`

| **Method** | **Endpoint** | **Body**                      | **Description**   |
| ---------- | ------------ | ----------------------------- | ----------------- |
| POST       | `/register`  | `name, email, password, role` | Register new user |
| POST       | `/login`     | `email, password`             | Login             |
| POST       | `/refresh`   | —                             | Refresh tokens    |
| POST       | `/logout`    | —                             | Clear cookies     |

> Tokens are stored in **HTTP-only cookies** (`accessToken` expires in 15m, `refreshToken` in 7d).

---

### Material Routes — `/api/materials`

**Requires login**

| **Method** | **Endpoint**      | **Body / Notes**                     | **Description**         |
| ---------- | ----------------- | ------------------------------------ | ----------------------- |
| POST       | `/upload`         | Form-data: `file` + optional `title` | Upload study material   |
| GET        | `/`               | —                                    | List your materials     |
| GET        | `/:id`            | —                                    | Get one material        |
| DELETE     | `/:id`            | —                                    | Delete material         |
| POST       | `/:id/summarize`  | —                                    | AI summarize            |
| POST       | `/:id/flashcards` | `{ count: 5 }`                       | Generate flashcards     |
| POST       | `/:id/quiz`       | `{ count: 5 }`                       | Generate MCQ quiz       |
| POST       | `/:id/study-plan` | `{ goal, hoursPerDay, days }`        | Personalized study plan |

---

### Admin Routes — `/api/admin`

**Admin role only**

| **Method** | **Endpoint** | **Description**               |
| ---------- | ------------ | ----------------------------- |
| GET        | `/users`     | List all users                |
| DELETE     | `/users/:id` | Delete user + their materials |
| GET        | `/stats`     | Total users & materials count |

---

## Cookie Details

| **Cookie**     | **Expiry** | **Flags**                     |
| -------------- | ---------- | ----------------------------- |
| `accessToken`  | 15 min     | `httpOnly`, `sameSite=strict` |
| `refreshToken` | 7 days     | `httpOnly`, `sameSite=strict` |

> In production, both cookies have `secure: true`.

```

### One small improvement

I changed the setup code blocks to use proper GitHub syntax highlighting:

- `bash` for terminal commands
- `env` for `.env`
- `text` for the project structure

So GitHub will render your README more cleanly, similar to the screenshot.
```


Demo/API Testing Video: https://drive.google.com/file/d/17XNg0VWXg4s1TG67KlzQLXZa8AVNxbdw/view?usp=sharing

Code Explanation Video: https://drive.google.com/file/d/1vRYgmyhx81Z5OszdTSX8BhVdqNg-L-Qd/view?usp=sharing

Main Documantation: https://docs.google.com/document/d/12TXtFsqMExZaMz2abFLbGkORXK8Ccsew/edit?usp=sharing&ouid=102536545098638402040&rtpof=true&sd=true

Phase-wise documentation: https://drive.google.com/drive/folders/1gD1tYKndIlPupyu29fyVOHK0KIm7suJM?usp=sharing

