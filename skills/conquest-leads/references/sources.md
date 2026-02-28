# Lead Sources — Scanning & Extraction

This file contains the URL patterns, scan logic, and data extraction rules for each platform. Always extract real data — never guess or invent listing details.

---

## Source Priority Order

| Priority | Platform | Why |
|----------|----------|-----|
| 1 | **Craigslist** | Easiest to scan, fastest, highest volume, phone numbers often visible, no login |
| 2 | **CarGurus Private** | Clean data, good seller contact info, good make/model filtering |
| 3 | **AutoTrader Private Sellers** | High quality listings, phone numbers often exposed |
| 4 | **OfferUp** | Good for lower-price vehicles, mobile seller base |
| — | Facebook Marketplace | Skip for now — too slow and JS-heavy |

---

## CRAIGSLIST

### Search URL Pattern

```
https://[CITY].craigslist.org/search/cta?[FILTERS]
```

**City slugs (examples):**
| City | Slug |
|------|------|
| Miami | miami |
| Fort Lauderdale | broward |
| Orlando | orlando |
| Atlanta | atlanta |
| Dallas | dallas |
| Los Angeles | losangeles |
| New York | newyork |
| Chicago | chicago |
| Phoenix | phoenix |
| Houston | houston |

**Filter parameters:**
```
min_price=10000        → minimum asking price
max_price=60000        → maximum asking price
auto_make_model=BMW    → specific make (or "bmw+5+series" for model)
posted_today=1         → only listings from last 24 hours
search_distance=25     → radius in miles
zip=33101              → center zip code
```

**Full example — BMW listings in Miami under $60k posted today:**
```
https://miami.craigslist.org/search/cta?auto_make_model=BMW&max_price=60000&posted_today=1
```

**General cars for sale in Broward County:**
```
https://broward.craigslist.org/search/cta
```

---

### Craigslist — What to Extract

**From the search results page:**
Navigate to the search URL. For each listing result, extract:
- Listing title (year, make, model, trim if included)
- Asking price
- Post date/time
- Neighborhood/area
- Listing URL (for clicking through)

**From each individual listing page:**
Click through to get the full details:
- Full title
- Asking price
- Mileage (in the description or attributes section)
- Condition
- Full description text (look for: accident history, reason for selling, contact preference)
- **Phone number** — Craigslist often shows "show contact info" — click it and extract the number
- Photos (first photo URL for use in outreach)
- Post ID
- Seller location

**Phone extraction:** Look for the "show contact info" or "show phone number" button on the listing. Click it to reveal the number. This is the primary contact method for conquest outreach.

---

### Craigslist — Scan Flow

```
1. Build the search URL from the Search Profile (city + make/model + price range)
2. Navigate to the search results page
3. Collect all listing URLs from the results (up to the requested limit)
4. For each listing URL:
   a. Navigate to the listing
   b. Extract: title, price, mileage, description, phone, photos
   c. Add to the session's listing queue
5. Show summary to associate
```

---

## CARGURUS — PRIVATE PARTY

### Search URL Pattern

```
https://www.cargurus.com/Cars/inventoryresults.action?zip=[ZIP]&distance=[MILES]&sellerTypes=PRIVATE&listingTypes=USED
```

**With make/model filter:**
```
https://www.cargurus.com/Cars/inventoryresults.action?zip=33101&distance=50&sellerTypes=PRIVATE&trim=BMW+5+Series
```

**What to extract per listing:**
- Year, make, model, trim
- Mileage
- Asking price
- Seller name (private sellers show real names on CarGurus)
- Seller phone (often visible)
- Seller location
- Vehicle history notes (accidents, owners)
- Listing URL
- Primary photo URL

---

## AUTOTRADER — PRIVATE SELLERS

### Search URL Pattern

```
https://www.autotrader.com/cars-for-sale/all-cars/cars-between-[MIN]-and-[MAX]/[CITY]-[STATE]?sellerTypes=private
```

**Example — private BMW sellers in Miami:**
```
https://www.autotrader.com/cars-for-sale/bmw/miami-fl?sellerTypes=private
```

**What to extract per listing:**
- Full vehicle specs (year, make, model, trim, mileage, transmission)
- Asking price
- Seller phone number (often displayed on the page)
- Seller name
- Listing description
- Photos
- Listing URL

---

## OFFERUP

### Search URL Pattern

```
https://offerup.com/search/?q=[MAKE+MODEL]&radius=[MILES]&location=[CITY]
```

**Example:**
```
https://offerup.com/search/?q=BMW&radius=50&location=Miami+FL
```

**What to extract per listing:**
- Vehicle title, price
- Seller profile name and rating
- Location
- Photos
- Description
- Listing URL (individual item URL for contact)

**Note:** OfferUp contact requires navigating to the listing and using their message UI. Phone numbers are sometimes in the description. Extract whatever contact info is visible in the listing text.

---

## Multi-Source Scan Mode

When associate says "scan all sources" or "find trade-in leads today":

Run scans in this order:
1. Craigslist (city from Search Profile)
2. CarGurus private (zip from Search Profile)
3. AutoTrader private (city/state from Search Profile)

Collect all results into a unified listing queue. Deduplicate by VIN or (make + model + year + price) if VIN not available.

---

## Listing Summary Display

After scanning, display results in a clean table:

```
📡 CONQUEST SCAN RESULTS — [DATE]
Source: Craigslist Miami | BMW | Under $60k | Posted Today
─────────────────────────────────────────────────
Found [N] listings:

#  | Year | Make/Model      | Miles  | Asking  | Phone        | Location     | URL
---|------|-----------------|--------|---------|--------------|--------------|-----
1  | 2021 | BMW 5 Series    | 32,000 | $38,500 | 305-555-1111 | Coral Gables | [link]
2  | 2020 | BMW X5          | 47,000 | $44,000 | No phone     | Doral        | [link]
3  | 2019 | BMW 3 Series    | 58,000 | $27,900 | 786-555-2222 | Hialeah      | [link]
4  | 2022 | BMW M4          | 18,000 | $59,000 | 305-555-3333 | Brickell     | [link]
─────────────────────────────────────────────────
✅ [N] with phone numbers | ⚠️ [N] email-only

What do you want to do?
A) Contact all listings with phone numbers (batch mode)
B) Pick specific ones to contact
C) Save all to my lead list without contacting yet
D) Filter this list (price, mileage, year)

Reply A, B, C, or D.
```

---

## Data Quality Rules

- **Never invent contact info.** If no phone is found, mark as "email-only" and use the platform's message/reply system
- **Always note the listing source** (Craigslist, CarGurus, etc.) in the lead log
- **Always save the listing URL** — needed for reference in outreach and for logging
- **Never scrape the same listing twice in the same session** — check session queue before navigating
- **If a listing is marked SOLD or DELETED**, skip it and note it in the scan summary
