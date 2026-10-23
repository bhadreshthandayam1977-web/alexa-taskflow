# ALEXA voice assistant guide

This adds a Alexa-style browser assistant to the existing Alexa TaskFlow project. It supports browser voice recognition where available, spoken responses, a small set of safe commands, website opening, web searches, a browser-local task list, and optional OpenAI-powered answers.

## Requirements
- Node.js 20.6+ (Node 22 LTS recommended)
- A modern browser; Chrome is recommended for Web Speech API support
- Internet connection for AI mode and web search

## Windows setup
1. Extract the ZIP.
2. Open PowerShell in the `AWS ALEXA` folder.
3. Copy `.env.example` to `.env`:
   ```powershell
   Copy-Item .env.example .env
   ```
4. Install packages:
   ```powershell
   npm ci
   ```
5. Build and run:
   ```powershell
   npm run build
   npm run dev
   ```
6. Open `http://localhost:3000/demo` in Chrome. Allow microphone access when prompted.

## Optional AI setup
Open `.env` in a text editor and set `OPENAI_API_KEY` to your own API key. Keep `.env` private and never commit it or paste the key into the browser. Restart the server after changing it. The AI endpoint uses the OpenAI Responses API and `OPENAI_MODEL` (default `gpt-4.1-mini`). API usage may incur charges.

## Example commands
- “What time is it?”
- “What is today's date?”
- “Open YouTube” / “Open Gmail” / “Open Google” / “Open GitHub”
- “Search for Python tutorials”
- “Add task finish my assignment”
- “Show my tasks”
- “Help”

Tasks are stored in the current browser's local storage. Clearing browser data removes them. Website opening and task commands work without an OpenAI key. General questions use AI mode when configured.

## Important limits
This is a practical starter assistant, not a full system-level agent. A webpage cannot safely or reliably control all desktop applications, send messages, access private accounts, or change system settings without additional integrations and explicit permissions. The current version does not execute arbitrary shell commands. Ask for confirmation before adding consequential actions such as sending messages, deleting files, or purchases.

## Expanded local ALEXA commands

On Windows, while the server is running locally, the demo can open these allowlisted applications: Notepad, Calculator, Paint, File Explorer, and Task Manager. It can open the Desktop, Documents, Downloads, and Pictures folders. Try commands such as `Open Calculator`, `Open Notepad`, or `Open Downloads folder`.

Desktop actions are restricted to loopback requests and fixed application/folder allowlists; arbitrary shell commands, shutdown, deletion, and unrestricted file access are not implemented. Do not expose this development server directly to the internet. Browser speech recognition depends on browser support and microphone permissions. General AI chat needs `OPENAI_API_KEY` in the server `.env` file and may incur API charges.
