# Outreach Message Templates

Build every message using the car details pulled from the dealer link and the lead intake info. Replace all `[BRACKETS]` with real data before showing the draft.

Always show the draft in the review block format from SKILL.md before sending.

---

## iMessage Templates

### HOT LEAD — First Contact (iMessage)

```
Hey [FIRST NAME]! This is [SALESPERSON] over at [DEALERSHIP].

I saw you were interested in the [YEAR] [MAKE] [MODEL] — great choice. We still have it on the lot and I wanted to reach out personally before someone else snags it.

Here's the quick rundown:
🚗 [YEAR] [MAKE] [MODEL] [TRIM]
📍 [MILEAGE] miles
💰 Priced at [PRICE]
✅ [KEY FEATURE 1]
✅ [KEY FEATURE 2]
✅ [KEY FEATURE 3]

We work with [FINANCING PARTNER 1] and [FINANCING PARTNER 2] so we can get you competitive rates even if your credit isn't perfect.

Want to come take it for a spin? I can have it ready for you today or tomorrow — just say the word.

Reply YES and I'll hold it for you. 🔑
```

---

### WARM LEAD — Re-engagement (iMessage)

```
Hey [FIRST NAME], it's [SALESPERSON] from [DEALERSHIP].

I know we talked a while back about the [YEAR] [MAKE] [MODEL] — just wanted to pop back in because [CHOOSE ONE: the price dropped / we got a similar one in / rates just came down / I've been thinking about your situation].

Still available: [DEALER WEBSITE LINK]

No pressure at all — just wanted to make sure you had the latest. If the timing is better now, I'm here. If not, no worries either way.

Either way, what's your situation looking like? 🤙
```

---

### DEAD LEAD — Win Back (iMessage)

```
Hey [FIRST NAME] — [SALESPERSON] here from [DEALERSHIP]. Hope you're doing well.

I know it's been a minute since we last talked. I'm not reaching out to bug you — I actually just got something in that made me think of you.

[YEAR] [MAKE] [MODEL] — [MILEAGE] miles, [PRICE]. Clean, solid car.

[DEALER WEBSITE LINK]

If the timing ever lines up, I'm your guy. And if you've got a trade-in, values are actually pretty strong right now — worth checking at least.

No reply needed if it's not the right time. Just wanted you to know we're here. 👊
```

---

### PAID LEAD — Immediate Response (iMessage)

```
Hi [FIRST NAME]! I'm [SALESPERSON] at [DEALERSHIP] — I saw your inquiry about the [YEAR] [MAKE] [MODEL] and wanted to reach out right away.

Good news: it's still available. Here's what you're looking at:

🚗 [YEAR] [MAKE] [MODEL] [TRIM]
📍 [MILEAGE] miles
💰 [PRICE] (financing available)
🔗 Full details: [CAR LINK]

We work with multiple lenders so we can find you the best rate. Do you have a trade-in? That could bring your monthly payment down nicely.

When are you free to come see it? I can get you in and out quick — I know your time is valuable.
```

---

## Email Templates

Use email as the follow-up to iMessage OR as the primary channel if that's what the lead prefers. All emails are sent as **HTML via Gmail draft**.

**Two-message flow every time an email is drafted:**

1. **Gmail draft is created** (the full HTML car package email to the client)
2. **Client gets an iMessage automatically** — a short personal intro from the salesperson telling them to check their email:
   ```
   Hey [FIRST NAME]! It's [SALESPERSON] from [DEALERSHIP] — I just sent you something over email about the [YEAR] [MAKE] [MODEL] you were asking about. Check your inbox when you get a sec, I put together the full details for you. 🔑
   ```
3. **Associate gets an iMessage automatically** — notifying them the draft is ready and waiting:
   ```
   📨 Draft ready: "[EMAIL SUBJECT]"
   To: [LEAD NAME] ([EMAIL])
   Car: [YEAR MAKE MODEL] — [PRICE]
   
   👉 Open Gmail and hit send when you're ready.
   ```

