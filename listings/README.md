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

### Photos — you're sending these
Every image slug starts with `PH-` and renders as a dark tile until swapped. Replace one at a
time in `GAL` / `ROOMS` / `HERO_LOOP` near the top of the script. When the last `PH-` is gone,
set `USE_PLACEHOLDERS = false` so a typo shows as a broken image instead of hiding silently.

Also confirm the upload folder — the file assumes `.../uploads/2026/08/`.

Shot list the page is built around:

- **Hero + rotation (4):** balcony/river view, living room at sunset, building exterior, Georgetown from the balcony
- **Rooms (9 leads):** entry, living room, dining area, galley kitchen, primary bedroom, primary bath, second bedroom, second bath, washer/dryer
- **Room extras (9):** living ×3, dining ×1, kitchen ×2, primary ×2, primary bath ×1, bedroom 2 ×1
- **Views (5):** balcony, Potomac view, Georgetown sunset, balcony seating, view at night
- **Building (4):** Art Deco facade, lobby, elevator, garage entry
- **Neighborhood (7):** building from above, West End from above, Georgetown Waterfront, Potomac & Rock Creek, Foggy Bottom–GWU Metro, Kennedy Center, M Street
- **Floor plan (1)**

The hub block needs the hero photo URL in two places (`data-hero` and the thumb `src`).

### Fill in
- `TOUR_URL` — the **public** 3D tour link. Empty = the hero button and tour card hide/downgrade themselves, no dead link.
- `VIDEO_ID`, `AREA_VIDEO_ID` — YouTube ids. Same downgrade behaviour.
- Proxi map `data-id` — currently `REPLACE_WITH_2600_PENN_MAP_ID`.
- The listing page URL, if it isn't `/2600-pennsylvania-ave-nw-8a-washington-dc/` (used in the hub block and the hero fallback).

### Verify with the landlord / property manager
- **Is the garage space included in the rent, or extra?** The page currently implies included.
- **Application fee $50 — per adult, or per application?**
- Renter's insurance required?
- Is the $300 move-in fee refundable, and is it the building's or the landlord's?
- Square footage is MLS "estimated" — the page says so; confirm you're comfortable publishing it.
- Fireplace: working, gas or wood, or decorative?

### Verify yourself
- Every walk time / distance in `LOC_FACTS`. They currently say "Walkable" / "Nearby" rather
  than a number **on purpose** — do not publish a distance you haven't checked.
- The DCPS boundary finder link, and whether you want the named in-boundary schools listed
  (see `[P5]` in the schools section).
- `BUILDING_FACTS` — floors, elevator, intercom, garage.
