# Saral: Product Requirements Document (PRD)

**Course:** Design Thinking
**Prototype:** Saral test bench (single-file web app, `saral.html`)
**Live link:** https://claude.ai/artifact/JbQ4fLHwz6Aw2x4k3Rp3P2
**Status:** Prototype v1, proxy-tested (no interviews with real drivers yet)

---

## 1. Problem statement

Users completing everyday transactions (sending UPI money, checking a bank balance, booking a train ticket) make costly mistakes or give up because of **tiny fonts, icon-only buttons with no text labels, and text-heavy pop-ups that are hard to close.**

**Anchor case:** an auto driver with presbyopia repeatedly sends UPI money to the wrong contact because avatars do not scale and fonts are tiny.

**Related pain points (out of scope for v1, listed for future work):**
- Marketplace photo upload fails silently.
- Bus-pass renewal is locked behind a mandatory complex password.

## 2. Scope decision

| In scope (v1) | Out of scope (future work) |
|---|---|
| One flow: pay the right person on UPI | Balance check, train booking |
| Side-by-side comparison with a typical app | Photo upload, bus-pass renewal |
| Simulated weak near-vision for testing | Real payment, bank or NPCI integration |

**Why one flow:** one flow tested properly is stronger evidence than three flows built thinly.

## 3. Target user (working persona)

**Balwinder, 52, auto-rickshaw driver, Punjab.** Budget Android phone, used one-handed in sunlight between rides. Pays for fuel, tea and repairs by UPI daily. Has presbyopia and no reading glasses while driving.

> **Limitation:** this persona is built from the problem statement and general knowledge, not from interviews. Real driver interviews are the first next step.

## 4. Goals and non-goals

**Goals**
1. Reduce wrong-contact payments.
2. Make every screen readable without glasses.
3. Make risky actions deliberate.
4. Always let the user close a message in one tap.

**Non-goals**
- Moving real money.
- Replacing a bank's security checks.
- Claiming the results apply to all users.

## 5. Hypotheses (to be tested, not assumed)

| ID | Hypothesis | Status |
|---|---|---|
| H1 | Large faces with relationship tags and phone endings reduce wrong-contact picks. | Untested |
| H2 | Hold-to-pay prevents accidental sends, **or** it is harder for shaky hands than a big Tap button. | Compare in test |
| H3 | Reading the amount and name aloud helps users catch mistakes. | Untested |
| H4 | A short send delay with a big Cancel button saves mistaken payments. | Concept only |
| H5 | Larger text and no icon-only buttons shorten time on task. | Untested |

## 6. Solution overview

Saral is compared against a deliberately typical UPI-style screen set that has tiny fonts, tiny identical avatars, icon-only buttons, a text-heavy promo pop-up with a tiny close mark, and a single-tap Pay.

### Functional requirements

| ID | Requirement |
|---|---|
| FR1 | Contact list shows a large avatar (60px+), name (22px+ bold), relationship tag, last 3 digits of the phone number, and last amount paid. |
| FR2 | Two contacts share the name "Gurmeet Singh" (Brother and Tyre shop) to test disambiguation. |
| FR3 | Amount screen has a 64px+ keypad and shows the amount in digits and in words. |
| FR4 | Confirm screen shows a large avatar, name, tag, phone ending, amount in digits and words. |
| FR5 | "Listen to this" reads the payment details aloud (browser speech synthesis). |
| FR6 | Pay button style is switchable: **Hold to pay** (1 second, visible fill) or **Tap to pay**. |
| FR7 | After paying, an 8-second "sending soon" screen with a countdown and a large "Wrong? Cancel now" button. |
| FR8 | Text size slider from 100% to 160%, with layout that reflows. |
| FR9 | No icon-only buttons in Saral. Every control has a visible word. |
| FR10 | No pop-ups in Saral. Messages appear in-screen, never over the page. |
| FR11 | A blur slider simulates weak near-vision for anyone testing. |
| FR12 | Each attempt logs: design, contact paid, amount, seconds, taps, correct or wrong. |
| FR13 | A summary table compares both designs: tries, wrong payments, average seconds, average taps. |

