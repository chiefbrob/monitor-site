# monitor.dabotap.com

Static landing page, privacy policy and support page for Monitor. No build step and no
JavaScript. Open `index.html` directly or serve the folder:

```bash
cd site
python3 -m http.server 8899
# http://127.0.0.1:8899/
```

## Pages

| URL | File |
| --- | --- |
| `/` | `index.html` |
| `/privacy.html` (also `/privacy` via `_redirects`) | `privacy.html` — the Play privacy policy |
| `/support.html` (also `/support`) | `support.html` |
| `/screenshots/home.png` etc. | Full-height app captures used by the hero mockup |

`_headers` sets a strict CSP (no scripts, no inline styles), `_redirects` gives the short privacy and
support URLs, and `robots.txt` / `sitemap.xml` point at the canonical domain.

## Deploy

The GitHub workflow `.github/workflows/site.yml` deploys this folder to **Cloudflare Pages** on a push
that touches `site/` (or manually). It needs two repository secrets:

```bash
gh secret set CLOUDFLARE_API_TOKEN -R chiefbrob/baby-monitor   # Pages:Edit
gh secret set CLOUDFLARE_ACCOUNT_ID -R chiefbrob/baby-monitor
```

Then create the Pages project and attach the domain, once:

1. Cloudflare dashboard → Workers & Pages → Create → Pages → **Direct Upload**.
2. Project name: **`dabotap-monitor`**.
3. Run the *Deploy site* workflow (or push a `site/` change) — the first deploy creates the
   production branch.
4. Pages project → Custom domains → **`monitor.dabotap.com`**. The `dabotap.com` zone is already on
   Cloudflare; add the CNAME/Pages record it proposes.
5. Confirm `https://monitor.dabotap.com/privacy.html` loads over HTTPS without a login.
6. Put that URL in Play Console → Store listing → Privacy policy.

Without the two secrets the workflow exits with a notice and does not deploy; it does not fail the
build. The site source is always the deliverable, even when the domain is not connected yet.

## Before publishing

- Keep the privacy policy in step with the app: `docs/PRIVACY.md` and `site/privacy.html` are the
  same policy.
- Replace `brian@dabotap.com` everywhere if the support inbox changes.
- Do not add analytics, tracking pixels or a mailing-list form; the app's privacy promise and the
  Play Data safety form say there is none.
