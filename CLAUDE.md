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
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap,
Product briefs, 4.2 comments) and `00-rook/company/notes/handoff-from-priya.docx`.
I'm the new PM for **Rook Dispatch**, replacing Priya Raghunathan (left 21 Aug 2026).
Wiki data is as of the dates shown; re-check before relying on it.

### Company and products
- Rook Industries: coordination and provisioning software for the protective-response
  sector. Customers are masked responders (independent, not employees) and the
  handlers and quartermasters who support them. Subscription, priced per active responder.
- **Rook Dispatch** (mine): responder coordination. Incident comes in, Dispatch ranks
  available responders, pings the top one's phone, and they take it or turn it down.
  Handlers use the web console; responders use a native phone app. Monthly releases,
  4.x numbering. Routing config ships in the release; it is not a runtime setting.
- **Rook Supply**: gear provisioning (requisitions, maintenance, field failure reports).
  Handlers and quartermasters. Dispatch writes the Responder Availability Record; Supply reads it.
- **Confidentiality is contractual**: cover identities are never mapped to legal identities
  in production. Never design anything that assumes that mapping or tries to infer
  identity. Read Security Policy 4.1 before touching responder records.

### People (Dispatch team)
Wiki comments use roles, not names. Mapping:
| Role in comments | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran | Eng manager, Dispatch (Site Aleph). Priya's "start here" contact. |
| Staff engineer | Wen Li | Built the ping-ranking logic (Berlin). No written doc; talk to Wen. |
| Support lead | Nadia Hoffmann | Owns tickets (Berlin). Suggested standing 15 min. |
| Product designer | Sofia Marino | Console and phone app; ran the September interviews. |
| Director of Product | Helen Achebe | My manager. Owns roadmap and commitments. |
| Data analyst | Ravi Menon | Singapore. Reports weekly on ping acceptance. |
| Priya | Priya Raghunathan | Previous PM, gone. Only reachable via Marcus. |
Supply names that appear in briefs: Halloran (quartermaster). Interview handlers include
Aunt Dot, Mr. Ambrose, Kip (responder names are cover personas).
HQ is Site Aleph (ice shelf); offices in Berlin, Singapore, Cornwall.

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: one callout offered to one responder.
- **Taken / Turned down / Missed**: yes / no / no answer in time. Turned down and
  missed both move the ping on, but are recorded separately.
- **Ping wait**: how long a ping sits before counting as missed (90s before 4.2, 60s now).
- **Routing priority**: score ranking responders. Inputs: proximity (travel-time estimate),
  availability, capability match, recent acceptance history. Declining or missing lowers
  the recent-acceptance part, so a responder drops in later orders.
- **Acceptance rate** (headline metric: taken / all pings), **time-to-accept** (median s
  to taken), **coverage gap** (no available responder had the needed capability tags;
  distinct from low acceptance).
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic,
  crowd-management, de-escalation. **Mutual aid**: cross-city cover, unsupported, Q4 exploration.
- Supply: **requisition**, **field failure report**, **service interval**.

### Where things stand (as of mid-Oct 2026)
**Releases:** 4.0 (7 Apr): new nav, profile redesign, routing override audit log.
4.1 (16 Jun): travel-time proximity, bulk callout, push reliability.
4.2 (12 Aug): proximity weighted up vs recent acceptance, ping wait 90s to 60s,
persistent console filters, three defect fixes.

**The 4.2 problem (my first priority):**
- Since 4.2, callout tickets ~3x normal; split ~2/3 "phone never goes off", ~1/3
  "gone before I could answer". Volume flat as of 26 Aug. A handler emailed Nadia directly.
- The 1/3 is explained by the 60s ping wait. The 2/3 is unexplained.
- Priya's and Marcus's story is "seasonal August dip, will recover in September." **No
  numbers have been shown to support it**, and it's now October. Treat as unverified.
  Ask Ravi for weekly acceptance rate, split into taken / turned down / missed, before and after 12 Aug.
- Open design question from Marcus (14 Aug, unanswered; Wen was away): the proximity change
  doesn't distinguish responders who've been declining from everyone else. Was that a
  decision or did it fall out? One hypothesis to test, not a conclusion: weighting
  proximity over acceptance history reorders who gets pinged and may leave some responders
  never offered pings. Wen is the person to ask.
- Priya's guidance: don't make this a revert-4.2 debate (the change was long requested by
  wide-area responders). Fair to weigh, but it shouldn't block looking at the data.
- Marcus agreed (28 Aug) to regroup with me on the 4.2 picture and not hand me a conclusion.
  Nadia has the ticket breakdown.

