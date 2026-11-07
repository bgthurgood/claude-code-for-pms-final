# Acceptance criteria: When a responder goes quiet

**Brief:** `05-super-speed/brief.md` (companion: `brief-meteor-mite-detail.md`) · **Build:** `05-super-speed/prototype.html`, treated as staging · **Drafted:** 7 Nov 2026 · **Status:** Draft, awaiting approval

## Summary
| | Must | Should | Could | Total |
| --- | --- | --- | --- | --- |
| UI-testable | 18 | 9 | 3 | 30 |
| Not testable here | — | — | — | 7 |

## Criteria
"Brief mode" = the build's **With this brief** setting. "Mite" = Meteor Mite, the default responder. Brief line numbers refer to `brief.md`.

| ID | Pri | Area | Title | Given | When | Then | Source |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AC-01 | Must | Phone | Answer from the lock screen | Brief mode, phone idle | A ping is sent to Mite | The lock screen shows **Take** and **Not now** on the notification, without unlocking | L18 |
| AC-02 | Must | Phone | Countdown shown | Brief mode | A ping arrives | A countdown is visible, starts at 60 and counts down | L18, L32 |
| AC-03 | Must | Phone | Take works | A ping is on the lock screen | Mite taps Take | The phone confirms the callout is taken, and the score does not go down | L18 |
| AC-04 | Must | Phone | Not now is free | A ping is on the lock screen | Mite taps Not now | Mite is told it doesn't count against them, and the score is unchanged | L19 |
| AC-05 | Must | Phone | Running out explained | A ping is on the lock screen | The countdown reaches 0 | The phone says "This one moved on to the next responder." | L20 |
| AC-06 | Must | Rules | A miss costs less than today | The same starting score in both modes | One ping runs out in Today mode and one in Brief mode | The Brief-mode drop is smaller than the Today drop (0.12) | L19 |
| AC-07 | Must | Phone | No score or rank shown | Brief mode, any phone state | Any action is taken | The phone never shows a score, rank or position number | L20 |
| AC-08 | Must | Phone | No blame | Brief mode | A ping runs out, once or 3 times in a row | No phone message blames Mite (no "you missed", "failed" or similar) | L20 |
| AC-09 | Must | Phone + Console | Eases back after a bad stretch | Brief mode, Mite below neutral | "A few days pass" | The score moves toward 0.50, the phone says Mite is back in (or returning to) the normal rotation, and the card says "Recovering" | L21 |
| AC-10 | Must | Rules | Eases back only to neutral | Brief mode, Mite below neutral | "A few days pass" several times | The score never rises above 0.50 from easing alone | L29 |
| AC-11 | Should | Rules | New misses still count | Brief mode, Mite eased back to near neutral | Mite misses 3 in a row | The score drops again, and the card goes back to "Quieter than usual" | L29 |
| AC-12 | Must | Phone + Console | Day-one fresh start | Brief mode, Mite at 0.00 (6 Sep) | "Day one: fresh start" | The score is 0.50, the phone shows the "change on our side… reset your standing" message, and the card shows the fresh start | L22 |
| AC-13 | Should | Rules | Reset only for those pushed down | Brief mode, The Gale or Sgt. Falkirk selected | "Day one: fresh start" | That responder's score doesn't change and they get no reset message | L22 |
| AC-14 | Should | Rules | Reset is one-time | Brief mode, fresh start already applied | Fresh start is pressed again | The score doesn't go above 0.50 and no duplicate effect builds up | L22 |
| AC-15 | Must | Console | Every card explains itself | Brief mode | Any responder is selected | Each card shows a plain-words status line and no raw score | L23 |
| AC-16 | Must | Console | Quiet card gives the reason | Brief mode, Mite at 0.50 | Mite misses 3 in a row | Mite's card reads "Quieter than usual: 3 missed pings moved Mite down the order" (count matches) | L23 |
| AC-17 | Must | Console | Same-day warning | Brief mode | Mite misses 3 in a row | Kip's card shows a warning about 3 missed pings straight away | L23 |
| AC-18 | Could | Console | Warning can be acknowledged | The warning is showing | Kip clicks to acknowledge | The warning clears and comes back only after new misses | L23 (implied) |
| AC-19 | Should | Console | The Gale's card evens out | Brief mode, Mite selected | "A few days pass" or fresh start | The Gale's card moves from "Busier than usual" toward "Evening out", marked as expected rather than proven | L24 |
| AC-20 | Must | Cross-view | Phone actions update the console | Brief mode | Mite takes a ping | Mite's card updates straight away (shown as on a callout) | L23 |
| AC-21 | Should | Today mode | Today reproduces 4.2 | Today mode | Ping, Not now, miss, days pass | No lock-screen buttons; a no and a miss both cost 0.12; nothing eases back; Mite and Kip are told nothing | L18–23 "Today" column |
| AC-22 | Should | Rules | Wait stays 60s | Either mode | A ping is sent | The countdown starts at 60, not 90 | L32 |
| AC-23 | Must | Policy | No legal identity | Every responder, every mode | Any screen | Only cover names, handler names and areas appear; no real names or personal details for responders | L49 |
| AC-24 | Must | Phone | Repeated Not now stays free | Brief mode | Not now is tapped repeatedly | The score never drops | L19 |
| AC-25 | Should | Access | Keyboard and labels | Any mode | Using Tab and Enter only | Take, Not now, the Today mode notification and all controls can be reached and used, and each has a readable name | General |
| AC-26 | Should | Layout | Phone width | 375px-wide viewport | The page is loaded and used | No sideways scrolling, and the phone and console are both usable | General |
| AC-27 | Should | Quality | No console errors | Any | Through all flows | The browser console shows no errors | General |
| AC-28 | Could | Coverage | All responders work | Brief and Today modes | Each of the 6 responders is selected | The page renders with the right handler and area, and switching resets the state | General |
| AC-29 | Could | Timer | Real-time option | Brief mode, "Real-time 60s" ticked | A ping is sent | The countdown runs in real seconds | General |
| AC-30 | Must | Phone | Can't answer after it runs out | A ping has run out | (no action possible) | No Take or Not now button stays on screen | L20 |

