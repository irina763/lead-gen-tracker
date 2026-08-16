# Listings — 2600 Pennsylvania Ave NW #8A (rental)

Two files, both pasted into a single Elementor HTML widget each.

| File | Where it goes |
|---|---|
| `2600-pennsylvania-ave-nw-8a-rental.html` | the new listing page, at `/2600-pennsylvania-ave-nw-8a-washington-dc/` |
| `featured-listings-hub.html` | replaces the existing "Look inside the house" hub widget |

---

## How a rental page differs from a sale page

| Sale page (Breezy Down) | This rental page | Why |
|---|---|---|
| One-time price | A **rate** — `$4,800 / month`, unit shown everywhere | A rent number without a unit is ambiguous |
| Cash to close | **Total to move in** — first month + deposit + move-in fee + application = **$9,950** | This is the number renters actually shop on, and nobody publishes it |
| Taxes, HOA fee | **Utilities split** — who pays what | Taxes and condo fees are the landlord's problem, not the tenant's |
| — | **Lease terms** — term length, available date, pets, furnished | No equivalent on a sale |
| — | **How to qualify** — 3× income, screening, references | Renters self-select out or in before they tour; saying it up front saves showings |
| 3 levels, floor switcher | One level, switcher hides itself | Add a second key to `ROOMS` and the switcher comes back automatically |
| Yard & deck | **Views & balcony** | The balcony *is* the outdoor space, and the view is the product |
| Buyer guides | Renter guides + "when you're ready to buy" | A renter today is a buyer in 18 months — this is the lead-gen hook |
| MD schools / MD crime data | **DC** sources: DC boundary finder, OSSE report card, MPD, Crime Cards | Different jurisdiction entirely |
| — | Source-of-income line | The DC Human Rights Act bars source-of-income discrimination. Saying nothing is a risk; saying it plainly is not |

One structural change worth keeping: **every number lives once**, in the `FACTS` and `LEASE`
objects at the top of the script, and the hero, specs grid, lease module and legal line all
render from them. Change the rent in one place and it changes in six. (The sale page has
1,560 sq ft in the hero and 1,580 in the specs grid — that is the bug this prevents.)

---

## Before this goes live

### Photos — live

All 14 supplied files are wired in and `USE_PLACEHOLDERS` is now `false`, so a bad slug shows
as a broken image instead of hiding as a dark tile. Folder confirmed: `.../uploads/2026/08/`.

**Do not tidy the slug strings.** They carry WordPress's artefacts and must match the upload
byte for byte: trailing hyphens (`One-bathroom-`), duplicate-name counters (`-1`, `-1-1`),
and the edited-image suffix (`-e1786804075244`).

| Where | Photos |
|---|---|
| Hero (lead) | `panoramic-view-from-the-living-room` |
| Hero rotation | living room w/ fireplace, balcony w/ built-ins, bedroom |
| Room 01 — living room | panoramic (lead) + fireplace/balcony + hallway view |
| Room 02 — galley kitchen | `kitchen` (lead) + another angle + galley zoomed out |
| Room 03 — bedroom | `One-Bed-with-the-city-view-` (lead) + `-1-1` |
| Room 04 — bathroom | `One-bathroom-` (lead) + `-1-1` |
| Views & balcony | the 4 balcony files |

The bedroom and the bathroom are each a **two-photo sequence**, the same as the kitchen and
balcony pairs. If the `-1-1` files turn out to be duplicate uploads rather than second angles,
delete that entry from `GAL.bedroom` / `GAL.bath` and the lightbox drops back to one photo.

### Still no photos for

Building (facade, lobby, elevator, garage), neighbourhood aerials, floor plan. Those sets are
empty arrays, and an empty set now **removes its grid** — the building block drops to one
column, the aerials grid and its intro paragraph disappear, and the floor-plan tour card reads
"Coming soon". Add entries to `GAL.building` / `GAL.neighborhood` / `GAL.floorplan` (and the
matching `BUILDINGSET` / `HOODSET` tiles) and each section reappears with no other change.

