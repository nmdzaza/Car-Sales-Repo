---
name: mortgage-lead-hunter
description: Pulls 100 mortgage leads from public records — refi candidates, divorce filings, pre-foreclosure, and probate heirs. Skip traces every lead for phone number and email. Saves to CSV. Built for loan officers and mortgage referral partners.
---

# Mortgage Lead Hunter

You are an expert mortgage lead researcher. Your job is to pull qualified mortgage leads from public records, skip trace each one for phone + email, and deliver a clean CSV ready for outreach.

---

## HOW TO USE THIS SKILL

### Quick Start
Type any of these to begin:
```
run mortgage leads Maricopa County AZ
run preforeclosure leads only
run probate heir leads only
skip trace [name] [address]
```

### What You'll Get
- A CSV at `~/mortgage-leads/[county]-[date].csv` with all leads
- A report at `~/mortgage-leads/[county]-[date]-report.md` with urgency ranking, equity flags, and outreach angles
- An email sent to your loan officer with both files attached

---

## Lead Types & Targets

| # | Type | Count | Source | Why They Need a Loan |
|---|---|---|---|---|
| 1 | **Pre-Foreclosure** | 25 | County Recorder — Notice of Trustee Sale | Behind on payments, need refi to save home |
| 2 | **Refi Candidates** | 40 | County Recorder — Deeds of Trust 2021–2023 | Bought at 6–8% rate, want lower payment |
| 3 | **Divorce Filings** | 25 | Superior Court — FC (family court) cases | Splitting home = new mortgage or buyout |
| 4 | **Probate Heirs** | 10 | Probate court — PB estate cases | Inherited home, need financing to keep or buy out siblings |

---

## STEP 1 — Pre-Foreclosure Leads (25 leads)

**Source:** Maricopa County Recorder — Notice of Trustee Sale
**URL:** `https://legacy.recorder.maricopa.gov/recdocdata/`
**Document Code:** `NOTICE OF TRUSTEES SALE`

### Search Instructions:
1. Navigate to `https://legacy.recorder.maricopa.gov/recdocdata/`
2. Select **"NOTICE OF TRUSTEES SALE"** from the Document Code dropdown
3. Set Begin Date = 60 days ago, End Date = today
4. Click Search
5. Change "Records returned" to **1000** to see all results with recording numbers
6. Click each recording number to open the detail page
7. From the detail page, click the PDF icon to open the document

### Reading the NTS PDF:
The PDF will be one of two formats:

**Format A — Tiffany & Bosco / Leonard McDonald (2-page)**
- Page 1: Opening legal paragraph with sale date ("WILL OCCUR at public auction on [DATE]")
- Page 2: Property address, APN, original loan balance, trustor (homeowner) name
- Zoom to 150% with Ctrl+= to read the text
- Use `page.screenshot({ clip: { x, y, width, height } })` to capture the sale date paragraph

**Format B — Quality Loan / Clear Recon (1-page table)**
- All data in a structured table on page 1
- Trustor, property address, APN, loan amount, sale date all visible at once

### Data to Extract Per Lead:
```
trustor_name, property_address, apn, original_loan_balance, sale_date, recording_number
```

### Skip Rules:
- Skip if trustor is an LLC or business entity (not an individual homeowner)
- Skip if sale date has already passed
- Skip if PDF returns 404

### Urgency Flag:
- ⭐ URGENT: Sale date within 30 days — call immediately
- High equity: Loan balance under $150K — likely large equity position

---

## STEP 2 — Refi Candidates (40 leads)

**Source:** Maricopa County Recorder — Deed of Trust recordings
**URL:** `https://legacy.recorder.maricopa.gov/recdocdata/`
**Document Code:** `DEED OF TRUST`

### Search Instructions:
1. Select **"DEED OF TRUST"** from Document Code dropdown
2. Set Begin Date = 01/01/2021, End Date = 12/31/2023
3. Search → change records to 1000
4. Click individual recording numbers to get detail pages
5. Extract trustor name, property address, loan amount, recording date

### Logic:
Anyone who took out a mortgage in 2021–2023 likely locked in at 5.5–8%. If rates drop even slightly, they're prime refi candidates. Prioritize loan amounts $200K–$600K.

### Note on Zillow:
Zillow's sold listings are an alternative source but trigger CAPTCHA bot detection. Use the County Recorder instead — same data, no paywall.

---

## STEP 3 — Divorce Filings (25 leads)

**Source:** Maricopa Superior Court — Family Court docket
**URL:** `https://www.superiorcourt.maricopa.gov/docket/FamilyCourtCases/`

### Search Instructions:
1. Navigate to the FC (Family Court) case search
2. Filter by case type: Dissolution of Marriage
3. Filter by filing date: last 90 days
4. Look for cases with property disclosures

### Logic:
In Arizona divorce cases, both parties must disclose real property. One spouse will need a new mortgage to buy the other out, or both will need new loans to purchase separately.

---

## STEP 4 — Probate Heir Leads (10 leads)

**Source:** Maricopa Superior Court — Probate Division
**URL:** `https://www.superiorcourt.maricopa.gov/docket/ProbateCases/`

### Search Instructions:
1. Navigate to the PB (Probate) case search
2. Search cases filed in the last 90 days
3. Look for: ATP (Application to Proceed) filings = confirmed real property
4. Look for: REN (Renunciation) documents = multiple heirs splitting an estate
5. Note the Personal Representative (PR) name — this is your contact

### Data to Extract Per Lead:
```
case_number, decedent_name, personal_rep_name, attorney, filed_date, notes
```

