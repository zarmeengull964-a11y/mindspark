 Project Overview
MindSpark is a web-based EdTech platform designed to teach students programming languages in an interactive and engaging way. Similar in concept to W3Schools or freeCodeCamp, it features a custom UI, a built-in authentication system, a quiz engine, progress tracking, and a certificate generator — all in one application.

Tech Stack

Layer	Technology	Version
Frontend Framework	React	18.3.1
Build Tool	Vite	7.0.0
Routing	React Router DOM	6.26.2
Styling	Bootstrap + Custom CSS	5.3.3
Authentication	Google OAuth + LocalStorage	@react-oauth/google ^0.13.5
Backend (Optional)	PHP REST API	Custom endpoints

Project Structure
mindspark_fixed/
├── src/
│   ├── pages/          All main pages (Home, CoursePage, Quiz...)
│   ├── components/     Reusable UI components (Navbar, Footer...)
│   ├── context/        Global state (Auth, Theme, Progress, Toast)
│   ├── data/           Course content, quizzes, assignments
│   └── utils/          Helper functions (notes, scroll)
├── .env                Google OAuth Client ID & API base URL
├── index.html          App entry point
└── vite.config.js      Vite build configuration

Pages & Routes

Route	Page	Description
/	Home	Hero section, course cards, and features showcase
/course/:language	CoursePage	Topic-wise lesson viewer with live code preview
/tutorials	Tutorials	Curated video tutorials listing
/reference	Reference	Quick syntax reference cards
/exercises	Exercises	Coding exercises and assignments
/quiz	Quiz	Multiple-choice quiz per topic
/progress	Progress	Visual learning progress tracker
/certificate	Certificate	Downloadable course completion certificate
/pdfs	PDFs	PDF notes and study resources
/chatbot	Chatbot	AI-powered assistant for learner help
/tools	Tools	Developer utility tools
/login	Login	User login page
/signup	Signup	New user registration page

Available Courses
MindSpark currently includes two complete programming courses:

Course	Topics	Features
HTML	18 topics	Introduction to mini-project, live preview, YouTube videos
CSS	16 topics	Flexbox, Grid, Animations, Responsive Design, Variables
JavaScript	Planned	Full JS curriculum coming soon

Each course includes:
•Multiple lessons with live in-browser code previews (iframe-based)
•A syntax quick-reference table
•Embedded YouTube video links for each topic
•Related exercises and quizzes

Authentication System
MindSpark uses a dual-mode authentication system that works both offline and online.

1. Local Authentication (Offline-first)
•User accounts are stored in the browser's localStorage
•Passwords are hashed using SHA-256 via the Web Crypto API
•Signup and login work fully offline without any backend

2. Google OAuth
•Powered by the @react-oauth/google library
•User details are extracted from the Google JWT credential
•One-click sign-in experience

3. PHP Backend (Optional Sync)
•If a backend is available, syncs to /login.php, /signup.php, and /google.php
•Gracefully falls back to localStorage if the network is unavailable

Key Features

Feature	Description
Dark / Light Theme	App-wide theme toggle managed via ThemeContext
Progress Tracking	Per-course and per-topic progress stored via ProgressContext
Toast Notifications	Global success and error messages via ToastContext
Error Boundary	Graceful error handling — prevents full app crashes
Scroll to Top	Automatically scrolls to top on every route change
Accessibility	Skip link, ARIA attributes, and semantic HTML throughout
Auth Gate	Certain features require login, enforced by AuthGateContext
Signup Modal	Inline signup modal — no redirect needed
PDF Resources	Downloadable PDF notes in the resources section
AI Chatbot	Dedicated chatbot page for learner assistance
Certificate Generator	Generates a personalized certificate on course completion
Code Editor Promo	Interactive live code editor section on the homepage

State Management (Context API)
The app uses five nested React Context Providers for global state:
•ThemeProvider — Manages dark/light mode across the app
•AuthProvider — Handles user auth state: login, signup, logout, Google login
•ProgressProvider — Tracks course and topic completion progress
•ToastProvider — Provides a global notification/toast system
•AuthGateProvider — Controls access to protected features

Setup & Installation

Prerequisites
•Node.js (latest LTS version recommended)
•npm or yarn
•A Google OAuth Client ID (optional, only needed for Google login)

Installation Steps
Step 1 — Unzip and navigate into the project:
unzip mindsparkfinal.zip && cd mindspark_fixed

Step 2 — Install dependencies:
npm install

Step 3 — Set up the environment file:
cp .env.example .env
# Add your Google OAuth Client ID inside .env

Step 4 — Start the development server:
npm run dev

Step 5 — Build for production:
npm run build

Environment Variables

Variable	Description	Default Value
VITE_GOOGLE_CLIENT_ID	Your Google OAuth Client ID	Pre-set in .env
VITE_API_BASE	URL of the PHP backend	http://localhost/backend

Summary
MindSpark is a full-featured EdTech React application that includes:
•Complete HTML and CSS courses with live in-browser code previews
•Robust dual-mode authentication (local storage + Google OAuth)
•Learning progress tracking and certificate generation
•A quiz engine and coding exercises
•An AI chatbot for learner support
•A PDF resources section
•Dark and light theme toggle
•Fully responsive design built with Bootstrap

The PHP backend is entirely optional. The app runs as a fully standalone frontend application using localStorage, making it easy to deploy anywhere without a server.
- AI Chatbot (`/chatbot`)
- PDF notes (`/pdfs`)
- Progress, Quiz submissions, Certificate
