# OKB Accomplishment Dashboard

Percent accomplishment of every waterway, drainage and ISF record under **Oplan Kontra Baha (OKB)**, rolled up Region › Site › Waterway.

**Live pages**

| Page | Link | Who it is for |
|---|---|---|
| Sign-in dashboard | https://oplankontrabaha.github.io/accomplishments/ | regions, with their OKB password |
| VIP dashboard | https://oplankontrabaha.github.io/accomplishments/vip.html | anyone holding the link, no sign-in |

## How it works

| Part | Where it lives | What it does |
|---|---|---|
| `index.html` | this repository (GitHub Pages) | sign-in screen + dashboard, PDF and CSV export |
| `vip.html` | this repository (GitHub Pages) | the same dashboard with no sign-in |
| `Accomplishment.gs` | the Apps Script project bound to the OKB SSOT (not in this repo) | reads the SSOT tabs, replays the Accomplishment Log, checks region passwords, caches the data |

The pages talk to the server through the Apps Script `/exec` link, saved as `API_URL` in both HTML files.
Every request is one `POST` with `{ "fn": "...", "args": [...] }`, and Accomplishment.gs only answers the functions listed in its `API_FUNCTIONS`.

## VIP link

- `vip.html` uses the word `vip`. `vip.html?key=WORD` uses another word.
- The server checks the word against `VIP_PAGE_KEY` in Accomplishment.gs. Change it there (and redeploy) to cut off every old VIP link. Set it to `''` to switch the VIP page off.
- Old links like `.../accomplishments/?vip` are forwarded to `vip.html`.

## Updating

- **Page changes:** edit the HTML here and commit. GitHub Pages updates within a minute or two.
- **Server changes:** paste the new `Accomplishment.gs` into Apps Script, then
  **Deploy → Manage deployments → ✏️ Edit → Version: New version → Deploy**.
  Always edit the existing deployment: a new deployment gets a new `/exec` link, and `API_URL` would have to change too.
- **Access:** the deployment must be *Execute as: Me* and *Who has access: Anyone*.
- **Check the server:** open the `/exec` link with `?ping=1` at the end. It should answer with `"ok": true`.
