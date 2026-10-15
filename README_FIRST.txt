KLIKTIVA — CLOUDFLARE WORKER FIXED v3

Purpose:
This revision specifically neutralizes stale _redirects files that may remain in a GitHub repository when new files are uploaded without deleting old files. It keeps the Worker-based route handling and static asset configuration.

IMPORTANT — apply once, carefully:
1. Extract this ZIP.
2. In the existing GitHub repository, upload the CONTENTS of this ZIP to the repository root (not the ZIP itself and not a nested folder).
3. Allow GitHub to replace existing files. Ensure both `public/_redirects` and root `_redirects` are replaced by the included comment-only files. Do not leave the old redirect rules in the repository.
4. Keep `wrangler.jsonc`, `src/index.js`, `package.json`, `public/index.html`, and `public/admin.html` at the shown paths.
5. Wait for the newest Cloudflare build to finish and confirm the newest version is active in production before testing.
6. The Cloudflare dashboard screenshot shows APPS_SCRIPT_URL already exists as a Production runtime variable. Do not change its value as part of this routing fix. Wrangler may show a configuration-sync warning because the variable is managed in the dashboard; that warning alone does not explain ERR_TOO_MANY_REDIRECTS.

Worker route behavior:
- `/` is served from public/index.html.
- `/admin` and `/admin/` are served internally from public/admin.html; the Worker does not issue an HTTP redirect.
- `/api` and `/api/*` are handled by the Worker and forwarded to Apps Script.

This is still a pilot package. It has been syntax/configuration checked, but I cannot claim live Cloudflare recovery until the deployed version is verified. Do not change DNS or delete prior deployments during recovery.
