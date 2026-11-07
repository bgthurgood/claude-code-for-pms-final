# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Answer only the question the student asks, from the sources they
  name. Don't investigate beyond it or offer a theory about what
  Release 4.2 changed unless they ask for one.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

I'm the new PM for **Rook Dispatch**. I took over from Priya Raghunathan, who left 21 Aug 2026 with no overlap.
Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap, Product briefs) and
`00-rook/company/notes/handoff-from-priya.docx`. Fictional scenario.

### The company and products
- Rook Industries sells coordination and provisioning software to independent masked **responders** and
  the **handlers** and **quartermasters** who support them. Rook employs no responders. Billing is a
  subscription per active responder.
- **Rook Dispatch** (mine, and the flagship product): coordinates responders. It tracks who is available
  and nearby, which responder gets pinged for a callout, and whether they take it. Handlers use the
  desktop console. Responders use their phones.
- **Rook Supply**: gear provisioning. Covers requisitions, maintenance and field failure reports. Its
  users are handlers and quartermasters.
- Releases ship monthly on a train, numbered 4.x. Support has three tiers. Tickets filed during an
  active callout skip the queue.
- **Hard rule:** Rook never stores a responder's legal identity, only capability tags, availability and
  callout history. Read Security Policy 4.1 before designing anything that touches responder records.
  Never try to work out who a responder is.

### People (Dispatch team, directory as of 2 Sep 2026)
Wiki comments name people by **role**. Mapping:

| Role in comments | Person | Base | Notes |
| --- | --- | --- | --- |
| Director of Product | Helen Achebe | Site Aleph | My director. Owns roadmap and commitments |
| Engineering manager | Marcus Oyelaran | Site Aleph | Runs Dispatch eng. Priya: "start here" |
| Staff engineer | Wen Li (she) | Berlin | Built routing (who gets pinged). The logic lives in her head; no doc exists |
| Product designer | Sofia Marino | Site Aleph | Console and phone app. Ran the September interviews |
| Support lead | Nadia Hoffmann | Berlin | Owns tickets and hears handler pain first. Priya suggested a standing 15 min |
| Data analyst | Ravi Menon | Singapore | Owns the numbers. Weekly report on how often responders take their pings |
| (former PM) | Priya Raghunathan | — | Left 21 Aug. Marcus has her number |

Handlers named in the wiki: Aunt Dot (Vesper), Mr. Ambrose (Captain Vantage), Halloran (Sgt. Bulwark;
also a frequent Supply voice), Kip (Meteor Mite, The Gale).

### Vocabulary
- **Callout**: a request to attend an incident. It is the unit of work in Dispatch.
  **Ping**: one callout offered to one responder.
- Each ping ends one of three ways: **Taken** (yes), **Turned down** (no), or **Missed** (no answer
  before the ping wait ran out). Turned down and missed are recorded separately, but both move the
  ping to the next responder.
- **Ping wait** (also "ping timeout"): how long a ping stays on the phone. One value for everyone, set
  per release.
- **Acceptance rate**: the share of pings taken. It is the headline metric.
  **Time-to-accept**: median seconds from ping sent to ping taken.
- **Coverage gap**: no available responder had the required tags, so nobody *could* go. This is not
  the same as low acceptance.
- **Routing priority**: the score that ranks responders for a callout. Inputs are proximity
  (travel-time estimate), availability, capability match and recent acceptance history. Turning down or
  missing a ping lowers the acceptance component.
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic,
  crowd-management, de-escalation.
- **Responder Availability Record**: written by Dispatch and read by Supply for maintenance scheduling.
- **Mutual aid** = "Shared cover between responders": responders covering for each other. Not
  supported today.
- Supply terms: **requisition**, **field failure report**, **service interval**, **quartermaster**.

### Releases
- **4.0** (7 Apr): new console navigation, responder profile redesign, audit log for routing overrides.
- **4.1** (16 Jun): proximity uses a travel-time estimate, bulk callout, better phone push delivery.
- **4.2** (12 Aug): proximity weighted up relative to recent acceptance history in who gets pinged.
  Ping wait cut from 90s to 60s. Console filters persist. Three defect fixes.

### Where things stand on 4.2 (from the 4.2 page comments and the handoff)
- The release went out clean (Marcus).
- 14 Aug, Marcus asked: should the routing change apply to responders who have been turning jobs down,
  or only to everyone else? The config doesn't distinguish, and he wanted to know whether that was a
  decision or a side effect. Wen was away until the 24th. **No answer is recorded.**
