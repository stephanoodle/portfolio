---
layout: case-study
title: "Measuring whether documentation answers correctly"
description: "Built an evaluation from real customer questions, and let the data correct my conclusions twice."
tags: ["Evaluation", "Search", "AI retrieval"]
---

# Case study: measuring whether documentation answers correctly

**Stephanie Coulter · DNSimple, a domain registrar · July – September 2026**

Nothing measured whether the help center gave people the right answer, whether the reader was a customer typing into the search box or an AI assistant looking something up. I built an evaluation from real customer questions, measured the live site search, and read six months of search analytics nobody had opened. The measurement proved two of my own conclusions wrong before it produced one worth reporting, and it stopped a plausible search change from shipping.

---

## The problem

Documentation teams ship articles, but rarely know whether the right article reaches the person asking. That matters twice over now: customers still search, and AI assistants increasingly answer on the company's behalf using the same content. At a registrar, the questions where a wrong answer costs the most are the policy ones: transfers, disputes, registration data.

## What I did

**1. Built a retrieval evaluation from real questions.** Every question came from a support ticket, not from imagination. The correct article for each was assigned by reading the documentation, never by looking at what search returned. Questions were tagged routine or policy-sensitive, and a third were held back and never looked at while fixing anything, so improvements could be checked for tuning to the test.

**2. Didn't trust the first number.** The first run scored almost nothing. The cause was the labels, not the search: the automatic extraction had matched a certificate question to an API article, because that was the first link an agent happened to send in the thread. Every question got a human review before anything was scored.

**3. Audited how the live search works.** The site search is a fuzzy-matching library running in the browser. Reading its configuration showed that the summary field every article is written to include — written specifically as a direct answer for search and AI engines — wasn't searched at all. It also showed that curated pinned results only fired on an exact, full-query match.

**4. Tested fixes one at a time.** I had proposed three changes as a bundle. Measured separately:

- **Weighting the fields,** which looked obviously right, made results worse
- **A minimum match length** changed nothing
- **Indexing the summary field alone** did best of the six configurations, and the full bundle did worse than that one change on its own

**5. Checked the queries against real traffic, and corrected myself again.** My test queries averaged four words. Six months of search analytics showed real searches average under two, most of them one word. On realistic queries, the summary-field change was flat to slightly negative. So the pull request for it stayed in draft and was never merged ([#2073](https://github.com/dnsimple/dnsimple-support/pull/2073)).

The analytics had their own problems: about a third of the logged "searches" weren't searches at all, but page paths and half-typed words. Anyone reading that dashboard would have drawn the wrong conclusions about what customers look for.

## What it found

- **The search box works for how people actually use it.** Short queries find the right article.
- **Full-sentence questions, the way people ask AI assistants, retrieved about an order of magnitude worse** on the same content with the same configuration. The gap is in natural-language retrieval, not in the search box.
- **Policy-sensitive questions didn't move with any configuration change.** That segment needed terminology work, not a setting. That work is the follow-up case study: [Matching the help center to the words customers use](controlled-vocabulary.md), which moved it.
- **A repeating pattern:** a correct decision, written down, that nothing downstream uses. The unsearched summary field, pins that rarely fire, analytics nobody read.

## What the measurement can't tell you

Retrieval is the floor, not the answer. If the right article doesn't surface, no assistant can answer from it. But an article surfacing doesn't prove the answer built from it is correct. That needs a separate test of the answers themselves.

## What I'd carry to another team

- **Real questions, human-checked labels, a holdout set.** Each one closes a specific way to fool yourself.
- **Test changes one at a time.** The thorough-looking bundle was worse than the one-line change.
- **Match the test to the traffic.** A search box and an AI assistant get differently shaped questions, and scoring one with the other's produces a confident, meaningless number.
- **Read the analytics before trusting them.** A third of these weren't searches.
- **Keep the corrections in the record.** A number that survived two rounds of being wrong is worth more than one reported the first time.