The associate reviews the Gmail draft, then sends it manually. The client's intro iMessage goes out automatically so they're already looking for the email.

---

### IMAGE RULES FOR ALL EMAILS

**Step 1 — Get the real image URL from the listing page:**
When fetching car specs, also look for the vehicle photo URL hosted on the dealer's own domain (e.g., `chapmanbmwchandler.com/...`). Copy that exact URL.

**Step 2 — Embed it correctly:**
```html
<a href="[CAR LISTING URL]" target="_blank">
  <img src="[DEALER-HOSTED IMAGE URL]"
       alt="[YEAR] [MAKE] [MODEL] [TRIM]"
       width="620"
       style="display:block; width:100%; border:none;" />
</a>
```

**Rules:**
- ✅ Use image URLs from the dealer's own domain only
- ❌ Never use third-party CDN URLs (e.g., `images.dealer.com`, `dealereprocess.com`, `dealercarsearch.com`) — these are blocked by Gmail and most email clients
- ❌ Never hotlink manufacturer press images — they block external requests
- If no dealer-hosted image is found, replace with a bold styled header block instead:
```html
<div style="background:#000;padding:40px;text-align:center;">
  <h1 style="color:#fff;font-size:28px;margin:0;">[YEAR] [MAKE] [MODEL]</h1>
  <p style="color:#aaa;font-size:14px;margin-top:8px;">[TRIM] &nbsp;|&nbsp; [COLOR]</p>
</div>
```

---

### HOT LEAD — HTML Email Template

Build this as a full HTML email. Fill all `[BRACKETS]` with real data before creating the Gmail draft.

