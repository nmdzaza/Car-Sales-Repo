# Car Package Builder

When an associate provides a link to a vehicle on their dealership's website, fetch that page and extract all usable data. This becomes the foundation of every message, email, and info package sent to the lead.

---

## Step 1: Fetch and Extract from the Link

When given a URL, pull the following fields from the page. If a field isn't on the page, mark it as `[NOT LISTED]` — never guess or fabricate specs.

```
VEHICLE DATA EXTRACTED:
- Year:
- Make:
- Model:
- Trim level:
- Exterior color:
- Interior color:
- Mileage:
- Price (MSRP or asking):
- VIN:
- Engine / drivetrain:
- Transmission:
- Fuel type:
- MPG (city / highway):
- Key features (pull the top 5-6 from the listing):
- Dealer stock number (if listed):
- Condition (new / used / certified pre-owned):
- Any dealer specials or incentives on this car:
- Full listing URL (confirm it):
```

---

## Step 2: Build the Car Summary Block

Format extracted data into a clean summary block ready to drop into any message or email:

```
─────────────────────────────
[YEAR] [MAKE] [MODEL] [TRIM]
─────────────────────────────
💰 Price: [PRICE]
📍 Mileage: [MILEAGE]
🎨 Color: [EXTERIOR] / [INTERIOR]
⛽ [ENGINE] | [MPG] MPG
🔢 VIN: [VIN]

Highlights:
• [FEATURE 1]
• [FEATURE 2]
• [FEATURE 3]
• [FEATURE 4]
• [FEATURE 5]

🔗 Full details + photos: [URL]
```

---

## Step 3: Build the Financing Block

Use the dealership's financing partners from the Dealership Profile. Provide estimated monthly payments at common terms. Always note these are estimates pending credit approval.

```
─────────────────────────────
FINANCING OPTIONS
─────────────────────────────
We work with: [FINANCING PARTNER 1], [FINANCING PARTNER 2], [FINANCING PARTNER 3]

Estimated monthly payments on [PRICE] with $[DOWN PAYMENT] down:
• 48 months: ~$[CALC]/mo
• 60 months: ~$[CALC]/mo
• 72 months: ~$[CALC]/mo

(Rates vary based on credit. We work with all credit situations.)

👉 Apply online: [FINANCE APPLICATION LINK]
```

To estimate monthly payment use this formula (approximate):
`Monthly ≈ (Price - Down) × (rate/12) / (1 - (1 + rate/12)^-term)`
Use 6.9% APR as a default if no rate is specified. Always label estimates as approximate.

---

## Step 4: Build the Trade-In Block

If the lead has a trade-in, add this block. Use the dealership's trade-in tool link if provided.

```
─────────────────────────────
YOUR TRADE-IN
─────────────────────────────
Have a vehicle to trade? Values are strong right now.

Get your estimate in 60 seconds:
👉 [TRADE-IN TOOL LINK e.g. KBB / Edmunds]

Bring it in and we'll apply the value directly to your deal — could significantly lower your monthly payment.
```

If no trade-in tool link is in the Dealership Profile, use:
`https://www.kbb.com/car-values/` as a neutral fallback.

---

## Step 5: Assemble Full Package

When sending a full info package (hot lead email, or lead-response follow-up), combine all blocks:

1. Personalized greeting
2. Car Summary Block
3. Financing Block
4. Trade-In Block (if applicable)
5. Next step CTA

This full package goes in the email body. For iMessage, send the car summary + link only — keep texts short.

---

## PDF Generation (Optional)

If the associate wants a PDF instead of an email body, generate a formatted PDF using the PDF tools available. Structure it as:

- Page 1: Car photo placeholder + full vehicle summary
- Page 2: Financing options comparison table
- Page 3: Trade-in info + next steps + dealership contact

Label the file: `[YEAR]_[MAKE]_[MODEL]_[CUSTOMER_LAST_NAME].pdf`

Only generate a PDF if the associate specifically requests it or if the lead asks for something they can review later. Otherwise formatted email is sufficient.
