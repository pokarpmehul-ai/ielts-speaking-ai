# IELTS Speaking AI Assessment — Vercel + OpenRouter

This starter project contains a complete practice flow for IELTS Speaking Parts 1, 2 and 3, browser-based speech-to-text (where supported), editable transcripts, and AI feedback through OpenRouter.

## Important scope
- This project sends **text transcripts** to OpenRouter, not audio.
- Browser speech recognition is supported in some browsers (commonly desktop Chrome) and may depend on the browser's speech service and microphone permissions.
- Students can edit/paste transcripts if speech recognition is unavailable.
- Assessment covers Fluency and Coherence, Lexical Resource, and Grammatical Range and Accuracy only. It does not score pronunciation.
- Since assessment is transcript-based, actual pauses, speech speed, pronunciation, and delivery cannot be reliably assessed.
- AI scores are estimates for practice, not official IELTS results.

## Files
- `index.html` — the complete single-page practice website.
- `api/assess-speaking.js` — Vercel serverless endpoint that calls OpenRouter.

## Deploy as a new Vercel project
1. Create a new **private** GitHub repository, e.g. `ielts-speaking-ai`.
2. Put `index.html` in the repository root and keep the `api` folder at the root.
3. Import that repository as a **new project** in Vercel.
4. In Vercel → Project → Settings → Environment Variables, add:
   - `OPENROUTER_API_KEY` = your secret OpenRouter API key
   - `OPENROUTER_MODEL` = `openai/gpt-4o-mini` (or another supported chat model that follows JSON mode)
   - Optional: `SITE_URL` = your deployed site URL
5. Redeploy after adding environment variables.
6. Open the deployment URL, allow microphone access, select a part, start speech-to-text, speak, stop transcription, review/edit the transcript, and click **Assess this answer with AI**.
7. To assess all parts together, fill transcripts in each part (navigate between parts; they are saved in this browser's local storage) and click **Assess complete test**.

## OpenRouter API key
Create/manage a key at https://openrouter.ai/keys. Keep it only in Vercel Environment Variables. Never place it in `index.html`, commit it to GitHub, or expose it in client-side JavaScript.

## Costs and limits
OpenRouter model usage may cost money depending on the model and account. Check the model pricing before use. Vercel Hobby has usage limits and is for personal/non-commercial use under Vercel's terms. Vercel Functions have a 4.5 MB request-body limit, but this project sends text only, not audio, so it avoids large audio upload payloads.

## Security before public launch
This is a starter, not a production-hardened service. Before allowing public use:
- Add authentication or rate limiting to prevent API abuse and unexpected charges.
- Consider a CAPTCHA or other abuse prevention.
- Add privacy/consent wording and a retention policy if you store student information.
- Consider logging request IDs and safe error details, but never log API keys.
- Restrict allowed transcript length and consider per-user quotas.

## Troubleshooting
- `OPENROUTER_API_KEY` missing: set it in Vercel environment variables and redeploy.
- Model not found / provider error: choose a currently available model slug in OpenRouter and set `OPENROUTER_MODEL`.
- Speech recognition not supported: use a supported browser or type/paste the transcript.
- Assessment returns a provider/model error: check OpenRouter account credits, model availability, and Vercel Function logs.
