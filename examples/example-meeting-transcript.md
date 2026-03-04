# Example Meeting Transcript

Use this as sample input for the `/pm-workspace-setup` wizard if you don't have your own meeting notes handy.

---

**Meeting: Customer Portal Redesign — Stakeholder Alignment**
**Date:** March 3, 2026
**Attendees:** Sarah Chen (Head of Product), Marcus Webb (Engineering Lead), Priya Patel (Design Lead), James Kowalski (Customer Success), You (PM)

---

sarah: okay so let's just get into it, I've got another call at 3:30. where are we on the portal redesign?

you: so we've been through the discovery phase, talked to about 15 customers over the last two weeks. the biggest pain point is definitely the reporting dashboard — it's too slow, the data is stale, and people are exporting to excel just to get basic charts

marcus: yeah the export thing is a huge red flag. we're basically admitting our own tool can't do what they need

priya: from a design perspective i've been looking at how other tools handle this and honestly our information architecture is the root problem. users can't find things. the navigation was built like 4 years ago when we had 3 features, now we have 20

sarah: okay so are we saying the reporting dashboard is the priority or the overall navigation?

you: i think we need to separate those. the dashboard is the acute pain — customers are literally churning over this. navigation is the chronic issue. i'd say dashboard first, navigation in parallel as a design workstream

sarah: that makes sense. james what are you hearing from the CS side?

james: yeah so two of our enterprise accounts — Meridian and TechFlow — both flagged the dashboard in their last QBRs. Meridian specifically said they'd evaluate alternatives at renewal in June if we don't fix it. that's a $450K account.

sarah: june?? that's three months away

james: yeah. and honestly they're not the only ones, there's probably 5-6 mid-market accounts saying similar things, they're just less vocal about it

marcus: okay so timeline wise, if dashboard is priority one, I think we could do a meaningful v1 in about 6 weeks if we descope some things. the real-time data is the hard part. right now everything goes through a batch ETL that runs every 4 hours.

you: what would it take to get that closer to real-time?

marcus: we've been looking at this actually. there's two options — one is to move to a streaming architecture, which is the right long-term answer but probably 3-4 months of work. the other is to just increase the batch frequency to every 15 minutes, which we could do in about 2 weeks

priya: from the user side, 15-minute refresh would solve 90% of the complaints honestly. people don't need second-by-second data, they need data that isn't 4 hours old

sarah: let's do the quick fix first then. marcus, can your team start on the batch frequency this sprint?

marcus: yeah we can. i'll need to pull dave off the API migration though

sarah: the API migration can wait. priya, how fast can you get dashboard mockups ready?

priya: i've actually already started sketching. i can have high-fidelity mockups by end of next week if i get the data model from marcus's team. i want to make sure we're showing the right metrics. also — hot take — i think we should kill the current dashboard completely and rebuild from scratch rather than iterate. it's spaghetti

marcus: agreed honestly. the frontend code for that dashboard is from 2022 and nobody wants to touch it

you: so to summarize what i'm hearing — we're doing a phased approach. phase one is the quick batch frequency fix plus a complete dashboard redesign. phase two is the streaming architecture. and priya runs the navigation IA workstream in parallel

sarah: yes. and i want weekly updates on this. james, can you set up a shared slack channel with the Meridian account team so we have direct signal on whether our changes are landing?

james: yep, i'll set that up today

marcus: one more thing — we should probably also look at the mobile experience. i've been hearing that more customers are trying to check dashboards on their phones and it's basically unusable

priya: oh god yeah the mobile thing is bad. but let's not scope creep. can we add that as a follow-up?

you: agreed. i'll add it as a future consideration in the PRD. should not block phase one.

sarah: fine. what about the budget for the streaming architecture? that's going to need infrastructure investment

marcus: yeah so rough numbers — we'd need to spin up a Kafka cluster and probably hire or reallocate one more backend engineer. i'd estimate maybe $30-40K in infra costs per year plus salary. i can put together a detailed proposal

sarah: do that. get me the proposal by end of month so i can take it to the leadership review. anything else?

you: one thing — I want to run a beta of the new dashboard with 3-4 friendly customers before we GA. james, can you identify who'd be good candidates?

james: yeah Meridian would obviously be one. i'd say CloudBase and maybe Nexus Digital — they're both engaged and give good feedback

priya: oh also — can we get analytics on the current dashboard? i want baseline metrics so we can show improvement

marcus: we've got mixpanel on it. i'll pull a report this week

sarah: great. let's reconvene next wednesday same time. thanks everyone

you: thanks all. i'll send out a summary with action items today

marcus: sounds good

james: thanks!
