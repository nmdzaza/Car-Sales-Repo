# Buyer Lead Sources — Active Shoppers

This file covers finding people who are **actively looking to buy a car** on public platforms. These are people who have already expressed intent — your job is to reach them with a relevant offer before someone else does.

---

## Source Priority Order

| Priority | Platform | Why |
|----------|----------|-----|
| 1 | **Reddit** | API accessible, high intent posts, searchable by keyword + location |
| 2 | **Craigslist Wanted** | Direct contact info visible, highest intent (they made an effort to post) |
| 3 | **Twitter/X** | Real-time, location-filterable, public DMs possible |
| 4 | **OfferUp WTB** | Mobile buyers, "want to buy" posts, geo-targeted |

---

## REDDIT

### Best Subreddits for Buyer Intent

| Subreddit | Type of Buyer | Notes |
|-----------|--------------|-------|
| r/whatcarshouldibuy | Active shoppers with budget + needs | Highest intent, posts always include budget and city |
| r/askcarsales | People seeking dealer/market advice | High trust environment — reply carefully |
| r/personalfinance | Buyers researching auto loans | Good for financing leads |
| r/autofinance | People actively applying for auto loans | Very high intent |
| r/usedcars | Used car hunters | Budget-conscious, good fit for pre-owned inventory |
| r/cars | General — lower intent but high volume | Use for brand-specific threads |
| r/[city subreddits] | Hyper-local buyers | e.g., r/Miami, r/Atlanta, r/Dallas |

---

### Reddit Search URL Patterns

**Subreddit search (JSON — no auth):**
```
https://www.reddit.com/r/[SUBREDDIT]/search.json?q=[KEYWORDS]&sort=new&t=week&limit=25
```

**Multi-subreddit search:**
```
https://www.reddit.com/search.json?q=subreddit:whatcarshouldibuy+[KEYWORDS]&sort=new&t=week
```

**Examples:**

Search r/whatcarshouldibuy for posts this week mentioning Miami:
```
https://www.reddit.com/r/whatcarshouldibuy/search.json?q=miami&sort=new&t=week&limit=25
```

Search for budget buyers under $15k:
```
https://www.reddit.com/r/whatcarshouldibuy/search.json?q=under+15k&sort=new&t=week&limit=25
```

Search r/autofinance for people applying for loans:
```
https://www.reddit.com/r/autofinance/search.json?q=approved+car+loan&sort=new&t=week&limit=25
```

---

### Reddit — What to Extract Per Post

For each relevant post:
- Post title
- Post body (full text — contains budget, city, car needs)
- Username
- Subreddit
- Post date
- Post URL (for replying)
- Any flair tags (e.g., "Budget: $10k-$15k")
- Comment count (high comments = high interest post, worth prioritizing)

**Buyer intent signals to look for:**
```
"looking for", "in search of", "need a car", "budget is", "can afford",
"under $Xk", "what should I buy", "help me choose", "first car",
"need reliable", "daily driver", "commute", "family car",
"just got approved", "pre-approved for", "financing for"
```

**Location signals:**
```
"in [city]", "near [city]", "[city] area", "[state] resident",
zip codes, "30 minutes from", "just moved to"
```

---

### Reddit Scan Flow

```
1. Build search URL using Buyer Hunt Profile city + buyer intent keywords
2. Fetch the JSON results
3. Parse each post: extract title, body, username, URL, date, city mentions
4. Score relevance:
   - Budget mentioned: +3 points
   - City matches target area: +3 points
   - Timeline mentioned ("need ASAP", "this month"): +2 points
   - Specific make/model: +1 point
   - Already posted in multiple subreddits: +1 point
5. Sort by score descending
6. Show results table to associate
7. For selected posts: draft a reply (see outreach-buyer.md)
```

---

### Reddit Results Display

```
📱 REDDIT BUYER SCAN — r/whatcarshouldibuy + r/autofinance
Keywords: "Miami" + "car" | Posted: Last 7 days
──────────────────────────────────────────────────────
Found [N] relevant posts:

# | Score | User       | Budget    | Location | Summary                              | URL
--|-------|------------|-----------|----------|--------------------------------------|-----
1 | ★★★★★ | u/kevin_fl  | $15k      | Miami    | "Need reliable SUV for family, 5 ppl"| [link]
2 | ★★★★☆ | u/firstcar | $10k      | Doral    | "First car, bad credit ok if small"  | [link]
3 | ★★★★☆ | u/miamigrl  | $20k      | Brickell | "Leaning BMW vs Audi used, thoughts?" | [link]
4 | ★★★☆☆ | u/carguy99 | Unknown   | FL       | "Just got pre-approved $18k..."       | [link]
──────────────────────────────────────────────────────
Reply to these posts? (A=all / pick numbers / C=skip)
```

---

## CRAIGSLIST WANTED

### URL Pattern

Craigslist has a dedicated **"wanted"** section for cars — people post what they're looking to buy:

```
https://[CITY].craigslist.org/search/wca
```

**Category codes:**
- `wca` = wanted: cars & trucks (by owner)
- `wco` = wanted: cars & trucks (by dealer) — skip this one

**With keywords:**
```
https://miami.craigslist.org/search/wca?query=SUV
https://miami.craigslist.org/search/wca?query=BMW
https://broward.craigslist.org/search/wca
```

---

### Craigslist Wanted — What to Extract

These are the highest-intent leads — someone spent time writing out exactly what they want:

