# Pipeline Handoff — Feeding Conquest Leads into Car-Sales CRM

Every conquest lead contacted gets logged to the same `~/car-sales-leads/leads.csv` file used by the car-sales skill. This creates one unified pipeline — whether the lead came from a dealership inquiry or a Craigslist scan, everything lives in the same tracker.

---

## Lead Type Assignment for Conquest Leads

Conquest leads get their own type in the Lead Type column:

| Conquest Source | Lead Type in CSV |
|----------------|-----------------|
| Craigslist seller contacted | CONQUEST-CL |
| CarGurus private seller | CONQUEST-CG |
| AutoTrader private seller | CONQUEST-AT |
| OfferUp seller | CONQUEST-OU |
| Any private seller platform | CONQUEST |

---

## CSV Log Entry — Conquest Lead Format

Use the same leads.csv column structure from `car-sales/references/lead-tracker.md`, with these additions:

```
ID,Date,Time,Lead Name,Phone,Email,Lead Type,Car Year,Car Make,Car Model,Car Trim,Car Price,VIN,Channel,Subject/Message Preview,Status,Next Follow-Up,Notes,Source URL,Asking Price,Conquest Angle
```

**New columns added for conquest leads:**

| Column | Description |
|--------|-------------|
| Source URL | The full listing URL where this lead was found |
| Asking Price | What the seller is asking (may differ from "Car Price" which is market value) |
| Conquest Angle | TRADE-IN / PURCHASE / REPLACEMENT |

---

## Auto-Log Flow

When a conquest outreach message is sent (associate confirms):

1. Extract from the listing:
   - Seller name (or "Private Seller" if unknown)
   - Phone and/or email
   - Vehicle year, make, model, trim
   - Asking price
   - Source platform and URL
2. Append to `~/car-sales-leads/leads.csv`
3. Status = CONTACTED
4. Next Follow-Up = today + 2 days (conquest leads get a tighter follow-up — if they don't respond fast they'll get another offer)
5. Confirm to associate:

```
📋 Conquest lead logged:
   Seller: [NAME / "Private Seller"]
   Car: [YEAR MAKE MODEL]
   Asking: $[PRICE]
   Angle: [TRADE-IN / PURCHASE / REPLACEMENT]
   Source: [PLATFORM] — [URL]
   Next follow-up: [DATE — 2 days out]
   File: ~/car-sales-leads/leads.csv
```

---

## Conquest Lead Status Flow

Same statuses as regular leads, with one addition:

| Status | Meaning |
|--------|---------|
| CONTACTED | Outreach sent, no response |
| RESPONDED | Seller replied |
| APPOINTMENT | Appraisal or visit scheduled |
| SOLD | Deal closed (trade-in accepted or car purchased) |
| DORMANT | No response after full follow-up sequence |
| LISTED_SOLD | Listing was marked sold before we could contact |
| DECLINED | Seller said no or not interested |

---

## Conquest Follow-Up Sequence

Conquest leads move faster than dealership leads — sellers are motivated and may accept another offer if you're slow.

| Day | Channel | Action |
|-----|---------|--------|
| Day 1 | iMessage/Email | First outreach (trade-in or purchase offer) |
| Day 3 | iMessage | Quick bump: "Still interested in that appraisal?" |
| Day 7 | Email | Value-add: market data, what their car is worth, urgency |
| Day 14 | iMessage | Final touch: soft close |

After Day 14 with no response → mark DORMANT.

---

## Viewing Conquest Leads in the Pipeline

When associate says "show my conquest leads" or "what sellers have I contacted":

Filter `leads.csv` where Lead Type starts with "CONQUEST":

```
📡 CONQUEST PIPELINE — [DATE]
──────────────────────────────────────
CONTACTED (awaiting response):
001 | Private Seller (BMW 5 Series) | CL — $38,500 | Texted 5/12 | Follow-up: 5/14
004 | John M. | CarGurus BMW X5 | $44,000 | Emailed 5/11 | Follow-up: 5/13

RESPONDED:
003 | Sarah K. | AT BMW M4 | $59,000 | Replied: "send me a number"

APPOINTMENTS:
007 | Carlos R. | CL BMW 3 Series | Coming in 5/15 for appraisal

DECLINED:
002 | (No name) | CL X5 | Said already has buyer

Total conquest leads: 7 | Active: 4 | Appointments: 1 | Declined: 1 | Dormant: 1
```

---

## Upgrading a Conquest Lead to Full Car-Sales Lead

When a conquest lead responds positively and becomes a real buyer lead (e.g., they want to trade in AND buy something new):

Update their row:
1. Change Lead Type from `CONQUEST-CL` to `HOT` (or appropriate type)
2. Update Notes: "Was conquest lead — now active buyer — interested in [NEW VEHICLE]"
3. Hand off to car-sales skill for full outreach flow

Tell the associate:
```
🔥 [NAME] has been upgraded to a HOT lead.
They started as a conquest (selling their [YEAR MAKE MODEL])
and now want to look at [NEW VEHICLE INTEREST].

Switch to the car-sales skill to send them a full car package.
```

---

## Conquest vs. Standard Lead — Combined Pipeline View

When associate says "show my full pipeline" (all lead types together):

Show grouped by status, with conquest leads tagged with 📡:

```
🔥 HOT (2)
   Marcus James | BMW i7 | Emailed 5/12
   Derrick Brown | X5 | Texted 5/11

📡 CONQUEST — ACTIVE (3)
   Private Seller | BMW 5 Series (CL) | Texted 5/12
   John M. | BMW X5 (CG) | Emailed 5/11
   Sarah K. | BMW M4 (AT) | Replied — needs appraisal number

📆 FOLLOW-UPS DUE TODAY:
   005 | Ray Thomas | i4 | Day 5 bump text
   004 | John M. | Conquest BMW X5 | Day 3 bump text
```