- 18 Aug, Nadia reported callout tickets at roughly 3x normal. By 26 Aug the split was about two thirds
  "phone never goes off" and one third "gone before I could answer." She ties the second theme to the
  60s wait. She can't explain the first. A handler emailed her directly, which is unusual.
- Nadia asked for the trend on how often responders answer. Marcus offered "rough, not the real weekly
  numbers." Ravi doesn't appear in the thread.
- Priya (19 Aug and in the handoff) says the drop is mostly seasonal ("August is always soft") and
  expected a September recovery. She advised against reverting 4.2. The wiki has no data backing the
  seasonal claim yet.
- 28 Aug, Marcus planned to regroup on 4.2 once the new PM had had a week to look. Nadia will bring the
  ticket breakdown. Wen is back.

### Roadmap and open loose ends
The Q3 roadmap was last reviewed 30 Jun. Every item still lists Priya as owner.

| Item | Target | Status | Note |
| --- | --- | --- | --- |
| Change to who gets pinged | 4.2 | Committed | Shipped |
| Ping timeout tuning | 4.2 | Committed | Shipped as the 90→60s cut |
| Availability Confidence (confidence score on stated availability) | 4.2 | Committed | **Not in the 4.2 notes**, so it was apparently squeezed out |
| Requisition approval chains (Supply) | 4.3 | Committed | Brief says Supply team owns it. Brief scope has grown well past "second approval over $2,000" |
| Handler phone app | Q4 | Exploring | Brief (8 Sep) names Sofia as owner, not staffed |
| Shared cover between responders | Q4 | Exploring | = mutual aid |

- Priya's to-dos for me:
  - Agree with Helen which items squeezed out of 4.2 are still Q3 commitments. That conversation
    never happened.
  - Write the missing description of how routing decides who gets pinged.
  - Treat filter-persistence tickets as noise.
- Brief mismatches:
  - The Bulk Callout brief (Jan) says "nobody's picked it up yet," but bulk callout shipped in 4.1.
  - The Routing Override Audit Log brief reads as not-started, but the audit log shipped in 4.0.
  - Treat briefs as possibly stale.
- Priya's own caveat: she "made calls faster than I checked them." The weak spots are likely in parts
  of the product nobody has looked at closely.

- Session 1 findings: rook-database has tables callouts, pings, responders (name, handler, area), handlers
  and support_tickets. Tickets have no priority or category field, and the data ends 6–7 Sep.
- 107 tickets since 12 Aug. Around 30 are "few or no pings," from just 4 responders (Farlight, The Undertow,
  Corporal Ashgrove, Halfmoon). Around 15 are "gone before I could answer," spread across about 12
  responders. Around 12 are filter persistence problems (silent resets, shared computers).
- September interviews (Sofia) back both themes. Vesper and Meteor Mite were also quiet, but their
  handlers filed no tickets, so ticket counts undercount the problem.
