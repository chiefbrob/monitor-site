# monitor.dabotap.com

Static landing page, privacy policy and support page for Baby Monitor. No build step and no
JavaScript. The live site is published from the public **`chiefbrob/monitor-site`** repo via GitHub
Pages, with a proxied Cloudflare CNAME for `monitor.dabotap.com` in front of it.

## Source

- `index.html` — landing
- `privacy.html` — Play privacy policy
- `support.html` — FAQ
- `fgs-microphone.html` — Play Console demo: microphone foreground service
- `fgs-camera.html` — Play Console demo: camera foreground service
- `videos/` — the two demo MP4s and their posters
- `screenshots/` — app captures used by the phone mockup
- `CNAME` — `monitor.dabotap.com`
- `.nojekyll` — keep GitHub Pages from running Jekyll

## Publish

```bash
scripts/publish-site.sh
```

That copies this folder into `chiefbrob/monitor-site` and pushes. GitHub Pages rebuilds in a minute
or two; Cloudflare may serve a cached copy for up to ten minutes.

The older Cloudflare Pages workflow in the app repo (`.github/workflows/site.yml`) is manual-only
and is not the live path. Do not point the domain at both hosts.

## HTTPS

`monitor.dabotap.com` is a **proxied** Cloudflare CNAME to `chiefbrob.github.io`. Cloudflare
terminates TLS with the zone's `*.dabotap.com` certificate and GitHub Pages serves the files. Keep
the record proxied: with it switched to DNS-only, GitHub presents its `*.github.io` certificate and
every browser shows a name-mismatch error. Resolvers that cached the DNS-only answer keep the error
until that old TTL expires, even after the proxy is restored.

Check the edge directly when a browser still complains:

```bash
dig +short @adele.ns.cloudflare.com monitor.dabotap.com A
curl -sSI --resolve monitor.dabotap.com:443:<edge-ip> https://monitor.dabotap.com/
```

## Before publishing

- Keep `site/privacy.html` in step with `docs/PRIVACY.md` and the Play Data safety form. The app has
  no ad SDK; the policy must stay that way unless the product changes.
- Replace `brian@dabotap.com` if the support inbox changes.
- Do not add analytics, tracking pixels or a mailing-list form.
