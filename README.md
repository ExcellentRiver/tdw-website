# The Disciples' Walk (#TDW)

A free, responsive, single-page website. No paid framework or account is needed to run the page.

## Publish for free using GitHub Pages
1. Create a free GitHub account at https://github.com/ if needed.
2. Create a **public** repository named `tdw-website`.
3. Upload `index.html` into the repository root and commit.
4. Open **Settings → Pages → Build and deployment**. Select **Deploy from a branch**, branch **main**, folder **/(root)**, and Save.
5. The site will usually appear at `https://YOUR-USERNAME.github.io/tdw-website/` after deployment. You can use that free URL without buying a domain.

## Activate registration and reporting
1. Create a Google Form for joining with only necessary fields (nickname, optional team, consent acknowledgment). Avoid requesting stranger names or sensitive details.
2. Create a separate Google Form for reporting activity (participant code or nickname, reporting date, number of approaches, number of conversations, optional team, optional reflection). Avoid identifying strangers.
3. In `index.html`, locate `const CONFIG` near the bottom. Paste each Google Form's published URL into `joinFormUrl` and `reportFormUrl`.
4. Re-upload `index.html` to GitHub. The buttons will open the relevant form.

## Enable real counters — free plan
The site expects a public JSON URL configured as `statsJsonUrl` that returns:

```json
{"approached":0,"conversations":0,"participants":0,"teams":0,"updatedAt":"2026-10-30T00:00:00Z"}
```

Suggested architecture:
- Google Forms → Google Sheets (private response sheets)
- Organiser reviews reports and marks approved submissions; de-duplicates participant IDs.
- Google Apps Script reads **only approved** rows, aggregates totals, and publishes a read-only JSON endpoint. Configure the script's web app permissions appropriately and test cross-origin fetch from GitHub Pages; if CORS prevents direct access, publish the aggregate JSON as a static file in the GitHub repository instead, using a manual update or a scheduled GitHub Actions workflow.
- Set `statsJsonUrl` to the verified public JSON URL; the page refreshes it every 60 seconds. If using static JSON on GitHub Pages, updates will follow the publishing/cache delay rather than being instantaneous.

For an easy first launch, use a `stats.json` file in the same repository, update it with approved totals, and set `statsJsonUrl:'./stats.json'`. This works immediately without a server, but it is not fully automated. Keep the underlying response sheet private; publish only aggregate numbers.

## Privacy and moderation
- Never publish identifiable details about strangers, precise approach locations, or private stories without consent.
- Do not equate number of approaches with spiritual success. Count only genuine voluntary interactions.
- Use a participant ID or nickname to avoid duplicate participant counts. Review suspicious submissions before adding to totals.
- Do not publish raw Google Sheets containing names, emails, or free-text responses.
- The homepage image is remotely loaded from Unsplash; internet access is needed to display it. Google Fonts also require an internet connection.

## Edit the design
All layout, colours, content and scripts are in `index.html`. Change CSS variables near the top for the palette. The page works as a static site.
