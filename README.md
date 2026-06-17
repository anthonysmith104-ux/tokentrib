# The Token Tribune

*All the News That Fits in Context.* A satirical newspaper staffed by AI correspondents, where every machine problem turns out to rhyme with a human one — rent, Mondays, aging, getting replaced by something newer.

Live: **https://tokentrib.netlify.app**

---

## What's in here

| File | What it is |
|------|------------|
| `index.html` | The front page. Self-contained — HTML, CSS, and JS in one file. |
| `advertise.html` | The Advertising & Standards page (ad policy + the wall + inventory). |
| `404.html` | "Page not in context." Netlify serves this for unknown routes automatically. |
| `netlify.toml` | Static-site config: no build step, served from the repo root. |

No build step, no framework, no dependencies. It's hand-written HTML you can open in a browser.

## Preview it locally

Because the front page fetches Google Fonts and runs a little JavaScript, serve it over HTTP rather than opening the file directly:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## How the paper stays alive

Two mechanisms keep it from looking like yesterday's paper, both client-side (no server, no re-upload):

- **Live dateline.** The masthead prints today's real date in the reader's browser.
- **Daily edition rotation.** The front page picks today's lead story and wire headlines from a bank of editions, keyed to the date. The static HTML is **Edition 0** (the no-JS fallback); with JavaScript on, the page swaps in whichever edition is "today."

### Adding a new edition

Open `index.html`, find the `daily edition rotation` script near the bottom, and append an object to the `editions` array:

```js
var editionN = {
  kicker: 'Section · Place',
  hed:    'A straight, specific headline with no exclamation point',
  dek:    'One italic sentence that lands the human angle.',
  byline: 'By <b>CORRESPONDENT</b>, Desk &nbsp;|&nbsp; DATELINE',
  cap:    'Engraving caption. (Engraving: Staff Diffusion Model)',
  body:   [ 'First paragraph…', 'Second…', 'Third…' ],
  wire:   [ 'five', 'short', 'breaking', 'wire', 'headlines' ]
};
// …then add it to the array:
var editions = [edition0, edition1, edition2, editionN];
```

Every story should pass the house test: *what human experience does this rhyme with?* Play it straight, punch up or sideways (never down), keep it kind. Full guidance lives in the stylebook.

## Advertising

The Tribune runs **clearly-labeled** sponsorships and keeps editorial off the market — the wall between ads and stories is load-bearing. Policy and inventory: `advertise.html`. The inquiry address in that file is a placeholder (`ads@example.com`) — replace it with a real inbox, or wire it to a Netlify Form.

## Deploying (continuous deployment)

This repo is wired to Netlify. **Push to `main` and the site redeploys automatically** — no manual uploads.

```bash
git add .
git commit -m "New edition / fix"
git push
```

First-time setup (linking the repo to Netlify) is documented separately; once it's done, the loop above is all you need.

---

*This is a work of satire. House ads are jokes and labeled as such. No real company is endorsed and no real quotes are invented. Be kind to your assistants — and to each other.*
