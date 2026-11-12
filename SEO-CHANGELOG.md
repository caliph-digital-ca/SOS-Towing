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

## Open issues (not yet changed)
- The street address is not shown anywhere visibly on the site (e.g. footer or Contact page).
- St. Albert slug is `st-albert2`.
- Roadside Assistance service slug is misspelled: `roadside-assitance`.
