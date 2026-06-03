# bXSS Discovery

**English** | [中文](./README.zh-CN.md) | [Français](./README.fr.md)

Local-first, OPSEC-aware workbench for building scoped search queries to discover public intake surfaces during authorized bXSS assessments.

## Overview

bXSS Discovery is a compact browser-based workbench for building scoped search queries that help identify public intake surfaces during authorized security assessments.

The tool focuses on discovery, triage, and repeatable notes. It does not submit payloads, run scans, or interact with target applications directly.

## Intended Use

Use this only for authorized work: internal assessments, client-approved testing, or bug bounty programs where the target scope explicitly permits discovery activity.

Generated queries narrow public search results. They are not proof of vulnerability and should not be treated as validation. Manual review is still required.

## Features

- Scoped query builder using a normalized domain or host
- English default UI with Chinese and French language switches
- Template library with category and keyword filtering
- Numbered workflow panels for scope, template, query, parameters, triage, and explanation
- Single search engine selection for Google, Bing, or DuckDuckGo
- Detailed query explanations for scope, template matching, search engine choice, and result filters
- Queue and history views for triage context
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
3. Filter or select a template from the template library.
4. Read the generated query and explanation before opening results.
5. Adjust query parameters, including one selected search engine and optional result filters.
6. Open the query only when scope and authorization are correct.
7. Queue promising queries with a short triage note.
8. Review results manually and keep evidence tied to the original scope and query.

## OPSEC Notes

- Keep searches scoped to domains or hosts that are explicitly authorized.
- Prefer exact hosts when authorization is narrow.
- Do not submit payloads from this discovery tool.
- Treat search engine history, browser history, screenshots, local storage, and notes as assessment artifacts.
- Do not paste private target data into public search engines unless the engagement rules allow it.
- Review redirects carefully; results may point to third-party help desks, hiring systems, or support portals.

For more operational guidance, see [OPSEC.md](./OPSEC.md).

## Customizing Templates

Templates are defined in the `dorks` array inside `index.html`. Each entry includes:

- `id`: stable template identifier
- `title`: English template name
- `category`: grouping used by the library
- `icon`: Font Awesome class used for the compact UI marker
- `intensity`: triage hint such as `Low noise`, `Targeted`, or `Broad`
- `operator`: internal syntax tag used for search/filtering; the UI presents this as title, URL, or page-text matching
- `description`: what the template is intended to find
- `query`: search query fragment appended after `site:{scope}`

Keep new templates specific, explainable, and easy to triage. Avoid broad terms that mostly return marketing, policy, or documentation pages.

## Deployment And Storage

This is a static app. You can host it through GitHub Pages, an internal static site, or any static file server.

For sensitive work, prefer a local-only instance and avoid analytics, remote error collection, or access logs that capture target names and query terms.

The app stores UI preferences and queue/history entries in browser `localStorage`. Clear local storage when required by engagement rules.

## License

Copyright © RedteamNotes. All rights reserved.
