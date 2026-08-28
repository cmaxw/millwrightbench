---
title: "Policy"
description: "How AI systems actually work, and what that means for the people writing AI legislation. Technical perspective from an engineer who builds these systems."
layout: "standard"
draft: false
params:
  cta:
    line: >-
      If you're working on AI legislation and want a technical read on
      something, I'm at
      [chuck@millwrightbench.com](mailto:chuck@millwrightbench.com).
    label: ""
    url: ""
---

AI policy is where government puts guardrails on technology so that people are protected. It is also where government decides what it will allow itself to do: whether it enables or restrains its own use of these systems, and its own use of the data it has already collected about people.

Both halves matter, and the second one gets far less attention than it deserves.

The early rules matter more than the ones that come later. Not because anyone can predict where this technology goes, but because the frame set now is the frame everything gets adjusted from. Definitions written today will still be doing work in ten years, in situations nobody has thought of yet. Getting the structure roughly right while it is still early is worth more than getting the details exactly right about the systems we happen to have this year.

## The gap between the technology and the debate

Most people writing AI legislation are working from headlines, and most people who understand how these systems behave are not in the room. That gap produces rules that sound decisive and do not survive contact with software.

It shows up in specific ways. Definitions that catch far more or far less than intended, because "artificial intelligence" is genuinely hard to define in statute and the obvious formulations either sweep in a spreadsheet or exclude next year's model. Requirements that assume a system knows something it does not. Obligations written as though a model behaves consistently, when the same prompt can produce different answers on different days. Rules aimed at model capability when most real harm shows up further down, in how a system gets wired into a business and what happens when it fails at three in the morning.

None of that comes from anyone acting in bad faith. It comes from a vocabulary problem. The words available to describe these systems in public were mostly written by people selling them.

## How I think about AI and legislation

<!-- VERIFY: this is drafted from things you have said plus the engineering
     reality, and it is the section a staffer will judge the page on. Read it
     as though someone else wrote it, because someone else did. Cut anything
     that is not actually your view. Sharpen it with real examples from the
     Utah bills once you have read them. -->

I do not have a general theory about how much regulation is right. That is a question for the people who were elected to answer it. What I can say is which rules turn into working software and which ones do not, because I have had to build against requirements like these.

A few things I keep running into.

**Rules about observable behavior hold up. Rules about internal mechanism do not.** You can check what a system did. You can log it, audit it, and hold somebody to it. You cannot meaningfully check what a model "understood" or "intended," because those words do not describe anything the software actually has. A requirement written in terms of the second kind is unenforceable no matter how strongly it is worded.

**Anything that assumes consistency will break.** The same input can produce different output on different days. If a statute requires that a system always does something, that guarantee has to be built in the deterministic code around the model, not asked of the model itself. That is a real and achievable engineering requirement, but only if the rule is written knowing it is one.

**Do not require a system to know something it cannot know.** Whether a user is a minor, what they intend, whether they are in crisis: these are inferences with error rates, not facts a system possesses. Rules that treat them as known quantities put a company in the position of either guessing or collecting far more personal data to reduce the guessing. That second outcome is usually worse than the problem the rule was aimed at, and it is rarely the one anybody intended.

**Definitions carry the most weight and get the least attention.** Every substantive obligation in a bill hangs off what counts as "artificial intelligence" or an "AI system." The obvious formulations either sweep in ordinary software or fail to describe what ships next year. This is the single highest-leverage place to get technical input, and it is usually settled before anyone technical is asked.

**The deployment layer is where enforcement can actually reach.** Rules aimed at model developers land on companies that may be anywhere and may not have anticipated your use case. Rules aimed at whoever put the system in front of a customer land on someone identifiable, accountable, and within reach. That is also where most real harm occurs.

**Logging and provenance requirements work unusually well** for the same reason. They are checkable. A rule that produces an artifact somebody can later inspect is worth several that depend on good intentions.

**Do not write rules ahead of the capacity to enforce them.** The EU deferred its high-risk obligations from August 2026 to December 2027, in part because the technical standards were not finished and Member States had not designated the authorities meant to do the enforcing. That is worth studying regardless of what you think of their approach. A deadline that arrives before the machinery does damages the credibility of the whole framework.

## What I follow closely

**Government use of AI, and government use of data it already holds.** The half of this that gets least attention. Agencies deploying these systems, and what happens when AI is pointed at records collected for some other purpose.

**Disclosure regimes and what they ask of software.** Utah's approach, and how it compares to the alternatives. This is where the gap between statutory language and system behavior is widest.

**Model capability and its limits.** What these systems can actually do, as opposed to what the marketing and the alarm both suggest.

**The deployment layer.** Where a system is wired into a business, who is accountable when it fails, and why most real harm shows up here rather than in the model.

**State activity, starting with Utah.** The nine bills from the 2026 session and whatever follows them.

**The EU, as a comparison case.** Not because it should be copied, but because it is the largest running experiment in regulating these systems and its stumbles are informative.

<!-- Add a "## Related writing" section here once there are two or three policy
     pieces in /writing/ worth linking. Leaving it out until then, since an
     empty section advertises that nothing has been written. -->

