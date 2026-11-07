# When a responder goes quiet

**For:** Helen Achebe · **From:** Dispatch PM · **Status:** rough draft, for discussion · **Data:** `pings` table, 29 Jun – 6 Sep 2026 · Fictional course scenario

**In short:** Don't only change a number. Keep the 60s ping wait, make missing a ping something you can recover from, and make that visible: Meteor Mite should see what happened and get a fresh start, and Kip should see why Mite's card went quiet.

## What happened to Meteor Mite (Kip's responder, Eastgate)
- **Before 4.2:** about 11 pings a week, 2 of 70 missed. **After:** about 4 a week, 8 of 14 missed, then no pings at all on 22–27 Aug and 29 Aug–5 Sep.
- **The Gale** (Kip's other responder, same area) went from about 13 to about 19 pings a week.
- Mite didn't start saying no. Mite answers a few seconds too slowly for 60s: our estimate is about 61–64s, modelled rather than measured. Each miss costs the same as a no, and the code never adds points back except for a taken ping. So once Mite was down, Mite stayed down.
- Kip: "one card's dead quiet and the other's on fire." Mite "thinks Mite's been forgotten."

**Why not just change the number:** Mite's score is already at zero. A smaller penalty, or going back to 90s, doesn't bring Mite back (that's what the Module 4 simulation showed), and it explains nothing to Kip or Mite. It would be fine as a stopgap, but not on its own.

## What changes, for the people it happens to
| Moment | Today | With this brief |
| --- | --- | --- |
| **A ping arrives** | Mite has to get into the app to answer, and the ping is "gone before I could answer."\* | **Take** and **Not now** on the lock screen, with a countdown. The 60s starts when the ping reaches the phone (check whether it already does). |
| **Mite can't go** | Saying no and letting it run out cost the same. | **Not now is free.** Only running out costs anything, and less than before. |
| **The ping runs out** | It disappears with no reason given. | "This one moved on to the next responder." No score or rank is shown, and nothing blames Mite. |
| **After a bad stretch** | Mite's score sits at zero indefinitely. | The score **eases back toward neutral** and the pings return. "You're back in the normal rotation." |
| **Day one** | — | **A fresh start:** a one-time reset to neutral for the responders 4.2 pushed down, with the message: "That was a change on our side, and we've reset your standing." |
| **Kip's console** | Two cards, no explanation. Kip says "hang in there." | Each card has a status line, e.g. "Quieter than usual: 3 missed pings moved Mite down the order. Recovering." It also warns Kip the same day after a run of misses. Kip has never filed a ticket, so the card may be the only way he finds out. |
| **The Gale** | "Exhausted." | Expected (not proven): some Eastgate callouts go back to Mite, and The Gale gets some relief. |

\*Phone steps today not yet checked with Sofia.

## Wen's 2019 note, answered
Wen asked whether the score should ease back on its own. **For:** a bad month shouldn't follow you into spring. **Against:** if someone has stopped taking work, that should stick. **Our answer is yes, ease back, but only to neutral.** That gets a responder pinged again, so the system learns what they're doing *now*. If they still don't take work, new misses push them back down. That way both of her points hold. Wen proposes how fast scores ease back, Ravi tests it against the ping history, and you sign it off. I'll write the routing description Priya never got to, so this rule is recorded and doesn't end up as another TODO.

## The honest trade-off
- **What we keep:** 60s, and 4.2's higher weight on proximity. Reverting "trades one angry group of responders for another" (Priya).
- **What the faster ping does:** it should save Mite a few seconds, but some pings will still run out. The rest of this brief makes sure a miss no longer leads to silence. It doesn't make misses go away.
- **Optional, your call:** a once-per-ping "I'm looking" tap, adding about 15s. It bends the 60s rule.

## How we'll know
- Mite is back to about 11 pings a week, with misses near the pre-4.2 level.
- No week-long silences for any available responder.
- Kip's two cards look more alike, and The Gale isn't left short of work.
- Fewer "phone never goes off" tickets.

## Decisions and open questions
- **Helen:** Should the reset cover the four quiet responders, or everyone whose score fell after 12 Aug? Is the "I'm looking" tap acceptable? Are you OK with a message that says the cause was on our side?
- **Wen:** How fast should scores ease back? Do scores survive a restart? When does the 60s clock start?
- **Ravi:** Real answer times. How much is lost to delivery, and how much to the responder?
- **Sofia:** The lock-screen ping and the card wording. The clickable prototype comes next.
- **Nadia:** Did quiet responders' handlers write in at all?

*Cover names and routing status only. Nothing records or infers a legal identity (Security Policy 4.1). Fuller reasoning and sources are in `brief-meteor-mite-detail.md`.*