- Post title (e.g., "WANTED: Reliable SUV, Cash, Under $20k")
- Full description (requirements, budget, timeline, condition preference)
- **Phone number** — often included by cash buyers
- Email (via Craigslist relay)
- Post date
- Listing URL

**Buyer intent from description:**
- Budget: "cash buyer", "up to $X", "under $Xk"
- Timeline: "need by [date]", "ASAP", "immediately"
- Condition: "newer preferred", "2018+", "under 50k miles"
- Flexibility: "open to similar models"

---

### Craigslist Wanted Scan Flow

```
1. Navigate to https://[CITY].craigslist.org/search/wca
2. Pull all listings from the page
3. Click through each relevant listing
4. Extract: title, budget, requirements, phone, post date
5. Display summary
6. Draft outreach for approved listings
```

---

## TWITTER / X

### Search URL Patterns

```
https://twitter.com/search?q=[QUERY]&f=live
```

**High-intent search queries to run:**

| Query | Finds |
|-------|-------|
| `"looking for a car" Miami` | Local shoppers |
| `"need a car" "Miami" OR "Broward"` | Urgent buyers |
| `"car shopping" near:Miami` | Active shoppers |
| `"just got approved" car loan` | Pre-approved buyers ready to shop |
| `"first car" budget` | First-time buyers |
| `"trade in" OR "trading in" car Miami` | Trade-in prospects |
| `"car payment" "can afford" Miami` | Budget-aware buyers |

**Encoded examples:**
```
https://twitter.com/search?q=%22looking+for+a+car%22+Miami&f=live
https://twitter.com/search?q=%22need+a+car%22+Miami&f=live
```

---

### Twitter — What to Extract

For each relevant tweet:
- Username + display name
- Tweet text
- Date/time posted
- Engagement (likes/replies — higher = more visible)
- Location (if disclosed in bio or tweet)
- Profile link (for DM)

**Response method:** Reply publicly to the tweet OR send a DM. Always reply with a concise, helpful message — not a pitch. Full details in outreach-buyer.md.

---

## OFFERUP — WTB (Want to Buy) Posts

### URL Pattern

```
https://offerup.com/search/?q=wanted+car&radius=50&location=[CITY]+[STATE]
https://offerup.com/search/?q=wtb+car&location=Miami+FL
https://offerup.com/search/?q=looking+for+car&location=Miami+FL
```

**Search for WTB posts:**
```
https://offerup.com/search/?q=want+to+buy+car&location=Miami+FL&radius=25
```

---

### OfferUp — What to Extract

- Post title and description
- Seller/poster profile
- Location
- Photos (if any)
- Post date
- Contact via OfferUp messaging

---

## Multi-Source Sweep Mode

When associate says `"pull people looking for cars"` or `"full sweep"`:

Run all sources in parallel:
1. Reddit: r/whatcarshouldibuy + r/autofinance + local city subreddit — last 7 days
2. Craigslist Wanted: city from profile
3. Twitter: top 3 buyer intent queries for the city
4. OfferUp: WTB search for city

Combine results, deduplicate, rank by intent score:

```
🎯 BUYER LEAD SWEEP — [DATE]
City: Miami | Sources: Reddit, Craigslist Wanted, Twitter, OfferUp
──────────────────────────────────────────────────────────────────
📱 Reddit (4 posts)
   ★★★★★ u/kevin_fl | r/whatcarshouldibuy | $15k | Family SUV in Miami
   ★★★★☆ u/autofl | r/autofinance | $18k | Pre-approved, now shopping
   ★★★☆☆ u/miamigrl | r/cars | $20k | BMW vs Audi debate
   ★★★☆☆ u/firstcar | r/whatcarshouldibuy | $10k | First car in Doral

📋 Craigslist Wanted (2 posts)
   🔥 Cash buyer | SUV under $20k | Timeline: this week | Phone: 305-555-1111
   💬 Email only | 2018+ sedan | Budget flexible

🐦 Twitter (3 tweets)
   @miamidriver | "Finally got pre-approved 🙌 now shopping for a car"
   @coral_gables | "Car shopping tomorrow, anyone know dealers in Miami who don't BS?"
   @florida_mom | "Looking for something reliable under 15k for my teenager"

📲 OfferUp (1 WTB post)
   "WTB: Toyota Camry or Honda Accord 2017+ under $14k, cash"

──────────────────────────────────────────────────────────────────
Total: 10 buyer leads found

Reply with numbers (e.g., "1, 3, 5") to contact specific leads
Or: A = contact all | B = contact top 5 | C = save all without contacting
```

---

## Keyword Bank — Buyer Intent Signals

When scanning any platform, these keywords indicate active car buying intent:

**Direct:**
`"looking for a car"`, `"need a car"`, `"want to buy"`, `"WTB"`, `"ISO"`, `"in search of"`, `"car shopping"`, `"buying a car"`, `"first car"`, `"new car"`

**Budget signals:**
`"budget is"`, `"can spend"`, `"under $Xk"`, `"max $X"`, `"cash buyer"`, `"have $X down"`

**Financing signals:**
`"just got approved"`, `"pre-approved"`, `"financing for"`, `"car loan"`, `"monthly payment"`

**Urgency signals:**
`"ASAP"`, `"need by"`, `"this week"`, `"starting new job"`, `"license just"`, `"just moved"`

**Location signals:**
City name, zip code, neighborhood, `"near me"`, `"in the area"`
