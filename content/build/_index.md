---
title: "Build"
description: "AI implementation and developer tooling for engineering teams: shipping AI-powered features, building internal tools, and advising on what to build."
layout: "standard"
draft: false
params:
  cta:
    line: >-
      If you're trying to get something working and it isn't working yet,
      that's a good conversation to have. Book a time and tell me what you're
      stuck on.
---

I build software that uses AI, and I help other people do the same. Some of that is writing code. Some of it is sitting with a team that already has engineers and working out what is worth building, what is going to break in production, and what they should not attempt yet. For a small business with no engineers at all, it usually starts further back: which parts of your week are actually automatable, and which tools will do that without creating a second job managing them.

The demo is never the hard part. Getting something to work once, in front of a friendly user, on a good day, is a weekend. Getting it to work every time, for people who did not read the instructions, is the job.

## Who this is for

**Engineering teams** with an AI feature to ship, or a prototype that impressed everyone in the demo and has not survived contact with real users. Also teams still deciding what to build, where the useful conversation is often about what to skip.

**Small businesses** where AI could take real work off someone's plate: intake, scheduling, quoting, drafting the same document for the fortieth time. You do not need engineers on staff for this, and you usually do not need custom software either. Often the right answer is three existing tools wired together properly, and I will tell you when that is the case rather than selling you a build.

## What I build

- AI-powered applications, from the interface down to the retrieval and evaluation layers
- Developer tooling that makes AI useful inside an existing codebase
- Integration work: connecting AI to the systems a business already runs on
- Evaluation and feedback infrastructure, so you can tell when the thing is wrong
- Advisory, for teams who want to build it themselves and want someone who has already made the mistakes

## Selected projects

One of these runs in production every day. The others are in beta or still in progress. Together they are where most of what I know about shipping AI has come from.

### Top End Devs

I run a podcast network: 25 shows, 18 years, more than 4,600 episodes. The whole back catalog runs through a pipeline I built. Episodes are transcribed and embedded, show notes and titles and descriptions are generated for each one, and the transcripts feed a RAG chat agent so listeners can query 18 years of episodes instead of scrolling a feed.

This is the one that has been in production the longest, and it taught me the most. Two parts were hard.

Generation quality on titles and show notes is deceptively difficult because a human who listened to the episode will immediately know when the summary is wrong. There is no hiding behind plausible output. A show note that is 80 percent right reads as careless, not as impressive.

Harder still was getting the system to recognize things mentioned in an episode and link to them. Someone says a library name, a book, a person, a company, and the transcript has it slightly wrong because that is what speech recognition does with proper nouns. Recognizing that a thing was referenced at all, working out which thing it was, and linking to the right one is a chain where every step can fail quietly. It is the part of the pipeline I have spent the most time on.

Underneath both of those sits a less glamorous problem: working out which model to use for which job. Model choice is not a spec sheet decision. The one that writes the best show notes is not the one that does the best entity extraction, and neither is necessarily the one worth paying for at 4,600 episodes. Most of what I know about this came from trial and error across a large corpus, and a lot of prompt iteration on top of it. When I tell a client a particular model fits their job, it is because I have run the comparison, not because I read a benchmark.

### LegiBill

[legibill.app](https://legibill.app) is a research assistant for the Utah legislature. You can ask a question about any individual bill, or about the whole session, and get an answer drawn only from the bill text with citations back to it. It is in beta right now. If you work on Utah legislation and it would be useful to you, email me and I will get you in.

The hard parts were grounding and chunking. Legislative text does not divide neatly, and an answer that cites the wrong section is worse than no answer at all in this domain. I made citation a hard requirement rather than a nice-to-have, then built feedback mechanisms that surface failures in an admin interface so they can be reviewed and the output refined. That last piece is the one most people skip. Retrieval is straightforward; knowing when your system got it wrong is not.

### BossVoice

BossVoice is a planning and accountability tool built around the 12 Week Year, currently in beta. You work through what you want to accomplish in a twelve week cycle, break it into strategies and tactics, schedule the blocks to actually do it, and check in with AI coaches along the way.

Three things have been genuinely hard. The first is handoff between the coaching, scheduling, and accountability agents, which I am still working through.

The second is getting a model to give real critical feedback. Models are trained to be agreeable, so the default behavior is to nod along while you plan four impossible things for a twelve week cycle. A coach that does that is worse than no coach. Getting useful pushback on overloading means working against how the model wants to behave, not adding a feature on top of it.

The third is teaching it to tell long term vision apart from short term planning. Those are different kinds of thinking, and a model will happily blur them: it turns a three year ambition into next Tuesday's task list, or answers a concrete scheduling question with something inspirational. Keeping the two straight, and knowing which one the user is actually doing right now, took more work than any other part of the coaching logic.

### Podaroo

Podaroo is a podcast player with a transcription engine behind it, still in progress. Once an episode is transcribed you can ask the player to find the part where something was discussed and play that stretch, build a playlist across shows on a topic, or get recommendations based on what you actually want to hear rather than what is trending.

The interesting problem here has been economics rather than architecture. Transcription costs real money, and transcribing every episode of every show before anyone has signed up is a good way to spend a lot on a corpus nobody asked for. So transcription is selective and pay gated, which means the paywall funds the corpus and the corpus grows as more people join. Every subscriber makes the product better for the ones after them. The goal is to reach a transcribed backlog of the shows people keep asking for, at which point the selectiveness can go away.

That tradeoff is worth mentioning because it comes up constantly in client work. Plenty of AI features work fine in a demo and fall apart the moment you multiply them by real usage. Knowing what a feature costs to run is part of designing it, not something to discover after launch.

## Working together

Most engagements start with a call where you tell me what you are trying to do and I tell you whether I think it is the right thing to build. Sometimes that conversation ends with a smaller project than you came in with, or none at all, which is a fine outcome.

From there it is usually either a scoped build, or a stretch of advisory work with your team doing the building. I am one person, so I take on work I can actually finish, and I will say so when something needs a bigger shop than me.
