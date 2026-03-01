# Lead Tracker — Automated CRM Log

Every lead interaction is automatically logged to `~/car-sales-leads/leads.csv`. This is the live CRM — no manual entry needed.

---

## Tracker File Location

```
~/car-sales-leads/leads.csv
```

**If the file doesn't exist:** create it automatically using Desktop Commander `write_file` with just the header row, then append the first lead.

**Always use Desktop Commander `read_file` before appending** to get the last ID number and avoid duplicates.

---

## CSV Column Structure

```
ID,Date,Time,Lead Name,Phone,Email,Lead Type,Car Year,Car Make,Car Model,Car Trim,Car Price,VIN,Stock#,Channel,Subject/Message Preview,Status,Next Follow-Up,Notes
```

| Column | Description |
|--------|-------------|
| ID | L001, L002, L003... (read last row to get next number) |
| Date | YYYY-MM-DD |
| Time | HH:MM (24hr) |
| Lead Name | Full name |
| Phone | Lead's phone number |
| Email | Lead's email |
| Lead Type | HOT / WARM / DEAD / PAID / BUYER-HUNT / SUBPRIME / CONQUEST |
| Car Year | Year of vehicle |
| Car Make | Make |
| Car Model | Model |
| Car Trim | Trim level |
| Car Price | Listed price (numbers only, no $) |
| VIN | VIN if available |
| Stock# | Stock number if available |
| Channel | EMAIL / IMESSAGE / BOTH / REDDIT / TWITTER / PLATFORM |
| Subject/Message Preview | Email subject line OR first 60 chars of iMessage |
| Status | See Status Definitions below |
| Next Follow-Up | YYYY-MM-DD of next scheduled touch |
| Notes | Any context (trade-in, financing question, source URL, etc.) |

---

## How to Write to leads.csv (EXACT STEPS)

### Adding a new lead:

```
1. Use Desktop Commander read_file on ~/car-sales-leads/leads.csv
2. Find the last row's ID (e.g., L007)
3. Increment by 1 (L008)
4. Build the new CSV row with all columns filled
5. Use Desktop Commander write_file in APPEND MODE on ~/car-sales-leads/leads.csv
   - Mode: append
   - Content: the new row as a single line ending with \n
6. Confirm the log to the associate
```

### Updating an existing lead's status:

```
1. Use Desktop Commander read_file on ~/car-sales-leads/leads.csv
2. Find the row matching the lead name / email / ID
3. Modify the Status column value in that row
4. Update Notes if relevant
5. Use Desktop Commander write_file in REWRITE MODE — write the ENTIRE file back
   (header row + all rows, including the updated one)
6. Confirm the update to the associate
```

**NEVER delete rows. NEVER skip the read step. NEVER guess the next ID.**

---

## Auto-Log Rule — What Triggers a Log Entry

| Trigger | Status to Log |
|---------|--------------|
| Gmail draft created | DRAFT |
| iMessage sent to lead | CONTACTED |
| Associate confirms email sent in Gmail | CONTACTED (update from DRAFT) |
| Lead replies (any channel) | RESPONDED |
| Test drive / visit scheduled | APPOINTMENT |
| Deal closed | SOLD |
| 21-day sequence done, no response | DORMANT |
| Lead imported from list | NEW |
| Social media post drafted (Reddit/Twitter) | DRAFTED — not CONTACTED until associate confirms they posted |

---

## Status Definitions

| Status | Meaning |
|--------|---------|
| NEW | Lead added, no outreach yet |
| DRAFT | Gmail draft created, client iMessage sent — waiting for associate to hit send in Gmail |
| CONTACTED | Outreach sent (email sent by associate, iMessage delivered) |
| DRAFTED | Social platform draft produced — associate needs to post it manually |
| RESPONDED | Lead replied on any channel |
| APPOINTMENT | Test drive or visit scheduled |
| SOLD | Deal closed |
| DORMANT | 21-day sequence done, no response |
| NO_RESPONSE | Confirmed undeliverable / bounced |

---

## Draft Creation Confirmation Block

Every time a Gmail draft is created, show this to the associate:

```
✅ Done — here's what just happened:

📧 Gmail draft created: "[EMAIL SUBJECT]"
   → Open Gmail and hit Send when you're ready

📱 [CLIENT FIRST NAME] got an iMessage: "check your email"
📱 You got an iMessage on [ASSOCIATE_PHONE]: draft details

📋 Logged to leads.csv:
   ID: [L00X] | [LEAD NAME] | [YEAR MAKE MODEL]
   Status: DRAFT | Next follow-up: [DATE + 5 days]

Say "sent" once you've sent it in Gmail and I'll update the tracker.
```

---

## Status Update Confirmation Block

When associate says "sent" / "done" / "sent it":

```
✅ [LEAD NAME] updated → CONTACTED
   Email: [SUBJECT]
   Sent to: [EMAIL]
   Next follow-up: [DATE] (Day 5 bump)
   ~/car-sales-leads/leads.csv updated
```

---

## Viewing the Pipeline

When associate says "show me my leads" / "what's my pipeline" / "show pipeline":

1. Use Desktop Commander `read_file` on `~/car-sales-leads/leads.csv`
2. Parse all rows
3. Display grouped by Status:

```
📊 LEAD PIPELINE — [TODAY'S DATE]
──────────────────────────────────
🔥 HOT / WARM (N)
   L001 | Marcus James | BMW i7 | Emailed [DATE] | Next: [DATE]

📨 DRAFT — waiting for you to hit send (N)
   L003 | Kevin Davis | X5 | Draft created [DATE]

💰 PAID LEADS (N)
   L002 | Chris Williams | M4 | Emailed [DATE] | Next: [DATE]

✅ APPOINTMENTS (N)
   L004 | Janelle Moore | X7 | Coming in [DATE]

🎯 BUYER HUNT / CONQUEST (N)
   L005 | Reddit u/kevin_fl | SUV ~$15k | iMessage sent [DATE]

💀 DORMANT (N)
   ...

──────────────────────────────────
Total: [N] | Active: [N] | Sold: [N]

📆 FOLLOW-UPS DUE TODAY:
   L002 | Chris Williams | M4 | Day 5 bump text due
```

---

## Follow-Up Due Detection

At the start of every session:

1. Read leads.csv
2. Find rows where Status = CONTACTED or RESPONDED AND Next Follow-Up ≤ today's date
3. Surface them first:

```
📆 YOU HAVE [N] FOLLOW-UPS DUE:

1. [NAME] — [CAR] — Day [N] [CHANNEL] follow-up
   Last contact: [DATE] ([N] days ago)

Reply with the number to generate that follow-up message now.
```

---

## File Integrity Rules

- Always read the file before writing — get the real last ID
- When updating a row, rewrite the entire file (not just the changed row)
- Never delete rows — use DORMANT instead
- If file doesn't exist, create it with header row first, then append
- If file grows past 500 rows, suggest archiving DORMANT/SOLD rows to `leads-archive.csv`
- Every column must have a value — use empty string for unknown fields, never skip columns
