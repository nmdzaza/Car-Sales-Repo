# Dealership Denied & Dead Leads — Reactivation

These are the **hottest cold leads** you'll ever work. They already chose YOUR dealership. They already showed up or called. Life just got in the way — credit wasn't there, timing was off, or they went cold.

Time changes everything:
- Credit scores improve (on-time payments, collections fall off)
- Income changes (new job, raise, second income)
- Down payment situations change (saved money, tax return season, inheritance)
- Life circumstances shift (moved in together, baby coming, job requires travel)

The right reactivation at the right moment is one of the highest ROI moves in car sales.

---

## Lead Sources to Pull From

### Source 1 — Dealer's Own Denied Finance Leads

These are people who came in, went through the finance process, and got declined. They wanted to buy — they just couldn't at that moment.

**How to pull them:**
Associate says: "work my denied leads" or "pull my finance denials"

AI reads `~/car-sales-leads/leads.csv` and filters:
- Status = `DENIED` or Notes contains "denied" or "declined" or "finance failed"
- Lead Type = `SUBPRIME` with Status = CONTACTED/DORMANT
- Any lead where Notes mention "credit issue", "down payment needed", "co-signer", "income verification"

If the dealership has a separate denial list file (CSV export from their DMS):
```
Associate says: "import my denied leads from [file path]"
```
AI reads the file, maps columns, categorizes, and loads into leads.csv with Type = `DENIED-REACTIVATION`.

---

### Source 2 — Dead Leads from Your Own Pipeline

Pull from leads.csv where:
- Status = DORMANT or DEAD
- Lead Type = HOT/WARM/PAID and has gone cold
- Last contact was 60+ days ago
- No sale, no appointment, no clear reason for closure

These people were interested — they may still be.

**Filter command:**
```
Associate: "work my dead leads"
```
AI filters and ranks:
- Highest priority: Dormant leads where Notes mention "checking financing", "saving for down payment", "coming back after tax season", specific timeline that has now passed
- Medium priority: Leads who engaged (replied once) but then went quiet
- Lower priority: Leads who explicitly said "not interested" or "bought elsewhere"

---

### Source 3 — Seasonal Reactivation Windows

Certain times of year are perfect for reaching back out to denied/dead leads:

| Season | Angle |
|--------|-------|
| **January–February** | "Tax refund season — if you've been saving or expecting a return, now's the time" |
| **March–April** | "Tax season — a refund could cover your down payment entirely" |
| **May** | "Rates just shifted — your situation may qualify now even if it didn't before" |
| **August–September** | "New model year rollout — great deals on last year's inventory right now" |
| **November–December** | "Year-end deals — dealers are clearing inventory, approvals are looser" |

AI automatically suggests the right seasonal angle based on the current month.

---

## How to Work Denied Leads

### Step 1 — Pull and rank the list

```
📋 DENIED / DEAD LEAD REACTIVATION
──────────────────────────────────────────────
Pulling from ~/car-sales-leads/leads.csv...

Found [N] leads eligible for reactivation:

DENIED FINANCE (came in, couldn't get approved):
1. Marcus H. | Denied 3/10/24 | 520 score | Had $800 down | Wanted X5
2. Tanya R.  | Denied 1/15/24 | No credit history | Wanted Corolla-type
3. Luis M.   | Denied 2/5/24  | Repo 18 months ago | Wanted pickup truck

DEAD / DORMANT (went cold, no sale):
4. Kevin D.  | Last contact 11/2/23 | HOT lead, test drove 3 Series, went silent
5. Jasmine T.| Last contact 8/15/23 | Said "not right now" — saving for down payment

Reason to reach out now: [AI fills in seasonal angle based on current date]
──────────────────────────────────────────────────────────────────
Contact all? Or pick specific leads?
```

---

### Step 2 — Match their situation to what's changed

Before drafting outreach, check what's different now vs. when they were denied:

| Then | Now |
|------|-----|
| Denied: credit too low | Time has passed — credit may have improved |
| Denied: income verification issue | New job or raise may have happened |
| Denied: needed co-signer | May have found one |
| Dead: "not right now" | Timing has likely changed |
| Dead: "saving for down payment" | Tax season = potential down payment now |
| Dead: financing fell through | New lenders or programs available |

Always write the outreach from the angle of "something has changed" — not "hey remember us?"

---

### Step 3 — Draft reactivation outreach

See `outreach-buyer.md` for full templates. Key angles:

- **Tax refund angle** (Jan–April): Their refund could be the down payment they needed
- **Time = healed credit** angle: Credit scores improve over time
- **New program angle**: "We just added [LENDER] who specializes in situations like yours"
- **New inventory angle**: "That [VEHICLE] they wanted is in stock at a better price"
- **Rate shift angle**: "Rates shifted — what didn't work before might work now"

---

## CSV Columns Used for Denied Lead Tracking

When logging a denied lead:
- Lead Type: `DENIED-REACTIVATION`
- Status: `DENIED` initially, then `REACTIVATED` when reached back out to
- Notes: "Denied [DATE] — [REASON] — [CREDIT SCORE IF KNOWN] — [DOWN PAYMENT SITUATION]"
- Next Follow-Up: 60 days after denial date (or tax season if in winter)

---

## Denied Lead Status Flow

```
DENIED → [60 days pass] → REACTIVATION-QUEUED → CONTACTED → RESPONDED/DORMANT → APPOINTMENT → SOLD
```

When a denied lead gets reactivated and converts, update:
- Status → SOLD
- Notes → "Reactivated from denial [original date]. Closed [sale date]. [Vehicle sold]."

These conversion stories are powerful testimonials for your pitch to other dealers.

---

## Importing Denial Lists from DMS / CRM Exports

If the dealership has a DMS (Dealer Management System) like:
- **Reynolds & Reynolds**
- **CDK Global**
- **DealerSocket**
- **VinSolutions**
- **Tekion**

They can export denied/dead leads as CSV. Associate drops the file path:

```
"Import my denial list from ~/Downloads/VinSolutions_export_05-2024.csv"
```

AI reads the file, maps columns to the standard format, categorizes leads, loads into `leads.csv`, and immediately surfaces the top candidates for reactivation based on time elapsed and seasonal angle.

**Common DMS export columns → standard mapping:**
| DMS Column | Maps To |
|------------|---------|
| Customer Name | Lead Name |
| Cell Phone | Phone |
| Email | Email |
| Vehicle of Interest | Car Year/Make/Model |
| Last Activity | Date |
| Status | Notes |
| Credit Score | Notes (credit situation) |
| Denial Reason | Notes |
| Down Payment Available | Notes |