## Not testable here
| ID | Requirement | Why not | Who can verify |
| --- | --- | --- | --- |
| NT-1 | The 60s starts when the ping reaches the phone | Delivery timing isn't in a prototype | Wen / Marcus |
| NT-2 | The right pace for easing back | Values are placeholders | Wen proposes, Ravi checks against the ping history |
| NT-3 | Mite back to ~11 pings a week, no week-long silences | Needs live data after release | Ravi |
| NT-4 | Fewer "phone never goes off" tickets | Needs live tickets | Nadia |
| NT-5 | The Gale's load actually evens out | Needs live data | Ravi |
| NT-6 | Who the reset covers, and the message wording | Helen's decision | Helen |
| NT-7 | Real OS lock-screen actions and push delivery | Needs a phone build | Sofia / engineering |

## Too vague to test as written
| Brief says | Suggested testable version |
| --- | --- |
| "Fewer 'phone never goes off' tickets" (L40) | "These tickets fall by X% within 4 weeks of release, against Aug–Sep" |
| "Kip's two cards look more alike" (L39) | "Mite and The Gale are within N pings a week of each other by week 4" |
| "The score eases back toward neutral" (L21) | "A responder at 0.00 with no new misses reaches 0.50 within N days" (N from Wen) |

## Open questions (with suggested default)
1. **The "Behind the scenes" score panel.** It's labelled "for Helen, not shown to Mite or Kip." **Default:** treat it as a demo aid, so it doesn't count against AC-07 and AC-15.
2. **"Not now".** `brief.md` says it's free, but the detail file says a fast no costs a little. **Default:** test against `brief.md` (free) and log the contradiction as a finding.
3. **Today mode in scope?** **Default:** yes, as Should (AC-21). The comparison is part of what Helen asked for.
