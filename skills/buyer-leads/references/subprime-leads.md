# Subprime Lead Sourcing — Bad Credit & Finance-Challenged Buyers

This file handles finding people who need a car but are worried about getting approved. These are often the most ignored buyers — but if your dealership has flexible financing, subprime lenders, or BHPH (Buy Here Pay Here) options, they are **incredibly high intent** and almost no one is competing for them correctly.

---

## Who These Buyers Are

| Type | Description | What They Need to Hear |
|------|-------------|----------------------|
| **Bad credit buyers** | 500–620 credit score, worried about approval | "We work with lenders that specialize in situations like yours" |
| **No credit buyers** | Thin file, first-time borrowers, recent immigrants | "No credit history isn't the same as bad credit — we can work with that" |
| **Recent repo buyers** | Had a car repossessed, now need transport | "Time matters — 12+ months since repo and we have options" |
| **Bankruptcy buyers** | Filed Chapter 7 or 13, worried | "Post-bankruptcy can actually mean fresh start — we help with that" |
| **Denied elsewhere** | Got turned down at another dealer | "One lender saying no doesn't mean all lenders say no" |
| **ITIN buyers** | No SSN, ITIN only | "We work with ITIN applicants through [LENDER]" |
| **No down payment** | Can't put money down | "We have $0 down programs for qualifying buyers" |

---

## Where These Buyers Post Online

### Reddit Subreddits

| Subreddit | Search URL |
|-----------|------------|
| r/badcredit | `https://www.reddit.com/r/badcredit/search.json?q=car&sort=new&t=week` |
| r/autofinance | `https://www.reddit.com/r/autofinance/search.json?q=bad+credit+car&sort=new&t=week` |
| r/personalfinance | `https://www.reddit.com/r/personalfinance/search.json?q=car+loan+credit&sort=new&t=week` |
| r/povertyfinance | `https://www.reddit.com/r/povertyfinance/search.json?q=car&sort=new&t=week` |
| r/firsttimebuyer | Check for car mentions |
| r/askcarsales | `https://www.reddit.com/r/askcarsales/search.json?q=bad+credit&sort=new&t=week` |

---

### High-Intent Subprime Search Queries

Use these across Reddit, Twitter, and Craigslist Wanted:

```
"bad credit car loan"
"can I get approved with 500 credit score"
"need a car bad credit"
"repo on my record car"
"bankruptcy car loan"
"denied for car loan"
"second chance financing"
"no credit car"
"BHPH" OR "buy here pay here"
"dealer that works with bad credit"
"cosigner car loan"
"first time buyer no credit"
"ITIN car loan"
```

---

### Subprime Buyer Reddit Scan Flow

```
1. Search r/badcredit, r/autofinance, r/personalfinance with subprime keywords
2. Filter for posts where:
   - They mention needing a car for work/commute/family
   - Credit score is mentioned (under 650)
   - They express urgency or frustration
   - They ask "does anyone know a dealer who..."
3. Extract: username, post URL, credit situation summary, city/location
4. Score by urgency:
   - Mentions job/work: +3
   - Has cash down: +2
   - Specific car in mind: +1
   - Multiple lenders declined: +2 (frustrated = motivated)
   - Recently moved: +1
5. Show ranked list, draft outreach for selected posts
```

---

### Subprime Results Display

```
💳 SUBPRIME BUYER SCAN — Reddit + Twitter
Keywords: bad credit, denied, financing, car loan | Last 7 days
──────────────────────────────────────────────────────────
Found [N] potential leads:

# | Score | User          | Score | Situation                              | City    | URL
--|-------|---------------|-------|----------------------------------------|---------|-----
1 | ★★★★★ | u/workneedcar  | ~540  | "Denied twice, start new job Monday"   | Miami   | [link]
2 | ★★★★☆ | u/repo2yrs    | ~580  | "2 year old repo, have $1500 down"     | Hialeah | [link]
3 | ★★★★☆ | u/itinbuyer   | N/A   | "ITIN only, need family car"           | Doral   | [link]
4 | ★★★☆☆ | @miamiworks   | ~560  | "Anyone know dealer in Miami good w/bad credit?" | Miami | [tweet]
──────────────────────────────────────────────────────────
Contact? Reply with numbers or A=all
```

---

## What NOT to Do with Subprime Buyers

❌ Don't lead with the car — lead with the solution (approval)
❌ Don't say "we can get ANYONE approved" — sounds predatory and false
❌ Don't quote specific interest rates in cold outreach — save that for the conversation
❌ Don't pressure them — they've already been turned down and are sensitive
❌ Don't mention their credit score back to them in the first message — feels invasive

---

## Subprime Outreach Tone

Warm, professional, hopeful — not salesy. They've probably been told no before. Your message needs to feel like a genuine path forward, not a pitch.

**Lead with:** "We specialize in situations like yours"
**Follow with:** One concrete thing you can do that others couldn't
**Close with:** One low-friction action (call/text, no commitment)

See `outreach-buyer.md` for full templates.

---

## Craigslist Wanted + Twitter Subprime Search

**Craigslist Wanted — bad credit buyers:**
```
https://[CITY].craigslist.org/search/wca?query=bad+credit
https://[CITY].craigslist.org/search/wca?query=need+financing
https://[CITY].craigslist.org/search/wca?query=second+chance
```

**Twitter subprime search:**
```
https://twitter.com/search?q="bad+credit+car"+Miami&f=live
https://twitter.com/search?q="need+financing"+car+Miami&f=live
https://twitter.com/search?q="denied+car+loan"&f=live
```

---

## Tracking Subprime Leads

Log to `~/car-sales-leads/leads.csv` with Lead Type = `SUBPRIME`

Additional notes column entries:
- Credit situation (e.g., "540 score, 2-year-old repo")
- Down payment available
- Lender requirements
- Urgency level

Follow-up is critical for subprime buyers — they may not respond the first time but come back when they're more desperate. Don't write them off after one no-reply.

Subprime follow-up sequence:
| Day | Channel | Message |
|-----|---------|---------|
| Day 1 | Platform reply/DM | Initial outreach |
| Day 3 | iMessage (if phone found) | Gentle follow-up |
| Day 7 | Email (if found) | Value email: "here's what we can do for your situation" |
| Day 21 | iMessage | Soft final touch |
