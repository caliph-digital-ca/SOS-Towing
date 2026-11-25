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

### 301 redirects (added by owner in Site settings, 2026-11-13)
- `/services/roadside-assitance` → `/services/roadside-assistance`

### Waiting on owner input
- Google Business Profile could not be read from the cloud work environment (Google returns a CAPTCHA), so these are still open.
- Years in business: site currently says "Over 10 Years" (home/Start heading + paragraph), "13+ Years" (stat on Home, About,
  Start, Locations template), "15+ Years Experience" (`section-call` component, 6 pages), and "Since 2010" / "founded in 2010"
  (About, Services template, Blog, Locations template).
- Customer stat "500+ Customers" (Home, About, Start, Services template, Locations template).
- Business email to replace sostowinc@gmail.com (footer component, Contact page); footer email to become a mailto: link.
- Social URLs (Facebook / LinkedIn / X) for the 3 footer icons, all currently `#`.
- Whether to show the GBP address (10742 81 Ave NW, Edmonton, AB T6E 1Y2) in the footer and Contact page.
- Optional pricing line near "Get a Free Estimate".

### Second batch (staged)
| Issue | Where it lives | Change |
|---|---|---|
| Wrong phone (780) 720-5535 | Services template (all service pages) | Two "CALL NOW" labels and the quote paragraph now say (780) 280-5535; the call button that dialed 720 now dials 7802805535 |
| "Affrodable" | Services template heading | "Affordable" |
| Mobile call bar linked to URL `7802805535` | Home page `call-mobile` instance (prop override) | Now a phone (tel:) link to 7802805535 |
| Hero "Get A Free Estimate" had no link | Home page | Links to `#free-estimate`; added DOM id `free-estimate` to the `section-form` component root |
| "Average Response Time" card linked to `#` | `section-form` component, Link 3 prop default | Now a phone link to 7802805535, matching the other two cards |
| Footer credit link `caliphdigital.ca` (relative) | `footer` component | `https://caliphdigital.ca`, opens in new tab |
| "the the" + hidden U+2060 character | Parking Enforcement CMS item body | Removed both |
| St. Albert slug `st-albert2` | Locations CMS item | Now `st-albert` (CMS-bound links update automatically) |
| Blog said 30–60 min response | Roadside Assistance blog post body (2 places) | Now states SOS Towing's ~15-minute average, with the weather/demand caveat kept |
| Blog image alt text missing | Blogs CMS | Cheap Towing post: "Flatbed tow truck picking up a Chevy Cruze beside a highway". Roadside post: "Tow truck hooking up a damaged car on a snowy roadside in winter" |

### 301 redirects (added by owner, 2026-11-13)
- `/location/st-albert2` → `/location/st-albert`

### Still open (report only)
- Reviews heading in `section-reviews` says "Join Hundreds of Satisfied Customers" while the badge says 200+ five-star reviews; align once the customer figure is known.

## 2026-11-19 — New blog posts 1 and 2 (PUBLISHED 2026-11-19)

### "How Much Does Towing Cost in Edmonton? (2026 Price Guide)" (Post 1 of 4)
Blogs CMS item `6aff252bb7ad248f736568e1`, saved as a **draft**. It stays
off the live site, even on a full site publish, until it is switched to
published in Webflow.

| Field | Value |
|---|---|
| Name / H1 | How Much Does Towing Cost in Edmonton? (2026 Price Guide) |
| Slug | `towing-cost-edmonton` → `/blog/towing-cost-edmonton` |
| Meta description (156) | 2026 towing prices in Edmonton: hook-up fees, per-km rates, flatbed and winch-outs. Free accident towing with direct insurance billing. Call (780) 280-5535. |
| Feature image | New asset `towing-cost-edmonton-flatbed-sedan-1200.webp` (1200px WebP, 99 KB), resized from the existing stock photo of an operator loading a sedan onto a flatbed |
| Image alt | Tow truck operator strapping a dark sedan onto a flatbed tow truck |

Notes:
- The meta description in the draft was 161 characters; "Real" was dropped from the start to fit the 160 limit.
- Meta title: the Blog template builds the title as `{h1} | SOS Towing`, so the title is
  "How Much Does Towing Cost in Edmonton? (2026 Price Guide) | SOS Towing" (70 characters).
  The draft's meta title ("How Much Does Towing Cost in Edmonton? 2026 Prices") would need its own template field.
- The feature image alt text describes the photo itself. The draft's alt text ("...on an Edmonton street at dusk")
  doesn't match this stock photo; use it once a real SOS job photo replaces the image.
