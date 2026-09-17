---
layout: case-study
title: "Answering technical tickets without waiting on engineering"
description: "Used AI to check product code against the docs, so support could find the cause and fix it."
tags: ["Support", "AI"]
---

# Case study: answering technical tickets without waiting on engineering

**Stephanie Coulter · DNSimple, a domain registrar · September 2026**

Some support tickets can't be answered from the documentation. The docs say how the product should behave, and the customer is telling you it doesn't. Usually the next step is asking a developer and waiting. Since the start of summer 2026, I've been answering most of these myself by having AI check the product code against the support docs, with me deciding what to do and confirming the fix. At least two tickets a day now go this way.

---

## The problem

On a small team, every technical question sent to engineering takes a developer away from their work, and the customer waits for an answer. As engineering time got harder to come by, that wait got longer. The information support needed was already in the code. Support just couldn't read it quickly enough to use during a reply.

## How the work is split

| AI does | I do |
|---|---|
| Reads the relevant code and support articles side by side | Decides which ticket needs this, and what question to ask |
| Explains what the product actually does, and where it differs from the docs | Checks the explanation against live results before trusting it |
| Suggests a cause and a fix | Chooses the fix and runs it with admin tools |
| Drafts the reply | Confirms the fix worked, checks every link, and sends the reply |

The AI never takes an action on an account, and nothing goes to a customer until I've checked it against what's actually happening.

## A worked example

**The ticket.** A customer had transferred two domains in, kept DNS hosting with us, and set up redirects on the root and `www` of both. None of the redirects worked.

**The cause.** The redirect records were fine. The previous provider had signed the domains with DNSSEC, and its DS records were still at the registries. We weren't signing either zone, so validating resolvers like Google's and Cloudflare's rejected every answer, and nobody's browser ever reached the redirect.

**Why it hadn't fixed itself.** Checking the code explained why the old records hadn't been removed automatically, and which admin action would remove them.

**The fix, confirmed.** I removed the records and queried the registry servers directly. About 12 minutes later, none of them returned a DS record. Both domains resolved, and all four hostnames returned a redirect over HTTP.

**What I caught before replying.** HTTPS still failed on all four hostnames because no certificate was installed for them. The reply explained the cause and the fix, warned that one resolver might keep the old failure cached for up to an hour, and gave the certificate steps. Before sending it, I confirmed the customer's plan included HTTPS redirects, since not every plan does, and checked each linked article.

## The limits, stated

- **At least two tickets a day is my estimate, not a count.** I haven't been tagging these tickets.
- **AI can explain code confidently and still be wrong.** That's why the live checks happen before anything changes for the customer. The code tells you what should happen, and the checks tell you what did.
- **This doesn't replace engineering.** Real bugs still go to developers, with better detail than before. What changes is that support no longer has to ask engineering what the product does.

## What I'd carry to another team

1. **Give support read access to the code,** alongside the help center, and an AI tool that can search both.
2. **Ask why, not just what.** "Why didn't this clean itself up?" finds the real cause, where "what's wrong?" can stop at the symptom.
3. **Confirm with live checks** before acting and after, from outside your own systems.
4. **Keep the actions human.** AI explains and drafts, and a person changes accounts and sends replies.
5. **Tag these tickets from the first day,** so you have a real count, not an estimate.
