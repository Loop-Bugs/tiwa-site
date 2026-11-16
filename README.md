# TIWA site

Public static site for the TIWA research app:

- Landing page: [https://tiwa.loopbugs.com/](https://tiwa.loopbugs.com/)
- Privacy policy (Play Console URL): [https://tiwa.loopbugs.com/privacy](https://tiwa.loopbugs.com/privacy)

Plain HTML/CSS only — no build step or framework. Deployed with **GitHub Pages** from GitHub Actions. Custom domain: `tiwa.loopbugs.com`.

## Contents

| Path | Purpose |
| --- | --- |
| `index.html` | Short landing page |
| `privacy/index.html` | Privacy policy (`/privacy/` and `/privacy`) |
| `styles.css` | Shared styles |
| `CNAME` | Custom domain for Pages |
| `.nojekyll` | Serve files as-is (skip Jekyll) |
| `.github/workflows/deploy-pages.yml` | Pages deploy workflow |

## Enable GitHub Pages

1. Open the repo on GitHub → **Settings** → **Pages**.
2. Under **Build and deployment** → **Source**, choose **GitHub Actions**.
3. Merge (or run) the deploy workflow so the first Pages deployment completes.
4. Under **Custom domain**, enter `tiwa.loopbugs.com` and save.
5. Wait for DNS checks to pass, then enable **Enforce HTTPS**.

The workflow uses `actions/upload-pages-artifact` and `actions/deploy-pages`. It runs on every push to `main` and via **workflow_dispatch**.

## Cloudflare DNS

In the Cloudflare zone for `loopbugs.com`:

1. Add a **CNAME** record:
   - **Name:** `tiwa`
   - **Target:** `loop-bugs.github.io`
   - **Proxy status:** **DNS only** (grey cloud) — do not orange-cloud proxy while GitHub manages the certificate for Pages.
2. Keep the `CNAME` file in this repo as `tiwa.loopbugs.com` (already present).
3. After DNS propagates, confirm HTTPS on `https://tiwa.loopbugs.com/privacy`.

> GitHub Pages custom domains expect the CNAME target of the form `<org-or-user>.github.io`. For this org that is `loop-bugs.github.io`.

## Local preview

No install required. From the repo root:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080/` and `http://localhost:8080/privacy/`.

## Privacy policy notes

The privacy policy is grounded in the `Loop-Bugs/tiwa-app` source (on-device SQLCipher storage, consent-gated Supabase sync, encrypted voice notes, metadata-only to-do sync, no ad/analytics SDKs). Items the study team still needs to confirm are marked `[TO CONFIRM: …]` in `privacy/index.html`.
