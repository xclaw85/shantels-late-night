# Shantel's Late Night Dinner Service

Business site for a late night dinner delivery, after-hours grocery, and concierge
errand service in the Lake Arrowhead area.

**Phone:** (909) 636-0919
**Hours:** Nightly, 8:00 PM – 3:00 AM

Single static HTML file. No build step, no dependencies, no trackers.

## Design

"Night Canopy": a dark forest-green theme drawn from the local mixed-conifer forest.
The pines hang from the top edge so the visitor is looking up into the canopy, lit by a
moonlit sky behind them. The ridgelines, bough, cone, acorn and owl are generated SVG
(see notes below), not stock art.

Dynamic pieces:

- **Live open/closed status.** Reads the visitor's clock and shows "Open now",
  "Open - last orders" after 2:30 AM, or "Opens in 4h 12m" when closed. Updates
  every 30 seconds. Appears in the hero and above the phone number.
- **Inverted canopy** in the hero, silhouetted against a moonlit sky gradient.
- **Drifting mist** band that slowly crosses the canopy.
- **Blinking owl** (great horned, *Bubo virginianus*) in the concierge section.
- **Reveal-on-scroll** for each section, staggered, plus a card hover lift.

All motion is disabled under `prefers-reduced-motion`, and every section stays
visible with JavaScript switched off.

### Regenerating the artwork

The SVG path data was produced by a generator (seeded, so it is reproducible):
conifers are stacked triangles with a width taper, ridgelines lay them out across
a 1440-unit span, and the bough sweeps needles back along a bezier. The paths are
baked into `index.html`, so there is no build step to run.

## Hosting (GitHub Pages)

Repo → **Settings** → **Pages** → Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → Save.

Live at `https://xclaw85.github.io/shantels-late-night/` within a minute or two.
A `.nojekyll` file is included so the site is served exactly as written.

### Custom domain (optional)

For something like `shantelslatenight.com`:

1. Buy the domain.
2. At your DNS provider add four `A` records for the apex, all host `@`:
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. Add a `CNAME` record: host `www` → `xclaw85.github.io`
4. Repo → Settings → Pages → Custom domain → enter the domain → Save, then tick
   **Enforce HTTPS** once the certificate is issued (can take up to an hour).

## Editing the site

Everything lives in `index.html`. Common edits:

| What to change | Where |
|---|---|
| Phone number | 4 places, each marked `<!-- PHONE -->`. Keep the `tel:` links in E.164 form (`+19096360919`) |
| Hours | Hero `.hours-note`, the Hours row in `#area`, and the contact `.sub` line |
| Service area towns | `#area` → the "Area" row |
| Service descriptions | `#services` → the three `.card` blocks |
| Concierge list | `#concierge` → the `<ul>` |
| Colors | The `:root` block at the top of `<style>` |

To change the phone number everywhere at once:

```bash
sed -i 's/+19096360919/+1NEWNUMBER/g; s/(909) 636-0919/(NEW) FORMAT-TED/g' index.html
```

## Details to verify before promoting the site

These were written as sensible defaults and should be confirmed:

- Hours of 8:00 PM – 3:00 AM, last dinner order 2:30 AM
- Service area list: Blue Jay, Cedar Glen, Crestline, Running Springs, Twin Peaks,
  Sky Forest, Lake Gregory, Arrowbear
- Payment methods: card, cash, mobile payment
