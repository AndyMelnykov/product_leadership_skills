# Customer Interview Transcripts: Shift Handoffs on Relay

**Research question:** When a support ticket crosses a shift boundary on Relay (our support-ticketing/collaboration product), do agents lose context in a way that's costing teams real time or customer goodwill — and if so, for which teams?

**Method:** 4 semi-structured interviews, ~30 minutes each, conducted August 25–29, 2026, with Relay customers across 3 accounts. No survey or usage-analytics pull was run alongside these interviews.

**Participants:**
- Priya Nair — Support Team Lead, Northwind Analytics (22-agent support team, 3 shifts/day, no shift overlap)
- Marcus Delgado — Support Ops Manager, Vantage Metrics (~140-agent global support org, follow-the-sun coverage)
- Jordan Ashe — Support Agent (frontline), Vantage Metrics (same account as Marcus)
- Elena Cho — Support Team Lead, Loopwell (8-agent team, single shift with a 2-hour overlap window)

---

## Transcript 1: Priya Nair, Support Team Lead, Northwind Analytics

**Interviewer:** Walk me through what happens when a ticket is still open at the end of your shift.

**Priya:** It depends on the agent, honestly. We have a shared handoff channel in Relay where people are supposed to leave a note before they log off, but it's basically a firehose — by the time the next shift starts, there are forty messages in there and nobody's reading back through all of them to find the one that matters for their ticket.

**Interviewer:** What happens when the next agent picks up a ticket without having seen that note?

**Priya:** They open the ticket, see the customer's last message, and they ask a clarifying question that the customer already answered six hours ago. I'd guess it happens on maybe a third of the tickets that carry over a shift boundary — that's not a real number, just my sense of it watching escalations come through. But when it happens, the customer's reaction is exactly what you'd expect. We had someone reply "I already told you this" in all caps last week. We probably re-ask the same question three times before a customer gets an actual answer, and every time it happens they get a little more annoyed with us.

**Interviewer:** Has this gotten better or worse recently, or has it been steady?

**Priya:** Steady, as far as I can tell. It's just been an annoying fact of having three shifts since we started running them a year and a half ago.

---

## Transcript 2: Marcus Delgado, Support Ops Manager, Vantage Metrics

**Interviewer:** How does context get passed between shifts on your team?

**Marcus:** We're follow-the-sun now — Americas, EMEA, and as of about six weeks ago, APAC. Officially agents fill in a "handoff summary" field on the ticket before it rolls to the next region. In practice, maybe half of them do it, and when they do it's often just "see above."

**Interviewer:** Do you have any sense of how often this actually causes a problem downstream?

**Marcus:** I pulled our ticket data before this call, actually. We reassign about 18% of open tickets across a shift boundary in a given week, and the reopen rate on those is almost double the reopen rate on tickets that stay with one agent the whole way through. I don't have the export in front of me right now, I'm going off what I remember from looking at the dashboard last week, but that's roughly the shape of it.

**Interviewer:** You mentioned the APAC shift is new. Has that changed anything?

**Marcus:** Yeah, noticeably. Before APAC, most tickets that carried over went through one handoff, Americas to EMEA overnight, and EMEA agents had gotten decent at guessing what happened even without a great note. Now a ticket can cross two boundaries in a day, and the compounding effect is real — by the third agent, nobody really knows the full history unless they scroll back through the entire thread. It's the main reason I agreed to this interview, honestly — it's gotten worse for us specifically since APAC went live.

**Interviewer:** What would actually fix it, in your view?

**Marcus:** Something automatic. If Relay could generate a short summary of what's happened on a ticket whenever it's about to cross a shift boundary, agents wouldn't have to remember to write anything — it would just be there. I don't trust our agents to reliably fill in a manual field; we've tried making it required and people still write "see above."

---

## Transcript 3: Jordan Ashe, Support Agent, Vantage Metrics

**Interviewer:** Marcus mentioned there's a required handoff-summary field on tickets. Do you use it?

**Jordan:** Honestly I don't even open the handoff notes anymore, I just DM the next person if it's actually important. The field's always there but half the time it's stale or it's someone else's shorthand that doesn't mean anything to me, so I stopped trusting it a while ago.

**Interviewer:** So how do you keep track of what's actually important to hand off?

**Jordan:** I keep my own spreadsheet, actually — just a running list of "sticky" tickets, what's going on, what I'm waiting on. If one of those is about to cross a shift and I think it matters, I'll message the next person directly or leave a note in the team chat, not in the ticket field. The official field is more like a formality at this point, something you fill in so the ticket doesn't get flagged as incomplete.

**Interviewer:** If Relay auto-generated that summary for you instead of asking you to type it, would you read it?

**Jordan:** Maybe? I guess it depends whether it's actually right. I don't have strong feelings either way — I've just given up on the field as it exists now.

---

## Transcript 4: Elena Cho, Support Team Lead, Loopwell

**Interviewer:** How does your team handle tickets that are still open at the end of the day?

**Elena:** We're small enough that it's not really a problem for us. We run one shift with about a two-hour overlap in the afternoon, so if something's unresolved, the two people just talk about it directly before the first person leaves. The only time it's ever an issue is over the weekend — we don't have coverage Saturday or Sunday, so anything open on Friday sits until Monday, but customers mostly expect that from a company our size.

**Interviewer:** Marcus, at a much bigger account, mentioned wanting Relay to auto-generate handoff summaries. What's your reaction to that?

**Elena:** I'd be pretty cautious about that, honestly. If Relay is writing a summary of what happened on a ticket and it gets something wrong — says we promised a refund we didn't promise, or misstates what the customer's actually asking for — that's now potentially something an agent repeats back to the customer as fact. I'd rather have a short structured field, like three fixed questions the outgoing agent has to answer, than a freeform AI summary I'd have to double check anyway. For us, given how rarely this comes up, I don't think we'd want to be an early adopter of anything automated here regardless.

**Interviewer:** Is loss of context during handoff something your team has ever raised as a complaint?

**Elena:** Not really, no. If anything, when we've talked about it internally, it's more "let's just make sure we chat before someone logs off" than anything we've wanted Relay to solve for us.
