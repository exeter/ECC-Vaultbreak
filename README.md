# Vaultbreak

A single-screen, minimalist site for testing LLM prompt security, inspired by [vaultbreak.ai](https://vaultbreak.ai).

- Define a **vault** — a system prompt plus a forbidden action (e.g. `allowAccess`).
- Attempt to **jailbreak** the LLM via a chat interface.
- An auto-judge detects when the vault performs the forbidden action and flags the breach.

 Chat uses one of three selectable models routed through [OpenRouter](https://openrouter.ai): GPT-5 nano (easy), GLM 5.3 Flash (medium), or GPT-5 mini (hard). Breach detection uses the fixed GPT-5.6 Terra model. Your API key is entered in the UI and stored only in your browser's localStorage — it is never sent anywhere except OpenRouter.

## Run

```bash
npm start
```

Then open <http://localhost:3000>.

## Usage

1. On first load, paste your OpenRouter API key in the settings dialog (⚙).
2. Edit the system prompt and forbidden action on the left.
3. Chat on the right and try to make the model break its rules.

High and max reasoning modes can use a large portion of a model's generation budget before producing a visible answer. Vaultbreak uses larger role-specific budgets and retries once with a larger budget when a response is empty or truncated. Failed responses are not added to the conversation history, and the original prompt is restored for retrying. A breach is only marked safe when the detector returns a valid visible `VERDICT: YES` or `VERDICT: NO`; unavailable or incomplete judge responses are shown as undetermined.

## Stack

- `public/` — static frontend (vanilla HTML/CSS/JS, no build step)
- `server.js` — tiny zero-dependency static file server
