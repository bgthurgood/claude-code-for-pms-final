# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
Which files had significant updates in 4.2?

### 2.
Where did the change occur that changed the routing timer from 90 seconds to 60s

### 3.
Were there any benefits to this time change that would cause us to question whether to go back to the 4.1 approach?

### 4.
Fill in the blanks - "The reason some responders are getting no pings at all is ____ because _____."

### 5.
Is the time of day the pings came through for the 4 who miss so much different than those who didn't miss? Especially in the 24-48 hours immediately after the 4.2 release? (E.g. My hypothesis is that responders may have received their initial 4.2 pings at a time of day that is particularly difficult to respond - like the night - where they may be asleep and have trouble responding in 60 seconds.)

### 6.
Looks like the engineering manager left a question on the 4.2 release page in Rook's wiki - check it out

### 7.
In plain language, using visuals wherever possible, show me how the code scored responders in 4.1 versus 4.2

### 8.
I am assuming that responders distance didn't change along with the 4.2 release - they probably were largely where they were before and after that release... so if the response portion of their score became so much less weighted, what is the exact mechanism for how it lowers the scores for the quiet 4 and doesn't allow them to recover. Visual preferred

### 9.
What would have happened if the weighting hadn't changed, just the time from 90s to 60s and the resulting missed pings?

### 10.
If yesses are only 25% of the score, how does a score drop all the way to zero? Is the code actually weighting the score increment that is awarded at each call?

### 11.
Find everything in the code that puts points back on a responders score

### 12.
Give me a model to play with outcome of a 4.3 fix. Count of misses a ping, recovery, ping wait, and simulate the output with a confidence score

### 13.
Update that simulator to show each of the quiet four individually

### 14.
If we want to optimize the system for response time, how can we structure the score to align responders' incentives with an overall lower response time. E.g. if they have no penalty for missing, then they would never say no, they would just let the clock run out.
