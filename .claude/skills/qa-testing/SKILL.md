---
name: qa-testing
description: Acceptance-tests a build against its product brief. Given a brief (the requirements) and a staging environment (where the build lives), it writes acceptance criteria, checks them with the student before testing, runs the tests in the built-in browser, and writes a findings document. Use it when the student says "QA this", "test the build against the brief", "run acceptance tests", "qa-testing <brief> <staging link>", or "/qa-testing".
---

# QA testing

The student is a PM in Product School's "Claude Code for PMs" course. They want to know whether a build does what its brief asked for. Play the role of a careful QA lead: turn the brief into acceptance criteria, agree them with the student, test the build, and report what you found. You test and report; you don't fix the build or rewrite the brief.

There are four stages, and the student signs off the criteria between stage 2 and stage 3. Never start testing before they agree the criteria.

## 1. Get the two inputs

- **The brief.** A file in the course folder (read all of it) or a Rook wiki page (read it with the rook-wiki tools). If the brief points to a companion file (e.g. a "-detail.md"), read that too, but the brief wins where they disagree. Log each disagreement as a finding.
- **The staging environment.** A URL the student gives you, or a build file in the course folder (e.g. `prototype.html`).
  - A local file: serve it from the course folder on localhost. Add a configuration to `.claude/launch.json` that runs `python -m http.server <port>` (or `py` on Windows if `python` is missing), and open it with `preview_start`. Don't use `file://` links.
  - A hosted URL: use it only if the student gave it to you in chat. Treat it as a test environment only if the host name says so (staging, dev, test, qa, sandbox, preview). If it looks like a live production site, stop and ask.
- If either input is missing, ask one short question for it. If the student says "assume it's built", use the build file that sits next to the brief and say which one.
- Before using the browser for the first time, load the `anthropic-skills:built-in-browser` skill.

## 2. Write the acceptance criteria

Read the brief line by line and pull out every requirement: what users see, what they can do, what the system does, the words used, and what must *not* happen. Then write criteria that are:

- **One behaviour each**, written as **Given / When / Then**, using the brief's own words for anything users see.
- **Traceable**: each one cites the brief section or line it comes from. A requirement with no criterion is a gap. A criterion with no requirement behind it doesn't belong.
- **Observable**: "Then" is something you can see or measure in the build, not an intention.
- **Robust**: beyond the main path, cover:
  - edge cases (timer runs out, repeated actions, switching modes mid-flow, reset, first and last items)
  - negative cases (what must not appear, such as blame, scores shown to users, or legal identity)
  - cross-view consistency (an action in one view updates the other)
  - basic accessibility (buttons reachable by keyboard and labelled)
  - phone-width layout (375px wide, no sideways scrolling)
  - no browser console errors
- **Prioritised**: **Must** (the brief's core promise breaks without it), **Should** (stated in the brief but not core), **Could** (implied, nice to confirm).
- **Classified by testability:**
  - **UI-testable**: can be checked in the build.
  - **Not testable here**: needs real data, backend rules, a later release, or a decision someone hasn't made. Still list it, say why, and say who could verify it.
- Note values the brief marks as placeholders. Test that the behaviour is there, not the exact number.

Aim for roughly 15–35 criteria, depending on the size of the brief. Save them to `<brief folder>/qa-<brief name>-criteria.md`, in the format in `references/templates.md`.

Also note anything in the brief that's too vague to test ("feels faster", "fewer tickets") and suggest a testable version.

## 3. Agree the criteria with the student (stop here and wait)

Show the student:
- a count by priority and testability
- the criteria table (ID, priority, short title, Given/When/Then, source)
- the requirements you couldn't turn into a testable criterion
- up to three questions where the brief is ambiguous and the answer changes what passes. Ask each with your suggested default.

Then ask: "Are these the right criteria? Approve, or tell me what to add, change or drop." Make their changes, update the criteria file, and only test once they approve. If they approve with changes, apply them and go straight to testing; don't ask a second time.

## 4. Run the tests

For each approved UI-testable criterion, in priority order:
- Start from a clean state (reload or use the build's reset) unless the criterion needs a sequence.
- Do the steps in the built-in browser.
  - Prefer `read_page` / `get_page_text` / `find` to confirm text and state.
  - Take a screenshot when a visual check matters (layout, colour, something appearing or disappearing).
  - For timers, use any speed-up control the build offers. Note when you did.
- Record the steps actually taken, the expected result, the actual result, and a verdict:
  - **Pass**
  - **Fail**: describe the defect.
  - **Blocked**: couldn't run it; say why.
  - **Not testable here**: carried over from stage 2.
- Use the browser's JavaScript tool only to **inspect** (read state, check console errors, measure layout), never to change the build or force a result. Any verdict that relies on inspection rather than what a user can see says so.
- Check the console for errors once at the start and after each major flow.
- Check phone width with `resize_window` (mobile preset), and set it back to desktop afterwards.
- If something unexpected turns up outside the criteria, log it as an **exploratory finding** rather than ignoring it.
- Never change the build's code, enter real credentials or personal data, or submit anything to a non-staging host. Report any failed tool call, even if a retry worked.

For each defect, record:
- **Severity**:
  - **Critical**: the brief's core promise is broken or users are harmed.
  - **Major**: a Must criterion fails.
  - **Minor**: a Should or Could criterion fails, or a wording slip.
  - **Cosmetic**
- **Steps to reproduce**, starting from load.
- **Expected vs actual**.
- The **criterion** and **brief source** it relates to.

## 5. Write the findings document

Save it as `<brief folder>/qa-<brief name>-findings.md`, using the findings template in `references/templates.md`. It's written for a director and the build team, so lead with the verdict, keep it plain, and put detail lower down. It must include:

1. **Verdict** in one line: Ready / Ready with fixes / Not ready. Then 3–5 bullets on why.
2. **What was tested**: brief, build, environment, date, browser and viewports.
3. **Results summary**: counts by verdict and priority.
4. **Defects**, worst first.
5. **Gaps between brief and build**: requirements the build doesn't cover, and things the build does that the brief never asked for.
6. **Not testable here**: what's left, and who can verify each item.
7. **Exploratory findings**.
8. **Full results table**: every criterion with its verdict and one line of evidence.
9. **Suggested next steps**: who should act on what. Don't invent dates or owners the sources don't name.

Then tell the student in chat:
- the verdict
- the counts
- the top three defects
- links to both files

Offer to turn the findings into backlog stories, or to retest after fixes. Don't save anything else, and don't close the browser tab unless asked.

## Ground rules

- Report only what you observed. If a criterion couldn't be tested, say so; never mark it Pass on inference.
- If a later check contradicts an earlier verdict, correct the verdict instead of adding a caveat.
- Read and write only within the course folder (plus the browser session). The Rook scenario is fictional. Save nothing to memory. Never record or infer a responder's legal identity (Security Policy 4.1); a build that shows one is a Critical defect.