- Webflow rich text has no tables, so the price table is a bulleted list.
- The body contains the draft's placeholders as-is (`[price range]`, `[rate per km]`, `[X] km`, the author byline,
  the night/weekend surcharge policy, accident-towing conditions, payment methods, the first-hand
  "What We See on Edmonton Roads" paragraph and 2 job photos). Fill these before publishing.
- "Related reading" titles are plain text until those posts exist.
- Not done: Article and FAQPage JSON-LD. The Blog template has no per-post schema field; this needs a template
  custom-code embed bound to CMS fields, or schema added per post once it's final.

### "Car Won't Start in the Cold? Boost, Battery Replacement or Tow" (Post 2 of 4)
Blogs CMS item `6aff26c5364e1bdcb473152c`, saved as a **draft** (not on the live site).

| Field | Value |
|---|---|
| Name / H1 | Car Won't Start in the Cold? Boost, Battery Replacement or Tow |
| Slug | `car-wont-start-cold-edmonton` → `/blog/car-wont-start-cold-edmonton` |
| Meta description (154) | Car won't start in the cold? Learn if you need a boost, a new battery or a tow, and what each costs in Edmonton. 24/7 mobile service. Call (780) 280-5535. |
| Feature image | New asset `car-wont-start-cold-battery-replacement-640.webp` (640px WebP, 23 KB), from the stock battery photo already used on the Battery Replacement service page |
| Image alt | Technician lifting a new car battery into place under an open hood |

Notes:
- Page title from the template: "Car Won't Start in the Cold? Boost, Battery Replacement or Tow | SOS Towing"
  (75 characters). The draft's meta title ("Car Won't Start in Edmonton Cold? Boost, Battery or Tow") needs its own template field.
- The only battery photo on the site is 640px wide, which is low resolution for a feature image. Replace it with a
  real job photo (battery test in a snowy driveway) at 1200px or wider, then use the draft's alt text.
- The symptom table is a bulleted list (Webflow rich text has no tables).
- Placeholders kept as in the draft: boost price, replacement price range, battery age, warranty, boost-fee credit,
  battery sizes, replacement time, byline, first-hand paragraph and 2 photos.
- Not done: Article and FAQPage JSON-LD (same reason as Post 1).

### Related-reading links between Posts 1 and 2
- Post 1 "Related reading" now links "Car Won't Start in the Cold?" to `/blog/car-wont-start-cold-edmonton`.
- Post 2 "Related reading" now links "How Much Does Towing Cost in Edmonton?" to `/blog/towing-cost-edmonton`.
- Both posts are drafts, so each link 404s until both posts are published. Publish them together.
- "Is Accident Towing Free in Edmonton?" and "Stuck in Snow or a Ditch?" stay plain text until Posts 3 and 4 exist.

### Published Posts 1 and 2 (2026-11-19)
Both CMS items published (item publish, not a full site publish):
- https://www.sostowing.ca/blog/towing-cost-edmonton
- https://www.sostowing.ca/blog/car-wont-start-cold-edmonton

Before publishing, I checked the prices against the site. No tow, boost or battery prices are published
anywhere I could check (Services CMS items list none; only parking-enforcement storage of $60/day), and
pricing is still waiting on owner input. So every price was removed rather than guessed:
- Post 1: the price table became "How SOS Towing Prices Each Service" (how each service is priced, no amounts);
  quick answer, FAQ and takeaways describe hook-up fee + per-km pricing without figures. Removed the night/weekend
  surcharge FAQ and the payment-methods FAQ (no confirmed policy). Removed the "Time of day and weather" H3.
  Meta description changed to: "How towing is priced in Edmonton: hook-up fees, per-km rates, flatbed and
  winch-outs. Free accident towing with direct insurance billing. Call (780) 280-5535." (158)
- Post 2: removed prices and the "[X] years" battery age ("several years old" instead); battery-cost FAQs now
  point to a phone quote. Removed the battery-size, warranty and boost-credit details (no confirmed policy).
  Meta description changed to: "Car won't start in the cold? Learn if you need a boost, a new battery or a tow
  in Edmonton. 24/7 mobile battery service. Call (780) 280-5535." (141)
- Both: removed the author byline, "What We See..." first-hand sections, photo placeholders, owner notes, and the
  related-reading placeholders for Posts 3 and 4. Posts 1 and 2 still link to each other.
