# Meri Jaisi Proof Layer - interactive prototype

**Meesho DICE Challenge S3 · Business Track · Prototype Submission Round**
Archit Singla · Abhinav Sagar

Creator demos become suitability-matched proof on the Meesho PDP, matched on skin tone, skin type or hair type, and paid only on delivered conversions. This is a clickable version of our Round 2 deck: the shopper's PDP, the creator programme, the brand coverage matrix and the attribution ledger, running end to end on mock data.

**Live demo:** https://itsarchitsingla.github.io/meri-jaisi-prototype/
Press ▶ 2-minute guided demo on the page; it drives itself.

![Shopper view: the Meesho PDP with the Meri Jaisi module at the shade selector, and the gate trace beside it](screenshots/shopper.png)

## Two-minute walkthrough for judges

Click the guided-demo button and press Next; the page runs the steps below by itself. To do it by hand:

1. **Shopper tab, Tier 2, Matte Lipstick.** Nothing is asked on page load. Tap the chip on the product image (“Meri jaisi skin pe dekho”). The 3-tap quiz opens: closest face on a 6-band scale, skin and hair, language pre-filled from the app. Finish it and the best-matched demo plays.
2. **Watch the demo.** The sealed pack opens at 0:02, product is on skin from 0:05. Tap “Yeh shade kharidein”, then “» Buy at ₹199”. The confirmation names the demo that gets attributed and why.
3. **Ledger tab.** Deliver the order, end the 7-day return window. ₹12 (60% of the link rate on ₹199) releases to the creator. Try “Return” or “Refuse at door” on a second order to see nothing pay out.
4. **Creator tab.** The creator's earnings now include that payout. Confirm her AI-pre-filled attribute profile in one tap, submit a demo through the QC gate, and see the payout throttle (full / half / none per band).
5. **Brand tab.** The coverage dashboard shows which tone × language cells have views but no demo. Fund a kit into an empty cell; it appears on the creator's Demo-Wanted board. Trip the return-rate circuit breaker and the Vitamin C Serum (coverage tier B, inherited demos) falls back to the honest “no demo yet” state.
6. **Back on Shopper.** Switch to Tier 3 and Tier 4: no quiz, matched from pincode and app language, regional copy, 6-second 240p clips, and a swatch-strip image fallback. In Tier 4, tap the chip or the module title to hear the copy read aloud.
7. **Anti-Frizz Shampoo.** Same model, different attribute: the quiz leads with hair type, the module matches on hair, and the Brand tab's matrix becomes hair type × language.
8. **Edges.** Switch to the Liquid Lipstick (tier C) for the honest empty state, and the Steel Water Bottle to see the Proof Layer stay out of a non-beauty PDP entirely.

![Four phone states: matched module, demo player, Tier 4 lite mode, and the honest no-demo state](screenshots/phone-states.png)

![The Anti-Frizz Shampoo matched on hair type (wavy)](screenshots/shampoo.png)

## What is in it

| Tab | Who it is for | What it shows (deck slide) |
|---|---|---|
| Shopper | The buyer | Mock Meesho PDP with chip A, match module B, review filter C and 3-tap quiz D; tier switcher for Tier 1–4 capture; live trace of the five gates on every PDP open; Puchho Q&A grounded only in demos, matched reviews and ingredients (slides 6, 9) |
| Creator | The Creator Club member | Tag (AI-pre-filled attribute vector, confirm in one tap, delete), Attach (reel → cluster mapping with confidence, QC gate), Demo-Wanted board with bounties, earnings per demo with 90-day window (slides 5, 8) |
| Brand | The seller / brand | Coverage dashboard (cluster × band × language), fund-a-kit into empty cells, return-rate circuit breaker on inherited demos, “didn't suit my tone” as a routing signal (slides 5, 7, 8) |
| Ledger | The platform | Attribution rules applied to every event: what pays, what never pays, the 90-day cap, margin neutrality; payout throttle per band (slides 5, 7) |
| All four tabs | Everyone | Three suitability axes: skin tone (lipstick), skin type (serum), hair type (shampoo); one attribute model, one set of mechanics. |
| Guided demo | A judge with two minutes | A 16-step tour that drives the page itself: chip, quiz, demo, cash-on-delivery order, ledger payout, creator earnings, coverage matrix, circuit breaker, Tier 4, the shampoo, and gate 1 |

## What is real and what is mocked

| Element | Status |
|---|---|
| Gate logic (5 gates, never/fallback rules) | Implemented as written on slide 9 |
| Matching (axis distance → secondary attributes → language → region; language-first in Tier 3/4) | Implemented, rule-based (the v0 ranker). Weights are ours, to be replaced by learning-to-rank on delivered-not-returned conversion in v1 |
| Attribution (deliberate engagement, 90-day window, pay after delivery + return window, last-engaged wins, one payout per user × cluster, never-pays list) | Implemented; all events are logged in-session |
| Payout throttle, Demo-Wanted bounties, kit funding, circuit breaker | Implemented |
| Tier-wise capture and copy | Implemented. Regional copy is illustrative and would be creator-approved before launch |
| Guided tour | Implemented; it drives the real logic, so the payout it shows is computed, not scripted |
| Tier 4 speech | Uses the browser's Hindi voice if one is installed; silent otherwise |
| Creators, demos, reviews, views, prices, orders | Mock data, chosen to be plausible |
| Images | Creator portraits and demo frames are AI-generated illustrations and stills of fictional people; no real people. Product shots are AI-generated and unbranded. Any missing image falls back to a drawing |
| Videos | Simulated player with the QC markers (sealed pack at 0:02, on skin from 0:05) |
| Payment, delivery, returns | Simulated with buttons so the money can be followed |
| Screens | A mock of Meesho's live Android PDP as of October 2026 (delivery banner, trust strip, single Buy button); drawn, not screenshotted. |
| Persistence | The shopper's saved quiz lives in the browser's localStorage only. Nothing leaves the browser |

One deliberate change from the deck's static mock on slide 6: the module never shows a tone word (the mock showed “Wheatish”). Slides 7 and 9 say the UI only ever says “like you”, so the prototype follows that rule.

## Run it

Open `index.html` in any browser. No build step, no dependencies. Images load from `img/`; if one is missing, the page shows a drawing in its place. The only network requests are the Mukta and DM Sans web fonts; without them the page falls back to the system font.

## Deploy to GitHub Pages

1. Create a public repository, `meri-jaisi-prototype`.
2. Upload `index.html`, `README.md`, `img/` and `screenshots/` (or `git push` this folder).
3. In the repository, open **Settings → Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute the site is live at https://itsarchitsingla.github.io/meri-jaisi-prototype/.

## Repository layout

```
index.html            the whole prototype (HTML, CSS and JavaScript in one file)
README.md             this file
img/                  avatars/, products/, frames/ (all JPEG), hero.jpg, og.jpg (link preview)
screenshots/          images used above
```

## What v1 adds (not in this prototype)

Per slide 10: AI creator tagging from reels and audio, reel → cluster mapping service with human review on low confidence, learning-to-rank on delivered-not-returned conversion, the attribution ledger as a service, creator-approved dubbing into 8 languages, and the coverage dashboard wired to live PDP-view data. v0, which this prototype represents, needs none of that: a PDP widget pointing at Video Finds, a tagging sheet and a weekly manual payout run.
