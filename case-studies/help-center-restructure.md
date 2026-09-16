---
layout: case-study
title: "Restructuring a help center around what readers are trying to do"
description: "Restructured nine categories of a 500-article help center around what readers are trying to do."
tags: ["Information architecture", "Diátaxis"]
---

# Case study: restructuring a help center around what readers are trying to do

**Stephanie Coulter · DNSimple, a domain registrar · January – September 2026**

A developer-facing help center of more than 500 articles had grown one article at a time, with no shared rule for what kind of article went where. I led a category-by-category restructure around the Diátaxis framework, from the written standard to a hub page for every category, and restructured nine categories over nine months.

---

## The problem

Readers arrive with different needs. Someone who wants to *do* something needs steps. Someone who wants to *understand* something needs an explanation. Someone who needs an exact value needs a reference table. When one article tries to do all three, it does none of them well, and a search or AI tool that pulls one passage out of it gets a mix of all three.

The categories had the same problem at a larger scale. There was no consistent place to look for "how do I", "what is", or "what are the exact limits", and each new article was filed wherever it seemed to fit.

## What I did

**1. Wrote the standard down first.** The team had adopted Diátaxis, which sorts documentation by reader intent: tutorials, how-to guides, reference, and explanation. I added it to the contributing guidelines, required sub-categories to follow those article types, and made two summary fields mandatory on every article, one for readers and one for search and AI engines ([#1747](https://github.com/dnsimple/dnsimple-support/pull/1747)). The site also needed nested categories to hold the new structure ([#1760](https://github.com/dnsimple/dnsimple-support/pull/1760)).

**2. Restructured one category at a time.** Each category followed the same pattern: split mixed articles by intent, write the missing explanation and reference articles, regroup the category into sections, and add a pillar page that orients a reader and links out to everything else.

| Category | Examples |
|---|---|
| DNS and DNSSEC | Nested sub-categories ([#1758](https://github.com/dnsimple/dnsimple-support/pull/1758)) |
| Domains, Transfers, and TLDs | How-to and reference articles, a new TLDs category, pillar pages ([#1786](https://github.com/dnsimple/dnsimple-support/pull/1786)) |
| SSL certificates | Explanation articles ([#1810](https://github.com/dnsimple/dnsimple-support/pull/1810)), then how-to, reference, glossary, and troubleshooting in coordinated releases ([#1825](https://github.com/dnsimple/dnsimple-support/pull/1825)), and a follow-up audit across 52 files ([#1849](https://github.com/dnsimple/dnsimple-support/pull/1849)) |
| Name servers | Restructured into getting started, explanation, and how-to sections, with a glossary ([#1915](https://github.com/dnsimple/dnsimple-support/pull/1915)) |
| Contacts, WHOIS Privacy, Templates, Connectors | Restructures, new articles, and four pillar pages in one coordinated set of changes ([#2048](https://github.com/dnsimple/dnsimple-support/pull/2048)) |

**3. Went back for consistency.** A restructure done over nine months drifts. I aligned article headings with their titles ([#2096](https://github.com/dnsimple/dnsimple-support/pull/2096)), brought the pillar pages into line with each other ([#2136](https://github.com/dnsimple/dnsimple-support/pull/2136)), and then wrote the pillar page convention into the rules ([#2137](https://github.com/dnsimple/dnsimple-support/pull/2137)). The shape of a pillar page had existed only as precedent inside the pages themselves, which is how it drifted. The new rule includes the one requirement that keeps a pillar current: a new article gets added to its category's pillar in the same change.

## What didn't work the first time

The first pass at the name servers category was six pull requests in January, and they were closed unmerged. The category was restructured again in May, after the pattern had been worked out on other categories.

## What shipped

- **Nine categories restructured:** DNS, DNSSEC, Domains and Transfers, SSL certificates, Name Servers, Contacts, WHOIS Privacy, Templates, and Connectors. Secondary DNS is in progress
- **A pillar page for each**, following one written convention
- **The standard in the contributing guidelines and the AI writing rules,** so new articles, including AI-drafted ones, start in the right shape

All of it is in the public [dnsimple-support](https://github.com/dnsimple/dnsimple-support) repository.

## What I'd carry to another team

- **Write the standard before the content.** Restructuring without one produces a new, different inconsistency.
- **One category at a time, same pattern each time.** Each finished category becomes the example for the next.
- **Plan a consistency pass.** Long projects drift, and the pass is part of the work, not a cleanup after it.
- **If a convention only exists in the pages, write it down.** Precedent doesn't survive the next person, or the next AI draft.