- Kept only facts the site already states: free accident towing with direct insurance billing, 24/7 service,
  15-minute average response, on-site battery testing and replacement.

To add later (improves E-E-A-T): real prices, author byline, first-hand paragraphs and job photos, and
Article/FAQPage schema.

## 2026-11-23 — 404 fixes (redirects to be added in Webflow UI)

### 404s from old site URLs (301 redirects)
Search Console reported 404s on URLs left over from the previous site. Each is
mapped to the closest live page. The site is not on an Enterprise plan, so the
Webflow API cannot create redirects; these are added by hand in
Site settings → Publishing → 301 Redirects, then the site is republished.
Webflow matches with or without the trailing slash, so one rule covers both.

| Old path (404) | Redirect to | Why |
|---|---|---|
| `/towing-services` | `/services/emergency-towing` | No services index page exists; emergency towing is the core towing service |
| `/towing-near-me-in-edmonton-fast-help-with-sos-towing` | `/location/edmonton` | "Towing near me in Edmonton" intent matches the Edmonton location page |
| `/contact-us` | `/contact` | Renamed page |
| `/about-us` | `/about` | Renamed page |

After publishing, check each old URL returns 301 to its target, then use
"Validate fix" on the 404 report in Search Console.

## 2026-11-25 — New blog posts 3 and 4 (PUBLISHED 2026-11-25)

Both created in the Blogs CMS and published (item publish, not a full site publish):
- https://www.sostowing.ca/blog/free-accident-towing-edmonton
- https://www.sostowing.ca/blog/car-winching-cost-edmonton

### "Is Accident Towing Free in Edmonton? How Insurance Billing Works" (Post 3 of 4)
| Field | Value |
|---|---|
| CMS item | `6b06f5510f8e3c5e8e273c55` |
| Name / H1 | Is Accident Towing Free in Edmonton? How Insurance Billing Works |
| Slug | `free-accident-towing-edmonton` |
| Meta description (158) | After a collision in Edmonton, SOS Towing tows your vehicle free and bills your insurer directly. Learn how it works and what to do next. Call (780) 280-5535. |
| Feature image | Existing asset `roadside-assistance-car-loaded-on-tow-truck-1000.webp` (1000px WebP, 62 KB) |
| Image alt | Tow truck operator loading a silver car onto a flatbed tow truck |

### "Stuck in Snow or a Ditch in Edmonton? Winch-Out Cost and What to Do" (Post 4 of 4)
| Field | Value |
|---|---|
| CMS item | `6b06f5510f8e3c5e8e273c57` |
| Name / H1 | Stuck in Snow or a Ditch in Edmonton? Winch-Out Cost and What to Do |
| Slug | `car-winching-cost-edmonton` |
| Meta description (154) | Stuck in snow, mud or a ditch in Edmonton? See what affects winch-out cost, how it differs from a tow and what to do while you wait. 24/7: (780) 280-5535. |
| Feature image | New asset `car-winching-snowy-ditch-1200.webp` (1200px WebP, 52 KB), resized from the existing 1920px snowstorm stock photo |
| Image alt | Tow truck on a snowy rural road near a dark SUV stuck in a roadside ditch |

### What was changed from the drafts
Same approach as Posts 1 and 2: anything the owner hasn't confirmed was removed rather than guessed.
- Post 3 meta description was 171 characters; shortened to 158 ("at no cost to you" → "free").
- Post 4 meta description said "See what a winch-out costs", but no price is published; now "See what affects winch-out cost".
- Feature image alt text describes the stock photos actually used; the drafts' alt text needs real SOS job photos.
- Tables (billing steps, winch-out vs tow) became lists, since Webflow rich text has no tables. The winch-out
  list drops the price column.
- Removed: author bylines, the "What We See..." first-hand sections and photo placeholders, owner notes,
  "Before Publishing" checklists, and every placeholder answer.
- Post 3 FAQs removed (no confirmed policy): basic-coverage pricing, storage fees after an accident tow,
  shop referral payments. Removed "what happens when the other driver is at fault". "We do this every week"
  became "We can do this for you". Billing step 3 says "invoice" (dropped "and photos").
- Post 4: quick answer and cost FAQ point to a phone quote instead of a price range or recovery time. Removed
  FAQs on insurance/roadside-plan coverage and on paying when a recovery fails; removed the rural travel fee.
  Storm response FAQ keeps the 15-minute average and says times can be longer in heavy snow (no figure).
- Kept: free accident towing with direct insurance billing (GBP and site), 24/7, 15-minute average response,
  the EPS and AMA facts as cited in the drafts.

