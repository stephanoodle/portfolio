---
layout: case-study
title: "Matching the help center to the words customers use"
description: "Decided the terms a help center uses, checked them against how customers write, and measured search before and after."
tags: ["Terminology", "Search", "Evaluation"]
---

# Case study: matching the help center to the words customers use

**Stephanie Coulter · DNSimple, a domain registrar · September 2026**

Customers asked for the same thing using four or five different names, and the help center used several of them too. Search and AI tools match words, so a question worded one way could miss the article written another way. I decided which terms the documentation should use, checked those decisions against how customers actually write, and measured retrieval before and after the change, on our own evaluation and on the live site search.

---

## The problem

Moving a domain to another registrar needs a code from the current registrar. The help center called it a *transfer code*, *authorization code*, *auth code*, *auth info*, and *EPP code*, and no one name was used in most articles. Another term was ambiguous in a way that mattered: *transfer* meant moving a domain to another registrar in some articles, and moving it between two accounts at DNSimple in others. Those are different processes with different consequences.

Transfers are the policy-sensitive part of a registrar's documentation. A wrong answer there is a compliance problem, not just an inconvenience, and it was the group of questions where earlier search changes had made no difference.

## What I did

**1. Found where the documentation disagreed with itself.** I counted every variant of each term across the help center and ranked them: policy-sensitive terms first, then terms on the pages AI assistants cite most, then terms that were consistent but could drift.

**2. Decided each variant, one of three ways.**

| Decision | Meaning | Example |
|---|---|---|
| **Rewrite** | The variant is drift. Replace it | *sub-domain* → *subdomain* |
| **Alias** | Keep it, but name it once, on first mention | *authorization code (also called auth code, EPP code, transfer code, or auth info)* |
| **Distinct** | Not a synonym. Write down the difference | *transfer* is registrar to registrar; *move* is account to account |

The alias category is the important one. A blanket find-and-replace looks tidy, but it deletes the exact words customers search with, and those searches then find nothing.

**3. Checked the decisions against how customers write.** Before rewriting anything, I searched the first message of every support ticket since January 2025 for the terms. Two things changed the plan:

- **All four common names for the code were in real use.** That confirmed keeping them as aliases, and it corrected an early proposal to deprecate *EPP code*, which customers and registries still use every day.
- **Customers call an account move a transfer.** Removing the word *transfer* from the account-move article would have made it harder to find. So the article names it once — *"sometimes called a transfer between accounts"* — and says *move* everywhere else.

The ticket search also turned up two gaps no article covered: an error message customers were seeing, and an old interface label, *Domain Push Identifier*, that a partner still used in its instructions long after the product renamed it.

**4. Measured before changing anything.** The existing evaluation set had no questions about the code at all, so re-running it would have shown nothing. I built a new set of real customer questions from those tickets and recorded a baseline on the unchanged documentation.

**5. Made the change, then measured again, twice.**

- **Retrieval evaluation:** the same question set, re-run after the rewrites.
- **Live site search:** the site search matches differently from the evaluation, so I tested it separately with short queries, the way people type into a search box. There was no saved copy of the search index from before the change, so I rebuilt it from version control, then confirmed the rebuild by checking that the rebuilt *after* version scored exactly like the live site.

## What shipped

All in the public [dnsimple-support](https://github.com/dnsimple/dnsimple-support) repository:

- [**#2148**](https://github.com/dnsimple/dnsimple-support/pull/2148) — a preferred-terms table in the writing rules that AI-assisted drafting follows, so new articles start with the right terms
- [**#2149**](https://github.com/dnsimple/dnsimple-support/pull/2149) — the rewrites across 13 articles: *authorization code* with its aliases, *move* for account-to-account, a new section for the unexplained error, and the old interface label named once. No URLs changed, and existing links to renamed sections still work
- [**#2147**](https://github.com/dnsimple/dnsimple-support/pull/2147) — a deprecated product name removed from the billing article
- [**#2150**](https://github.com/dnsimple/dnsimple-support/pull/2150) — exact-match search pins for short queries that fuzzy matching still ranked badly

## Results

- **Retrieval improved on both the evaluation and the live search.** The biggest gain was short searches finding the right article somewhere in the top three.
- **Searches that returned nothing now land first.** On the live site, searching *authorization code* now returns the authorization code article first, and so does the partner's old label.
- **Two searches got slightly worse.** *Transfer code* and *EPP code* each dropped a place, because the reference article's title no longer says *Transfer Code* and the site search weighs titles most. That was an expected cost of the decision.
- **Some short searches still missed,** and no wording change could fix them: the site's fuzzy matching put a discount-codes article first for *auth code*. Those needed search pins, not rewrites.
- **The original evaluation set didn't move,** because it barely touched these topics. Measuring the change needed questions about the change.

## What the measurement can and can't tell you

- **It shows the right article now surfaces for the words customers use.** It doesn't show that AI assistants answer more accurately. That needs a separate test of the answers themselves.
- **The short search queries were written from ticket language,** not taken from search analytics, because the analytics had almost no searches on these topics. They show direction, not traffic-weighted impact.
- **Part of the account-move gain came from a second pass after seeing the first results:** one sentence describing why people move domains, in the words customers use. That's a normal editing loop, but it means the held-back test questions weren't fully independent.

## What I'd carry to another team

- **Measure before you change anything, with questions about the thing you're changing.** A general benchmark can hide a real improvement.
- **Aliases beat purges.** Pick one term, and name the others once.
- **Tickets are the dictionary.** How customers phrase a problem, before we teach them our words, decides what they search for.
- **Put the rules where the writing happens.** A style guide nobody opens drifts. Writing rules that AI-assisted drafting reads apply to every new article.
- **Report what didn't work.** Two searches got worse, and some needed a different fix. Saying so is what makes the rest believable.
