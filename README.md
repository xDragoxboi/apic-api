# Epic Games Free Games API

A simple Cloudflare Worker that returns the current and upcoming free games on the Epic Games Store as clean JSON.

## Endpoint

```
GET https://apic.shalle.workers.dev/
```

No parameters or authentication required.

## Response Format

Returns a JSON array of free game objects:

```json
[
  {
    "title": "The Ouroboros King",
    "desc": "The Ouroboros King combines the strategic depth of chess with the build variety and replayability of roguelikes. Assemble a formidable army, discover powerful relics, and buy surprising gadgets to defeat the Coven.",
    "img": "https://cdn1.epicgames.com/spt-assets/33630d7105014582a478094e89953f49/the-ouroboros-king-jwabx.jpg",
    "url": "https://store.epicgames.com/en-US/p/the-ouroboros-king",
    "price": 999,
    "start": "2026-06-11T15:00:00.000Z",
    "end": "2026-06-18T15:00:00.000Z"
  }
]
```

### Field Reference

| Field   | Type   | Description |
|---------|--------|-------------|
| \`title\` | string | Game title |
| \`desc\`  | string | Short description |
| \`img\`   | string | Cover image URL |
| \`url\`   | string | Link to the Epic Games Store page |
| \`price\` | number | Original price in **USD cents** (e.g. \`999\` = $9.99, \`1999\` = $19.99) |
| \`start\` | string | ISO 8601 timestamp for when the offer becomes free |
| \`end\`   | string | ISO 8601 timestamp for when the offer expires |

## Usage Example

```bash
curl https://apic.shalle.workers.dev/
```

```js
const res = await fetch("https://apic.shalle.workers.dev/");
const games = await res.json();
console.log(games[0].title);
```

## Notes

- Prices are in USD, represented as integer cents.
- Built on Cloudflare Workers for fast, edge-cached responses.