### Non-functional requirements
- Works in a modern mobile or desktop browser, no backend, no login.
- Text uses relative units and respects the text size slider.
- Text and background contrast at least 7:1 in Saral.
- Tap targets at least 64px in Saral.
- Works in light and dark mode on the test page.

## 7. Design principles

1. **Readable first.** Big type, high contrast.
2. **Words beat icons.** Every action is named.
3. **Big, spaced targets.** Hard to hit the wrong thing.
4. **Slow down the risky step.** Confirm, then hold or tap, then a short delay.
5. **Say what is happening.** Nothing is silent.

## 8. Honest constraints

- **Real UPI payments are final.** The 8-second delay is a design concept. In production, the app would hold the payment briefly before sending it, and would need to be built into the payment app itself.
- The prototype simulates payments. No money moves.
- Speech output depends on the browser and device language support.
- Results come from a small convenience sample with simulated vision loss.

## 9. Test plan

**Task given to each tester:** "Pay Rs. 500 to Gurmeet who runs the tyre shop."

**Procedure**
1. Tester tries the **Typical** app, then **Saral**. Alternate which comes first between testers to reduce order effects.
2. Turn the blur slider up (for example 2 to 3) to simulate weak near-vision.
3. For Saral, test **Hold** and **Tap** with at least 2 testers each.
4. Do not coach. Observe where they hesitate.
5. Ask the follow-up questions below.

**Participants:** at least 5 people, ideally aged 40+ (family, neighbours, teachers), plus classmates.

**Metrics**

| Metric | Source |
|---|---|
| Wrong-contact rate | Results table |
| Time on task (seconds) | Results table |
| Taps | Results table |
| Hold vs Tap preference | Observation + question |
| Used Listen? Did it help? | Observation |
| Would they use it? | Question |

**Follow-up questions**
1. Where did you hesitate? What did you expect to happen?
2. Did you use the Listen button? Did you trust it?
3. Which was easier: holding or tapping to pay?
4. Was the text easy to read? (1 to 5)

## 10. Results template (fill in after testing)

| Design | Tries | Wrong | Avg seconds | Avg taps |
|---|---|---|---|---|
| Typical | | | | |
| Saral (Hold) | | | | |
| Saral (Tap) | | | | |

**Key observations:**
-
-
-

**Hypothesis outcomes:**

| ID | Supported / Not supported / Unclear | Evidence |
|---|---|---|
| H1 | | |
| H2 | | |
| H3 | | |
| H4 | | |
| H5 | | |

**One change we would make because of what we saw:**

## 11. Risks and limitations

| Risk | Mitigation |
|---|---|
| Testers are not real auto drivers | State this clearly. Use the blur simulation. Plan real interviews next. |
| Small sample | Report counts, not percentages. Avoid broad claims. |
| Learning effect between versions | Alternate which version is tried first. |
| Blur does not equal presbyopia exactly | Call it a proxy, not a replacement. |
| Delay concept not possible in real UPI today | Present as a design idea needing app and bank support. |

## 12. Next steps

1. Interview 3 to 5 real drivers or shopkeepers. Rewrite the persona from what they say.
2. Test with real vision-impaired users, with consent.
3. Add Punjabi and Hindi screens and voice.
4. Extend to balance check, then train booking.
5. Add the photo-upload and bus-pass flows (honest progress states, simple PIN sign-in).
6. Explore a "Is this the right person?" check built into contact saving.

## 13. Presentation outline (5 minutes)

1. **Empathise:** the auto driver story and a screenshot of a tiny-font UPI screen.
2. **Define:** problem statement and the single flow chosen.
3. **Ideate:** the five hypotheses.
4. **Prototype:** live demo, Typical with blur, then Saral with blur.
5. **Test:** results table, what surprised you, what you would change.
6. **Limits and next steps:** be honest about proxy testing and the delay concept.
