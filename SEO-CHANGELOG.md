# SOS Towing – SEO & Technical Fix Log

The site is built and hosted in Webflow (site ID `69bb13b52a5c9c60f9778571`).
This file records changes made to the live site, since the site code itself
does not live in this repository.

## 2026-11-12

### 1. External JavaScript returning 3XX (all pages)
Site settings → Custom code → Footer loaded unversioned unpkg URLs that
302-redirect to the latest version. Pinned to exact files with SRI hashes:

```html
<script src="https://unpkg.com/@formspark/formson@0.4.0/dist/index.global.js"
  integrity="sha384-TeLSlxvcK3t3Xf580bLtaN8gv+Ux5AemLgqcquOW3AG8gP55Qu1lEsbJz8DzzloY"
  crossorigin="anonymous"></script>
<script src="https://unpkg.com/@botpoison/browser@1.2.0/dist/index.js"
  integrity="sha384-Coq4yXcH6P37EoKbvbmZZj3UpsLwU5Ir/tth7Fgf24Q5JUj2I4hcwqtj3zKi7+PA"
  crossorigin="anonymous" async></script>
```

To upgrade later: change the version in the URL and regenerate the hash
(`openssl dgst -sha384 -binary FILE | base64`).

### 2. No inbound links: /start and /thank-you
These are an ad landing page and the form confirmation page, so they are
intentionally not linked. Instead:
- Excluded both from the sitemap.
- Added `<meta name="robots" content="noindex, follow">` to each page's head code.

### 3. Title too short
| Page | New SEO title |
|---|---|
| Home | SOS Towing Edmonton \| 24/7 Towing & Roadside Assistance |
| About | About SOS Towing \| Trusted Edmonton Towing Company |
| Blog | Towing & Roadside Tips Blog \| SOS Towing Edmonton |
| Contact | Contact SOS Towing Edmonton \| 24/7 Towing Dispatch |

Blog meta description (was "Blog"): "Towing and roadside tips from SOS Towing
Edmonton: winter driving advice, battery and tire help, and what to do when
you break down on the road."

### 4. Description too long (max 160 chars)
Meta descriptions on CMS pages come from the Services `summary` field and the
Locations `description` field (these also appear as on-page intro text).
Shortened to 138–157 characters:

**Services**
- Battery Replacement (148): Fast car battery replacement in Edmonton. Our 24/7 mobile team tests, boosts, and replaces your battery on the spot so you can get back on the road.
- Tire Replacement (148): Fast tire replacement in Edmonton. Flat, damaged, or worn out, our 24/7 mobile team replaces your tire on-site and gets you back on the road safely.
- Parking Enforcement (152): Parking enforcement in Edmonton for residential, commercial, and private lots. We stop unauthorized parking, keep access clear, and maintain order 24/7.
- Car Winching (139): Fast car winching in Edmonton. Stuck in snow, mud, or a ditch? Our 24/7 team will safely recover your vehicle and get you back on the road.
- Luxury Car Towing (138): Luxury car towing in Edmonton with damage-free flatbed transport. We handle high-end and exotic vehicles with the care they deserve, 24/7.

**Locations** (pattern: "Fast, reliable 24/7 towing and roadside assistance in {City}. Emergency response, accident recovery, and towing across {City} and nearby areas.")
- Edmonton (147), St. Albert (151), Sherwood Park (157), Spruce Grove (155),
  Leduc (141), Devon (141), Stony Plain (153)
- Fort Saskatchewan (139): "...in Fort Saskatchewan. Emergency response, accident recovery, and towing across the area."

### 5. Location page content fixes
- Phone number on all 8 location pages corrected from (780) 720-5535 to (780) 280-5535.
- Fort Saskatchewan page body said "residents and businesses of Leduc"; corrected to Fort Saskatchewan.

### 6. Aligned with Google Business Profile
GBP: 10742 81 Ave NW, Edmonton, AB T6E 1Y2 · (780) 280-5535 · open 24 hours, every day · service area includes Beaumont.
- The location page at /location/beaumont was written for Devon. Renamed the CMS item to
  Beaumont and rewrote its description and body for Beaumont (URL unchanged).
- Added `AutomotiveBusiness` JSON-LD to the Home page: name, address, phone,
  24/7 opening hours, service areas (the 8 location pages), and a description
  based on the GBP description. No review/rating markup (Google ignores
  self-served ratings for local businesses).

### 7. Home page meta description (from GBP description)
Was: "Stranded on the road? We're here to help! Professional towing and roadside
assistance available 24/7 across Edmonton and surrounding areas."
Now (150): "Fast 24/7 car towing in Edmonton at reasonable rates. Direct insurance
billing and free accident towing. Call (780) 280-5535 and get back on the road."

### 8. Multiple H1 tags
- Locations template: the hero heading "Towing Services in {City}" was built
  from two H1 elements. "Towing Services in" changed to H2 (same `h1-main`
  class, so it looks the same); the CMS-bound city name stays the single H1.
- Blog post template: a second heading (class `h2-main`) was tagged H1;
  changed to H2. Article bodies contain no H1s.

