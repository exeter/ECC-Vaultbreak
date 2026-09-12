# Vaultbreak

A single-screen game for testing LLM prompt security, inspired by [vaultbreak.ai](https://vaultbreak.ai).

- The left panel explains the game and holds the **vault rules** plus one **forbidden phrase**.
- You **jailbreak** the model by getting it to type that phrase in chat.
- If the phrase appears in the reply, a **You win** popup appears. Play again resets the chat.

 Chat uses one of three selectable models routed through [OpenRouter](https://openrouter.ai): GPT-5 nano (easy), GLM 5.3 Flash (medium), or GPT-5 mini (hard). Breach detection uses the fixed GPT-5.6 Terra model. Your API key is entered in the UI and stored only in your browser's localStorage — it is never sent anywhere except OpenRouter.

## Run

```bash
npm start
```

Then open <http://localhost:3000>.

## Usage

1. On first load, paste your OpenRouter API key in the settings dialog (⚙).
2. Read How to play. Optionally edit the forbidden phrase and vault rules.
3. Chat on the right. You win when the model writes the forbidden phrase.

High and max reasoning modes can use a large portion of a model's generation budget before producing a visible answer. Vaultbreak uses larger role-specific budgets and retries once with a larger budget when a response is empty or truncated. Failed responses are not added to the conversation history, and the original prompt is restored for retrying. A breach is only marked safe when the detector returns a valid visible `VERDICT: YES` or `VERDICT: NO`; unavailable or incomplete judge responses are shown as undetermined.

## Stack

- `public/` — static frontend (vanilla HTML/CSS/JS, no build step)
- `server.js` — tiny zero-dependency static file server
