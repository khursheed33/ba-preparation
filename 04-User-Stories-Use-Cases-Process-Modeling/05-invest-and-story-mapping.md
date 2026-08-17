# INVEST and User Story Mapping

## Definition

**INVEST** is a quality check for a user story: Independent, Negotiable, Valuable, Estimable, Small, Testable.

**User story mapping** is a visual backlog: activities along a **backbone** (the journey), stories underneath as slices, then **releases** drawn as horizontal cuts. A **walking skeleton** is the thinnest end-to-end slice that proves the journey works.

## Why it matters

INVEST catches fat, technical, or untestable items before planning. Mapping shows missing steps and exception stories that a flat backlog hides. Checkout that only has "pay" and "done" will fail the first guest user with a failed card.

## Concepts

### INVEST — pass / fail examples

| Letter | Meaning | Fail | Pass |
|---|---|---|---|
| **I**ndependent | Can be delivered without a twin story | "Pay" blocked forever on "new wallet platform" in the same sprint | Guest checkout with card; wallet as a later story |
| **N**egotiable | Details can change; not a contract spec | 14-page UI spec as the story body | Story + AC; UI labels negotiable in the sprint |
| **V**aluable | A user or business sees benefit | "Create payments table" | "Guest can pay and see order number" |
| **E**stimable | Team can size it | "Integrate whatever the bank sends" | Known card gateway; spike if bank spec missing |
| **S**mall | Fits a sprint | Whole ShopEase checkout | "Guest pays with saved-enough card details" |
| **T**estable | Clear pass/fail | "Checkout should feel premium" | Given valid card, When pay, Then order id shown |

A story can fail more than one letter. Fix independence by splitting; fix testable by adding AC; fix estimable with a spike.

### User story mapping: backbone, walking skeleton, releases

1. **Backbone:** high-level activities in user order (left to right).
2. **Stories under each activity:** variants, details, exceptions (down the column).
3. **Walking skeleton:** one story from each necessary backbone step — ugly but complete.
4. **Releases:** horizontal lines. Release 1 = skeleton + must-have exceptions. Later releases add convenience.

### Map for ShopEase checkout: guest vs login, address, payment, confirmation

**Backbone (left → right):** Identify shopper → Address → Payment → Confirmation

| Backbone | Walking skeleton (Release 1) | Release 2 | Later / exceptions |
|---|---|---|---|
| Identify | Continue as guest with email | Login / create account | Social login, 2FA mid-checkout |
| Address | Enter a single delivery address | Saved addresses, edit | Invalid pincode, COD not available |
| Payment | Pay with card (success) | UPI, saved cards | Card decline, timeout, 3DS fail |
| Confirmation | Order id + email | SMS + "track order" link | Payment success but order persist fail |

Walking skeleton: guest + one address + successful card + order number. That is demoable. Login is not required to learn whether payment and inventory reservation work.

### How mapping finds missing exception stories

Walk the map with support and QA and ask at each cell: "What if this fails?" Gaps become stories:

- Guest email bounces → "resend confirmation" or "edit email."
- Address pincode not serviceable → stop before payment (do not charge then fail).
- 3DS timeout → retry without double charge.
- Payment captured, order insert fails → finance exception story (ops queue), not a footnote.

If it is not on the map, it will not be in the release, and it will appear as a production incident.

## Real-world examples

1. **MediCare+:** Mapping "book appointment" surfaces no-show and cancellation (often missing from the happy backbone).
2. **ShieldSure:** Mapping "buy policy" surfaces KYC fail and payment fail as exception rows, not "phase 2 maybe."

## Scenario / Use case

### Context

ShopEase PO lists flat stories: login, cart, pay. Guest checkout is assumed. Support already knows card-decline volume is high. Mapping has never been done.

### Stakeholders

Buyer (guest and registered), payments, warehouse, support, PO, BA, QA, fraud.

### BA actions

1. Facilitate a 90-minute mapping workshop on a board (physical or Miro).
2. Build backbone; dump all known stories under columns.
3. Draw Release 1 as walking skeleton + top exceptions (decline, unserviceable pincode).
4. Run INVEST on Release 1 stories; split login away from guest pay.

### Sample artifact

A story map photo/export with yellow backbone, blue Release 1, pink exception rows, and a parking lot for "wallet." INVEST notes on each Release 1 card.

### Failure if ignored

Team builds logged-in checkout only. Guests abandon. Card declines show a generic error; customers are charged twice on retry. Mapping would have made those stories visible before sprint 1.

## Weak vs strong

| Weak | Strong |
|---|---|
| INVEST as a poster nobody uses | Fail a story in refinement with a letter |
| Map = pretty journey with no exceptions | Exception rows under each backbone step |
| Walking skeleton = UI mock only | Real pay + real order id, limited variants |
| Release lines by team (front end) | Release lines by user-completable journey |

## Notes

- Independent does not mean zero dependency; it means you can ship value without waiting on a twin.
- Negotiable is not "no AC." AC still exist; implementation can flex.
- If the skeleton cannot be demoed, it is not a skeleton.
- Missing exceptions are the main ROI of mapping — invite support.
- Re-map after go-live when incident themes appear.
