# ALEXA Next Upgrade: Wake Word, Browser Memory, and Quick Commands

This update adds the following to the browser demo:

- Optional hands-free **“Hey Alexa”** wake-word mode using the browser Web Speech API.
- Browser-local preference memory with commands such as `Remember that my favorite language is Python` and `What do you remember?`.
- Quick local commands for the current time and date.
- Website opening for YouTube, Google, Gmail, GitHub, LinkedIn, ChatGPT, Wikipedia, Amazon India, and valid domain names.
- A help command (`help`) and buttons to inspect or clear saved browser memory.

## Run on Windows

1. Install Node.js 20 or later.
2. Extract the ZIP and open the `AWS ALEXA` folder in a terminal.
3. Copy the environment template: `Copy-Item .env.example .env` (PowerShell).
4. Install dependencies: `npm ci`.
5. Build: `npm run build`.
6. Start: `npm run dev`.
7. Open `http://localhost:3000/demo` in Chrome and allow microphone access.

## Try these commands

- `Hey Alexa, open YouTube`
- `Hey Alexa, what time is it?`
- `Hey Alexa, what is today's date?`
- `Hey Alexa, remember that my favorite language is Python`
- `Hey Alexa, what do you remember?`
- `Hey Alexa, add task: finish my assignment`
- `Hey Alexa, what are my tasks?`

## Important limitations and privacy

- Wake-word detection is **browser speech recognition**, not an always-on offline wake-word engine. Browser support varies; the tab must remain open and microphone permission must be granted. It may stop when the tab/device sleeps or the browser interrupts microphone access.
- Browser-local memory is stored in this browser profile's `localStorage`. It is not synchronized to another device and is not encrypted. Use the **Clear saved memory** button to remove it.
- Website opening is restricted to a small allowlist plus ordinary domain names. It does not launch arbitrary operating-system programs.
- This demo does not provide unrestricted desktop control, background listening, or a fully autonomous agent. Sensitive actions should require confirmation before future desktop-agent integrations.
- The original MCP task-management tools still run through the local server. AI chat with OpenAI is not added by this browser-only update.