**Roadmap (Q3, last reviewed 30 Jun by Priya; stale):**
| Item | Target | Status | Note |
| --- | --- | --- | --- |
| Change to who gets pinged | 4.2 | Committed | Shipped |
| Ping timeout tuning | 4.2 | Committed | Shipped (90s to 60s) |
| Availability Confidence | 4.2 | Committed | Not in 4.2 notes; presumably deferred. Confirm with Helen |
| Requisition approval chains | 4.3 | Committed | Supply |
| Handler phone app | Q4 | Exploring | Sofia |
| Shared cover between responders | Q4 | Exploring | |
Priya said some items got squeezed from 4.2 and that the "which are still Q3 commitments"
conversation with Helen never happened. It needs to.

**Briefs (check currency before citing):**
- Bulk Callout (Jan): shipped in 4.1 though brief still says unowned.
- Routing Override Audit Log (Mar): shipped in 4.0.
- Requisition Approval Chains (Jul, Supply): ask is a second approval over $2,000; the
  brief has scope creep (48h bypass, cross-site dashboard, replace Halloran's spreadsheet). Phasing TBD.
- Handler Phone App (8 Sep): notifications, status view, one-tap contact; Sofia exploring, unstaffed.
  Prompted by handler Aunt Dot's request to be notified too.

### Standing to-dos inherited from Priya
1. Write the missing description of how routing priority decides who gets pinged (with Wen).
2. Hold the commitments conversation with Helen.
3. Ignore console filter-persistence tickets (cosmetic noise).
4. Early on, question decisions in parts of the product nobody has examined closely.

### How to work with me
- Cite the source (wiki page, handoff, comment) and flag when something is inference.
- Don't state a cause for the 4.2 drop until the numbers are in.

### Found in the data (session of 13 Oct 2026; sources: rook-database `pings`, `support_tickets`; repo `00-rook/code/dispatch-routing`)
- Ping acceptance was 75–78% every week before 12 Aug, with no August dip. It fell to 54% in the week of 10 Aug and was back to 73% by 31 Aug. Missed pings went from about 2% to 13–22% of pings. Declines barely moved.
- Pings are concentrated since 4.2. Farlight, The Undertow, Meteor Mite and Vesper dropped from about 12 a week to 3–5 a week, while the busiest responders rose. My earlier "every responder still gets pinged" was true at weekly level and hid this, so don't rely on it.
- Support tickets since 4.2: about 30 are "my phone hasn't gone off / nothing coming through" (none before 12 Aug), and about 15 are "moved on before I could answer." Inference: the first is ranking starvation, from top-down offers plus the decline penalty with no decay (`history.py` TODO). The second is the 60s wait. Neither is confirmed.
- The push path is not in the repo: `push_to_device`, `poll_device` and `withdraw_from_device` are stubs in `offer.py`. A failed push is recorded as missed. No push delivery logs were found in the course folder or the database. To test whether phones receive offers, get push provider receipts (APNs/FCM) for 12 Aug to 6 Sep and ask Wen.
- Still open: whether the ranking change was meant to affect responders who decline (Wen), and whether the 2/3 "phone never goes off" tickets are the same group as the starved responders.
- Customer interviews (wiki database, 2–5 Sep, console redesign research run by Sofia): Aunt Dot, Mr. Ambrose, Halloran, Kip. Ambrose's "callout moved on while he was suiting up" matches ticket 3043 (13 Aug). Dot and Kip both describe quiet weeks alongside fast-vanishing ones. Interviews were not designed for the ping question; use them as color, not evidence.
- Tickets since 12 Aug (my count from the text, not a query): about 30 "phone never went off / few pings", 15 "moved on before I could answer". Before 12 Aug there is one "moved on" ticket (3014, out of signal) and no quiet-phone tickets. The two first "missed after a quiet stretch" tickets are 3110 (Farlight) and 3140 (The Undertow).
- Pings after 12 Aug: Farlight 7 missed of 11 sent; The Undertow 9 missed of 14. Ashgrove and Halfmoon have few misses (4 and 5) but still lost volume, so misses alone don't explain the drop. Weekly, Farlight's misses rose the week of 10 Aug before her volume fell.
- Routing code (`config.py`, `history.py`): timeouts and turn-downs call the same `record_declined()` with the same penalty (0.12); acceptance credit is 0.08; no decay. Weights are proximity 0.60 (was 0.45) and recent acceptance 0.25 (was 0.40). Ranking orders who is asked first but never removes anyone. My arithmetic: the acceptance term can shift ranking by at most about 9 minutes of travel time. Inference, not confirmed.
- Score history isn't stored anywhere in the data, so the spiral can't be checked directly. A replay of 4.2 callouts with 4.1 weights, and with misses not penalized, would separate the two causes.
- Session of 14 Oct 2026 (sources: rook-database `pings`, `callouts`, `support_tickets`; repo `dispatch-routing`). Farlight's last ping was 28 Aug. Of the 9 callouts she declined or missed after 12 Aug, 8 went to another responder (mostly Cindermark and Sgt. Falkirk). One Uptown callout on 19 Aug was taken by nobody.
- Daily pings: misses jumped on release day, 12 Aug (7 of 25 pings missed; 0–1 a day before). The earlier week-of-10-Aug rollup mixed in normal days, so the change starts on 12 Aug.
- Uptown callouts fell about 11% after 12 Aug (1.34 to 1.19 a day), against about 15% citywide. Falling demand doesn't explain Farlight's drop.
- The database covers only 29 Jun to 6 Sep 2026. There is no 2025 data, so the "August dip" can't be tested here; Ravi's older weekly reports would be the source.
- `pings` has no answer timestamp, so time-to-accept can't be calculated. It needs push or app event logs. The 90s-to-60s change has no recorded reason in the wiki or repo; the roadmap owner is Priya, and her handoff doc hasn't been checked yet.
- Recent-acceptance scores are held in memory (`history.py`, `_scores`). A restart would reset everyone to 0.5. Not confirmed whether that happened around 12 Aug.
- Code (`routing.py`, `history.py`): the 4.2 weight change applies to every responder equally. Nothing exempts people who were already declining, and their existing score carries over. The repo has one "Initial commit" (2 Oct), so the 4.2 diff isn't in git; the only 4.2 record is the comments in `config.py` and `CHANGELOG.md`.
- Pre/post 12 Aug check (`pings`): the four biggest losers (Meteor Mite, Farlight, The Undertow, Vesper) had 13–20 turn-downs before 12 Aug, but Stormwrack (17) and Nightwell (20) kept about three-quarters of their volume. Prior turn-downs explain part of the drop, not all of it. Inference, not a cause.
- Only two things change the recent-acceptance score: a yes (+0.08) and a turn-down or miss (−0.12). Nothing restores points except a yes. A replay isn't possible from the data: `callouts` has no location or skill tags, and scores and travel times aren't stored.
- Responder skill tags aren't in the `responders` table or the code. The wiki search only matches page titles, so the "Shared cover between responders" row hasn't been read.
- Open: a draft reply to Marcus's 14 Aug question is written but not sent. Wen is still the only person who can say whether the decline penalty was meant to apply to everyone.
- Session of 16 Oct 2026 (sources: `05-super-speed/director-request.txt`, wiki Glossary, Team directory, 4.2 comments, Priya's handoff). Helen wants a one-pager on what we'd build instead of quietly changing a number, from the point of view of the person it happens to, plus something clickable. The note Wen left is the 2019 TODO in `history.py`; her side argues quiet should stick until the person takes work again.
- Draft brief is `05-super-speed/brief.md`: a "welcome-back" ping with a full 90s wait for quiet responders who qualify, a Quiet label with the reason on the handler's card, and a lighter penalty for a miss (0.06) than a turn-down (0.10), with a yes still +0.08. These are my proposals; Wen hasn't checked them, and it hasn't been sent to Helen.
- Clickable mock-up is `05-super-speed/prototype.html` (one file, Kip's cards for Meteor Mite and The Gale, Mite's phone, a roster of other responders). Every number in it is made up; the dark "Harbour dusk" palette and rook logo are placeholders. Kip asked for dark mode in his 4 Sep interview.
- Open: what counts as "quiet" (the 9-day threshold is a guess), whether a miss should cost less than a turn-down (Wen), push receipts for 12 Aug to 6 Sep, and whether welcome-back pings slow callouts. The module intro in `05-super-speed/prompts.md` says the shorter timeout "did it", but our data points to ranking starvation for the "phone never goes off" tickets; unresolved.
- Later on 16 Oct 2026: I made a reusable skill, `review-checklist`, at `.claude/skills/review-checklist/SKILL.md` (in this course folder only). It runs four checks on any brief: named owner, how we'll know it worked, scope at the end matches the start, problem before the fix. Review only; it never edits. A session loads skills at its start, so it only works by name in a new session.
- First run on `05-super-speed/brief.md` came back "fix first" (owner, success measure and scope were partial; problem-before-fix passed). I then set the owner to Adam (Helen to confirm), the measure to pings per quiet responder per week with baseline 8 and target more than 10, and moved the scoring change into the top of the brief.
- The baseline of 8 and the target are my own working numbers, not from the data (the four starved responders were at 3–5 a week, down from about 12). Ravi could confirm. Still not done: the time-to-accept gap (needs event logs from Wen), and whether "confirm available in the app" stays in scope.
