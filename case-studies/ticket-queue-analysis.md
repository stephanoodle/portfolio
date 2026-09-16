---
layout: case-study
title: "Reading a support queue for retention"
description: "Applied churn and data-quality frameworks to twenty months of support tickets."
tags: ["Support data", "Retention"]
---

# Case study: reading a support queue for retention

**Stephanie Coulter · DNSimple, a domain registrar · August 2026**

A support queue records why customers get in touch, but nobody was reading it for who might be about to leave. I took the churn and data-quality frameworks from my customer success certifications and applied them to twenty months of support tickets. A sizeable share of contact turned out to be retention-related, nothing in the process acted on it, and the ticket tags couldn't support the analysis until they were fixed.

---

## The problem

Support teams usually count tickets by topic. That answers "what are people asking about?" but not "who is about to leave, and why?" Payment failures, expiring domains, transfers to another provider, and cancellation requests all pass through support first, but they're handled one at a time and never added up.

## What I did

**Worked from tags and timestamps only.** About 6,000 tickets across 181 tags, over twenty months. No message bodies were read, so no customer details entered the analysis.

**Applied four frameworks:**

| Framework | Source | Used for |
|---|---|---|
| **The four types of churn** — voluntary, involuntary, happy, fake | Customer Retention Certified: Masters | Mapping tags to churn types, to measure retention pressure in the queue |
| **The six dimensions of data quality** | Customer Success Metrics Certified: Masters | Scoring the tag vocabulary itself, since every count depends on it |
| **The four types of retention analytics** — descriptive to prescriptive | Customer Retention Certified: Masters | Placing the support function on that ladder, to show why it was stuck reacting |
| **The feedback loop** — ask, categorize, act, follow up | Customer Success Metrics Certified: Masters | Finding where the loop broke |

## What it found

- **A meaningful share of all contact was retention-shaped,** split between involuntary causes, such as failed payments and expiring domains, and voluntary ones, such as transfers out and cancellations. Nothing in the process acted on either.
- **Voluntary-shaped contact rose sharply over one winter.** A leading indicator had been sitting in the data the whole time.
- **The tag vocabulary couldn't carry the analysis.** Every ticket was tagged, but duplicate and malformed tags were common, and the tag meant for churn had barely been used against hundreds of transfer-out tickets.
- **The feedback loop broke after asking.** Feedback was collected. Acting on it and following up didn't happen.
- **Involuntary churn was already fully recorded** in the application database, and nobody read it.

## What came out of it

- **A data-quality scorecard** for the ticket tags, and a proposed merge list
- **Two playbooks:** one for saving customers at risk of involuntary churn, and one for transfer-out requests
- **Specs for the real churn analyses,** naming the data they need, ready for when access to billing and account data exists

## The limits, stated

**A ticket is not a churn event.** A question about transferring out isn't a lost domain. Real churn rates need billing and account data a support team often can't query, which is why the last step was writing specs rather than reporting a churn rate.

## What I'd carry to another team

1. **Export tags and timestamps only,** unless message bodies have been scrubbed of customer details.
2. **Map tags to churn types.** Report happy and fake churn as unmeasurable rather than forcing them into a bucket.
3. **Score the tag vocabulary** before trusting any count built on it.
4. **Chart the monthly trend, not just the total.** The trend is the leading indicator.
5. **Find the system that already records the real events,** and spec the analysis against it.
