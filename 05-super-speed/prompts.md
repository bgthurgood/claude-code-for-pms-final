# 05 · Super Speed — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent three sessions finding out what went
wrong: the two piles of feedback that didn't agree, the numbers that
hid four people inside an average, and the code that settled it —
the shorter timeout is what did it.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
Is there anything we could add to the brief and eventual prototype that would address the issue of the phone making it quicker to respond to cut that 1 to 4 seconds off the quiet 4s typical response time in order to get them under 60 seconds?

### 2.
write the brief, don't build the prototype yet

### 3.
Walk me through the director's request one step at a time and lets evaluate the brief you wrote against each specific part of her request and improve the brief as we go.

### 4.
Save the brief exactly as it stands now as 05-super-speed/brief.md. Show me the file when it's done.

### 5.
Take the brief you just wrote (brief.md) and build me a working prototype, an actual screen I can click through, not a description of one. Save it as 05-super-speed/prototype.html, a single file I can just open in my browser. Show me where this would actually happen, and make at least one thing on it respond when I click it.

### 6.
Right now the prototype works great for Meteor Mite. Make an option to select any of the quiet 4 plus 2 responders who suddenly became very busy after the release (indicate in the selection section whether they are the quiet 4 or people who benefited it).

### 7.
create a second html that looks just like this prototype, but uses actual data of pings and responses from the release date through sept 6th to show, at an accelerated rate, exactly what happened to the selected responder between aug 12 and sept 6th to get to the starting point. It should play through the scenario in the same layout as the prototype, but automatically play out the scenario as described by the actual data. Call this file whathappened.html

### 8.
Add an option to whathappened.html to run the scenario using the exact data and pings, but what would have happened if the new rules from the brief had been in play.
