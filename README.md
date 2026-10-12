# Curd Runner: The Last Wheel

A cyberpunk match-3 about the end of cheese. The world ran out of dairy, society collapsed over it, and courier Brie Vasquez (plus Rennet, the sarcastic AI living in her neural jack) is hunting the last wheel of aged gouda in a vault under Neo-Wisconsin. Lord Casein would like a word.

**HTML5 game, single file, deployed on Cloudflare Pages and built to be embedded in another website via iframe.**

## Play

- Tap a tile then tap a neighbour, or drag, to swap. Three in a row clears.
- Match **4** or an **L/T** shape to spawn a chaos tile: **+200**, **Swap 7**, **Reverse** (gravity flips for 3 turns), **Skip** (refunds a move).
- Match **5** for a **Wild**. Swap it with any tile to wipe that colour. Swap two Wilds to wipe the board.
- From sector 6, Lord Casein's raiders lock tiles. Locked tiles can't move. Match through them to break them.
- 10 story sectors, then **Wasteland Run** endless mode with a saved high score.
- "Limited moves?" at the start toggles a per-sector move budget. Run out and you get a Blue Screen of Death.

## Project layout

```
public/index.html   the entire game (build output)
public/_headers     Cloudflare Pages headers
wrangler.jsonc      Cloudflare Pages config (pages_build_output_dir = ./public)
package.json        dev + deploy scripts
```

No build step. No external assets. Art, SFX, and music are generated in code.

## Run locally

Any static server pointed at `public/` works:

```bash
npx wrangler pages dev public
```

or

```bash
python3 -m http.server 8787 --directory public
```

## Deploy to Cloudflare Pages

Option A, CLI:

```bash
npm install
npx wrangler login
npm run deploy
```

Option B, Git integration: connect this repo in the Cloudflare dashboard (Workers & Pages → Create → Pages → Connect to Git). Build command: none. Build output directory: `public`.

## Embed on another site

```html
<iframe
  src="https://curd-runner.pages.dev/"
  width="100%"
  height="720"
  style="border:0;max-width:1100px;aspect-ratio:16/10"
  allow="autoplay"
  loading="lazy"
  title="Curd Runner: The Last Wheel">
</iframe>
```

The game fills whatever frame it's given and supports touch. Audio starts on the first tap because browsers block autoplay. Progress saves to `localStorage`; some browsers block storage inside third-party iframes, in which case the game still runs but won't remember progress between visits.
