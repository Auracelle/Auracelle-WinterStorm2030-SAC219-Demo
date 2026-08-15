# Security

## How this application works

WinterStorm2030 is a **single, self-contained, client-side HTML file**. There
is no backend server, no database, and no data collection pipeline of any
kind associated with this repository:

- Everything runs locally in the reviewer's own browser.
- The only outbound network calls the application makes are: (1) attempts to
  call the Anthropic API directly from the browser for the Agentic AI Red
  Team and Suggested Blue Team Moves features, and (2) attempts to fetch
  public map-tile/elevation data (ArcGIS World Imagery, AWS's public
  elevation-tile service) for the optional 3D Terrain View. Both fail
  gracefully to a local fallback if unreachable or unauthorized — this is
  expected behavior in an environment without a proxied API key, not a
  malfunction.
- Session data (scenario state, move logs, scores) is stored only in the
  browser's local storage on the device running it, for the autosave/resume
  feature. Nothing is transmitted to Auracelle AI Governance Labs or any
  third party by this application.
- No credentials, API keys, or secrets are embedded in this repository.

## Login screen

The in-app login (username/password gate on the landing screen) is a **soft
access control**, not authentication in the security sense — credentials are
checked client-side in plain JavaScript and are not a substitute for actual
access control on wherever this file is hosted. Do not rely on it to
restrict access to sensitive deployments; host the file itself behind
appropriate access controls if that's required.

## Classification / handling

This instrument is marked **UNCLASSIFIED // FOR OFFICIAL USE // SAC-219
PANEL ONLY** in-app. Scenario content is illustrative and unclassified;
do not enter classified, controlled unclassified (CUI), or personally
identifiable information (PII) into any field, as none of them are designed
or reviewed for that handling level.

## Reporting a vulnerability

If you find a security issue in this repository (e.g., an XSS vector, a
way the local-storage session data could be exposed to an unintended
origin, or a dependency with a known CVE), please report it directly to
Grace-Alice Evans, Founder & Principal Investigator, Auracelle AI
Governance Labs, rather than opening a public issue, so it can be assessed
and fixed before disclosure.

## Third-party dependencies

This file loads the following third-party libraries via public CDN at
runtime (no bundled/vendored copies are included in this repo):

- pdf.js (Mozilla) — PDF parsing for the Governance Lab document upload
- mammoth.js — DOCX parsing
- Tesseract.js — OCR
- Three.js (r128) — 3D Terrain View rendering

Reviewers running this behind a restrictive network policy should expect
these CDN calls and the map-tile/Anthropic API calls above to fail closed
(with a graceful fallback) rather than break the application.
