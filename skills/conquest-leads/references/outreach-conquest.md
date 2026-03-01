# Conquest Outreach Templates

These templates are for contacting **private sellers** — people already listing their car for sale on Craigslist, CarGurus, AutoTrader, or OfferUp. The goal is to convert them into a **trade-in lead**, **direct purchase lead**, or **replacement buyer**.

Always fill in all `[BRACKETS]` with real data from the listing before showing the draft.

---

## The Three Angles

Choose the angle based on the associate's Search Profile and what the listing suggests:

| Angle | Use When | Goal |
|-------|----------|------|
| **Trade-In Offer** | Seller might want to upgrade/replace | Get them to trade it in with your dealership |
| **Direct Purchase** | They just want the car gone fast | Buy the car outright (adds to dealer inventory) |
| **Replacement Buyer** | They're selling to buy something different | Be their next car too |

You can stack angles — lead with one, mention the others as options.

---

## iMessage / Text Templates

### TRADE-IN ANGLE — iMessage

```
Hey [FIRST NAME OR "there" if no name], saw your [YEAR] [MAKE] [MODEL] listed at $[PRICE].

This is [SALESPERSON] at [DEALERSHIP]. Instead of dealing with the hassle of private buyers and lowball offers — have you thought about trading it in?

We can do a fast appraisal, give you a real number, and apply it directly to your next vehicle. You'd be surprised what your car is worth right now.

Worth 5 minutes? I can pull comps for your exact car today.

[SALESPERSON]
[DEALERSHIP]
[PHONE]
```

---

### DIRECT PURCHASE ANGLE — iMessage

```
Hey [FIRST NAME / "there"], [SALESPERSON] from [DEALERSHIP] here.

Saw your [YEAR] [MAKE] [MODEL] on [SOURCE — Craigslist/CarGurus/etc.]. We're actively buying vehicles like yours right now.

If you want a fast, fair offer with no fees, no strangers coming to your house, and same-day payment — I can make that happen.

Just reply back and I'll get you a real number within the hour.

[SALESPERSON] | [DEALERSHIP] | [PHONE]
```

---

### REPLACEMENT BUYER ANGLE — iMessage

```
Hey [FIRST NAME / "there"] — [SALESPERSON] from [DEALERSHIP].

Noticed your [YEAR] [MAKE] [MODEL] for sale at $[PRICE]. Great car.

If you're looking to move into something else, I might be able to handle both sides — take your car as a trade and put you in something new for close to what you'd net on a private sale anyway.

No pressure, just wanted to put the option in front of you. What are you looking to get into next?

[SALESPERSON] | [DEALERSHIP] | [PHONE]
```

---

### CRAIGSLIST EMAIL REPLY — No Phone Available

When no phone number is found, use the listing's email/reply form. Keep it short — Craigslist inboxes get buried:

```
Subject: Quick question about your [YEAR] [MAKE] [MODEL]

Hi,

I'm [SALESPERSON] with [DEALERSHIP]. Came across your listing — nice [YEAR] [MAKE] [MODEL].

I work with buyers and can also offer a direct purchase or trade-in appraisal if you'd rather skip the private sale process.

Would a fair cash offer work for you? Happy to give you a real number fast — no obligation.

Best,
[SALESPERSON]
[DEALERSHIP]
[PHONE] | [EMAIL]
```

---

## HTML Email Templates

Use when seller has an email address (from CarGurus, AutoTrader, or extracted from listing).

---

### TRADE-IN OFFER — HTML Email

