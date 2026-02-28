# Lead Tracker — Automated CRM Log

Every time an email or iMessage is sent to a lead, a log entry is automatically written to the dealership's lead tracker file. This file acts as a running CRM — no manual entry needed.

---

## Tracker File Location

The tracker lives at:
```
~/car-sales-leads/leads.csv
```

If that file doesn't exist yet, create it automatically the first time a lead is logged. Always append — never overwrite.

---

## CSV Column Structure

```
ID,Date,Time,Lead Name,Phone,Email,Lead Type,Car Year,Car Make,Car Model,Car Trim,Car Price,VIN,Channel,Subject/Message Preview,Status,Next Follow-Up,Notes
```

| Column | Description |
|--------|-------------|
| ID | Auto-increment (001, 002, 003...) |
| Date | MM/DD/YYYY |
| Time | HH:MM AM/PM |
| Lead Name | Full name from intake |
| Phone | Lead's phone number |
| Email | Lead's email |
| Lead Type | HOT / WARM / DEAD / PAID |
| Car Year | Year of vehicle |
| Car Make | Make |
| Car Model | Model |
| Car Trim | Trim level |
| Car Price | Listed price |
| VIN | Vehicle Identification Number |
| Channel | EMAIL / IMESSAGE / BOTH |
| Subject/Message Preview | Email subject line OR first 60 chars of iMessage |
| Status | CONTACTED / RESPONDED / APPOINTMENT / SOLD / DORMANT / NO_RESPONSE |
| Next Follow-Up | Date of next scheduled touch (from sequence) |
| Notes | Any additional context (trade-in mentioned, financing question, etc.) |

---

## Auto-Log Rule

**Every time a send is confirmed (associate says "sent"), immediately:**

1. Read the current `leads.csv` to get the last ID number
2. Append a new row with all available fields filled in
3. Confirm to the associate:

```
📋 Lead logged to tracker:
   Lead: [NAME] | [EMAIL/PHONE]
   Car: [YEAR MAKE MODEL]
   Channel: [EMAIL/IMESSAGE]
   Status: CONTACTED
   Next follow-up: [DATE based on sequence — Day 5 from today]
   File: ~/car-sales-leads/leads.csv
```

---

## Status Definitions

| Status | Meaning |
|--------|---------|
| CONTACTED | First outreach sent, no response yet |
| RESPONDED | Lead replied (any channel) |
| APPOINTMENT | Test drive or dealership visit scheduled |
| SOLD | Deal closed |
| DORMANT | 21-day sequence completed, no response |
| NO_RESPONSE | Sent, bounced or confirmed undeliverable |

---

## Updating a Lead's Status

When an associate reports a lead replied, booked, or bought:

Associate says: "Marcus James replied, he wants to come in Friday"

AI should:
1. Find the row where Lead Name = Marcus James
2. Update Status → APPOINTMENT
3. Update Notes → "Wants to come in Friday [DATE]"
4. Update Next Follow-Up → day before appointment
5. Confirm:
```
✅ Marcus James updated → APPOINTMENT
   Next follow-up reminder: [DATE - 1 day before]
   ~/car-sales-leads/leads.csv
```

---

## Viewing the Tracker

When the associate says "show me my leads" or "what's my pipeline":

1. Read `~/car-sales-leads/leads.csv`
2. Display a clean summary table grouped by Status:

```
📊 LEAD PIPELINE — [TODAY'S DATE]
──────────────────────────────────
🔥 HOT (3)
   001 | Marcus James | BMW i7 | Emailed 5/12 | Next: 5/17
   004 | Derrick Brown | 330i | Texted 5/11 | Next: 5/16
   007 | Janelle Moore | X5 | Emailed 5/10 | Next: 5/15

💰 PAID (2)
   002 | Chris Williams | M4 | Emailed 5/12 | Next: 5/17
   006 | Tasha Grant | 5 Series | Texted 5/11 | Next: 5/14

✅ APPOINTMENTS (1)
   003 | Kevin Davis | X7 | Coming in 5/15

💀 DEAD (5)
   ...

📆 FOLLOW-UPS DUE TODAY:
   005 | Ray Thomas | i4 | Day 5 bump text due
──────────────────────────────────
Total leads: 11 | Active: 6 | Dormant: 0 | Sold: 0
```

---

## Follow-Up Due Detection

At the start of every session, check `leads.csv` for any rows where:
- Status = CONTACTED or RESPONDED
- Next Follow-Up date = today or earlier

If any are found, surface them first:

```
📆 YOU HAVE [N] FOLLOW-UPS DUE TODAY:

1. [NAME] — [CAR] — Due: Day [N] [CHANNEL] follow-up
   Last contact: [DATE] ([N] days ago)
   [Quick action: generate follow-up message?]

Reply with the number to generate that follow-up message now.
```

---

## Batch Status Review

If associate says "show me everyone I haven't heard from in 10+ days":

Filter leads.csv where:
- Status = CONTACTED
- Date column is 10+ days ago

Display grouped list and offer to generate bulk follow-up messages.

---

## Notes on File Handling

- The CSV file should be created at `~/car-sales-leads/leads.csv` if it doesn't exist
- Always read the file before appending to get the correct next ID
- When updating a row, read the full file, modify the row in memory, and write back the full file
- Never delete rows — use DORMANT status instead of removing leads
- If the file grows large (500+ rows), suggest the associate archive old DORMANT/SOLD leads to a separate `leads-archive.csv`
