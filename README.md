# Brand Kit Generator — Specimen site

Single-file static frontend for the n8n **Brand Kit Generator** workflow. Deployed on Vercel.

## Setup

1. Expose n8n over HTTPS (public visitors can't reach `localhost`, and `https://` pages block `http://` calls as mixed content):
   ```bash
   ngrok http 5678
   ```
2. Set the production webhook URL at the top of `index.html`:
   ```js
   const DEFAULT_WEBHOOK_URL = 'https://YOUR-NGROK-HOST/webhook/brand-kit-generate';
   ```
   The workflow must be **ACTIVE** (published) in n8n.
3. Push to `main` — Vercel redeploys automatically once the repo is imported.

Tip: test a tunnel without redeploying via `?webhook=https://…`, e.g.
`https://brand-kit-generator-seven.vercel.app/?webhook=https://abc123.ngrok.io/webhook/brand-kit-generate`

## Notes

- Generation takes ~2 minutes (Google Fonts + LLM + validation); the client times out after 3 minutes with a specific message.
- Errors are classified in-page: timeout vs unreachable/CORS vs 404 (wrong URL or inactive workflow) vs empty kit (AI returned invalid JSON — check the n8n execution).
