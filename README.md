<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://ai.google.dev/static/site-assets/images/share-ais-513315318.png" />
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/6311a953-2a53-4276-bdfd-5ac4b5296cf0

## Run Locally

**Prerequisites:**  Node.js

1. Install dependencies:
   `npm install`
2. Set the `GEMINI_API_KEY` in [.env.local](.env.local) to your Gemini API key
3. Run the app:
   `npm run dev`

## Voice ordering assistant (ElevenLabs)

The "Talk To Order" button uses an ElevenLabs Conversational AI agent (it replaces a previous
Vapi integration). One-time setup:

1. Put your ElevenLabs **secret** API key in a local `.env` file (already gitignored):
   ```
   ELEVENLABS_API_KEY=
   ```
   ⚠️ If this key has ever been pasted into a chat, doc, or screenshot, treat it as compromised
   and rotate it in the ElevenLabs dashboard before using it here.
2. Run the one-time setup script to create the agent:
   ```
   node scripts/create-elevenlabs-agent.mjs
   ```
   This prints an **Agent ID**.
3. Paste that Agent ID into `ELEVENLABS_AGENT_ID` near the top of `src/App.tsx`. The Agent ID is
   safe to keep in the front-end code — it is not a secret, the same way the old Vapi assistant
   ID wasn't.
4. In the ElevenLabs dashboard, open the agent and add a **Client tool** named exactly
   `fill_order_form` (Tools tab) with parameters `customer_name`, `mobile_number`,
   `delivery_address`, `notes`, and `items` (array of `{ product_id, quantity }`). Tick
   "Wait for response". Then in the Advanced tab, make sure authentication is **disabled** so
   the public Agent ID works directly from the browser.

Your secret API key is only ever used by the local setup script — it never goes into the
website's code or bundle.

