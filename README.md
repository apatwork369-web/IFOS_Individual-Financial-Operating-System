# IFOS — Individual Financial Operating System (Scorecard Prototype)

Interactive prototype of the **IFOS Household Money Score** questionnaire.

- **Client side:** game-style 40-question scorecard + conditional add-ons, score reveal, free check-up CTA. No formulas, points, or advisor logic visible.
- **Advisor side:** locked console (🔒 Advisor, top-right) with submissions table, per-client diagnostic, section score bars, lowest/highest areas, suggested conversation track, JSON export.
- Single self-contained file: `index.html`. No build step, no dependencies, no server code.

## Run locally

Download `index.html` and double-click it — it opens in any modern browser.

## Host free on GitHub Pages (recommended for the test run)

1. Create the repository (e.g. `ifos-scorecard`) on GitHub — keep it **Public** (Pages on private repos requires a paid plan).
2. Upload `index.html` and `README.md` (drag-and-drop via **Add file → Upload files**, or use git — see below).
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Branch: `main`, Folder: `/ (root)` → **Save**.
6. Wait 1–2 minutes. Your live link appears at the top of the Pages settings:
   `https://<your-username>.github.io/ifos-scorecard/`
7. Share that link with friends and family for the test run.

### Using git from the command line

```bash
git clone https://github.com/<your-username>/ifos-scorecard.git
cd ifos-scorecard
# copy index.html and README.md into this folder, then:
git add .
git commit -m "IFOS scorecard prototype v1"
git push origin main
```

Any future edits: change `index.html`, commit, push — the live page updates automatically in ~1 minute.

## Configuration

Open `index.html` and edit the `IFOS_CONFIG` block near the top of the `<script>` section:

- `bookingUrl` — paste your booking/calendar link for the "Book My Free Check-up" button.
- `advisorCodeHash` — SHA-256 hash of the advisor access code. The code itself is never stored in the file and cannot be recovered from the hash. Default demo code: `IFOS-ADVISOR-2026`.
  To set a new code, run this in the browser console and paste the printed hash into `advisorCodeHash`:
  ```js
  crypto.subtle.digest("SHA-256", new TextEncoder().encode("YOUR-NEW-CODE")).then(b=>console.log([...new Uint8Array(b)].map(x=>x.toString(16).padStart(2,"0")).join("")))
  ```

## Demo shortcuts

Append to the URL for quick demos:

- `?screen=question` — jump into the questionnaire
- `?screen=results` — sample results screen
- `?screen=admin` — opens the advisor login (access code still required; no bypass)
- `?screen=login` — advisor login modal

## Important limits (prototype)

- **Submissions are stored in each visitor's own browser only** (localStorage). They do not sync to you. For the test run, ask testers to screenshot their result, or check the advisor console on the same device they used.
- **The advisor login is hash-protected but still client-side.** The access code cannot be extracted from the source (only its SHA-256 hash is stored). However, the advisor console *layout* code is visible to anyone reading the source, and submissions live unencrypted in the browser’s localStorage on the device where they were made. Do not collect real sensitive client data with this version.
- Before public launch: connect a real form backend / CRM (e.g. GoHighLevel, webhook, Google Sheet endpoint) and real authentication so advisor data never lives in the client page.

## Disclaimer

This scorecard is educational and does not replace personalized financial, tax, legal, investment, or insurance advice.
