# screwpile-web

Static legal/support pages for **Screwpile** (hybrid-casual mobile puzzle game),
served via GitHub Pages from the root of `main`.

Live: <https://agilemindconsultant.github.io/screwpile-web/>

This repo intentionally contains **no game source, no CI secrets, and no assets**
from the Screw Puzzle game repo. It is public — everything here is published.
One repo per game, deliberately: see AGIAAAA-2524 for the cross-project leakage
bug this separation avoids.

## Contents

- `index.html` — privacy policy. **Currently a placeholder.**
- `support.html` — support / contact page. **Currently a placeholder.**
- `.nojekyll` — disables Jekyll processing; this is a plain static site.

## Before store submission

Both pages are placeholders and must be replaced with real copy before Screwpile
is submitted anywhere. Owner: CMO (copy), gated on the M0.7 data-safety answers
(PM + CTO).

Do **not** copy Squirrel Trigger's privacy policy here. That text states the build
contains no analytics, advertising or crash-reporting SDK, which is true for
Squirrel Trigger and **false for Screwpile** — Screwpile is planned to monetize via
rewarded ads, interstitials and a banner (AGIAAAA-2431), so it will carry an ads SDK
and will collect at least an advertising identifier. A copied policy would be an
inaccurate data-safety declaration.

Follow the document-is-source-of-truth pattern already used for Squirrel Trigger:
the wording lives in a Paperclip document and is mirrored here, not authored here.

## How changes land

This initial scaffold was committed directly to `main` (new empty repo, nothing to
review, and GitHub Pages can only build from `main`). **Every content change after
this one goes via a branch and a pull request**, matching the `squirrel-trigger-web`
precedent — including the CMO's real privacy and support copy.

## Hosting

GitHub Pages, `main` branch, `/` root, on the existing `AgileMindConsultant`
GitHub account. No new account, no custom domain, $0/year (AGIAAAA-2524).

Note: `AgileMindConsultant` is a personal GitHub **user** account, not an
organization, despite being referred to as "the org" in earlier planning
documents. The Pages URL pattern is identical either way, but repo creation
goes through `POST /user/repos`, not `POST /orgs/.../repos`.
