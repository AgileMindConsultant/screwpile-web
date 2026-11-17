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
   only. That is the C7 consent module — specified in AGIAAAA-2449 §4.6 as a wrapper
   over the already-vendored AdMob UMP plugin, but **not implemented as of this
   commit**; the work sits on AGIAAAA-2509.

   Each sentence is conditioned on its platform, so the page stays accurate on an
   Android-only launch (ATT is iOS-only, and iOS is separately blocked on a Mac and
   an Apple Developer membership — AGIAAAA-2449 §4.6). What is *not* optional for an
   Android launch into the EEA/UK is the UMP half: if that ships without working
   consent gating, this page misdescribes the build.
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
