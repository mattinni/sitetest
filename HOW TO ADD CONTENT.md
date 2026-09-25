# Adding artists, releases and merch

Everything on the site comes from three files in the `content/` folder. You don't need to touch any code.

| File | Page |
|---|---|
| `content/artists.json` | Artists |
| `content/releases.json` | Releases |
| `content/merch.json` | Merch |

Images go in these folders (square 1:1, JPG or PNG, around 1500×1500px):

- `images/artists/`: artist photos
- `images/releases/`: release artwork
- `images/merch/`: merch product shots
- `images/site/`: general site images

In the content files, write just the image's file name (`"niall.jpg"`), not the whole folder path.

## Shopify buy buttons

Your shop's details are saved once in `content/shop.json`. To add a buy button to a release or merch item:

1. In Shopify, open **Buy Button** → create a button for the product → copy the embed code.
2. In that code, find the line `id: '15563820400966',` and copy the number.
3. Paste the number into the entry's `shopifyProductId` field: `"shopifyProductId": "15563820400966"`.

Entries without a number show a placeholder instead.

## How tags connect things

- Each **artist** and **release** has a `tag`. That's its name tag, e.g. `"Niall Breslin"` or `"The Place That Has Never Been Wounded"`.
- Releases and merch have a `tags` list saying what they belong to.
  - A release tagged `["Niall Breslin"]` shows on Niall Breslin's page and links back to it.
  - Merch tagged `["The Place That Has Never Been Wounded"]` shows on the The Place That Has Never Been Wounded release page and on Niall Breslin's page, because The Place That Has Never Been Wounded already belongs to Niall Breslin.
  - For merch that belongs to an artist but not to a specific release, just tag the artist: `["Niall Breslin"]`.
  - For INNI label merch that has no artist or release, leave tags empty: `"tags": []`. It shows as "INNI" merch.
  - A collaboration can list more than one artist: `["Niall Breslin", "Other Artist"]`.
- Tags must match exactly, but capitals don't matter.

## Adding a new entry

1. Copy an existing entry, from its `{` to its `}`, including the comma between entries.
2. Change the values. Keep the quotes, commas and brackets as they are.
3. Set `"published": false` to hide an entry without deleting it.

Common mistakes: a missing comma between entries, a comma after the last entry, or quotes that aren't closed. If the site shows nothing, paste the file into jsonlint.com to find the error.

### Artist fields
`tag`, `name`, `country`, `photo`, `photoCredit`, `bio` (a list of paragraphs), `listenEmbed` (optional: paste a normal Spotify link, e.g. `https://open.spotify.com/album/…`, or a Bandcamp embed URL), `published`

### Release fields
`tag`, `title`, `tags` (artists), `type` (Album / EP / Single…), `year`, `catalogueNumber`, `artwork`, `description` (paragraphs), `formats` (name + price), `buyLabel` (what the release's own buy button sells, e.g. "Digital Album"), `shopifyProductId`, `listenEmbed`, `published`

### Merch fields
`title`, `tags` (release and/or artist), `category` (Vinyl / Apparel / CD…), `format` (short button label on the release page, e.g. "12\" Vinyl LP"), `image`, `description`, `options` (name + price), `shopifyProductId`, `published`

Listing order is alphabetical, so the order of entries in the file doesn't matter. Merch category buttons come from `content/categories.json`: they always show, in that order, even when empty. Any new category used in `merch.json` is added automatically after the listed ones. Release Format buttons build themselves from the release entries.
