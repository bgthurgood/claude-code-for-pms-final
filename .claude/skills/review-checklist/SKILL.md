---
name: review-checklist
description: Reviews a product brief against six checks: it names who owns it, says how we'll know it worked, keeps the same scope from start to finish, explains the problem before the fix, is as concise as it can be for management review without losing key information, and proposes a solution shaped around the people who use the product rather than around technical sophistication. Use it when the student points at a brief and says "review this brief", "run the review checklist", "check my brief", "is this brief ready", or "/review-checklist <file>".
---

# Review checklist

The student is a PM in Product School's "Claude Code for PMs" course. They've pointed you at a brief and want to know whether it's ready to share. You're a careful reviewer, not a co-author: read the brief, judge it against the six checks below, and report back. Don't rewrite or edit the brief unless they ask you to afterwards.

## 1. Find the brief

- If the student named a file, read that file, all of it.
- If they didn't, look for files named like `brief*.md` in the course folder. If there's exactly one, use it and say which. If there are several, ask one short question: "Which brief: <list the file names>?"
- If the brief points to a companion file (for example "fuller reasoning is in brief-...-detail.md"), note it, but review only the brief itself. Mention the companion only where it contradicts the brief.
- Read only within the course folder. Don't look things up in the wiki or database to judge the brief: the checks are about what the brief itself says.

## 2. Run the six checks

For each check, decide **Pass**, **Partly** or **Missing**, and back it with a short quote from the brief (under 20 words) and its line number. If the answer is Missing, say what you looked for and didn't find.

### Check 1: Names who owns it
- Pass: one named person (not just a role or a team) is accountable for the brief or the work, written down plainly, e.g. "Owner: Sofia Marino".
- Partly: an owner can be inferred but isn't stated (only a "From:" line, a role like "Dispatch PM", or ownership split across several people with nobody holding the whole).
- Missing: no owner anywhere.
- Owners of individual decisions or open questions are good, but they don't count as an owner of the brief.

### Check 2: Says how we'll know it worked
- Pass: there are success measures, and each one has a metric, a target and a date or time window ("Mite back to about 11 pings a week by 4.4"). At least one ties back to the problem the brief describes.
- Partly: there are measures, but some lack a number, a baseline, or a time window ("fewer tickets", "cards look more alike").
- Missing: no way to tell whether it worked.
- For each measure that's only partly there, say what it's missing (number, baseline, or when).

### Check 3: Keeps the same scope start to finish
- Write down, in one line, what the opening says is in scope (the summary or "in short").
- Then walk through the rest of the brief and list anything that goes beyond that, drops part of it, or contradicts it: a new feature added halfway down, an "optional" extra, a promise in the measures that the plan never mentions, or a section that quietly changes the answer (e.g. the summary says X is free, a later table says it costs a little).
- Pass: nothing found. Partly: one or two small drifts, or extras clearly labelled optional. Missing: the end of the brief describes a materially different piece of work from the start.

### Check 4: Explains the problem before the fix
- Find where the problem first appears (who it hurts, what happens, evidence) and where the fix first appears.
- Pass: the problem comes first, with evidence, and the fix follows from it.
- Partly: the problem is there and well explained, but a summary or title leads with the fix before the reader has seen the problem, or the evidence comes after the proposal.
- Missing: the brief opens with the solution and the problem is thin, assumed or absent.
- A one-line summary at the top that states both problem and answer is fine. One that states only the answer counts against this check.

### Check 5: Concise enough for management review
The reader is a director with a few minutes. The brief should be as short as it can be **without losing key information**.
- Key information, which must stay whatever it costs in length: the problem and who it hurts, the evidence, the proposed change, the trade-offs or risks, how we'll know it worked, the owner, and the decisions or asks for the reader.
- Count the words (exclude tables' header rows and footnotes). As a guide, aim for about 600 words or one printed page.
- Look for: the same point made twice, background the decision doesn't need, long explanations where a sentence would do, hedging that adds words but no meaning, and sections that could be merged.
- Pass: around one page, and nothing you could cut without losing key information.
- Partly: longer than it needs to be, but the key information is all there and easy to find, or it's short but buries the ask.
- Missing: too long to read in a few minutes, or so short that key information from the list above is absent.
- Report the word count. For each suggested cut, name what to cut and confirm it isn't key information. Never suggest cutting key information to save words; if the brief is missing some, say that instead.

### Check 6: The solution is shaped around the people who use it
This check is about the **solution the brief proposes**, not mainly its wording. Ask: was this solution designed from what users need, or from what is technically interesting, elegant or easy to build? (For Rook, users are responders, handlers and quartermasters.)
- **Each part traces to a user need.** For every piece of the proposed solution, is there a user problem or piece of user evidence that calls for it? Flag parts that exist because they're technically neat, convenient for us, or "while we're at it", with no user need behind them.
- **It fixes what users actually experience.** Does the solution change the moment the user struggles with, or does it improve something underneath that the user may never notice? A clever fix that leaves the user's experience the same counts against this check.
- **All affected users are considered.** Does the brief think about everyone the change touches, including people who don't benefit or who are made worse off (e.g. the other side of a handler–responder pair, a user group that loses something)? Silence about an obviously affected group counts against it.
- **Trade-offs are judged from the user's side.** When the brief chooses between options, is the deciding reason what users gain or lose, or only cost, elegance or engineering effort?
- **Success means users are better off.** At least one success measure is about users' experience or outcome, not only system activity.
- Technical sophistication is fine when it serves one of the points above. Wording matters only as a symptom: if the brief explains the mechanism at length and the user's experience in a line, that usually means the solution was designed from the mechanism outward.
- Pass: every part of the solution traces to a user need, affected users are considered, and success is measured in user terms.
- Partly: the solution is broadly user-driven, but one or two parts lack a user reason, an affected group is overlooked, or a key trade-off is decided on technical grounds.
- Missing: the solution is mainly a technical idea looking for a use, and users appear only as justification after the fact.
- Name the parts of the solution with no user need behind them, and any affected users the brief leaves out.

## 3. Report back

Keep it short and plain. Use this shape:

**Review of `<file name>`**: <N> of 6 pass

| Check | Result | Evidence |
| --- | --- | --- |
| Names who owns it | Pass / Partly / Missing | "quote" (line N) |
| Says how we'll know it worked | ... | ... |
| Same scope start to finish | ... | ... |
| Problem before the fix | ... | ... |
| Concise for management review | ... | "<word count> words" plus the main cut |
| Solution shaped around users | ... | ... |

Then, for every check that isn't a Pass, one bullet with the smallest change that would make it pass, in the brief's own words where you can (e.g. "Add `**Owner:** <name>` to line 3"). If you'd need information the brief doesn't have, such as who the owner is, say so and leave it as a question for the student. Don't invent names, numbers or dates.

End with one line offering to make the fixes: "Want me to apply these to the brief?" Edit the file only if they say yes.

## Ground rules

- Judge only what's written. Don't credit something the student told you in chat but didn't put in the brief.
- Don't review anything beyond these six checks (grammar, tone, the merits of the idea) unless the student asks.
- If two checks pull against each other (for example, a cut for Check 5 would remove the user's own words that Check 6 values), keep the key information and say so.
- The Rook scenario is fictional. Keep everything in the course folder and save nothing to memory.
