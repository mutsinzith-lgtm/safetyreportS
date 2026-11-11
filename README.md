# SafetyReport — email-enabled HTML + Vercel API

This project sends submitted voluntary reports to `tmutsinzi@caa.gov.rw` using a Vercel serverless API and Resend. The Resend API key is stored only as a Vercel server-side environment variable; it is never included in the HTML.

## Files
- `index.html` — standalone HTML/CSS/JS reporting form
- `api/report.js` — Vercel serverless function that validates the submission and sends an email
- `vercel.json` — Vercel configuration

## Deploy
1. Create a new GitHub repository, e.g. `safetyreport-email`.
2. Upload the CONTENTS of this folder to the repository root. The root must contain `index.html`, `api/`, and `vercel.json`.
3. Import that repository into Vercel. No Next.js framework is required; choose Other if asked.
4. In Vercel > Project > Settings > Environment Variables, add:
   - `RESEND_API_KEY` = your Resend API key (Secret; do not expose it)
   - `REPORT_TO_EMAIL` = `tmutsinzi@caa.gov.rw`
   - `REPORT_FROM_EMAIL` = a sender address on a domain verified in Resend, e.g. `SafetyReport <reports@your-verified-domain.example>`
5. Redeploy after adding environment variables.

## Resend sender-domain requirement
Create a Resend account and verify a domain you own by adding the DNS records Resend supplies. The `REPORT_FROM_EMAIL` must use that verified domain. Do not use a sender address you do not control. Resend's test sender may be limited to the account owner's verified email and is not a production solution for this recipient.

## Test
After deployment, submit a clearly labelled TEST report. Confirm it arrives in the target inbox and check spam/quarantine. Do not use real safety information for initial tests.

## Important safety and privacy limitations
This is a basic email-notification prototype, not a complete operational voluntary reporting system. It does not persist a central case record, provide an administrator portal, implement robust rate limiting/abuse prevention, encrypt report content at application level, separate reporter identity into a protected store, or provide retention/audit workflows. Email is not necessarily an approved repository for confidential safety data. Before operational use, obtain organizational approval for the mailbox and handling process, perform a security/privacy assessment, implement rate limiting and monitoring, and preferably store reports in a secured database with role-based access. Do not promise absolute anonymity: hosting/network logs may contain technical metadata.
