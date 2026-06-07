# Segwit vs BIP-110 Support

A static wiki-style comparison table based on the archived [Bitcoin Wiki Segwit support](https://en.bitcoin.it/wiki/Segwit_support) page (2017), with a researched BIP-110 column for the same developers and businesses, plus influencers.

Live miner signaling stats load once from [bip110monitor.com](https://bip110monitor.com/).

## Run locally

```bash
# Python
python -m http.server 8765

# or Node
npx serve .
```

Open `http://localhost:8765/index.html`.

## How to add or update entries

All table data lives in **`data.js`**. Edit that file, refresh the browser — no build step.

### Position values (BIP-110 column)

Use one of these strings (colors match the [Bitcoin Wiki](https://en.bitcoin.it/wiki/Segwit_support) legend):

| Value | Meaning |
|-------|---------|
| `prefer` | What they would choose if it were only up to them |
| `acceptable` | Workable solution |
| `weak` | Better than nothing |
| `wanting` | Likes the idea but sees insufficient support |
| `evaluating` | Still evaluating |
| `deficient` | Okay with the idea but not enough community support |
| `accjuly` | Workable if activated before Aug 1, 2017 (BIP148-compatible) |
| `no` | Does not support |
| `unknown` | No public position found |

Use `""` for empty 2017 segwit columns where the person was not on the original wiki list.

### Influencers

Add objects to the `INFLUENCERS` array (alphabetical by name):

```javascript
{
  name: "Jane Doe",
  handle: "@janedoe",
  bip110: "prefer",
  notes: "Short summary of their public stance",
  source: { label: "Source name", url: "https://example.com/article" }
}
```

- **Always include a source URL** for BIP-110 positions.
- Use `unknown` if they have not stated a position (do not infer from media alone).
- Use `source: null` only if there truly is no link (avoid when possible).

### Developers & businesses

Add one-line objects to `DEVELOPERS` or `BUSINESSES`:

```javascript
{ name: "Jane Doe", aff: "Core", segwit: "prefer", bip141: "prefer", bip148: "prefer", bip149: "acceptable", bip91: "weak", segwit2x: "no", bip110: "unknown", source: null },
```

- **Developers**: keep alphabetical by surname where possible.
- **Businesses**: `aff` is the service type (wallet, exchange, miner, etc.).
- Set `bip110` and `source` when you have a cited 2026 position; otherwise `bip110: "unknown", source: null`.
- Leave 2017 segwit fields as `""` for entries not on the original wiki.

### Checklist before submitting a change

1. Public statement or primary source exists (tweet, blog, GitHub, podcast with clear position).
2. Entry is in the correct table (developer vs influencer vs business).
3. No duplicate rows for the same person unless intentional (e.g. Mechanic is influencer-only).
4. Open `index.html` locally and confirm the row renders and filters work.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Page layout and tables |
| `data.js` | All entries |
| `app.js` | Rendering, sort, filter, live stats fetch |
| `styles.css` | Wiki-style colors and layout |

## Disclaimer

Segwit columns are from the 2017 archived wiki. BIP-110 positions reflect public sources as of research date — not an endorsement tracker. Verify sources before relying on any cell.
