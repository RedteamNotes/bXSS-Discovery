# bXSS Discovery

bXSS Discovery is a compact browser-based workbench for building scoped search queries that help identify public intake surfaces during authorized security assessments.

The tool focuses on discovery, triage, and repeatable notes. It does not submit payloads, run scans, or interact with target applications directly.

## What It Helps Find

- Contact, feedback, support, ticket, and report forms
- Career, resume upload, partner, vendor, quote, demo, and callback workflows
- Review, testimonial, registration, complaint, and other user-input surfaces
- Search-result patterns that may lead to staff-reviewed or back-office intake paths

## Intended Use

Use this only for authorized work: internal assessments, client-approved testing, or bug bounty programs where the target scope explicitly permits discovery activity.

The generated queries are meant to narrow public search results. They are not proof of vulnerability and should not be treated as validation. Manual review is still required.

## Features

- Scoped dork builder using a normalized domain or host
- English default UI with Chinese and French language switches
- Template library with category and keyword filtering
- Numbered workflow panels that show scope, template, query, parameters, triage, and explanation order
- Single search engine selection for Google, Bing, or DuckDuckGo
- Detailed query explanations for how scope, template matching, search engine choice, and result filters affect discovery
- Queue and history views for keeping triage context
- Light theme by default, with a dark theme toggle
- Static single-file app that can be hosted anywhere

## Quick Start

Open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:4173/
```

## Workflow

1. Set the authorized target scope, for example `redteamnotes.com` or `app.redteamnotes.com`.
2. Confirm that you have testing authorization for that scope.
3. Filter or select a template from the left-side template library.
4. Read the generated query and the query explanation before opening results.
5. Adjust query parameters, including one selected search engine and optional result filters.
6. Open the query only when the scope and authorization state are correct.
7. Queue promising queries with a short triage note.
8. Review results manually and keep evidence tied to the original scope and query.

## OPSEC Notes

- Keep searches scoped to domains or hosts that are explicitly authorized.
- Prefer exact hosts when authorization is narrow.
- Avoid submitting test payloads from this tool's discovery phase.
- Treat search engine history, browser history, bookmarks, screenshots, and notes as assessment artifacts.
- Do not paste private target data into public search engines unless the engagement rules allow it.
- Review redirects carefully; search results may point to third-party help desks, ATS platforms, or support portals outside the allowed scope.

For more operational guidance, see [OPSEC.md](./OPSEC.md).

## Customizing Templates

Templates are defined in the `dorks` array inside `index.html`. Each entry includes:

- `id`: stable template identifier
- `title`: English template name
- `category`: grouping used by the library
- `icon`: Font Awesome class used for the compact UI marker
- `intensity`: triage hint such as `Low noise`, `Targeted`, or `Broad`
- `operator`: internal syntax tag used for search/filtering; the UI presents this as a matching area such as title, URL, or page text
- `description`: what the template is intended to find
- `query`: the search query fragment appended after `site:{scope}`

Keep new templates specific, explainable, and easy to triage. Avoid adding overly broad terms that produce mostly marketing, policy, or documentation pages.

## Deployment

This is a static app. You can host it through GitHub Pages, an internal static site, or any static file server.

For sensitive assessments, prefer a local-only instance and avoid adding analytics, third-party telemetry, or remote logging.

## Browser Storage

The app stores local UI preferences and queue/history entries in browser `localStorage`. This is convenient for triage, but it also means the browser profile may retain assessment context. Clear local storage when needed.

## Project Status

This project is intended as a lightweight discovery aid, not a vulnerability scanner. The safest default is to keep it small, auditable, and easy to run locally.

## Copyright

Copyright © RedteamNotes. All rights reserved.