- 16 responders across 15 areas (Kip's two share Eastgate). Area is a responder's home patch: pings
  route citywide, and turned-down or missed pings mostly go to responders in other areas.
- Leaning: prioritize the "few or no pings" group, and raise the 60s ping wait with Marcus and Helen in
  parallel. Open next step: compare pings per responder before and after 12 Aug in the pings table.

- Session 2 findings: all 147 tickets (29 Jun–7 Sep) sorted into 11 groups. Every "few or no pings" (30) and
  "gone before answering" (15) ticket is on or after 12 Aug. Supply is the 2nd-largest group (26). Many
  tickets reuse identical wording, so counts overstate distinct voices. Only Mr. Ambrose filed a ticket of the 4 interviewees.
- Interviews vs tickets: "handler can't see a live/missed callout" is 3 of 4 interviews but almost absent from
  tickets. Overload (The Gale) appears in no ticket. Account/sign-in and layout issues fill tickets but no
  interview. Halloran says maintenance scheduling improved; 4 tickets contradict him.
- Working hypothesis (unverified): a feedback loop. The 60s wait causes misses, misses lower the routing
  acceptance score, and responders get fewer pings and can't climb back. Farlight and The Undertow each missed their first ping in days.
- Drafted (in chat only, not saved as files): weighted 4.3 backlog with P0 = both callout fixes, a revised 8-week
  4.3 roadmap, and a sprint initiative/epic/story with a 3-day spike (Ravi + Wen) to confirm the loop in the pings table.
- Still open: 4.3 date (ask Marcus), Availability Confidence in/out (Helen), Marcus's 14 Aug routing
  question, a fresh ticket export (Nadia), and whether to recompute scores retroactively.

- **Data rule (from student):** Before analyzing, check the structure of every table I'll use: describe it, then check its date range, row counts and column values. Report only numbers from queries actually run on the data provided. If a question can't be answered from the tables, say so plainly instead of guessing. If later checks contradict an earlier claim, correct the claim instead of adding caveats. Report any failed tool call, even if a retry works.
- Session 3 findings (pings, 1,696 rows, 29 Jun–6 Sep, split at 12 Aug): missed pings 2.3% → 18.0%, acceptance 76.6% → 64.0%;
  the rise in misses accounts for the whole drop and hit all 16 responders. Every callout got at least one ping (no coverage gaps);
  callouts pinged but never taken 5.5% → 11.1%.
- Hardest hit (pings/wk down ~70%): Farlight, The Undertow, Vesper, Meteor Mite. All four were in the busier half before 4.2 with
  normal response rates. Ashgrove and Halfmoon fell only ~20%; the other 10 got more pings. The four's share of first pings fell
  28.1% → 9.1%; Vesper went from first ping on 85% of Old Town callouts to 5 of 38 (0 of 4 in 12–16 Aug).
- Tickets vs pings: every ping count quoted in a ticket matches the data, but ticket volume doesn't track severity. Aunt Dot, Kip
  and Halloran have never filed a ticket; Mr. Ambrose filed one. Some ticket timestamps match ping times to the second, so they
  may be generated, not recorded (ask Nadia).
- Routing scores are not in rook-database (ask Wen or Ravi). Open: was Vesper's early drop caused by her misses or by the 4.2
  routing change itself?

- Session 4 findings (code in 00-rook/code/dispatch-routing/): only config.py changed in 4.2 (wait 90→60s, weights distance 45→60%,
  yes-score 40→25%, skills 15%). The code never removes anyone from the list; it only orders them. A miss costs the same −0.12 as a
  "no", a yes adds +0.08, and nothing else ever adds points back (no decay or reset; 2019 TODO left as-is). The scores sit in memory only.
- The yes-score (stored, 0–1, unweighted ±) is different from the overall ranking score (recomputed per callout; the 25% applies only there).
  Replaying the code's rules over the pings shows the four were at 0.84–1.00 at release (same as others), then fell to 0.00 by early Sep.
  So Marcus's "turn-downers" question doesn't explain the drop. Misses do, plus no way back.
- Time-of-day hypothesis ruled out: no night pings for the four in the first 48h; they miss 47–77% in every time band after 4.2.
  Fitted typical answer time is ≈61–64s for each of the four vs ≈38s for others, so 60s cuts right through them.
- Simulator (in chat only): from today's zero scores, 90s alone doesn't recover the four; 90s plus a reset or recovery does. Model is
  calibrated to replay but falls slower than reality. Old weights + 60s would likely have been worse (a miss is ≈4.8 vs 2.3 min of travel).
- Proposed scoring idea: charge per second a ping is held (fast no < slow no < miss), no penalty for marking unavailable, rolling window.
  Open: Vesper's day-one drop (travel-time estimates, ask Wen), stored scores, actual answer times (Ravi), whether scores persist across restarts.
- The responder I picked: **Meteor Mite** (Kip, Eastgate).
- Session 5 (Helen's request in 05-super-speed/director-request.txt: a rough one-pager from the user's point of view, plus something clickable).
  Built brief.md (one page; full version in brief-meteor-mite-detail.md), prototype.html (clickable phone + handler console) and
  whathappened.html (replays every real ping from 12 Aug to 6 Sep, with a switch to re-score them under the brief's rules).
- Brief's answer: keep 60s. Answer from the lock screen. "Not now" is free. Misses cost less. Low scores ease back toward neutral 0.5 (answers Wen's 2019 note
  in history.py, which weighs both sides). One-time reset with an "on our side" message. Status line and same-day warning on handler cards.
- Biggest gainers after 4.2: The Gale 13.0→18.6/wk and Sgt. Falkirk 10.0→14.0/wk. The Gale missed as many pings as Mite (8 each) but got 69 vs 14,
  so it recovered. Re-scoring the same pings under the brief's placeholder rules: Mite and Vesper end at 0.60, Farlight 0.50, The Undertow 0.45 (all 0.00 under 4.2).
- Open: Not now is free in the one-pager but costs a little in the detail file (settle it). The brief says Gale takes "Eastgate" callouts, but routing is citywide (fix).
  Today's phone flow is assumed, not checked with Sofia. The new-rule values are placeholders for Wen. Helen decides the reset's scope and the "on our side" wording.
