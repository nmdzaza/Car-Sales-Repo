# Lead Intake

This is the starting point when an associate has a lead they want to reach out to.

## What to Collect

Ask the associate for the following. Everything else can be generated from these inputs:

```
LEAD INTAKE FORM:
- Customer name:
- Phone number (for iMessage):
- Email address (for email):
- Lead type: HOT / WARM / DEAD / PAID
- Car they inquired about or were matched to (link from dealer site OR year/make/model):
- Do they have a trade-in? (yes/no — if yes, what car?):
- How long ago was last contact? (for dead leads):
- Any notes (what they said, what they needed, why they went cold):
```

If the associate gives a car link, immediately fetch the page and extract car details before drafting anything. See `references/car-package.md` for how to pull and structure that data.

## Lead Type Determines Strategy

### HOT LEAD
- Inquired within the last 48 hours OR was personally referred
- Strategy: Move fast. Send full car package + financing + test drive CTA in first message
- Tone: Confident, helpful, ready to serve
- Channel: iMessage first, email as follow-up with full details

### WARM LEAD
- Inquired 3–30 days ago, showed interest but didn't commit
- Strategy: Re-engage with something new — price update, financing news, or "I wanted to personally check in"
- Tone: Friendly, low pressure, personal
- Channel: iMessage or email depending on what they responded to before

### DEAD LEAD
- Went cold — no response in 30+ days, said "not right now," or bought elsewhere
- Strategy: Lead with value, not a sales pitch. New inventory, rate drop, trade-in spike
- Tone: Casual, like a neighbor not a salesperson
- Channel: iMessage (feels personal), follow up with email if no response in 48 hrs

### PAID LEAD
- Came from a third-party site (Cars.com, AutoTrader, CarGurus, etc.)
- Strategy: They are actively shopping RIGHT NOW — speed wins. First to respond usually wins the deal
- Tone: Direct and informative. They want specs, price, availability
- Channel: iMessage immediately, email with full package within the same hour

## After Intake

Once you have the lead info and car details:
1. Go to `references/outreach.md` to build the message
2. Show the full draft for review
3. Wait for associate to approve or edit
4. On approval:
   - Create the Gmail draft (full HTML email to client)
   - **Automatically** send the client an iMessage: "Hey [FIRST NAME], check your email — I just sent you the details on the [YEAR MAKE MODEL] 🔑"
   - **Automatically** send the associate an iMessage: "📨 Draft ready: [SUBJECT] — open Gmail and hit send when ready"
5. **Auto-log to tracker** — immediately after draft is created, write to `~/car-sales-leads/leads.csv` with Status = DRAFT
6. Confirm everything to the associate in one summary block
7. When associate confirms they sent the email, update Status → CONTACTED

## Single Lead Quick-Add

If the associate says "add a lead" or drops in contact info without going through full intake:

Accept any of these formats:
```
add a lead: Marcus James 954-555-0101 youngtrappy4@gmail.com BMW i7
```
```
new lead: Derrick Brown, 786-555-0202, interested in X5
```
```
lead: Tasha Grant tasha@gmail.com dead lead from 6 months ago
```

Parse whatever is given, fill in what's missing with defaults:
- Lead Type: HOT (default unless context says otherwise)
- Car: ask once if not provided and no default inventory URL is set
- Phone/Email: use whatever is provided — don't require both

Add to `leads.csv` with Status = NEW, then immediately ask:
```
✅ Tasha Grant added to your tracker.
Want to send outreach now? (yes / skip for now)
```
