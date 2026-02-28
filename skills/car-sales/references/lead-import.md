# Lead Import — Bulk Intake & Auto-Categorization

This file handles two scenarios:
1. **Associate drops in a list of leads** (pasted text, CSV, or one-by-one)
2. **Associate pulls from the existing tracker** to work a segment of leads

---

## How to Import Leads

### Method 1 — Paste a List

Associate pastes any format. Examples:

```
Marcus James, 954-555-0101, youngtrappy4@gmail.com, interested in BMW i7
Derrick Brown, 786-555-0202, derickb@gmail.com, looking for X5 under 60k
Janelle Moore, 305-555-0303, janelle@outlook.com, test drove 330i last month, went cold
```

Or a table copy from a CRM:
```
Name | Phone | Email | Last Contact | Notes
Chris Williams | 407-555-1111 | cwill@gmail.com | 3/10/24 | Inquired M4
Tasha Grant | 321-555-2222 | tasha@gmail.com | 1/5/24 | Old lead, no response
```

Or just names + phones:
```
Kevin Davis 305-555-4444
Ray Thomas 786-555-5555
```

**AI must accept any format and parse it.**

---

### Method 2 — CSV File Import

Associate says: "Import leads from my file at ~/Downloads/leads-today.csv"

AI reads the file, parses every row, and processes each lead.

Accepted CSV column names (any order, case-insensitive):
- name, first name, last name, full name
- phone, cell, mobile, number
- email, email address
- notes, comments, interest, car, vehicle
- last contact, last contacted, date
- status, lead type, type, category

If columns are missing, infer from context or ask once:
```
I can see names, phones, and emails but no car info.
Should I use a default car from inventory, or do you want to add it per lead?
```

---

### Method 3 — Pull from Existing Tracker

Associate says: "Work my dead leads" or "Show me everyone I haven't contacted in 30 days"

AI reads `~/car-sales-leads/leads.csv` and filters based on request:

| Request | Filter |
|---------|--------|
| "work my dead leads" | Status = DEAD or DORMANT |
| "work my hot leads" | Status = CONTACTED or RESPONDED, Type = HOT |
| "follow-ups due today" | Next Follow-Up = today or earlier |
| "leads I haven't touched in 30 days" | Date is 30+ days ago, Status ≠ SOLD |
| "everyone who didn't respond" | Status = CONTACTED, Date > 5 days ago |
| "my paid leads" | Lead Type = PAID |

Returns a list with quick-action options:
```
📋 Found 12 dead leads. Here's a preview:

1. Marcus James — BMW i7 — Last contact: 3/10/24 (72 days ago)
2. Derrick Brown — X5 — Last contact: 2/28/24 (82 days ago)
3. Janelle Moore — 330i — Last contact: 1/15/24 (125 days ago)
...

What do you want to do?
A) Generate outreach for all 12 (batch mode)
B) Go one by one
C) Filter this list further

Reply A, B, or C.
```

---

## Auto-Categorization

When leads are imported (any method), AI automatically assigns a Lead Type based on available info:

| Signal | Assigned Type |
|--------|--------------|
| Recent inquiry (< 7 days), no purchase yet | HOT |
| Previously contacted, no response (7–60 days) | WARM |
| Old contact (60+ days) or explicitly noted cold | DEAD |
| Came in from paid source (AutoTrader, Cars.com, etc.) | PAID |
| Test drive happened, no sale | WARM |
| Associate says "they went cold" or "stopped responding" | DEAD |
| No prior contact context | HOT (default for new lists) |

Show the categorization to the associate before locking it in:

```
📂 CATEGORIZED [N] LEADS:

🔥 HOT (assigned — recent inquiry):
   Marcus James | BMW i7 | youngtrappy4@gmail.com

💰 PAID (assigned — AutoTrader source noted):
   Chris Williams | M4 | cwill@gmail.com

🤙 WARM (assigned — 14 days, no response):
   Derrick Brown | X5 | derickb@gmail.com

💀 DEAD (assigned — 90+ days cold):
   Janelle Moore | 330i | janelle@outlook.com
   Ray Thomas | i4 | (no email)

✅ Does this categorization look right?
   Reply YES to lock it in and start outreach, or tell me which ones to recategorize.
```

---

## Batch Outreach Mode

Once leads are categorized and confirmed, associate can run batch mode:

```
🚀 BATCH MODE — [N] leads ready

I'll generate outreach for each lead one at a time.
You review and approve each draft, then confirm sent.
After each send I'll log it and queue the follow-up schedule.

Starting with:
Lead 1 of [N]: [NAME] — [LEAD TYPE] — [CAR/INTEREST]

[Pull car data if URL exists. If no car URL, ask once:
"Do you have an inventory link for this lead, or should I use a general intro message?"]

[Show draft in review block]
```

After each approval + send confirmation:
- Log to `leads.csv`
- Queue next follow-up date
- Move to next lead automatically

Progress tracker shown after each send:
```
✅ 1/[N] done — [NAME] logged
⏳ [N-1] remaining
```

---

## Assigning Cars to Leads Without a Link

If a lead has no specific car link:

1. Check if they have a noted interest (e.g., "looking for X5 under 60k")
2. If dealership inventory URL is on file, open it and search for a match
3. If no match can be found, generate a discovery-style first message instead:

```
Hey [NAME], this is [SALESPERSON] at [DEALERSHIP].
I see you were looking at [VEHICLE TYPE] — I've got a few things
that might work for you. What features matter most to you in your next car?
```

---

## Importing Your Own Lead File Format

If the associate has a custom file format (Google Sheet export, CRM export, dealership software export):

Associate says: "Here's how my leads export looks" and pastes a sample row.

AI maps their columns to the standard fields:
```
I see your file uses:
- "Customer" → Lead Name ✅
- "Cell" → Phone ✅
- "Email Address" → Email ✅
- "Vehicle of Interest" → Car (I'll look this up) ✅
- "Last Activity Date" → Last Contact ✅

Missing: Lead Type — I'll auto-categorize based on Last Activity Date.

Ready to import. Paste or share the file path.
```

---

## Lead Import Quick Commands

| Associate Says | AI Does |
|---------------|---------|
| "import leads" | Prompts for paste, file, or tracker pull |
| "load my dead leads" | Pulls DEAD/DORMANT from leads.csv |
| "I have 100 leads today" | Enters batch import mode |
| "work my follow-ups" | Shows all leads with Next Follow-Up = today |
| "show my pipeline" | Displays full lead tracker summary (see lead-tracker.md) |
| "add a lead: [name] [phone] [email]" | Adds single lead directly to tracker, starts intake |
| "mark [name] as sold" | Updates their row in leads.csv to Status = SOLD |
| "mark [name] as appointment" | Updates to APPOINTMENT, asks for appointment date |
