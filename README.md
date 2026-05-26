# Sozo Read Directory

A curated list of source-pack repos for [Sozo Read](https://github.com/Spyou/Sozo-Read). Users see this list inside the app's **Discover** tab and can install any entry with one tap.

## What lives here

Just one file: [`index.json`](./index.json). The Sozo Read app fetches it directly from GitHub's raw CDN, caches it for 24 hours, and renders each entry as a card.

## How it works for users

1. Open Sozo Read
2. Go to **Sources → Discover**
3. Tap **Install** on any card → the entry's `repoUrl` is added to your Repos tab
4. Open the **Repos** tab and install individual sources from the newly-added repo

## How to submit your repo

Open a pull request that adds one entry to `index.json`'s `entries` array. Each entry looks like this:

```json
{
  "name": "My source pack",
  "author": "your-github-handle",
  "repoUrl": "https://raw.githubusercontent.com/<you>/<your-repo>/main/index.json",
  "description": "One-line summary of what the pack covers.",
  "tags": ["manga", "novel", "english"]
}
```

### Required fields

| Field | What it is |
|---|---|
| `name` | Display name shown on the card (max ~40 chars) |
| `repoUrl` | Raw URL of YOUR repo's provider manifest — the `index.json` your scrapers are listed in |

### Optional fields

| Field | What it is |
|---|---|
| `author` | Your handle (shown as "by xxxxx" under the name) |
| `description` | One-line summary (max ~120 chars) |
| `tags` | Free-form labels rendered as chips, e.g. `["manga", "korean"]`. Up to 4 are shown. |
| `logo` | Optional logo URL — square, ~128x128, PNG/JPG/WEBP |
| `verified` | Reserved — maintainers set this on entries we've vetted. Don't set it in your PR. |

### Example minimal entry

```json
{
  "name": "Korean manhwa pack",
  "author": "exampledev",
  "repoUrl": "https://raw.githubusercontent.com/exampledev/sozoread-manhwa/main/index.json"
}
```

## How your repo should be structured

Your repo needs to follow the same shape as [Spyou/sozoread-providers](https://github.com/Spyou/sozoread-providers):

```
your-repo/
├── index.json          # provider manifest (lists your scrapers)
├── scraper-1.js
├── scraper-2.js
└── ...
```

`index.json` shape:

```json
{
  "name": "Your pack name",
  "description": "What this pack does.",
  "sources": [
    {
      "id": "siteName",
      "name": "Site Name",
      "file": "scraper-1.js",
      "type": "manga"
    }
  ]
}
```

`type` is one of `"manga"`, `"novel"`, or `"both"`.

## Review process

Before merging, we check:

- The `repoUrl` returns a valid `index.json`
- Each listed scraper file actually exists in your repo
- The scrapers don't do anything obviously sketchy (sending user data anywhere, mining crypto in the JS engine, etc.)
- The pack isn't a near-duplicate of an existing entry

We don't review for legal status of the sites being scraped — that's on you, the maintainer of your repo.

## Verified badge

Entries marked `"verified": true` have been spot-checked by a Sozo Read maintainer. The app shows a small checkmark next to verified names. Verification is optional — unverified entries still appear in the Discover tab.

## Removing an entry

If your repo is no longer maintained or you want it pulled from the directory, open a PR that removes your entry. We'll merge quickly.

## License

This directory file (`index.json`) is in the public domain. Each linked repo carries its own license — check before reusing code.
