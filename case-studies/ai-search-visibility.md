---
layout: case-study
title: "Measuring how often AI answers cite the help center"
description: "Found about 5 million AI-answer citations a quarter in dashboards nobody had opened, and the question none of them can answer."
tags: ["AI search", "Analytics", "Technical SEO"]
---

# Case study: measuring how often AI answers cite the help center

**Stephanie Coulter · Help center for a domain registrar · April – August 2026**

When someone asks ChatGPT or Google how to transfer a domain or what an SSL certificate chain is, is the company's help center the source, and is the answer right? Nobody owned that question. I pulled the AI-search data from two analytics tools the company already paid for, which nobody had opened for this. I fixed the technical faults the site audits turned up, and wrote a plan that separates what can be improved from what can only be guessed at.

---

## The problem

AI assistants increasingly answer customers' questions before they ever reach a help center. A documentation team can't see this from its own analytics. A citation inside an AI answer often produces no visit at all. And at a registrar, a confident wrong answer about transfer policy, with the company's name beside it, is worse than no citation.

## What I did

**1. Looked in the tools already paid for.** Google Search Console has a beta report for generative AI features. Ahrefs Web Analytics separates out traffic referred by AI assistants. Neither had been looked at for this.

**2. Read the definitions before the numbers.** Google defines an impression here as a link to the site shown to a user inside an AI feature. That makes it a citation measure. It doesn't show whether the help center's content composed the answer, whether anyone opened the link, or whether the answer was correct.

**3. Fixed what the site audits found.** Ahrefs and Search Console audits turned up meta descriptions and titles out of range, 34 orphan pages, a sitemap returning a server error, and an infinite redirect loop in the hosting redirect rules. I fixed them in the docs repository, rewrote the site's `llms.txt` for spec compliance, and confirmed `robots.txt` didn't block any AI crawler.

**4. Wrote a plan tagged by confidence.** Each step was marked established, plausible, or speculative. The plan split the work in two: *be retrievable* (crawlable, quotable, consistently worded), which is mostly known practice, and *be right*, which nobody measures.

## What it found

- **About 5 million citations in one quarter.** Google showed a link to the help center inside an AI answer about 5 million times in under three months. None of those answers had ever been checked for correctness.
- **About half came from one article.** A single explanation article about SSL certificates carried roughly half of all AI exposure. If it's ambiguous anywhere, it's ambiguous at a scale nothing else in the help center approaches. That makes it the first article to audit.
- **AI cites explanations, not how-tos.** Every top page in both tools was concept content: what a certificate chain is, how two DNS record types differ. That tied the help center restructure, which separated explanation from how-to, directly to the AI channel.
- **One assistant dominated.** ChatGPT sent nearly three quarters of AI-referred visitors. A correctness test only needs to cover one assistant well to cover most of the exposure.
- **The structured-data machinery was built and unused.** The site could emit machine-readable question-and-answer markup, and one article out of about 520 used it.

## What the numbers can't tell you

- **Impressions aren't clicks.** About 5 million citations against about a thousand AI-referred visitors in a year suggests most exposure never becomes a visit. But the two tools count different things, so that ratio isn't measured yet. The click-through data from the same report comes next.
- **The Google report is in beta.** Treat its figure as an order of magnitude.
- **No dashboard says whether the answer was right.** Search Console can tell you how often you're cited. Nothing in it can tell you whether the answer beside your name was correct.

The next step is the one that closes that gap. Audit the top article line by line against how the product and the protocol actually behave. Then run a set of real customer questions against ChatGPT, and score two things separately: whether the help center is cited, and whether the answer is right.

## What I'd carry to another team

- **Check the tools you already pay for.** The whole baseline came from two of them.
- **Read the metric's definition before quoting it.** "Impressions" in an AI report means something narrower than it sounds.
- **Find the concentration.** When half the exposure sits on one page, that page is where an hour of review does the most.
- **Separate what you can control from what you can't.** How AI engines choose sources is opaque and changes without notice. Whether the content they find is accurate, consistently worded, and easy to quote is not.
- **Don't build a case on `llms.txt`.** Keep it current, because it's cheap. Google has said it doesn't use it, and there's no evidence it moves anything.
