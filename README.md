# SourceLink

Pull every link, request and resource out of a page's source code — right in the browser, no server, no build step.

## Why

A page can't just `fetch()` another site's HTML from client-side JavaScript — the browser blocks it (CORS). SourceLink sidesteps that by working with source you already have, two ways:

- **Paste it.** Open `view-source:` on the page, copy everything, paste it in.
- **Bookmarklet.** Drag a link into your bookmarks bar and click it on any page — it reads that page's own source directly, no proxy involved.

## Features

- Two ways in: paste raw source, or a bookmarklet that reads the current page
- Resolves relative URLs (`/about`, `../img.png`) into full links once you give it the site's URL
- Picks up links from `href`, `src`, `srcset`, forms, CSS `url()`/`@import`, and inline `<script>` calls (`fetch`, `axios`, jQuery, `XMLHttpRequest`, `WebSocket`, `EventSource`, `sendBeacon`, dynamic `import`)
- **Advanced mode** — groups everything into 15 categories (Databases, APIs, WebSockets, Analytics & tracking, Fonts, Scripts, Stylesheets, Images, Media, Frames & embeds, Downloads, Social, Pages, External links, Contact, Other), each entry tagged with its inferred HTTP method
- **GET only** filter, for a quick look at what a page requests without side effects
- Light and dark theme, remembered between visits
- One HTML file. No dependencies, no build, nothing leaves the browser

## Usage

### Option 1 — Paste the source

1. Open `view-source:https://the-site.com` in a new tab
2. Select all, copy
3. Back in SourceLink, fill in the site URL (so relative links resolve correctly) and paste the code — or use the **Paste & extract** button to grab it straight from the clipboard

### Option 2 — Bookmarklet

1. Open `sourcelink.html`
2. Drag the **SourceLink** pill into your bookmarks bar
3. Click it on any page — a panel opens with that page's own links

The bookmarklet reads the page's own source, so CORS doesn't apply, and it remembers whatever theme and mode you last used.

## Advanced mode

Toggle **Advanced** to switch the flat list into grouped-by-category output, each line tagged with a method (`GET`, `POST`, `WS`, ...):

```
# APIs (2)
GET    fetch    https://example.com/api/v1/projects
POST   axios    https://example.com/api/v1/items
```

Methods come from matching patterns in the source (`fetch(...)`, `<form method="">`, `$.ajax({...})`, etc.), not from real network traffic — a URL only built at runtime won't be caught. Toggle **GET only** to filter down to just those.

## Limitations

- Method detection is static pattern matching, not a network inspector — dynamically built requests can slip through.
- Category rules are hand-picked domain and path patterns; an uncommon API or database host may land in the wrong bucket, or in "Other".
- The bookmarklet is desktop-only — some mobile browsers restrict `javascript:` bookmarks.

## Support

Use the **Help** button in the app, or find me on Discord: **@imnottheomagd**