```html
<!DOCTYPE html>
<html>
<body style="font-family:Arial,sans-serif;background:#f4f4f4;margin:0;padding:0;">
<div style="max-width:600px;margin:0 auto;background:#fff;border-radius:8px;overflow:hidden;">

  <!-- Header -->
  <div style="background:#000;padding:18px 28px;">
    <p style="color:#fff;font-size:12px;margin:0;letter-spacing:2px;text-transform:uppercase;">
      [DEALERSHIP NAME] &nbsp;|&nbsp; [SALESPERSON NAME]
    </p>
  </div>

  <!-- Car image from listing (if available) -->
  <!-- Use the listing's photo URL if it loads from their platform CDN -->
  <!-- If unavailable, use the styled fallback header below -->

  <!-- Body -->
  <div style="padding:28px;">
    <h1 style="font-size:20px;color:#000;margin-top:0;">
      We Saw Your [YEAR] [MAKE] [MODEL] — We Can Make This Easy
    </h1>

    <p style="color:#444;font-size:15px;line-height:1.8;">
      Hi,<br><br>
      I'm <strong>[SALESPERSON]</strong> with <strong>[DEALERSHIP]</strong>.
      I came across your listing for the <strong>[YEAR] [MAKE] [MODEL]</strong> at
      <strong>$[ASKING PRICE]</strong> and wanted to reach out personally.
    </p>

    <!-- Value prop box -->
    <div style="background:#f9f9f9;border-left:4px solid #000;padding:16px 20px;margin:20px 0;font-size:14px;color:#444;">
      <strong>Here's what we offer vs. a private sale:</strong><br><br>
      ✅ <strong>No strangers showing up to your home</strong><br>
      ✅ <strong>No lowball offers or wasted time</strong><br>
      ✅ <strong>Fast appraisal — real number within the hour</strong><br>
      ✅ <strong>Apply it as a trade-in credit toward your next vehicle</strong><br>
      ✅ <strong>Or we buy it outright — same-day payment</strong>
    </div>

    <p style="color:#444;font-size:15px;line-height:1.8;">
      Trade-in values on <strong>[MAKE] [MODEL]</strong> are holding strong right now.
      You might be leaving money on the table selling private — I'd love to show you our number.
    </p>

    <!-- CTA -->
    <div style="text-align:center;margin:28px 0;">
      <a href="tel:[SALESPERSON PHONE]"
         style="background:#000;color:#fff;text-decoration:none;padding:14px 36px;
                border-radius:4px;font-size:15px;font-weight:bold;display:inline-block;">
        📞 Get Your Free Appraisal — Call or Text
      </a>
    </div>

    <p style="color:#444;font-size:14px;line-height:1.9;">
      No obligation. Takes 5 minutes. I'll have a real offer ready for you.<br><br>
      📞 <strong>[SALESPERSON PHONE]</strong><br>
      ✉️ [SALESPERSON EMAIL]
    </p>

    <p style="color:#444;font-size:14px;">— [SALESPERSON]<br><strong>[DEALERSHIP]</strong></p>
  </div>

  <!-- Footer -->
  <div style="background:#000;padding:14px 28px;text-align:center;">
    <p style="color:#666;font-size:11px;margin:0;">
      [DEALERSHIP] &nbsp;|&nbsp; [SALESPERSON EMAIL] &nbsp;|&nbsp; [SALESPERSON PHONE]
    </p>
  </div>

</div>
</body>
</html>
```

---

### DIRECT PURCHASE OFFER — HTML Email

Same structure as above. Swap the body copy to:

```
Subject: We'll Buy Your [YEAR] [MAKE] [MODEL] — Fast Offer, No Hassle

Hi,

I'm [SALESPERSON] at [DEALERSHIP]. I came across your [YEAR] [MAKE] [MODEL] listed at $[PRICE] and wanted to reach out.

We're buying vehicles like yours right now and can make this extremely simple:

✅ Real cash offer — no games
✅ No strangers at your door
✅ No listing fees, no waiting
✅ We handle all the paperwork
✅ Same-day payment if numbers work

I can have an offer for your [YEAR] [MAKE] to you within the hour. Just reply or call me directly.
```

---

### REPLACEMENT BUYER — HTML Email

Same structure. Swap body copy to:

```
Subject: Selling Your [YEAR] [MAKE] [MODEL]? We Can Handle Both Sides

Hi,

I'm [SALESPERSON] at [DEALERSHIP]. I saw your [YEAR] [MAKE] [MODEL] on [SOURCE].

Here's something worth considering — if you're selling to buy something else, I can handle both sides:

✅ We take your [YEAR] [MAKE] as a trade-in (real appraisal, real credit)
✅ We put you in your next vehicle the same day
✅ Your trade-in credit comes straight off the purchase price
✅ We work with [FINANCING PARTNER 1] and [FINANCING PARTNER 2] — great rates available

In many cases, you end up in a newer car for a monthly payment that's lower than you'd expect — especially with what your [MAKE] [MODEL] is worth right now.

Worth a conversation? Call or text me:
```

---

## Tone Rules

- **Always transparent** — you're a dealership rep, not a random buyer
- **Lead with their convenience** — they're tired of flaky buyers, negotiations, strangers
- **Never lowball in the message** — make the offer over the phone/in person, not in cold outreach
- **Don't over-explain** — 3–4 value points max, then one CTA
- **Use their car details** — saying "your 2021 BMW 5 Series at $38,500" shows you actually looked, not a blast

---

## Batch Mode — Multiple Listings

When working multiple listings in sequence:

For each listing:
1. Show the listing summary (year, make, model, price, phone/email, source)
2. Confirm which angle to use (or auto-select based on Search Profile)
3. Show the draft
4. Associate approves → send via iMessage tool (if phone) or Gmail draft (if email)
5. Log to pipeline (see `pipeline-handoff.md`)
6. Move to next listing

Progress counter after each:
```
✅ [N] contacted | ⏳ [remaining] left in queue
```
