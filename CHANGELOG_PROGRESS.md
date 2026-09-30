# Change Log

Step-by-step production hardening and maintenance log for the repository.

## 2026-09-30

### Step 1 — Initialize change tracking
- Added this file so repository maintenance remains auditable.
- No application behavior changed in this step.

### Step 2 — Refresh application metadata
- Replaced the generic template title/description with repository-specific metadata.
- Added application name, keywords, robots directives, and a dark-friendly metadata baseline.
- Kept the existing runtime theme-color behavior intact.

### Step 3 — Harden Next.js response headers
- Disabled the Next.js powered-by response header.
- Added MIME sniffing, clickjacking, referrer-policy, permissions-policy, and HSTS headers.
- Restricted remote image loading to the intended HTTPS hostname.

### Step 4 — Improve developer verification
- Added an explicit TypeScript type-check script.
- Added a formatting verification script alongside the existing formatter.
- Existing development, build, and test commands were left unchanged.

## Verification

- Repository files were re-read from GitHub after the edits.
- The changes are committed separately so each maintenance step is easy to inspect or revert.
- Full local dependency installation/build was not executed in this environment, so runtime/build success still needs to be confirmed by GitHub Actions, Vercel, or a local pnpm install.
