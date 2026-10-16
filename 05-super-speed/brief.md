# A way back in for quiet responders — draft brief

For Helen · from the Dispatch PM · Owner: Adam (Helen to confirm) · draft, 16 Oct 2026 · not reviewed by Wen or Marcus

**What we'd build, in one line:** a way back for quiet responders. A welcome-back ping, a Quiet label with the reason on the handler's card, and a lighter penalty for a miss than for a turn-down.

## The problem
Since 4.2, some responders have gone quiet and stayed quiet. Routing only offers a callout to someone near the top of the ranking. The only way back up is a yes (+0.08). A turn-down or a miss costs 0.12, and nothing decays (`history.py`, TODO from 2019). Both cost the same, though a miss is often not a choice (the 60s wait, a dead zone, a push that never arrived), and misses jumped on 12 Aug (7 of 25 pings) while turn-downs barely moved. So a quiet responder is rarely asked, and not being asked is the only thing keeping them quiet. Their handlers have no way to see this or fix it. Kip: "Mite thinks Mite's been forgotten," and he has nothing better to say than "hang in there."

Evidence status: ping and ticket data show the concentration (Farlight, The Undertow, Meteor Mite, Vesper fell from about 12 pings a week to 3–5). The loop itself is read from the code, not replayed, because scores aren't stored. Whether the 2/3 "phone never goes off" tickets are these same responders is unconfirmed.

## Who it's for
1. **The responder who has gone quiet** (Meteor Mite, Farlight). They get a visible way to say "I'm here, ask me," and a fair turn.
2. **The handler who watches them** (Kip). Today he sees a quiet card next to a busy one and can't tell why. He needs the reason on the card and one thing he can do about it.

## What changes for them
- **Responder:** after a stretch with no offers, their next suitable callout comes as a labelled "welcome back" ping. It has a full 90s wait, because a short wait is how misses happen. A yes from it restores their standing; they don't have to climb back through busier callouts first. They can also confirm "available" in the app, which counts for something instead of nothing.
- **Handler:** the responder card shows a plain "Quiet" state and why ("no offers in 9 days; last 6 offers turned down or missed"). It has one action: "Offer them the next suitable callout."
- **Dispatch:** only a responder who is both quiet and a qualified, nearby match gets this. Everyone else routes as in 4.2.
- **Misses and turn-downs count differently.** Today both cost the same (0.12). Proposed: a turn-down costs 0.10 and a miss costs 0.06. A turn-down is a choice, so it should cost more than a miss, which can be the 60s wait, a dead zone or a push that never arrived. These values are a proposal for Wen to check, not settled, because we can't replay their effect on scores. A run of misses should still sink someone, just more slowly. This goes after what changed on 12 Aug (see the problem above).

## What it deliberately doesn't do
- **Doesn't revert 4.2** or change the proximity and acceptance weights. Wide-area responders asked for that change.
- **Doesn't remove the penalty for turning jobs down.** Someone who really is turning jobs down still drops, and drops faster than someone who misses.
- **Doesn't send anyone who isn't capable or close enough.** A coverage gap stays a coverage gap.
- **Doesn't force a yes** or penalise a turn-down on a welcome-back ping more than a normal one.
- **Doesn't touch identity.** Everything is by cover persona; no mapping to anyone (Security Policy 4.1).
- **Doesn't fix push delivery** or the handler phone app. Those are separate.

## Open questions before we build
- **Wen:** was the decline penalty meant to hit everyone? How much lighter should a miss be than a turn-down, and how many in a row before it should hurt as much? Her 2019 note argues that quiet should stick until the person takes work again. This brief says that's the trap, and she should get to answer that.
- **Push receipts, 12 Aug to 6 Sep:** if phones aren't receiving offers, welcome-back pings fail silently and make things worse. We need to rule this out first.
- **Cost:** a welcome-back ping goes to someone less likely to answer, so a callout could take longer. Limit it to when there's slack.
- **How we'd know it worked:** pings per quiet responder per week. Baseline 8, target more than 10. Also acceptance on welcome-back pings. Callout time-to-accept must not worsen (needs event logs, which we don't have today).
