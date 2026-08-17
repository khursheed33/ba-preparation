# Wireframing and UX Basics for BAs

## Definition

A **wireframe** is a skeletal screen: layout, content, and actions without visual design. **Low-fidelity** (low-fi) uses boxes and labels (Balsamiq, paper, Figma in grayscale). **High-fidelity** (high-fi) looks like the real app (Figma with brand, colour, real images). A **user flow** is the path of screens and decisions a person takes to finish a job.

**Figma** is the common product-design tool. **Balsamiq** is built for low-fi sketch speed. You do not need to become a designer. You need to show *what information and actions* a screen must support.

## Why it matters

Stories without UI still ship — and then UAT says "where is the return reason?" A low-fi wireframe makes missing fields obvious before Dev builds the wrong layout. Staying low-fi avoids fake sign-off on colours while rules are still wrong.

## Low-fi vs high-fi

| | Low-fi | High-fi |
|---|---|---|
| Looks | Boxes, lorem, grayscale | Brand, icons, real photos |
| Speed | Fast; easy to throw away | Slow; people treat it as final |
| BA use | Default | Only if PO/design asks, or no designer |
| Risk | Stakeholders say "too ugly" | Stakeholders debate hex codes, not rules |

**Why BAs should usually stay low-fi unless asked:** you are specifying behaviour, not branding. High-fi implies decisions you do not own (spacing, illustration). If ShopEase has designers, hand them low-fi + AC; they produce high-fi.

Exception: executive demo of a new MediCare+ patient app when leadership cannot read a box sketch — pair with a designer.

## Wireframing fundamentals

1. One job per screen (start return, not "returns + wallet + ads").
2. Name the screen and the user.
3. Show primary action (one main button).
4. Show empty, loading, error — not only the happy screenshot.
5. Annotate rules: "Return hidden if day > 7".
6. Number screens to match the user flow.

Balsamiq: drag controls, markup arrows, export PNG to Jira. Figma: frames, auto-layout optional; use a BA-friendly kit; comment, do not pixel-push.

## User flow: ShopEase add-to-cart → checkout

```text
Home / PDP
  → Add to cart (guest or logged in)
    → Cart
      → [Empty cart] dead end: "Continue shopping"
      → Checkout
        → Login / guest gate
        → Address
          → Fail: pincode not serviceable → pick another address
        → Delivery slot
        → Payment
          → Fail: payment declined → retry or change method
          → Success → Order confirmation
```

BA notes on the flow (not pixels):

| Step | Must show | Edge |
|---|---|---|
| Add to cart | Variant, qty, stock | Out of stock CTA |
| Cart | Line price, offer, delivery estimate | Item goes OOS while in cart |
| Address | Default + add new | Serviceability |
| Payment | Saved methods, UPI, COD rules | Partial wallet + card |
| Confirmation | Order id, ETA, support | Duplicate submit (double tap) |

Link this flow on the epic. Each box can become a story.

## UX concepts BAs must know

| Concept | Meaning | BA example |
|---|---|---|
| Affordance | Control looks usable | "Return" looks like a button, not plain text |
| Empty state | First use or no data | No orders: explain how to shop, not a blank table |
| Error state | What went wrong + how to fix | "OTP expired. Resend" not "Error 500" |
| Accessibility lite | Contrast, labels, not colour-only | Error not only red; include text. Large tap targets for MediCare+ elderly. |
| Happy path | Main success journey | Pay and see confirmation |
| Edge | Rare or failure path | Payment timeout, session expiry, COD blocked for this SKU |

You are not the accessibility auditor. You *are* the person who must write AC for empty and error, or QA will only test the happy path.

## Real-world examples

1. **NovaBank** fund transfer: low-fi shows "If amount > 10,000, OTP step". High-fi was delayed; Dev still built the extra screen from the wireframe + AC.
2. **QuickBite** restaurant closed: empty state on the menu ("Opens at 11:00") instead of a spinner forever.

## Scenario / Use case

ShopEase checkout drop-off is high on Android. The BA maps the user flow and sketches low-fi in Balsamiq: cart → address → payment. In a 30-minute review, CX says users do not see that COD is unavailable for the pincode until the last step. The BA adds an earlier warning on Address ("COD not available for this pincode") and an error state on Payment that offers UPI.

Design later produces high-fi. Stories ship with AC for the warning and the decline retry. The BA never chose the shade of green. Conversion is the outcome, not the mock beauty.

## Weak vs strong

| Weak | Strong |
|---|---|
| "Make it like Amazon" | Numbered flow + low-fi per step |
| Only happy path PNG | Empty, error, permission denied |
| BA polishing Figma shadows | Annotations + AC; designer owns visual |
| Flow in the BA's head | Flow on Confluence, linked to Jira |
| Colour-only "invalid" field | Text error + field label (a11y lite) |
| One screen for five jobs | Split; one primary action |

## Notes

- You do not need to master every tool; purpose and workflow matter more than Figma shortcuts.
- If you cannot draw the flow on paper, you are not ready to wireframe.
- Put wireframes on the Jira story; do not hide them in a Figma file nobody can open.
- Say "draft, not visual sign-off" at the top of every BA frame.
- Accessibility lite: alt text for meaningful images, visible labels, keyboard for NovaBank web — flag, do not pretend to be an a11y specialist.
- Guest checkout vs login is a business rule; show both in the flow.
- Change the wireframe when AC changes; stale mocks cause the same bug as stale AC.
