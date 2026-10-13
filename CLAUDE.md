# CruiseDeals (cruisedeals.shmor.ai)

A Shmor marketplace (shared rules in `../../CLAUDE.md`): its own brand, design and SEO. Compares cruise deals worldwide (ocean, river, luxury, family and expedition cruises) for US, UK and EU cruisers. Repo: `Shmorai/shmor-cruisedeals` (private until launch). Status: **building**, with no referral links yet.

## Where things are
| What | Where |
|---|---|
| Card on shmor.ai, search keywords, **referral links**, offers, SEO defaults | `shmor-site.json` |
| Pages (1 JSON file = 1 Google landing page) | `content/` (`home.json` = homepage, `content/blog/x.json` → `/blog/x/`) |
| Design: header, logo, footer | `templates/layout.html` |
| Design: styles | `assets/site.css` (kit defaults at the top; **CruiseDeals theme** block at the bottom) |
| "Cruise region" field in every search box | `assets/site.js` |
| Generated output (don't edit by hand) | `index.html`, `*/index.html`, `sitemap.xml`, `robots.txt`, `404.html`, `search/`, `search-index.json`, `blog/feed.xml` |

## Pages (18)
Home · caribbean-cruises · mediterranean-cruises · alaska-cruises · norwegian-fjords-cruises · river-cruises · last-minute-cruises · cruises-from-southampton · family-cruises · luxury-cruises · expedition-cruises · first-time-cruise-guide · cruise-destinations · blog (+4 posts: EES/ETIAS/UK ETA for cruise passengers, wave season, Christmas & New Year cruises, what to pack).
Top menu = pages with `navOrder` (Caribbean, Mediterranean, Alaska, River cruises, Last minute, Destinations, Cruise blog). The rest are in the footer and linked via `related`.

## Design
"Midnight voyage" (created 2026-10-13): deep-ocean navy pages (#071526, surfaces #0D2038), champagne gold #E3B04B (links, accents; the shmor.ai card accent), sea glass #5EC4D6 (deal badges), Fraunces serif headings (italic gold for highlights) + Inter body. Logo = white ship with a gold funnel and gold wave in a navy rounded square + "Cruise*Deals*" + "by Shmor.ai" pill. Home: sunset ship photo hero with a cream search card (Where to sail + "Cruise region" select, folded into `?q=`), quick chips, then "Start exploring" cards moved up with CSS `order`. Numbered tiles look like gold-rimmed portholes. Bottom CTA = navy-to-bronze sunset band. Mobile checked at 375px (search stacks, no horizontal scroll).
**Photos:** every page has a free-licence Unsplash `"image"` (hotlinked, resized by URL): banner + card + og:image. To change one, swap `src`/`credit`/`creditUrl` and rebuild.

## Content rules
Factual and evergreen: no invented fares, deals, statistics or reviews. Seasons are given as "roughly"; anything that changes (entry rules, fees) uses "as of" wording and links official sources (`"sources"` on posts). Copy covers UK/EU protections (ATOL, Package Travel Regulations/Directive) and US (line terms + insurance). Blog posts: researched, linked from 1–3 pages via `"related"`, and their topic terms added to `shmor-site.json` keywords.
- The entry-rules post (EES / ETIAS / UK ETA) was checked 2026-10-13: ETIAS not yet operating; re-check when the EU announces a start date and update `updated`.

## Search routing on shmor.ai
`shmor-site.json` keywords route cruise searches here. On 2026-10-13 the bare keyword "cruise" was removed from TravelDeals so "cruise" searches come to CruiseDeals instead.

## Commands (run here)
```bash
node tools/build.js           # rebuild after ANY change to content/, templates/ or shmor-site.json
node tools/build.js --check   # validate only
node tools/serve.js 4003      # preview http://localhost:4003  (preview config "cruisedeals")
```
After changing `shmor-site.json` (links, keywords, card), also run `node tools/sync-network.js` in `../../shmor-ai`.

## Adding referral links
1. Add to `shmor-site.json` → `"links"`: `"slug": { "merchant", "network": "awin|cj|…", "url": "https://…" }` (or `"url": { "us", "uk", "eu" }`). Prefix slugs with the merchant name.
2. Show it on pages: add the slug to a page's `"partners": [...]`, or add an `"offers"` entry (`"pages": ["slug"]` to limit where it shows).
3. `node tools/build.js`, then sync the master, then commit both repos.
Likely programmes: cruise lines and cruise agencies on Awin (UK/EU) and CJ/Impact (US).

## Ideas / next
Referral links · more port/region pages (Canary Islands cruises, Baltic, Greek islands, Bahamas, cruises from Miami/Seattle) · a social share image (`seo.image`) · a weekly blog task like TravelDeals'.
