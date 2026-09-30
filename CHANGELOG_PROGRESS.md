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

### Step 5 — Add push/PR CI quality workflow
- Added GitHub Actions CI for every branch push and pull request.
- Uses pnpm 9.12.3 with Node.js 20 and a frozen lockfile install.
- Runs TypeScript typechecking, formatting verification, and Biome linting.
- Added concurrency cancellation so superseded runs do not waste CI capacity.

### Step 6 — Add CodeQL security workflow
- Added CodeQL analysis for JavaScript/TypeScript on every branch push and pull request.
- Added a weekly scheduled security scan.
- Uses GitHub's security-and-quality query suite.

## Verification

- Repository workflow files and maintenance documentation were committed directly to GitHub.
- The CI workflow is configured to trigger on every push.
- The CodeQL workflow is configured to trigger on every push and pull request, plus a weekly scheduled scan.
- This environment cannot execute GitHub-hosted Actions jobs directly; the workflow commits themselves trigger the hosted runs automatically.
- Full local dependency installation/build was not executed in this environment.
