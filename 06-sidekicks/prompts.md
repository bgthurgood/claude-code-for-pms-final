# 06 · Sidekicks — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent five sessions on it: finding out what
went wrong, then building the fix nobody had — a working prototype,
by hand, in one sitting, for one room.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
Make a skill called review-checklist. When I point it at a brief, it checks that the brief: names who owns it, says how we'll know it worked, keeps the same scope start to finish, and explains the problem before the fix.

### 2.
Lets add another couple of checks to that skill. I want to ensure that the overall brief remains as concise as possible without losing key information to make it ideal for management review. I also want to ensure that the brief retains a customer-centric perspective and doesn't over-emphasize technical sophistication at the expense of end user experience.

### 3.
Do you have access to another person's brief to try this skill out?

### 4.
Run my check skill on Sofia's brief

### 5.
Check 6 focuses a bit to much on the technical language in the brief rather than the overall customer centric nature of the solution the brief represents.

### 6.
Make a skill called qa-testing. When I point to the product brief that outlines the requirements & the staging environment where the code build against it is housed, it creates robust acceptance criteria’s, validates them with me, performs the tests & generates a document with all findings.

Run a test on the my brief & assume we’ve built the prototype in a staging environment.

Ask me questions if you see fit.
