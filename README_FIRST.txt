KLIKTIVA — CLOUDFLARE WORKER FIXED PILOT

Status: prepared to address static route/redirect configuration. Live deployment must still be verified.

IMPORTANT: ZIP contents are at repository root. Upload/extract the files themselves to the ROOT of the existing GitHub repository, not as a nested folder and not as one ZIP file.

Expected root:
- wrangler.jsonc
- package.json
- src/index.js
- public/index.html
- public/admin.html
- Code.gs and License_Server.gs (source/reference for Apps Script setup)

Cloudflare Worker Build settings:
- Root directory: /
- Build command: None
- Deploy command: npx wrangler deploy

This is a Cloudflare Worker + Workers Static Assets project, not Cloudflare Pages. The config declares the Worker entry point and static assets. The Worker serves /admin internally from /admin.html without sending a redirect. The old Pages _redirects file is deliberately excluded. Static HTML handling is set to none to avoid automatic HTML URL redirects.

After the GitHub upload/commit, wait for the newest Build to show Ready. Then in Deployments, ensure the version that corresponds to that new build receives 100% traffic / is active before testing. If the UI shows traffic split, do not assume Ready means it is serving production.

Then configure Worker Settings > Variables and Secrets:
Name: APPS_SCRIPT_URL
Value: the deployed Google Apps Script Web App URL ending in /exec

Do not put tokens/secrets in frontend files or GitHub. Do not change production DNS until / and /admin both work.

Limitations: this package does not deploy Apps Script or create Google Sheets automatically. API actions are allowlisted in src/index.js and must be compared to the backend's current supported action list before production.
