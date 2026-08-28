---
title: "Compliance"
description: "Utah passed nine AI bills in 2026, covering schools, health care, deepfakes, companion chatbots, and age verification. The technical half of what they require."
layout: "standard"
draft: false
params:
  cta:
    line: >-
      If you're not sure where your systems land against the new statutes, a
      short call will usually tell you whether you have a real problem or not.
---

Utah has been writing AI law faster than almost any other state. The Artificial Intelligence Policy Act landed in 2024, got amended in 2025, and the 2026 session sent another nine AI bills to the governor. If you run a business here that touches AI anywhere, the rules changed underneath you and probably more than once.

I am not a lawyer and nothing here is legal advice. What I do is the technical half of the question, which is usually the half nobody has answered: what your systems actually do, in detail, written down clearly enough that your attorney can reason about the real thing instead of a summary someone wrote from memory. Most compliance problems I have seen are not disagreements about the law. They are cases where nobody could say precisely what the software was doing.

## Who this is for

Schools and districts working out what the classroom technology rules mean for the tools teachers are already using. Health care providers and insurers whose systems touch patient interaction or prior authorization. Anyone shipping a chatbot, particularly one that talks to minors or wanders anywhere near mental health. Businesses that generate or alter images and now have provenance obligations. And any company with a support bot, an intake form, or an internal tool that quietly became an AI system over the last two years without anyone deciding it had.

If you are reading this thinking "I do not think any of this applies to us," that is worth thirty minutes of somebody's time to confirm. The disclosure rules in particular catch companies that do not think of themselves as AI companies at all.

## What Utah passed in 2026

<!-- VERIFY: check every bill number, title, scope and effective date against the
     enrolled text at le.utah.gov before publishing. Session attribution on a few
     of these is genuinely murky in secondary sources. Getting this wrong on the
     page that is supposed to demonstrate you know the material is the one
     unrecoverable mistake here. -->

Start with the baseline, because the 2026 bills sit on top of it rather than replacing it.

**The Artificial Intelligence Policy Act (SB 149, 2024)** is the foundation. If a consumer clearly asks whether they are talking to a person or a machine, you have to tell them. Businesses in regulated occupations, the ones needing a Utah license or state certification, have a higher bar: they disclose up front, without being asked. **SB 226 (2025)** tightened this for higher-risk interactions, including those involving health, financial, or biometric data. **SB 332 (2025)** extended the Act's sunset.

The 2026 session then covered four areas:

**Schools and classroom technology.** HB 273 requires local education agencies, working through the State Board of Education, to adopt model policies on technology and AI in public school classrooms, effective July 1, 2026. SB 322 addresses AI in education grants.

**Deepfakes, provenance, and digital identity.** HB 276 enacts deepfake protections and requires AI operators to embed provenance data so a viewer can determine whether an image was AI-created or altered. SB 256 addresses misuse of personal identity and digitally created content.

**Health care and insurance.** SB 319 requires health insurers to disclose whether AI is used in reviewing prior authorization, to the Insurance Department, to providers, and to enrollees. HB 452 governs mental health chatbots, with real restrictions on what such a system may do and how it must handle a user in crisis.

**Chatbots and minors.** HB 438 addresses companion chatbots, including safety protocols and reporting. Separate legislation covers age verification and age gating for sites offering material harmful to minors.

**HB 320** amends the Office of Artificial Intelligence Policy, the state body that administers the regulatory sandbox and works with businesses on how the rules apply to novel products. Worth knowing about: the sandbox is a route to certainty that most companies do not realize exists.

## What the laws actually require of a system

Statutes describe outcomes. Software has to implement behavior. The gap between those two is where the actual work sits, and it is wider than it looks.

Take disclosure. "Disclose when asked" sounds like a one-line change until you ask the follow-up questions. What counts as being asked? A user typing "are you a bot" is obvious. What about "is this a real person"? Does your system detect either one, or does it answer from the model's own sense of what to say, which means the answer changes run to run? Does the disclosure survive a conversation being resumed the next day? If the interaction moves from chat to email, does it carry? Most systems I have looked at do not handle this reliably, not because anyone decided against it, but because nobody specified it.

Provenance obligations are similar. Embedding provenance data means picking a standard, deciding what happens when an image is resized or re-encoded or passed through a third-party tool that strips metadata, and knowing whether your pipeline preserves or destroys it. That is a question about your image handling code, and you cannot answer it from the outside.

Age gating raises the question of what your system actually knows about a user's age and when it knows it. Companion chatbot rules raise the harder one of what makes a system a "companion" at all, which is a design question the statute cannot fully settle for you.

Where the statutes are genuinely ambiguous about implementation, I will say so rather than inventing certainty. Some of these questions do not have clean answers yet, and the honest response is to document your reasoning, make a defensible choice, and be able to show your work later.

## What a technical review covers

I start with an inventory: every place AI touches your product or your operations, including the ones that arrived through a vendor and never got reviewed. Then, for each one, what it does with user data, what it says to users, what it logs, and who can see the output.

From there I work out which statutes plausibly reach it, and write up where your systems line up with those requirements and where they do not. The deliverable is a document your attorney can actually use: specific about system behavior, honest about what is uncertain, and organized so the legal questions are separated from the engineering ones.

Most of these engagements run two to four weeks. The findings usually split into things you can fix in an afternoon and things that need a real decision from someone senior. Both are worth knowing about before somebody else finds them.

## What this is not

This is not legal advice, it is not a legal opinion, and it does not replace counsel. I am an engineer, not an attorney.

What it does is establish what your systems actually do, in writing, so that your lawyers are reasoning about the real thing instead of a description. In my experience that is where compliance work goes wrong: the legal analysis is fine, but it was performed on an inaccurate picture of the software. If you do not have counsel on this yet, I am happy to point you toward Utah firms doing serious AI and privacy work.

## Working together

The first conversation is thirty minutes and free. Tell me where AI shows up in your business and I will tell you whether I think you have a real exposure or not. Sometimes the answer is that you are fine and you should stop worrying about it, which is a perfectly good outcome for a phone call.

If it is easier to write than to schedule, I am at [chuck@millwrightbench.com](mailto:chuck@millwrightbench.com).
