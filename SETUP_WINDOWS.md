# Alexa TaskFlow — Windows Setup

This project is an MCP server for developer task workflows that can be connected to a compatible Alexa+/MCP client. It is **not** the official Alexa app or a standalone wake-word assistant. The included browser demo simulates voice input using your browser's speech APIs.

## Requirements

- Node.js 20 or newer
- npm (installed with Node.js)
- PowerShell or Windows Terminal

Check installation:

```powershell
node --version
npm --version
```

## Install and run

1. Extract `AWS ALEXA.zip` to a folder you can edit.
2. Open PowerShell in the extracted `AWS ALEXA` folder (the folder containing `package.json`).
3. Install dependencies:

```powershell
npm ci
```

If `npm ci` fails because the lockfile or npm cache is damaged, try `npm install`.

4. Copy `.env.example` to `.env` in the same folder. In File Explorer, enable **View → Show → File name extensions** so it does not become `.env.txt`.
5. Edit `.env` in Notepad or VS Code. For local testing, set a private token, for example:

```dotenv
PORT=3000
API_TOKEN=replace-this-with-a-long-random-secret
CORS_ORIGIN=http://localhost:3000
RATE_LIMIT_PER_MIN=60
TASK_STORE=memory
AWS_REGION=us-east-1
DYNAMODB_TABLE_NAME=alexa-taskflow-tasks
```

Keep the token private. Do not upload `.env`, paste the token into screenshots, or commit it to Git. The provided `.env.example` is a template and is not loaded automatically; the app reads environment variables from the process. For a simple local setup, either use PowerShell to set them for the current terminal before starting, or install a dotenv loader if you want `.env` to load automatically. Example for the current PowerShell session:

```powershell
$env:PORT = "3000"
$env:API_TOKEN = "replace-this-with-a-long-random-secret"
$env:CORS_ORIGIN = "http://localhost:3000"
npm run dev
```

6. Open a second PowerShell window in the project folder and check the server:

```powershell
Invoke-RestMethod http://localhost:3000/healthz
```

7. Open `http://localhost:3000/demo` in your browser for the simulated voice demo. Allow microphone permission if you want speech recognition; browser and operating-system support varies.

## Build and tests

```powershell
npm run build
npm test
npm run smoke
```

The `smoke` command is optional and expects the server to be running. If the `smoke` script is not listed in `package.json`, run `node scripts/smoke.mjs` instead.

## AWS DynamoDB mode

The default task store is in-memory. To use DynamoDB, configure `TASK_STORE=dynamodb`, `AWS_REGION`, and `DYNAMODB_TABLE_NAME`, create the table using the template in `deploy/aws/`, and configure AWS credentials using the standard AWS SDK credential chain. AWS usage may incur charges.

## API key note

This project currently uses `API_TOKEN` to protect the MCP endpoint and optionally `GITHUB_TOKEN` for GitHub API rate limits. It does **not** currently use an OpenAI API key, so adding `OPENAI_API_KEY` to `.env` alone will not enable ChatGPT-style responses. A separate OpenAI integration would need to be implemented.

## Internet deployment warning

Do not expose this server publicly without a strong `API_TOKEN`, a restrictive `CORS_ORIGIN`, HTTPS, and review of the deployment configuration. The local demo is not a production security boundary.

## ALEXA desktop commands

After opening `http://localhost:3000/demo`, try `Open Calculator`, `Open Notepad`, `Open File Explorer`, `Open Downloads folder`, or `Open Documents folder`. The local desktop endpoint supports Windows only and only a fixed allowlist. It intentionally does not execute arbitrary terminal commands or destructive actions.
