# signaldelta-website

Public-facing holding page for `signaldelta.ai`. Static HTML, no build step, hosted on GitHub Pages.

## Branch isolation

Separate from `signaldelta-portal-preview` (which is the dev/preview tool for the operator-facing portal). Public website and dev portal are different concerns — keep the repos isolated.

## Files

- `index.html` — the entire site, single file, inlined CSS, no JS
- `CNAME` — tells GitHub Pages to serve at `signaldelta.ai`

## Deployment

### One-time setup

1. **Create the repo on GitHub** (use the SignalDelta GitHub account, not personal):
   - Name: `signaldelta-website`
   - Public
   - No README, no .gitignore, no license at creation time — we have our own files

2. **Push these files** to the `main` branch:
   ```
   index.html
   CNAME
   README.md
   ```

3. **Enable GitHub Pages**:
   - Repo Settings → Pages
   - Source: Deploy from a branch
   - Branch: `main` / root
   - Save
   - Wait ~1 min, then verify the github.io URL works (it'll show in the Pages settings panel)

4. **Configure DNS at Namecheap** (`signaldelta.ai` domain):
   - Namecheap dashboard → Domain List → `signaldelta.ai` → Manage → Advanced DNS
   - Add the following records (delete any conflicting ones first):

     | Type | Host | Value | TTL |
     |------|------|-------|-----|
     | A | @ | 185.199.108.153 | Automatic |
     | A | @ | 185.199.109.153 | Automatic |
     | A | @ | 185.199.110.153 | Automatic |
     | A | @ | 185.199.111.153 | Automatic |
     | CNAME | www | `<your-gh-username>.github.io.` | Automatic |

   - The four A records are GitHub Pages' apex domain IPs (official, stable).
   - The CNAME record makes `www.signaldelta.ai` redirect to GitHub Pages too.

5. **Verify in GitHub Pages settings**:
   - Repo Settings → Pages → Custom domain: enter `signaldelta.ai`, save
   - GitHub will run DNS check. Can take 10 min to a few hours to verify.
   - Once verified, check "Enforce HTTPS" (will be greyed out until the cert provisions — ~15 min after DNS check passes)

6. **Test**:
   - `https://signaldelta.ai` → site loads
   - `https://www.signaldelta.ai` → redirects to apex
   - Mobile (iPhone Safari + Chrome) — verify layout
   - Desktop (Chrome + Safari + Firefox)

### Future updates

Edit `index.html`, commit, push. GitHub Pages redeploys in ~30 seconds.

## Open items (not blocking launch)

- **Favicon** — currently none. Add `favicon.ico` + `apple-touch-icon.png` when SignalDelta logo is finalized for web use.
- **OG image** — `og:image` meta tag not set. Add a 1200×630 social-share image once available.
- **Sitemap.xml / robots.txt** — defer until pre-launch marketing push.
- **Analytics** — none. Add Plausible or Fathom (privacy-friendly, no consent banner needed) at Phase 4 prep.

## Design notes

- Fonts: Fraunces (serif display) + JetBrains Mono (mono body). Both Google Fonts, loaded via `<link>`.
- Dark theme with a single lime-green accent (`#d4ff3a`). No purple gradients. No "AI slop" aesthetics.
- All copy pulled from `signaldelta_pitch_long.docx` (Session 1 brand launch artifact).
- Fully responsive, mobile breakpoint at 760px.
- No external JS. No tracking. No cookies.

---

*Session 2 deliverable — May 24, 2026*
