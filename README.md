# <img src="https://cdn.simpleicons.org/semgrep/1B2A4A" height="32" align="center" /> Semgrep SAST Scan — manuelaklenke.com

Automated static application security testing for manuelaklenke-web source code using Semgrep OSS. Runs after every deployment and publishes reports to GitHub Pages.

---

## 📊 Security Report

Latest report: **[https://georget88.github.io/manuelaklenke-semgrep-security/](https://georget88.github.io/manuelaklenke-semgrep-security/)**

---

## 🛠️ Tech Stack

- [Semgrep OSS](https://semgrep.dev/) — static application security testing
- GitHub Actions — CI/CD pipeline
- GitHub Pages — report hosting

---

## 🔍 What Gets Scanned

The `src/` directory of `manuelaklenke-web` using the following rulesets:

| Ruleset | Covers |
|---|---|
| p/default | General security best practices |
| p/javascript | JavaScript-specific vulnerabilities |
| p/react | React security patterns |
| p/typescript | TypeScript-specific issues |

Semgrep checks source code for:
- XSS sinks and unsafe HTML injection
- Insecure React patterns (dangerouslySetInnerHTML, etc.)
- Hardcoded secrets and credentials
- Prototype pollution
- Insecure randomness and cryptography

---

## ⚙️ CI/CD Pipeline

The scan is triggered automatically by [GeorgeT88/manuelaklenke-web](https://github.com/GeorgeT88/manuelaklenke-web) after every push to `main`, once all E2E tests have completed. Semgrep runs in parallel with Snyk SCA:

```
📦 Push to manuelaklenke-web
        ↓
⏳ Vercel deployment confirmed live
        ↓
🎭 Playwright + 🔬 Selenium + 🌲 Cypress (parallel)
        ↓
🛡️ OWASP ZAP — skipped (manual/nightly only)
        ↓
⚡ repository_dispatch: vercel-deploy  ←─ Semgrep + Snyk triggered in parallel
        ↓
🔎 Semgrep scans manuelaklenke-web/src
        ↓
📊 HTML report published to GitHub Pages
```

The scan can also be triggered manually from **Actions → Semgrep SAST Scan → Run workflow**, and runs on a nightly schedule at **07:00 UTC**.

---

## 🏷️ Run Name Convention

| Trigger | Run name |
|---|---|
| Push via app repo | `Semgrep SAST Scan — triggered by Vercel deploy` |
| Manual | `Semgrep SAST Scan — manual run` |
| Nightly schedule (07:00 UTC) | `Semgrep SAST Scan — nightly run` |
