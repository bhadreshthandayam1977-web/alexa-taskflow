# ALEXA Ultimate — Voice-Controlled Personal Assistant

This project builds on your AWS ALEXA TaskFlow code and provides a Alexa-style browser interface with voice commands, spoken responses, website/search shortcuts, browser-local task management, optional OpenAI-powered chat, and a restricted Windows desktop-action endpoint.

## Start on Windows
1. Install Node.js 20 or newer (Node 22 LTS recommended).
2. Open PowerShell in this folder.
3. Run `Copy-Item .env.example .env` (skip if `.env` already exists).
4. Run `npm ci`.
5. Run `npm run build`.
6. Run `npm run dev`.
7. Open `http://localhost:3000/demo` in Chrome and allow microphone access.

## Enable AI answers (optional)
Edit `.env` on the server and set `OPENAI_API_KEY=your_key_here`. Keep the key private; do not put it in browser code or commit `.env`. Set `OPENAI_MODEL=gpt-4.1-mini` or another model available to your account. Restart the server after editing. API usage may cost money.

## Try these commands
- “What time is it?”
- “What is today's date?”
- “Open YouTube” / “Open Gmail” / “Open GitHub”
- “Search for Python tutorials”
- “Add task finish my assignment” / “Show my tasks”
- “Open Calculator” / “Open Notepad” / “Open Downloads folder” (Windows only)
- Ask a general question (requires AI key)

## Safety and honest limitations
- Browser wake-word listening is not a guaranteed always-on hotword service; browser/device permissions and speech-recognition support apply.
- Desktop commands are Windows-only and allowlisted. This does not run arbitrary shell commands or provide unrestricted computer control.
- Do not expose this development server to the public internet. Keep API keys private.
- Sending messages, deleting files, purchases, changing security settings, or other consequential actions should require confirmation and additional permissioned integrations.
- “Top level” does not mean equivalent to fictional Iron Man ALEXA; this is a runnable starter project that can be extended and tested feature-by-feature.

## Useful endpoints
- Demo: `http://localhost:3000/demo`
- Health check: `http://localhost:3000/healthz`

## Troubleshooting
- If `npm ci` fails, confirm Node.js version with `node --version`, then retry on a stable internet connection.
- If the build fails, copy the full terminal error for debugging.
- If microphone recognition is unavailable, use Chrome and check site microphone permissions.
- If AI says it is not configured, verify `.env` and restart the server.
