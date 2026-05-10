# yesilyelek-legal

Static, server-rendered legal pages for the Yeşil Yelek app. Hosted on
**GitHub Pages** at `https://legal.yesilyelek.com/` (custom domain via
CNAME).

This repo exists separately from the main app/landing-page repos because:

1. **Meta + Google's link unfurlers do not execute JavaScript.** The main
   landing page (`yesilyelek.com`) is a React SPA that returns an empty
   `<div id="root"></div>` shell on direct GET. A privacy/ToS/data-deletion
   URL must serve real HTML in the initial response. Static files via
   GitHub Pages do this without any build step.
2. **Independent infrastructure.** Bypasses any rate-limiting / WAF /
   anti-DDoS layer in front of the main domain that might 403 social
   crawlers.

## Files

| File | Hosted at | Purpose |
| --- | --- | --- |
| `index.html` | `legal.yesilyelek.com/` | Landing page linking the three documents |
| `delete-account.html` | `legal.yesilyelek.com/delete-account.html` | Meta-required user data deletion instructions |
| `privacy-policy.html` | `legal.yesilyelek.com/privacy-policy.html` | Privacy policy (Meta + Google Play) |
| `terms.html` | `legal.yesilyelek.com/terms.html` | Terms of service |
| `styles.css` | `legal.yesilyelek.com/styles.css` | Shared CSS, loaded by every HTML page |
| `robots.txt` | `legal.yesilyelek.com/robots.txt` | Explicit allowlist for FB/Meta/Google/Twitter crawlers |
| `CNAME` | (auto-created by GitHub Pages) | Contains `legal.yesilyelek.com` |

All HTML pages are bilingual (Turkish first, English second) with a clear
language divider.

## Where these URLs are referenced externally

- **Meta App Dashboard → Settings → Basic**
  - Privacy Policy URL: `https://legal.yesilyelek.com/privacy-policy.html`
  - Terms of Service URL: `https://legal.yesilyelek.com/terms.html`
  - User data deletion: `https://legal.yesilyelek.com/delete-account.html`
- **Google Play Console → App content**
  - Privacy Policy URL: `https://legal.yesilyelek.com/privacy-policy.html`

## Maintenance

- These documents must stay in sync with the app's actual data flows. If
  you add a new third-party SDK that processes user data (e.g. an
  analytics provider, a new auth provider), update the relevant section
  in `privacy-policy.html` **before** shipping.
- The "Last updated" date is at the bottom of every page. Bump it on any
  user-facing edit.
- These files are **legal-template content**, not legal advice. Have a
  lawyer review before relying on them in production. Adjust governing
  law, contact details, and jurisdiction-specific clauses to your actual
  business.

## Deploy

Pure GitHub Pages, no build:

1. Push to `main` — GitHub Pages publishes within ~1 minute.
2. First-time setup:
   - Settings → Pages → Source: `Deploy from a branch` → `main` / `(root)`
   - Custom domain: `legal.yesilyelek.com`
   - Enforce HTTPS: ✓ (becomes available after DNS resolves)
3. DNS (one-time at your registrar):
   ```
   legal.yesilyelek.com.  CNAME  <github-username>.github.io.
   ```