### Not verified
- The EPS ($5,000 threshold, $405 fine, tow to Collision Reporting Centre) and AMA pages could not be loaded
  from the cloud work environment. The facts are as written in the drafts; recheck the EPS page, since the
  threshold and fine can change.
- The Post 4 damage section ("recovery points or soft straps, slow straight pull") is kept from the draft;
  the owner should confirm it matches how operators work.

### Internal links
- Post 3 related reading links Posts 1 and 4; Post 4 links Posts 1, 2 and 3.
- Posts 1 and 2 (updated and republished 2026-11-25): "Related reading" in both now links Posts 3 and 4.
  Post 1's FAQ "Is accident towing really free?" also links to Post 3 ("how direct insurance billing works").
  No other text changed.
- Not done: Article and FAQPage JSON-LD (Blog template has no per-post schema field, same as Posts 1 and 2).

To add later: real winch-out and non-covered accident-tow prices, storage fee policy, author bylines,
first-hand paragraphs and job photos.

## 2026-11-25 — Drew's Autosports: ceramic coating blog posts

Note: these changes are on a different Webflow site, Drew's Autosports (site ID `6a29afc4bb1347dad843ffac`,
Blogs collection `6a4fbf6f5ab64cc8b8e1bb52`), not the SOS Towing site. They are logged here as requested.

| Post | Slug | Status |
|---|---|---|
| How to Maintain Your Ceramic Coating: A Kelowna Owner's Guide | `/blog/ceramic-coating-maintenance` | Published 2026-11-25 |
| Spray Ceramic vs Professional Ceramic Coating: What's the Real Difference? | `/blog/spray-ceramic-vs-professional-ceramic-coating` | Published 2026-11-25 (moved up from 2026-11-26 at owner's request) |

### Format
Matches the existing Drew's posts: H1 + italic summary at the top of the Article rich text, internal links
relative, external links open in a new tab, CTA block with quote link, phone, address and hours.
Tables (care schedule, spray vs pro comparison) became bold-label lists, since Webflow rich text has no tables.

### Facts filled from Drew's own site (Webflow CMS)
- "Certified in ceramic coating for over 8 years" (Ceramic Coating service description) was added to Post 2.
- Warranty range (2 years Bronze to lifetime Gold), CarFax registration, full address with postal code:
  as already published on the site and earlier posts.

### Removed (not confirmed, per owner instruction to skip unknowns)
- Author bylines and dates, both "first-hand" notes and photo placeholders, the "Before Publishing" checklists.
- Post 1: "[confirm cure guidance]" note (the first-week rules are kept as written in the draft), "[confirm if
  required for warranty]" on the 12-month inspection, and the FAQs "When can I wash my car after a ceramic
  coating?" and "Does my coating warranty require maintenance?".
- Post 2: the whole "What We See When Customers Try DIY" section (it was only a placeholder), the starting
  price in the comparison (now "higher"), and the cost FAQ now points to packages and a free quote instead of a price.

### Images
The drafts' alt text described photos that don't exist yet (beading on a black Porsche hood; spray bottle next
to a pro kit), so existing site photos were used and the alt text describes them:
- Post 1: black Chevrolet Silverado in the Drew's coating studio. This is the same photo as the PPF vs
  Ceramic post's featured image.
- Post 2: red sports car with its hood raised in a showroom.

### Internal links
- Post 1 links the home wash guide, PPF vs Ceramic, the ceramic coating service and pricing, Kelowna and Vernon.
  Post 2 links Post 1, PPF vs Ceramic, paint correction, ceramic coating and pricing, and the location pages
  for Kelowna, Vernon, Summerland, Oliver and Osoyoos (all confirmed live).
- Post 1's Related reading now also links Post 2 (republished 2026-11-25).

### Not done
- Meta title and description: the Drew's Blogs collection has no SEO fields, so the template sets these.
  The drafts' meta titles and descriptions were not applied.
- Article, HowTo and FAQPage JSON-LD: there is no per-post schema field.
- The Drew's website and the GBP link could not be loaded from the cloud work environment.

## Open issues (not yet changed)
- The street address is not shown anywhere visibly on the site (e.g. footer or Contact page).
- St. Albert slug is `st-albert2`. (Fixed 2026-11-13, staged; needs 301 redirect.)
- Roadside Assistance service slug is misspelled: `roadside-assitance`. (Fixed 2026-11-13, staged; needs 301 redirect.)
