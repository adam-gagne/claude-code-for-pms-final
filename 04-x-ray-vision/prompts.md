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

What has recently changed in the code that would leave the responders with no pings?

### 2.

can you replay the 4.2 callouts with 4.1 weghts?

### 3.

what was the weight of a miss in the 4.1

### 4.

Didn' the response time also change?

### 5.

Can you create a UML diagram of how the code works when a call comes in, how it is transferred when a call is missed?

### 6.

What is Wen's job and why do they have so much information? Wen is unavailable so I am not able to connect with them

### 7.

are there any comments from the developers?

### 8.

how does the supply team impact the current_record()?

### 9.

Engineering manager Aug 14, 2:47 PM
Quick one — did the change to who gets asked first apply to responders who'd already been turning jobs down, or just new ones? Can't tell from the code and don't want to guess on this. Anyone know?

The pings table on rook-database has last session's numbers. Read that alongside this code. Does it back up what I found in Lab A? And does that answer the engineering manager's question above?

### 10.

draft a reply to marcus

### 11.

Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on.

### 12.

If someone has been quiet for a month, what are the steps needed to get them to start getting calls again?

### 13.

If someone has a score of 0 how many calls would they need to get back to the middle of the pact?

### 14.

For the 4 heroes that are biggest impacted do we have their skills captured?

### 15.

Lets get back to the code and helping getting heroes back into getting asked - what are some enhancements we could make to help ensure all heros have an the ability to respond to pings?
