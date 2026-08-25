# Anıl Akbudak — Portfolio

A single-file, zero-build personal portfolio focused on cloud security and platform engineering. Everything — HTML, CSS and JavaScript — lives in `index.html`. No frameworks, no bundler, no dependencies beyond two Google Fonts and Cloudflare analytics.

## Features

- **Dark / light theme** with a pre-paint inline script that prevents theme flash; the choice persists in `localStorage`.
- **Bilingual (EN/TR)** content via a lightweight i18n dictionary (`translations` object) and `data-i18n` / `data-i18n-chip` attributes.
- **Live GitHub activity** (unauthenticated public API, each call fails independently and silently):
  - Open issues, public repos and total commit count stat cards
  - 12-week contribution heatmap built from push events
  - Top languages bar with theme-aware colors
  - Recent opened issues list
- **Semantic color system**: cyan (`--accent`) for primary/interactive states, green (`--helper`) for status/growth indicators.
- **Ghost CTA pairing** (Projects / Contact): neutral by default, colored glow on hover only.
- **Accessibility**: focus-visible outlines, `prefers-reduced-motion` support for scroll reveals and typing animation, semantic markup.
- **Click-to-copy PGP fingerprint** with localized feedback.
- **Privacy & security policy** panel in the footer describing logging, retention (365 days, Cloudflare KV) and cookie stance.

## Structure

```
index.html        # The entire site (HTML + CSS + JS)
README.md
```

### External integrations

| Integration | Purpose | Location in file |
|---|---|---|
| Cloudflare Worker (`SECURITY_ENDPOINT`) | Security telemetry — logs IP/User-Agent to Cloudflare KV for abuse/anomaly detection | end of main `<script>` |
| Cloudflare Web Analytics beacon | Privacy-friendly traffic analytics | bottom of `<body>` |
| GitHub REST API | Live activity data | `// Live GitHub data` section |

## Deployment

Static hosting is enough — no server-side code required.

**Cloudflare Pages (recommended, matches existing integrations):**

1. Push this folder to a Git repository.
2. In Cloudflare Pages, create a project from the repo.
3. Build command: *none*, output directory: `/`.
4. Deploy.

Any static host (Netlify, GitHub Pages, nginx) works as well.

## Customization

- **Colors**: edit the design tokens under `:root[data-theme="dark"]` and `:root[data-theme="light"]` (`--accent`, `--helper`, glows, language-bar ladder `--l1..--l5`).
- **Content/translations**: edit the `translations` object at the top of the script. Static HTML defaults should mirror the EN dictionary so first paint matches.
- **GitHub repo binding**: change `data-repo="user/repo"` on the hidden `#ghProfileStats` element.
- **Telemetry endpoint**: replace `SECURITY_ENDPOINT` if you fork this site — remove the block entirely if you don't operate your own worker.
- **Analytics token**: replace the `data-cf-beacon` token with your own Cloudflare Web Analytics token.

## Privacy

The site collects only what the published policy describes: IP address and User-Agent for network security and anomaly detection, stored in Cloudflare KV for a maximum of 365 days, then permanently destroyed. No advertising, profiling or third-party tracking cookies are used. See the privacy & security panel in the footer for the full policy.

## License

© Anıl Akbudak. All rights reserved unless otherwise noted.
