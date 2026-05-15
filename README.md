 MindSpark — v5 (updated)

## What changed in this update

- **Single Sign Up button in the navbar.** Clicking it opens a modal with both **Login** and **Sign Up** tabs. The duplicate "Sign In" button is gone.
- **Search bar is wider** now that the duplicate button is removed (desktop only — search collapses into the mobile drawer on small screens).
- **AI Chatbot icon refreshed.** Replaced the ✨ emoji with a proper sparkle SVG icon that follows the theme color.
- **Mobile hamburger drawer** now includes a **Home** link, plus Sign Up / Login buttons at the top and the search field.
- **Continue with Google** works as soon as you set `REACT_APP_GOOGLE_CLIENT_ID` (see `.env.example`).
- **PHP backend bug fixed** (`PDO::ATTR_ERRFMODE` → `PDO::ATTR_ERRMODE`) and `backend/data/` is pre-created so signup writes succeed on a fresh install.
- Auth flow stays exactly the same: backend stores users (`backend/data/user.json`), issues a Bearer token, and gates the chatbot/PDF features through `useAuthGate`.

## Run on XAMPP (Windows)

1. **Copy the project** into `C:\xampp\htdocs\mindspark` so the folder is `htdocs/mindspark/{src, backend, public, package.json, ...}`.
2. **Start Apache** from the XAMPP control panel. (MySQL is not required — users are saved to `backend/data/user.json`. The MySQL `schema.sql` is only there if you later want to migrate.)
3. **Test the backend** by opening:
   `http://localhost/mindspark/backend/login.php`
   You should see `{"ok":false,"error":"Email and password required."}`. If you instead see PHP source code or a 404, Apache isn't serving the folder — check the path.
4. **Install Node deps and start the React app:**
   ```bash
   cd C:\xampp\htdocs\mindspark
   npm install
   npm start
   ```
   The app opens at `http://localhost:3000`.
5. **Configure environment (optional but recommended).** Copy `.env.example` to `.env` in the project root, then restart `npm start`:
   - `REACT_APP_API_BASE` — leave the default if your folder is `htdocs/mindspark`.
   - `REACT_APP_GOOGLE_CLIENT_ID` — paste your Google OAuth Web Client ID to enable "Continue with Google". Leave empty to hide the button.

## Google Sign-In setup (5 minutes)

1. Go to https://console.cloud.google.com/apis/credentials → **Create Credentials → OAuth client ID → Web application**.
2. Authorized JavaScript origins: `http://localhost:3000` (and your production URL when deploying).
3. Copy the **Client ID** into `.env` as `REACT_APP_GOOGLE_CLIENT_ID=...` and restart `npm start`.
4. The "Continue with Google" button appears at the top of the Sign Up modal. The PHP `backend/google.php` verifies the token against Google's `tokeninfo` endpoint, creates the user if new, and returns a session token.

## Troubleshooting

- **"PHP backend is not running"** → Apache is not started, or the `REACT_APP_API_BASE` URL doesn't match where the `backend` folder lives. Open the URL above (step 3) in a browser to verify.
- **Sign Up button does nothing** → Open DevTools → Console. The modal is wired up via `AuthGateContext`; if you see a React error here it usually means a stale build — stop `npm start`, run `npm install`, then `npm start` again.
- **Permission denied writing user.json** → Right-click `backend/data` → Properties → Security → give Apache (`Users` on Windows) write permission. The folder is created automatically; it just needs to be writable.
- **Google button missing** → `REACT_APP_GOOGLE_CLIENT_ID` is empty or you didn't restart `npm start` after editing `.env`.

## Routes that require sign-in

These features call `requireAuth(...)` from `useAuthGate`, so they automatically pop the Login modal for guests:
- AI Chatbot (`/chatbot`)
- PDF notes (`/pdfs`)
- Progress, Quiz submissions, Certificate
