---
layout: case-study
title: "Rules for AI-drafted documentation, and why rules aren't enough"
description: "Wrote the rules AI follows when drafting documentation, then audited them and found why rules aren't enough."
tags: ["AI governance", "Docs as code"]
---

# Case study: rules for AI-drafted documentation, and why rules aren't enough

**Stephanie Coulter · DNSimple, a domain registrar · February – September 2026**

The support team drafts help center articles with AI coding assistants. Early drafts read as machine-written, and nothing checked whether a draft's product claims were true. I wrote the rules the assistants follow — voice, structure, and a policy that every product claim must be verified — and applied them across three documentation categories. Then I audited my own rules and found the harder problem: a rule written down is not a rule enforced.

---

## The problem

AI assistants follow whatever rule files are in the repository. Without them, drafts come back with the recognizable habits of generated text: throat-clearing openers, filler phrases, stacked synonyms, a recap at the end. Those are cosmetic. The serious risk is a confident, plausible, wrong statement about a price, a limit, or a policy, in documentation for a domain registrar, where some of those statements carry compliance obligations.

## What I did

**1. Wrote the rules.** The rules cover how an article should read, how it should be structured, and the workflow checkpoints around drafting and review, along with updated contribution guidelines and a pull request template ([#1815](https://github.com/dnsimple/dnsimple-support/pull/1815)). They name the specific patterns that make text read as generated, with a rewrite for each.

**2. Applied them to existing content.** Rules that only apply to new articles leave the rest of the site sounding different. I rewrote the DNS, DNSSEC, and Domains and Transfers categories against them ([#1816](https://github.com/dnsimple/dnsimple-support/pull/1816)), and kept tightening the rules as patterns showed up, such as banning em and en dashes ([#1865](https://github.com/dnsimple/dnsimple-support/pull/1865)).

**3. Added a content policy.** The policy requires verifying every product claim, price, limit, and syntax example against the app, the developer documentation, or a subject-matter expert ([#2025](https://github.com/dnsimple/dnsimple-support/pull/2025)).

**4. Audited the rules I'd written.** The structure was sound: one source of truth, other files pointing to it rather than restating it. Three findings were not:

- **The policy contradicted the repository.** It said the site had no `llms.txt` file and shouldn't gain one. The site had one, live in production, and I had rewritten it two months earlier. Both files were mine. Better I found it than someone else did. I corrected the policy to say the file exists, that Google's guidance covers only Google, and that measurement should decide whether to expand it ([#2151](https://github.com/dnsimple/dnsimple-support/pull/2151)).
- **The verification rule had no mechanism behind it.** Nothing checked whether claims were verified, and nothing measured whether the documentation produced correct answers. The evidence was my own cleanup commits: accuracy fixes made by hand, after the fact.
- **Rules only reach people who have the latest copy.** An assistant working from an out-of-date copy of the repository applies out-of-date rules, including the rule that says to update first. That makes weaker drafts a distribution problem, not a skill problem, and it can only be fixed on the server side, for example by requiring branches to be current before merging.

**5. Moved rules toward things that check themselves.** The audit's conclusion was to convert prose rules into automation wherever possible: linting for the mechanical rules, and measurement for the verification rule. The measurement became the retrieval evaluation in [Measuring whether documentation answers correctly](measuring-answer-quality.md). The same approach put a preferred-terms table into the rules in September ([#2148](https://github.com/dnsimple/dnsimple-support/pull/2148)), so AI drafts start with the right terminology instead of being corrected later.

## What shipped

- **Writing rules, workflow checkpoints, and a pull request template** that AI assistants and people both follow
- **Three categories rewritten** to the rules
- **A content policy** requiring every product claim to be verified
- **An audit** with concrete fixes, several of them server-side because a local fix can't reach an out-of-date copy

## What I'd carry to another team

- **Name the patterns, with rewrites.** "Sound human" isn't actionable. "Don't open with 'In this article'; start with the answer" is.
- **Audit your own rules.** Mine contradicted production, and I wrote both.
- **A rule without a check is a hope.** Decide which rules a linter can enforce, and measure the ones it can't.
- **Check how rules are delivered.** If the rule arrives by updating, anyone who hasn't updated never gets it.
- **Separate a distribution problem from a people problem** before anyone has a conversation about performance.