```html
<!DOCTYPE html>
<html>
<body style="font-family:Arial,sans-serif;background:#f4f4f4;margin:0;padding:0;">
<div style="max-width:620px;margin:0 auto;background:#fff;border-radius:8px;overflow:hidden;">

  <!-- Header bar -->
  <div style="background:#000;padding:18px 28px;">
    <p style="color:#fff;font-size:12px;margin:0;letter-spacing:2px;text-transform:uppercase;">
      [DEALERSHIP NAME] &nbsp;|&nbsp; [SALESPERSON NAME]
    </p>
  </div>

  <!-- Car image — use dealer-hosted URL only. If unavailable, use the fallback header block above -->
  <a href="[CAR LISTING URL]" target="_blank">
    <img src="[DEALER-HOSTED IMAGE URL]"
         alt="[YEAR] [MAKE] [MODEL] [TRIM]"
         width="620"
         style="display:block;width:100%;border:none;" />
  </a>

  <!-- Body -->
  <div style="padding:28px;">
    <h1 style="font-size:22px;color:#000;margin-top:0;">[YEAR] [MAKE] [MODEL] [TRIM]</h1>
    <p style="color:#444;font-size:15px;line-height:1.7;">
      Hey [FIRST NAME],<br><br>
      It's <strong>[SALESPERSON]</strong> over at <strong>[DEALERSHIP]</strong>.
      I pulled this together for you personally — this one's worth a serious look.
    </p>

    <!-- Specs table -->
    <table style="width:100%;border-collapse:collapse;font-size:14px;margin:20px 0;">
      <tr style="background:#f9f9f9;">
        <td style="padding:10px;color:#888;width:40%;">Exterior</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[EXTERIOR COLOR]</td>
      </tr>
      <tr>
        <td style="padding:10px;color:#888;">Interior</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[INTERIOR COLOR / MATERIAL]</td>
      </tr>
      <tr style="background:#f9f9f9;">
        <td style="padding:10px;color:#888;">Engine</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[ENGINE / HP / DRIVETRAIN]</td>
      </tr>
      <tr>
        <td style="padding:10px;color:#888;">Mileage</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[MILEAGE]</td>
      </tr>
      <tr style="background:#f9f9f9;">
        <td style="padding:10px;color:#888;">MSRP</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[PRICE]</td>
      </tr>
      <tr>
        <td style="padding:10px;color:#888;">Est. Payment</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[EST PAYMENT]/mo | [APR]% APR ([TERM] mo)</td>
      </tr>
      <tr style="background:#f9f9f9;">
        <td style="padding:10px;color:#888;">VIN</td>
        <td style="padding:10px;color:#000;font-weight:bold;">[VIN]</td>
      </tr>
    </table>

    <!-- Key features -->
    <h3 style="color:#000;font-size:16px;">What's On It:</h3>
    <ul style="color:#444;font-size:14px;line-height:2.2;padding-left:20px;">
      <li><strong>[PACKAGE / FEATURE 1]</strong> — [brief description]</li>
      <li><strong>[PACKAGE / FEATURE 2]</strong> — [brief description]</li>
      <li><strong>[PACKAGE / FEATURE 3]</strong> — [brief description]</li>
      <li><strong>[PACKAGE / FEATURE 4]</strong></li>
      <li><strong>[PACKAGE / FEATURE 5]</strong></li>
    </ul>

    <!-- Financing -->
    <div style="background:#f4f4f4;border-left:4px solid #000;padding:14px 18px;margin:20px 0;font-size:14px;color:#444;">
      We work with <strong>[FINANCING PARTNER 1]</strong> and <strong>[FINANCING PARTNER 2]</strong> —
      I can get you pre-qualified today with no impact to your credit score.<br><br>
      Got a trade? Check your value now:
      <a href="https://www.kbb.com" style="color:#000;font-weight:bold;">kbb.com</a>
      — I'll factor it into your numbers on the spot.
    </div>

    <!-- CTA button -->
    <div style="text-align:center;margin:28px 0;">
      <a href="[CAR LISTING URL]" target="_blank"
         style="background:#000;color:#fff;text-decoration:none;padding:14px 36px;
                border-radius:4px;font-size:15px;font-weight:bold;display:inline-block;">
        👁 View Full Vehicle Details
      </a>
    </div>

    <p style="color:#444;font-size:14px;line-height:1.9;">
      Ready to make a move? Reply here or hit me directly:<br>
      📞 <strong>[PHONE]</strong><br>
      ✉️ [EMAIL]
    </p>

    <p style="color:#444;font-size:14px;">— [SALESPERSON]<br><strong>[DEALERSHIP]</strong></p>
  </div>

  <!-- Footer -->
  <div style="background:#000;padding:14px 28px;text-align:center;">
    <p style="color:#666;font-size:11px;margin:0;">
      [DEALERSHIP] &nbsp;|&nbsp; [EMAIL] &nbsp;|&nbsp; [PHONE]
    </p>
  </div>

</div>
</body>
</html>
```

---

### DEAD LEAD — Re-engagement HTML Email

Same HTML structure as above. Change the body copy to:

```
Hey [FIRST NAME],

[SALESPERSON] here from [DEALERSHIP]. It's been a while — I'm not reaching out to bug you, I promise.

I just came across a [YEAR] [MAKE] [MODEL] that made me think of you. Figured I'd put it in front of you in case the timing is better now.

[Use specs table + CTA button — same as hot lead template above]

A couple things worth knowing:
• Rates have shifted — I may be able to get you a better monthly than before
• Trade-in values are holding strong right now — worth checking yours
• We've got more flexible financing options than we did last time

No pressure. If you're ready, I'm here. If not, no worries at all.

— [SALESPERSON]
[DEALERSHIP] | [PHONE] | [EMAIL]
```

---

## Sequence Logic

For leads that don't respond, follow this cadence automatically (show each draft before sending):

| Day | Channel | Message Type |
|-----|---------|--------------|
| Day 1 | iMessage | First outreach (template above) |
| Day 2 | Email | Full car package email |
| Day 5 | iMessage | Short bump ("Hey [NAME], just checking in — still available!") |
| Day 10 | Email | Value angle ("Rates dropped / similar car came in / trade-in values up") |
| Day 21 | iMessage | Final soft touch ("No worries if timing isn't right — here if you need me") |

After day 21 with no response, flag the lead as dormant and move on. Don't over-contact.