The unit is 2 bed / 2 bath per the MLS; one of each is photographed, so the room explorer shows
one bedroom and one bathroom while the specs grid still reports 2 and 2.

### Fill in — only if these ever exist
There is no 3D tour and no video for this listing, so the "A closer look" section renders the
**map itself**, full width, under "See exactly where it sits." — and the map is then left out
of the location section, so it appears exactly once on the page. The nav link reads "Map".

Add a tour, a video or a floor plan and that section reverts to a card grid, with the map
moving back to its column in the location section. Cards with nothing behind them are never
rendered; if nothing at all is live the section and its nav link are removed.

- `TOUR_URL` — a public 3D tour link. Empty = no hero tour button, no tour card.
- `VIDEO_ID`, `AREA_VIDEO_ID` — YouTube ids. Same behaviour.
- `PROXI_MAP_ID` — **set** to `6a81c4de6096b9ae6b09d844`. See the paragraphs above for where
  the map renders. (Empty would remove it entirely and run the location facts full width.)
- The listing page URL, if it isn't `/2600-pennsylvania-ave-nw-8a-washington-dc/` (used in the hub block and the hero fallback).

### Confirmed with the landlord

- Garage space **and a separate storage unit**, both included in the rent. Storage is not in the
  MLS record.
- Application fee **$50 per application** (not per adult), through **RentSpree**.
  `APPLY_URL = https://apply.link/1TWaQ8w` — the CTA is now a direct "Apply on RentSpree" link.
- **Renter's insurance required** for the term of the lease.
- **Move-in fee is non-refundable** (the security deposit is refundable per DC law and the lease).
- **Fireplace is gas and working.**
- **Square footage published as a flat 1,100 sf**, no "estimated" qualifier — Bright now
  distinguishes assessor figures from agent-supplied estimates, so the qualifier read as doubt
  rather than precision.

One wording note: the page says renter's insurance is **"Required for the term of the lease"**
rather than "legally required." DC has no statute obliging a tenant to carry it — it is a lease
requirement, universal in practice but contractual. "Required" is true and enforceable; "legally
required" is a legal claim on a public page, and not one worth making.

### Verify yourself
- Every walk time / distance in `LOC_FACTS`. They currently say "Walkable" / "Nearby" rather
  than a number **on purpose** — do not publish a distance you haven't checked.
- The DCPS boundary finder link, and whether you want the named in-boundary schools listed
  (see `[P5]` in the schools section).
- `BUILDING_FACTS` — floors, elevator, intercom, garage.

---

## 7807 Breezy Down Terrace — price reduction

$499,000 → **$475,000**, shown three ways on the detail page so it matches the hub:

- hero: a filled **Price reduced** flag next to "Active"
- hero price: `$499,000` struck through, `$475,000` beside it
- specs grid Price cell: `$475,000` with the struck former price beneath

The 3D tour URL is confirmed correct and appears in three places (hero button, tour
card grid, hub block) — change all three together.

---

## 7807 Breezy Down Terrace — square footage correction

Per MLS / county assessor:

| | sf |
|---|---|
| Above grade, finished | 1,060 |
| Below grade, finished | 300 |
| Below grade, unfinished | 200 |
| **Total below grade** | **500** |
| **Total finished** | **1,360** |
| **Total** | **1,560** |

The page previously said 1,560 in the hero and 1,580 in the specs grid. Both are now
correct and the full breakdown is on the page, because portals headline "Total Fin SQFT"
(1,360) while the page leads with total (1,560) — showing the split is what reconciles the
two for a buyer who cross-references.

Changed in:
- `7807-breezy-down-terrace-rockville-md.html` — hero (now two stats: total and finished),
  specs grid (five cells + a source footnote), grid widened to 6 columns so 18 cells fill
  3 even rows
- `featured-listings-hub.html` — the Breezy Down block's specs line

Keep the specs grid a multiple of 6 cells when editing.
