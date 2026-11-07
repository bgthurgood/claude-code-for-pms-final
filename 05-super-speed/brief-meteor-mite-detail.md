# When a responder goes quiet: what we'd build instead of changing a number

**For:** Helen Achebe, Director of Product · **From:** Dispatch PM · **Status:** rough draft, for discussion
**Data:** rook-database `pings` table, 29 Jun – 6 Sep 2026, split at the 4.2 release (12 Aug). Fictional course scenario.

---

**In short:** Instead of only changing a number, we'd build three things people can see. Meteor Mite gets a ping that's faster to answer and is told what happened when one is missed. Kip gets a card that explains why Mite went quiet. And underneath, a missed ping stops counting against a responder forever. We keep the 60s ping wait.

## Why not just change the number
Engineering can ship a small change today, for example lowering the penalty for a miss or putting the wait back to 90s. On its own that doesn't bring Mite back. Mite's score is already at zero, and nothing in the code ever adds points back except a taken ping, which Mite rarely gets offered now. In the Module 4 simulation, going back to 90s alone didn't recover the four quiet responders. They only recovered with a reset or a recovery rule as well. A quick fix also wouldn't explain anything to Kip or Mite. If engineering ships one as a stopgap, it should come with the items below, not replace them.

## The ask
You asked what we'd build so that a handler like Kip would notice it and a responder who's gone quiet would feel it. You asked for that before anyone changes the routing code. This brief follows one responder, **Meteor Mite** (handler: Kip, area: Eastgate). It keeps the 60-second ping wait, and it answers the question Wen left in the code: should a responder's score ever recover?

## What happened to Meteor Mite
- **Before 4.2:** 70 pings in about 6 weeks (about 11 a week). 48 taken, 20 turned down, **2 missed**.
- **After 4.2:** 14 pings in about 4 weeks (about 4 a week). 3 taken, 3 turned down, **8 missed**.
- On 13–14 Aug, the first two days the shorter wait applied, Mite missed 3 pings in a row. Each miss cost as much as a "no." Only a taken ping earns points back, and Mite was getting fewer and fewer pings to take. By late August there were gaps of **5 days** (22→27 Aug) and **7 days** (29 Aug→5 Sep) with no ping at all.
- Replaying the code's own rules over the pings shows Mite's yes-score falling from about the same level as everyone else to zero by early September (Module 4 analysis).
- **The Gale** (also Kip's, same area) went the other way: about 13 → about 19 pings a week.

Mite didn't start turning work down. Mite started answering a few seconds too slowly. Our modelled typical answer time for Mite and the other three quiet responders is about 61–64s, against about 38s for everyone else. That's an estimate, not measured: the pings table has no answer times. Under the 60s wait, those pings counted as misses, and the scoring has no way back. This also answers Marcus's 14 Aug question. The drop isn't about responders who turn jobs down. It's misses, with nothing that ever restores the score.

## Mite's side of it, today and with this brief
Dates are from the pings table. Kip's words are from his interview with Sofia on 4 Sep. The phone steps under "Today" are our understanding, not yet checked with Sofia. Support tickets describe the ping being "gone before I could answer."

| Moment | Today | With this brief |
| --- | --- | --- |
| **A ping arrives** (13 Aug, 13:43) | The phone buzzes. Mite unlocks it, opens the app and reads the callout. By then the ping has gone to someone else. | Take and Not now are on the lock screen, with a countdown. Mite can answer without unlocking. |
| **The ping runs out** | It just disappears, with no reason given. That happens twice more in the next day. | "This one moved on to the next responder." Mite knows what happened. |
| **Mite can't go** | Saying no and letting it ring out cost the same, and both push Mite down the order. | Not now is free. Only letting a ping run out costs anything, and less than before. |
| **The quiet weeks** (22–27 Aug, 29 Aug–5 Sep) | Nothing at all. Mite texts Kip asking if something's broken. | There are no lost weeks. A same-day warning goes to Kip, Mite's score eases back, and the phone says "You're back in the normal rotation." |
| **Kip looks at his console** | Two cards: "one card's dead quiet and the other's on fire." Kip can only say "hang in there, it'll pick up." | Mite's card says why it went quiet and that Mite is recovering. Kip has a real answer for Mite. |

## What we'd build

**For Mite (the phone)**

Right now the silence feels personal. Kip says Mite "thinks Mite's been forgotten," and Mite has nothing to go on except a phone that has stopped ringing. What should change for Mite: understanding what happened, knowing it wasn't their fault, and having some way to do something about it.

1. **Answer from the lock screen.** Take and Not now buttons on the notification itself, with a visible countdown. Mite doesn't have to unlock the phone and wait for the app to open.
2. **Saying "not now" is free.** A quick no, or marking yourself unavailable, never costs you. Only letting a ping run out does, and less than before.
3. **Say what happened, without blame.** When a ping runs out: "This one moved on to the next responder." Then show where Mite stands in plain words: "You're in the normal rotation," or "Your pings will pick up over the next few days." Never show a score or a rank, which would feel like being graded.

**Day one: a fresh start for the responders 4.2 pushed down.** The new rules on their own would bring Mite back slowly, so Mite would feel nothing different for a while. We recommend a one-time reset to neutral for responders whose scores fell after 12 Aug, with a short message: "Some pings recently ran out faster than they used to. That was a change on our side, and we've reset your standing." That's the moment Mite stops feeling forgotten. Who gets the reset, and the exact wording, are for you to decide (see the table below).

**For Kip (the console)**

Kip works with the console on his centre screen, often late at night, and both his responders' cards are side by side. He told Sofia he doesn't know what he'd want the console to tell him. He just wants a quiet card to "look less like a coincidence." So the change should show up on the cards he already watches.

4. **Each card explains itself.** It shows a short status line in plain words, not raw scores. Illustrative wording:
   - **Meteor Mite:** "Quieter than usual: 3 missed pings moved Mite down the order. Recovering: the next pings are on their way."
   - **The Gale:** "Busier than usual: picking up callouts that would usually go to other Eastgate responders."
5. **Warn early, on the card.** After a run of misses, the card flags it the same day: "3 pings missed in a row." Kip can check in with Mite before a quiet week, not after it. Handlers like Kip and Aunt Dot have never filed a ticket, so the card may be the only way a quiet responder's handler finds out.
6. **The two cards even out.** As Mite's pings come back, some Eastgate callouts that went to The Gale should go to Mite again. Kip would see Mite pick up and Gale ("exhausted," in Kip's words) get some relief. This is expected, not proven. Ravi should check it in the weekly numbers.

