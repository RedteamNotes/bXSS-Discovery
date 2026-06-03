# OPSEC Guidance

This project is designed for authorized discovery. The main operational risk is not the page itself, but where query data, browser history, notes, screenshots, and search activity may be stored.

## Scope Control

- Use the exact host when the rules only authorize a specific host.
- Use the root domain only when subdomains are explicitly included.
- Re-check scope after redirects to help desks, hiring systems, CRM forms, or third-party support portals.
- Keep a record of the original scope rule that justified the search.

## Search Engine Exposure

Search engines may log query strings, IP address, account context, browser metadata, and timing. Avoid searching private client names, internal-only hostnames, ticket identifiers, or sensitive data unless the engagement rules permit it.

When comparing search coverage, change one variable at a time. Keep the template and filters stable while switching between Google, Bing, and DuckDuckGo so notes and later review remain understandable.

## Browser Hygiene

- Use a dedicated browser profile for assessments.
- Clear local storage, history, downloads, and screenshots after the engagement if required.
- Avoid browser extensions that add telemetry or rewrite search results.
- Keep copied queries and notes out of shared clipboards.

## Triage Discipline

- Treat search results as leads, not findings.
- Prioritize pages that accept user-controlled input and are plausibly reviewed by staff.
- Do not submit payloads until testing authorization, payload rules, and reporting expectations are clear.
- Record why a result was selected, including the query, date, engine, and target URL.

## Hosting

For sensitive work, run the app locally. If hosted, avoid analytics, remote error collection, or access logs that capture target names and query terms.
