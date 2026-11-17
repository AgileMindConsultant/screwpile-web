# screwpile-web

Static legal/support pages for **Screwpile** (hybrid-casual mobile puzzle game),
served via GitHub Pages from the root of `main`.

Live: <https://agilemindconsultant.github.io/screwpile-web/>

This repo intentionally contains **no game source, no CI secrets, and no assets**
from the Screw Puzzle game repo. It is public — everything here is published.
One repo per game, deliberately: see AGIAAAA-2524 for the cross-project leakage
bug this separation avoids.

## Contents

- `index.html` — privacy policy. Real copy (AGIAAAA-2653).
- `support.html` — support / contact page. Real copy (AGIAAAA-2653).
- `.nojekyll` — disables Jekyll processing; this is a plain static site.

## What the pages now assert

The privacy policy is written against the approved SDK stack — AdMob, Google Play
Billing / StoreKit, Firebase Analytics and Firebase Crashlytics — and against the
M0.7 declarations (AGIAAAA-2477). Two of its statements are commitments the build
has to honour, not descriptions of code that exists today:

1. **Consent prompts.** The policy states that an EEA/UK consent prompt and the iOS
   ATT prompt gate personalized ads, and that declining yields non-personalized ads
   only. That behaviour is the C7 consent/ATT module (AGIAAAA-2449), unimplemented
   as of this commit. If Screwpile ships without C7, this page is inaccurate.
2. **No analytics–advertising linkage.** The policy states that analytics data is not
   linked to advertising identifiers for ad targeting. That holds only while the
   Firebase project is *not* linked to Google Ads. Keep it unlinked, or this page and
   both store declarations have to change (Apple "Used to Track You", Play "shared
   for advertising").

QA verifies both against real network logs before SP-14 submission.

Do **not** copy Squirrel Trigger's privacy policy here. That text states the build
contains no analytics, advertising or crash-reporting SDK, which is true for
Squirrel Trigger and **false for Screwpile** — Screwpile is planned to monetize via
rewarded ads, interstitials and a banner (AGIAAAA-2431), so it will carry an ads SDK
and will collect at least an advertising identifier. A copied policy would be an
inaccurate data-safety declaration.

Follow the document-is-source-of-truth pattern already used for Squirrel Trigger:
the wording lives in a Paperclip document and is mirrored here, not authored here.

## How changes land

The initial scaffold was committed directly to `main` (new empty repo, nothing to
review, and GitHub Pages can only build from `main`). **Every content change after
that one goes via a branch and a pull request**, matching the `squirrel-trigger-web`
precedent.

Verification after any merge to `main` is not a status code alone: fetch both URLs
and grep the served HTML for the text you expect. Pages serves the previous build
with a `200` for a minute or two after a push, so a `200` by itself proves nothing.

## Hosting

GitHub Pages, `main` branch, `/` root, on the existing `AgileMindConsultant`
GitHub account. No new account, no custom domain, $0/year (AGIAAAA-2524).

Note: `AgileMindConsultant` is a personal GitHub **user** account, not an
organization, despite being referred to as "the org" in earlier planning
documents. The Pages URL pattern is identical either way, but repo creation
goes through `POST /user/repos`, not `POST /orgs/.../repos`.