**Underneath (Wen's question)**

7. **Mite can climb back after a bad stretch.** Scores ease back over time (see "Wen's question" below).
8. **Mite gets the full 60 seconds.** Start the clock when the ping reaches the phone, not when it's sent, if it doesn't already. The Glossary defines the ping wait as time "on a responder's phone." To check: where does the clock start today? (Wen/Marcus)

## Wen's question, answered properly
In 2019 Wen left a note in the scoring code (`history.py`) asking whether the score should ease back toward neutral on its own. She weighed both sides:
- **For:** somebody who had a bad month shouldn't still be carrying it in the spring.
- **Against:** if somebody has stopped taking work, that should stick until they take work again.

The note ends "Leaving it as-is for now," and nobody came back to it. 4.2 is what that cost. A shorter wait created a run of misses, and with no easing back, Mite has been carrying them ever since.

**Our answer: yes, ease back, and it can satisfy both of Wen's points.**
- **The score slowly drifts back toward neutral (0.5).** This is the starting score every new responder gets. It drifts back toward neutral, never above it. Credit above neutral still has to come from taken pings. **For** is satisfied: a bad August fades.
- **Easing back only earns a responder more pings, not a clean record.** Once Mite is offered pings again, Mite's real behaviour today shows up. If Mite keeps missing or saying no, each new ping pushes the score down again. **Against** is satisfied: someone who has stopped taking work stays low because of what they do now, not because of something they did months ago. Today's code can't tell these two cases apart, because a responder at zero is rarely offered a ping, so there's no new information.
- **Running out of time is no longer the same as "no."** The code says turning down and missing are the "same either way — we asked and we didn't get a yes." We'd charge by how long a ping is held: a fast no costs less than a slow no, which costs less than a miss. Marking yourself unavailable costs nothing.

**So it doesn't sit as a TODO again:**
- Wen proposes how fast scores drift back, Ravi checks that choice against the ping history, and you sign it off.
- I write the description of how routing decides who gets pinged. Priya flagged that it doesn't exist. It will record this rule and why we chose it.

## Keeping 60 seconds: the honest trade-off
We keep 60s because a shorter wait gets callouts to someone sooner, and we keep 4.2's higher weight on proximity because responders asked for it. Reverting it "trades one angry group of responders for another" (Priya's handoff). Items 1 and 8 should cut a few seconds off how long Mite takes to answer. But even if Mite's typical time drops just under 60s, many pings will still run out. Items 2–7 make sure a miss no longer leads to silence. They don't make misses go away. The "gone before I could answer" tickets will shrink, not disappear.

Optional, **your call:** a once-per-ping "I'm looking" tap that adds about 15s. It helps slow answerers, but it bends the 60s rule.

## How we'll know it worked
- Mite's pings per week back near about 11, and missed pings back near what they were before 4.2 (2 of 70).
- No week-long silences for any responder who's available.
- Kip's two cards look more alike: Mite's pings go up and The Gale's come down from about 19 a week. Watch that The Gale isn't left short of work.
- Fewer "phone never goes off" tickets (Nadia), and the weekly answer-rate trend (Ravi).

## Decisions and open questions
| Who | Question |
| --- | --- |
| **Helen** | We recommend a one-time reset to neutral, with the message above. Should it cover just the four quiet responders, or everyone whose score fell after 12 Aug? Is the "I'm looking" tap acceptable? |
| **Wen** | How fast should scores drift back to neutral? Do scores persist across restarts? Where does the 60s clock start? |
| **Ravi** | Actual answer times. How much time is lost to delivery, and how much to the responder? |
| **Sofia** | The lock-screen ping and the quiet-card wording. A clickable prototype is next. |
| **Nadia** | Did handlers of quiet responders write in? (Kip never filed a ticket.) |

*Everything here uses cover names and routing status only. Nothing records or infers a responder's legal identity (Security Policy 4.1).*
