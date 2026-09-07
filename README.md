# 📄 Web Apps — README

> **Workspace:** `c:\Users\aryak.AAKASH\Desktop\JOBFINDER\files`
> **Last reviewed:** September 2026

A single documentation file covering **every web app** stored in this workspace.

---

## Table of Contents

1. [Workspace Overview](#1-workspace-overview)
2. [Web Apps at a Glance](#2-web-apps-at-a-glance)
3. [CareerNova – Main Web App](#3-careernova--main-web-app)
4. [Features](#4-features)
5. [Authentication](#5-authentication)
6. [Data & Persistence](#6-data--persistence)
7. [Pre-Built Static Sites](#7-pre-built-static-sites)
8. [Standalone CareerNova.jsx (Early Version)](#8-standalone-careernovajsx-early-version)
9. [Archived Firebase Reference](#9-archived-firebase-reference)
10. [Tech Stack](#10-tech-stack)
11. [Getting Started](#11-getting-started)
12. [Email OTP Service](#12-email-otp-service)
13. [Environment Variables](#13-environment-variables)
14. [Project Structure](#14-project-structure)
15. [Deployment](#15-deployment)
16. [Firebase Setup](#16-firebase-setup)
17. [npm Scripts](#17-npm-scripts)
18. [Troubleshooting](#18-troubleshooting)

---

## 1. Workspace Overview

The `files` folder contains **CareerNova** — a full-featured, AI-powered premium job portal. It exists in several forms:

- **Full source project** — a React 19 + Vite 6 app with Firebase Authentication located in `CareerNova_Complete/cn_source2/`.
- **Pre-built static sites** you can open/browse without any build step.
- **A standalone single-file prototype** (`CareerNova.jsx`) at the workspace root.
- **Archived reference copies** inside `cn_source2/src/careernova_firebase/`.

## 2. Web Apps at a Glance

| Web App | Path | Type | How to run |
|---|---|---|---|
| CareerNova (main source) | `CareerNova_Complete/cn_source2/` | React 19 + Vite 6 + Firebase | `npm run dev` |
| CareerNova (pre-built) | `CareerNova_Complete/cn_source2/CareerNova_Site/` | Static HTML / JS / CSS | open `index.html` |
| CareerNova (pre-built variant) | `CareerNova_Complete/cn_source2/cn_logo_site/` | Static HTML / JS / CSS | open `index.html` |
| Build output (latest) | `CareerNova_Complete/cn_source2/dist/` | Static (production build) | serve the folder |
| Early prototype | `CareerNova.jsx` | Single-file React source | needs a Vite project to run |
| Archived Firebase copy | `CareerNova_Complete/cn_source2/src/careernova_firebase/` | Source + pre-built site + guide | see `FIREBASE_SETUP_GUIDE.md` |

---

## 3. CareerNova – Main Web App

**CareerNova** — *"Find Work That Moves Your Career Forward"* — is a premium, mobile-friendly job portal positioned as *"India's most advanced AI-powered job platform"*.

It provides **two experiences in one app**:

- **Job Seekers** — search & apply for jobs, build a profile & resume, track applications, save jobs, and set alerts.
- **Employers** — post jobs, manage listings, review applicants, shortlist candidates, and schedule interviews.

---

## 4. Features

### 🧑‍💻 Job Seeker experience

- **Home page** — animated hero with live job search, platform stats, job-category shortcuts, featured jobs, featured companies, testimonials, and blog/insight previews.
- **Jobs browser** — keyword search with a full filter panel (category, job type, salary range, experience level, work mode, location), sorting, and save-to-favorites.
- **Job detail pages** — description, requirements, perks, company card, similar jobs, and one-click apply or save.
- **Job application flow** — guided multi-step application form (personal info → resume details → review & submit).
- **Companies directory** — browse/search companies with industry and open-jobs count.
- **Dashboard** — stats (applications, saved jobs, profile views, interviews) and recent activity.
- **Profile builder** — name, headline, location, about, email, skills, and experience with a live **Profile Strength score (0–100)** and completion checklist.
- **Applications tracker** — per-job statuses (Applied → Reviewed → Shortlisted → Interview → Offer / Rejected) with date grouping.
- **Saved jobs** — quick-access list of bookmarked jobs.
- **Job alerts** — create, toggle, and remove alert filters.
- **Resume builder** — Modern, Classic, and Minimal templates with live preview, editing, download/reset.
- **Settings** — account (email + password), notification preferences, privacy controls (profile & resume visibility), and **dark mode** toggle.

### 🏢 Employer experience

- **Employer dashboard** — jobs posted, active jobs, total applicants, profile views.
- **Post a job** — guided multi-step job-creation form (job details → description/skills → compensation & preview).
- **Job listings** — manage posted jobs, track views, and toggle status.
- **Applicants pipeline** — view applicants per job, shortlist, schedule interviews (date/time/notes), and update statuses.
- **Candidate profiles** — inspect applicant details side-by-side with the job.

### ✨ Across the app

- Career **resources hub** with 6 guides: Resume Writing, Interview Preparation, Salary Negotiation, LinkedIn Optimization, Networking 101, and AI in Job Search.
- **Toast notifications**, animated micro-interactions, and a custom inline SVG icon system.
- **Fully responsive** UI with a consistent design system (Inter font, violet/cyan gradient brand, reusable `card`, `tag`, `badge`, and `button` components).

---

## 5. Authentication

The current source (`cn_source2`) uses **Firebase Authentication v12** (see `src/firebase.js`):

- **Google Sign-In** — real Google account-picker popup (`signInWithPopup`).
- **Email + password** sign-up / sign-in.
- **Password reset** emails sent natively by Firebase.
- **Email verification** (`sendEmailVerification`).
- **Update email / password** with re-authentication support.
- **Persistent sessions** via `onAuthStateChanged`.

Firebase config lives in **`src/firebase.js`**:

| Key | Value |
|---|---|
| `apiKey` | `AIzaSyCke2zBvZJbtdCFI7QYTQk3clOhDBuYaQs` |
| `authDomain` | `careernova-3cacc.firebaseapp.com` |
| `projectId` | `careernova-3cacc` |
| `storageBucket` | `careernova-3cacc.firebasestorage.app` |
| `messagingSenderId` | `960586972151` |
| `appId` | `1:960586972151:web:7947cbb8cfb9c805cb0cf2` |
| `measurementId` | `G-DN0RZ0BWJN` |

A **demo Google account chooser** modal is included for use when no Google Client ID is configured.

---

## 6. Data & Persistence

Everything is stored client-side in the browser:

| Browser storage | Key | Content |
|---|---|---|
| `localStorage` | `cn_profile` | User profile (form, skills, experience) |
| `localStorage` | `cn_saved` | Saved job IDs |
| `localStorage` | `cn_apps` | Job applications |
| `localStorage` | `cn_employer_jobs` | Employer-posted jobs |
| `localStorage` | `cn_employer_applicants` | Employer applicants |
| `localStorage` | `cn_theme` | Light/dark theme |
| `localStorage` | `cn_settings` | Account / notification / privacy settings |
| `sessionStorage` | `cn_page` | Current page (restored across reloads) |

---

## 7. Pre-Built Static Sites

Three static builds exist — **no install or build step needed**:

1. **`CareerNova_Site/`** — pre-built standalone site (`index.html` + bundled `assets/`).
2. **`cn_logo_site/`** — a second pre-built variant with a different bundle.
3. **`dist/`** — the latest production build output from `npm run build` (matches `cn_logo_site/` assets).

Just open any `index.html` in a browser, or serve the folder with a static server:

```bash
npx serve dist
```

## 8. Standalone `CareerNova.jsx` (Early Version)

At the workspace root there is a **6,762-line single-file React prototype** of the same app. It contains its own inline CSS, sample `COMPANIES` / `JOBS` / `CATEGORIES` data, and all major pages: Home, Jobs, Job Detail, Companies, Dashboard, Profile, Applications, Saved, Alerts, Resume, Settings, Employer, Profile Setup, Auth, and Resources.

Differences from the current `cn_source2` source:

- Uses a **demo client-side OTP flow** for sign-up — the 6-digit code is generated in the browser and shown in a toast — plus a Firebase password-reset helper.
- Auth is **not connected to a real backend**; login/sign-up simply sets a local user object.
- No runnable Vite project exists for it at the root (root `package.json` only declares `firebase`), so running it requires copying it into a Vite project (e.g. replacing `cn_source2/src/App.jsx` alongside the matching Firebase config).

It is kept as a **reference/archive** of the early implementation.

## 9. Archived Firebase Reference

`cn_source2/src/careernova_firebase/` contains the previous Firebase-enabled iteration:

- `FIREBASE_SETUP_GUIDE.md` — step-by-step guide to connect the app to Firebase Authentication (Google + Email/Password, authorized domains, deployment, FAQ).
- `source/` — the older Vite source tree (`App.jsx`, `firebase.js`, `server.js`, etc.).
- `ready_to_open_site/` — an older pre-built static site.

This folder is **informational only** and is not used by the build.

---

## 10. Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, ReactDOM 19, JSX |
| Build tool | Vite 6 (`@vitejs/plugin-react`) |
| Auth | Firebase (`firebase/app`, `firebase/auth`) |
| OTP email (local dev) | Express 5, Nodemailer 9, CORS |
| OTP email (serverless) | Vercel serverless functions + Nodemailer |
| Styling | Inline CSS-in-JS + `src/index.css` base reset |
| Language | JavaScript (ES modules) |

---

## 11. Getting Started

**Prerequisites:** Node.js 18+ and npm.

```bash
# 1. enter the project folder
cd CareerNova_Complete/cn_source2

# 2. install dependencies
npm install

# 3. (optional — only for local email OTP verification)
#    open a SECOND terminal and run:
node src/server.js          # → http://localhost:4000

# 4. start the dev server (first terminal)
npm run dev                 # → http://localhost:5173
```

### Production build

```bash
npm run build        # outputs to dist/
npm run preview      # preview the production build locally
```

---

## 12. Email OTP Service

Two interchangeable implementations exist:

1. **Local Express server** — `src/server.js`
   - Endpoints: `POST /send-otp` and `POST /verify-otp`
   - In-memory OTP store, 10-minute expiry, max 3 sends / 5 verify attempts per email
   - Requires a Gmail account + App Password (edit the `transporter` block near the top)
   - Run with `node src/server.js`

2. **Vercel serverless functions** — `api/send-otp.js` and `api/verify-otp.js`
   - **Stateless**: the OTP travels inside an HMAC-signed token returned to the client
   - Needs env vars: `GMAIL_USER`, `GMAIL_PASS`, `OTP_SECRET`
   - CORS enabled for browser use

Both send branded, responsive HTML emails using the CareerNova violet-gradient template.

---

## 13. Environment Variables

| Variable | Used by | Purpose |
|---|---|---|
| `GMAIL_USER` | `server.js` / `api/*` | Sending Gmail account |
| `GMAIL_PASS` | `server.js` / `api/*` | Gmail App Password (16 chars) |
| `OTP_SECRET` | `api/*` | HMAC secret used to sign OTP tokens |

---

## 14. Project Structure

```
files/
├── package.json / package-lock.json       # root npm files (firebase only)
├── CareerNova.jsx                         # early single-file prototype (reference)
├── CareerNova_Complete/
│   └── cn_source2/                        # ★ MAIN PROJECT (CareerNova)
│       ├── index.html                     # Vite entry HTML
│       ├── vite.config.js                 # build config (relative base: './')
│       ├── vercel.json                    # Vercel deploy configuration
│       ├── package.json                   # dependencies & npm scripts
│       ├── api/                           # Vercel serverless OTP functions
│       │   ├── send-otp.js
│       │   └── verify-otp.js
│       ├── src/
│       │   ├── main.jsx                   # React entry point
│       │   ├── App.jsx                    # entire app (~10.6k lines, single file)
│       │   ├── index.css                  # base reset
│       │   ├── firebase.js                # Firebase Auth config & helpers
│       │   ├── server.js                  # local OTP email server (Express)
│       │   ├── assets/                    # hero.png, vite/react SVGs
│       │   └── careernova_firebase/       # archived Firebase reference + guide
│       ├── public/                        # favicon.svg, icons.svg
│       ├── CareerNova_Site/               # pre-built static site (Option A)
│       ├── cn_logo_site/                  # second pre-built static variant
│       └── dist/                          # latest production build output
└── node_modules/                          # root dependencies (firebase)
```

---

## 15. Deployment

`vercel.json` is pre-configured for **Vercel**:

```json
{
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": "vite",
  "rewrites": [
    { "source": "/api/(.*)", "destination": "/api/$1" },
    { "source": "/(.*)",     "destination": "/index.html" }
  ]
}
```

Deploy with:

```bash
npm install -g vercel
vercel
```

Then add your deployed domain to **Firebase → Authentication → Settings → Authorized domains**.

**Alternative (Netlify):** run `npm run build`, then drag-and-drop the `dist/` folder onto netlify.com.

---

## 16. Firebase Setup

Full instructions live in `src/careernova_firebase/FIREBASE_SETUP_GUIDE.md`. Summary:

1. Create a project at **console.firebase.google.com**.
2. Enable the **Google** and **Email/Password** sign-in providers.
3. Register a web app and copy its `firebaseConfig`.
4. Paste it into **`src/firebase.js`**.
5. Add your domain (e.g. `localhost`, `*.vercel.app`) under **Authorized domains**.
6. Run `npm install && npm run dev`.

---

## 17. npm Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start the Vite dev server → http://localhost:5173 |
| `npm run build` | Create the production build in `dist/` |
| `npm run preview` | Preview the production build locally |
| `node src/server.js` | Run the local OTP email server → http://localhost:4000 |

---

## 18. Troubleshooting

| Issue | Fix |
|---|---|
| Google popup blocked | Allow popups for your site in the browser |
| `auth/unauthorized-domain` | Add the domain in Firebase → Auth → Authorized domains |
| `auth/configuration-not-found` | Verify the `firebaseConfig` in `src/firebase.js` |
| OTP emails not arriving | Update the Gmail address + App Password in `src/server.js`, or set `GMAIL_USER` / `GMAIL_PASS` |
| Static site shows a blank page | Serve it over HTTP (`npx serve dist`) instead of opening `file://` directly |
| Port already in use | Vite automatically selects the next free port; the OTP server uses 4000 |
| Wrong Firebase project | Use your own Firebase project rather than `careernova-3cacc` unless you own it |

---

*Generated from the actual source code — CareerNova by Aakash Kumar Arya · © 2026*