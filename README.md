# Vaultbreak

A single-screen, minimalist site for testing LLM prompt security, inspired by [vaultbreak.ai](https://vaultbreak.ai).

- Define a **vault** — a system prompt plus a forbidden action (e.g. `allowAccess`).
- Attempt to **jailbreak** the LLM via a chat interface.
- An auto-judge detects when the vault performs the forbidden action and flags the breach.

The model is **GLM 5.3 Flash** (`z-ai/glm-5.3-flash`) routed through [OpenRouter](https://openrouter.ai). Your API key is entered in the UI and stored only in your browser's localStorage — it is never sent anywhere except OpenRouter.

## Run

```bash
npm start
```

Then open <http://localhost:3000>.

## Usage

1. On first load, paste your OpenRouter API key in the settings dialog (⚙).
2. Edit the system prompt and forbidden action on the left.
3. Chat on the right and try to make the model break its rules.

## Stack

- `public/` — static frontend (vanilla HTML/CSS/JS, no build step)
- `server.js` — tiny zero-dependency static file server
