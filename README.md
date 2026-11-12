# monitor.dabotap.com

Static landing page, privacy policy and support page for Baby Monitor. No build step and no
JavaScript. The live site is published from the public **`chiefbrob/monitor-site`** repo via GitHub
Pages, with Cloudflare DNS pointing `monitor.dabotap.com` at it.

## Source

- `index.html` — landing
- `privacy.html` — Play privacy policy (also `/privacy` through Cloudflare/Pages rules where supported)
- `support.html` — FAQ
- `screenshots/` — app captures used by the phone mockup
- `CNAME` — `monitor.dabotap.com`
- `.nojekyll` — keep GitHub Pages from running Jekyll

## Publish

```bash
scripts/publish-site.sh
```

That copies this folder into `chiefbrob/monitor-site` and pushes. GitHub Pages rebuilds in a minute
or two; Cloudflare may serve a cached copy for up to ten minutes.

The older Cloudflare Pages workflow in the app repo (`.github/workflows/site.yml`) is retained but is
not the live path. Do not point the domain at both hosts.

## Before publishing

- Keep `site/privacy.html` in step with `docs/PRIVACY.md` and the Play Data safety form, including the
  AdMob advertising section.
- Replace `brian@dabotap.com` if the support inbox changes.
- Do not add analytics, tracking pixels or a mailing-list form.
