# Vercel release: Beatstudio

**Intended production hostname:** `https://beatstudio.xsikomdigitalprojects.app`

Vercel access from this session is currently failing with **Access denied**. This guide lets the account owner complete deployment from a Vercel-authorized terminal/dashboard without sharing API tokens in chat.

## CLI deployment

1. Install/use the Vercel CLI and authenticate interactively: `vercel login`.
2. From the folder containing `index.html` and `vercel.json`, run `vercel` and link this directory to the intended Vercel account/team and project (create the project if required).
3. Select the **Other** static project preset. This site has no install or build command; deploy the files from the project root.
4. Once the preview is verified, run `vercel --prod`.

`.vercelignore` prevents README and audit/deploy notes being published as public website files.

## Assign the requested subdomain

1. In Vercel, open the project's **Settings → Domains** and add exactly `beatstudio.xsikomdigitalprojects.app`.
2. Follow the DNS record Vercel displays for that hostname at the registrar/DNS provider. Do not change the apex/root domain record. If the root domain's DNS is hosted by Vercel, the record may be managed there.
3. Wait for Vercel to verify DNS and issue HTTPS. Check the production deployment, `/`, `/impressum`, and `/datenschutz` over HTTPS. Device APIs and the PWA service worker depend on HTTPS.

The Vercel deployment tool in this session returned `Access denied` for project and domain reads; credential validation separately returned `Invalid credentials`. No project, deployment, or DNS record has been modified from this session.
