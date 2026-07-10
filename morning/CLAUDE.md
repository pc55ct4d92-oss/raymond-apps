# Morning App

## Git & Deployment
- This project is fully committed to GitHub and has been for many sessions
- DO NOT assume any directory is new or uncommitted
- Always run `git status` before any git assumptions
- Frontend deploys via Vercel (auto-deploy on push to main)
- Backend deploys via Railway (auto-deploy on push to main)
- Never skip .gitignore — .env files are already excluded

## Project structure
- `frontend/` — React + Vite → Vercel
- `backend/` — Node.js + Express → Railway
- `backend/` has its own git repo (separate from the parent raymond-apps repo)

## Known issues / gotchas

### USCCB daily readings parsing (`backend/routes/missal.js`)
- Readings are fetched from the USCCB daily email via Gmail API
- USCCB has used both Roman numerals (`Reading I`) and digits (`Reading 1`) for reading labels — both are handled
- USCCB has used `"Responsorial Psalm"`, `"Responsorial"`, and bare `"Psalm"` for the psalm label — all handled via `startsWith('responsorial')` or `startsWith('psalm')` (case-insensitive)
- If a reading stops showing, check Railway logs for `h4:` debug output to see what label format the email is using
- The Gmail OAuth refresh token lives in Railway env vars as `GOOGLE_REFRESH_TOKEN`. If it expires, run `node reauth.js` in `backend/` from a regular terminal (not Claude Code), sign in with `p.raymond.newsletters@gmail.com`, and update the token in Railway
- The Google OAuth app is **In production** (not Testing), so tokens should not expire on a 7-day cycle