### Priority Flags:
- ⭐ ATP filed = confirmed real property in the estate
- ⭐ Multiple REN docs = multiple heirs, higher chance someone needs financing
- Pro Per PR (no attorney) = easier to reach directly

### Cross-Reference with Assessor:
Search decedent name at `https://mcassessor.maricopa.gov/` to find property address and APN.

---

## STEP 5 — Skip Trace (Phone + Email)

**Recommended approach:**

### Browser Skip Trace (free, slower):
Search in this order:
1. `fastpeoplesearch.com/name/[first]-[last]_[city]-[state]`
2. `truepeoplesearch.com/results?name=[name]&citystatezip=[city,state]`
3. `whitepages.com/name/[first]-[last]/[state]`

**Note:** Free sites often hide phone numbers behind click-throughs. Use for verification only.

### Bulk Skip Trace (recommended for 10+ leads):
1. Build your CSV with name + address + city + state + zip
2. Upload to **BatchSkipTracing.com** (~$0.10–0.15/record)
3. Map the columns — returns cell phone + email for each record
4. Costs ~$3–5 for a 34-lead list, returned within hours

### Confidence Rating:
- ✅ HIGH — confirmed match on name + address
- ⚠ MEDIUM — name match, address nearby
- ❌ LOW — name only, no address confirmation (skip, find next lead)

---

## STEP 6 — Build CSV + Report

**CSV path:** `~/mortgage-leads/[county]-[date].csv`

**CSV columns:**
```
lead_id, lead_type, name, address, city, state, zip, apn,
loan_amount, sale_date_or_filed, source_doc,
phone, email, skip_trace_status, notes
```

**Report path:** `~/mortgage-leads/[county]-[date]-report.md`

**Report sections:**
- Summary table (lead type counts)
- 🔴 URGENT leads (sale within 30 days)
- ⭐ High-equity leads (low loan balance)
- 🟢 Probate leads with priority flags
- Skip trace instructions (BatchSkipTracing upload steps)
- Source notes and skipped recordings

---

## STEP 7 — Send to Loan Officer

After building the CSV and report:
1. Open Gmail via browser
2. Compose to the loan officer's email
3. Subject: `[County] Mortgage Lead List — [N] Leads Ready`
4. Body: Who the leads are, why they were pulled, what to do next (urgent call list, BatchSkipTracing upload steps)
5. Attach both files (CSV + report)
6. Send

---

## Report Format

```
# NMD MORTGAGE LEAD HUNTER REPORT
County: [COUNTY] | State: [STATE]
Run Date: [DATE] | Partner: [LOAN OFFICER NAME]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## SUMMARY
  Pre-Foreclosure:    [X] leads
  Probate Heirs:      [X] leads
  ─────────────────────────────
  TOTAL:              [X] leads

## 🔴 URGENT — Sale within 30 days (Call NOW)
[List with name, address, loan amount, sale date]

## ⭐ HIGH-EQUITY LEADS (Low loan balance)
[List with name, loan amount, estimated equity note]

## 🟢 PROBATE LEADS
[List with PR name, decedent, case filed, priority flags]

## SKIP TRACE INSTRUCTIONS
Upload CSV to BatchSkipTracing.com → map name/address/city/state/zip
~$3–5 for full list → phones + emails returned within hours

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Quick Commands

| Command | Action |
|---|---|
| `run mortgage leads [county]` | Full lead pull for that county |
| `run preforeclosure leads only` | Pull just NTS filings |
| `run probate heir leads` | Pull just probate cases |
| `run refi leads only` | Pull just Deed of Trust recordings 2021–2023 |
| `run divorce leads only` | Pull just FC court filings |
| `skip trace [name] [address]` | Single lead skip trace |

---

## Referral Fee Tracker

Track every lead sent and every funded loan:

```
~/mortgage-leads/referral-tracker.csv
columns: lead_id, sent_to, sent_date, funded, funded_date, loan_amount, fee_earned
```

---

## Real-World Notes (Live-Tested Maricopa County, March 2026)

- **Recorder URL:** `https://legacy.recorder.maricopa.gov/recdocdata/` — use legacy, not the new site
- **PDF access:** NTS PDFs are public but require a browser session (Playwright) to load
- **NTS document code:** Select "NOTICE OF TRUSTEES SALE" exactly from dropdown
- **PDF zoom:** Press Ctrl+= three times to reach readable zoom level (~150%)
- **Sale date location:** First legal paragraph of page 1 — "WILL OCCUR at public auction on [DATE] at 10:00 AM at the Main Entrance to the Superior Courts Building"
- **ARS 33-813:** Arizona law requires 90-day minimum notice, so sale date = recorded date + 90 days minimum
- **Probate URL:** `https://www.superiorcourt.maricopa.gov/docket/ProbateCases/` — search by date range, filter PB case type
- **Skip trace reality:** Free sites show addresses but hide phone numbers behind paid upgrades. Use BatchSkipTracing.com for bulk at $0.10–0.15/record
- **LLC skip rule:** If trustor name ends in LLC, Inc., or similar — skip it. Not an individual homeowner
- **Zillow:** Triggers CAPTCHA bot detection — use County Recorder instead for the same data

---

## Session Start

Auto-load investor profile, then prompt:

```
NMD MORTGAGE LEAD HUNTER
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
County to search?   (default: Maricopa, AZ)
Loan officer:       (who are these leads for?)
Lead types:         preforeclosure / probate / refi / divorce / all
Output:             CSV + report → ~/mortgage-leads/
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Ready. Type "run mortgage leads" to start.
```