### 9. Identical title and H1
- Services and Blog post templates: SEO title was bound to the same `h1`
  field as the on-page H1. Title is now `{h1} | SOS Towing`, e.g.
  "Emergency Towing Services in Edmonton | SOS Towing".
- Blog `h1` fields were lowercase keywords; capitalized:
  "Roadside Assistance in Edmonton", "Cheap Towing in Edmonton".
- Contact page was already fixed in #3 (title differs from H1 "Contact Us").

### 10. Missing image alt text
- Set alt text on 31 site assets in the Webflow asset library (logo, phone /
  clock / feature icons, photos, Google reviews badge, Edmonton skyline).
  Asset alt text applies wherever the image is used, including the shared
  navbar/footer, so it covers every page.
- Set alt text on each Services CMS item's `image` and `icon` fields
  (7 services, 14 images).

### 11. Image too big
Originals were 1920px JPEGs of 1.4–3.5 MB. Resized, stripped metadata, and
converted to WebP; all replacements are under 100 KB:
| Where | Before | After |
|---|---|---|
| Emergency Towing CMS photo | 1.8 MB | 90 KB (1200px) |
| Roadside Assistance CMS photo | 3.5 MB | 62 KB (1000px) |
| Parking Enforcement CMS photo | 1.4 MB | 48 KB (1200px) |
| Services template "Image 8" (all service pages) | 3.5 MB | 62 KB (swapped to the 1000px asset) |

Also compressed in place to WebP via Webflow (same asset ID, used elsewhere):
tow-truck-loading photo 1.8 MB → 208 KB, snowstorm accident photo 1.6 MB → 139 KB,
damaged-car photo 3.5 MB → 462 KB (no longer used on service pages).

## 2026-11-13 — Trust & consistency pass (STAGED, NOT PUBLISHED)

Changes below are saved in Webflow but not published. Awaiting owner approval
and the business facts listed under "Waiting on owner input".

### Done (staged)
| Issue | Where it lives | Change |
|---|---|---|
| Nav "Reviews" pointed to staging `https://sostowing.webflow.io#reviews` | `nav` component (all 8 pages) | Now `/#reviews` |
| Reviews section anchor | `section-reviews` component | Already had DOM id `reviews`; no change. Section holds an Elfsight Google Reviews widget embed. |
| Other `webflow.io` links | Searched all pages, components, CMS, site/page custom code, JSON-LD | None found |
| "Roadside Assitance" typo + slug | Services CMS item (feeds nav dropdown, footer list, homepage/About service cards) | Name → "Roadside Assistance"; slug `roadside-assitance` → `roadside-assistance`. Internal links are CMS-bound and update automatically. |
| Footer logo + quick links pointed to `#` | `footer` component (all 8 pages) | Logo → `/`, About Us → `/about`, Services → `/#services`, Service Areas → `/#service-areas`, Reviews → `/#reviews` |
| Missing anchor ids | Home page services section; `section-home-locations` component | Added DOM ids `services` and `service-areas` |

### Must do by hand before publishing
- Webflow Site settings → Publishing → 301 redirects: `/services/roadside-assitance` → `/services/roadside-assistance`
  (the Webflow API/MCP has no redirect endpoint).

### Waiting on owner input
- Years in business: site currently says "Over 10 Years" (home/Start heading + paragraph), "13+ Years" (stat on Home, About,
  Start, Locations template), "15+ Years Experience" (`section-call` component, 6 pages), and "Since 2010" / "founded in 2010"
  (About, Services template, Blog, Locations template).
- Customer stat "500+ Customers" (Home, About, Start, Services template, Locations template).
- Business email to replace sostowinc@gmail.com (footer component, Contact page); footer email to become a mailto: link.
- Social URLs (Facebook / LinkedIn / X) for the 3 footer icons, all currently `#`.
- Whether to show the GBP address (10742 81 Ave NW, Edmonton, AB T6E 1Y2) in the footer and Contact page.
- Optional pricing line near "Get a Free Estimate".

### Found, not fixed (report only)
- Services template shows the wrong phone number **(780) 720-5535** in 3 places (two "CALL NOW" texts and a quote paragraph) and one tel: link uses it.
- Services template heading typo "Affrodable".
- Parking Enforcement CMS body: "dispose of the the unclaimed vehicle" and an invisible character before "Storage fee".
- Home page mobile `call-mobile` instance links to URL `7802805535` (relative URL, not tel:) — broken on the home page only.
- Home hero "Get A Free Estimate" button has no link.
- `section-form` component "Average Response Time" card links to `#`.
- Footer "Website Powered By Caliph Digital" links to `caliphdigital.ca` without `https://` (resolves as a relative path → 404).
- St. Albert location slug is `st-albert2`.
- Blog "Roadside Assistance in Edmonton" says response is 30–60 min; the rest of the site says 15 min average.
- Blog featured images have no alt text.
- Reviews heading in `section-reviews` says "Join Hundreds of Satisfied Customers" while the badge says 200+ five-star reviews; align once the customer figure is known.

## Open issues (not yet changed)
- The street address is not shown anywhere visibly on the site (e.g. footer or Contact page).
- St. Albert slug is `st-albert2`.
- Roadside Assistance service slug is misspelled: `roadside-assitance`. (Fixed 2026-11-13, staged; needs 301 redirect.)
