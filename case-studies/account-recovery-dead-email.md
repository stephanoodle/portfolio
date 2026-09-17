---
layout: case-study
title: "When the password is right and the email is dead"
description: "Found why customers with the right password were locked out, and wrote the proposal that led to a fix."
tags: ["Support to product", "Account access"]
---

# Case study: when the password is right and the email is dead

**Stephanie Coulter · DNSimple, a domain registrar · August 2026**

Customers were writing in to say they knew their password but couldn't get into their account, because the account wanted to send them an email at an address that no longer existed. Each ticket went through a full identity check that took days. I found how often it happened, what it cost, and why, and wrote it up as a product proposal at the CEO's request. An engineer shipped the first fix three days later.

---

## The problem

The security rules asked some customers to confirm their email before continuing, either by resetting a password or by verifying their address. For a customer whose old mailbox was gone, both led to the same place: an email they would never receive.

These customers could prove who they were. They had the password. But from support, the only path was the process for a truly orphaned account, which meant an identity check, manager approval, and an engineer changing the email by hand. That took days, and often the customer was in a hurry: a domain about to expire, a site that was down, or a charge they wanted to stop.

## What I did

**Measured it from the queue.** I pulled twenty months of tickets and found the ones where a customer said their mailbox was dead and it was blocking them. Compared with the rest of the queue, those tickets took days to resolve instead of hours, and needed several times as many messages. They were also becoming more common: the tag for completed identity checks roughly doubled over the summer.

**Found the cause.** Reading the product code with AI showed that the customers weren't blocked by the rules. They were blocked by the pages. A way to change the email address already existed and was protected by the password, but neither page mentioned it. On one of them, the only button signed the customer out, which removed that option too.

**Said what I hadn't confirmed.** That conclusion came from reading code, not from trying it. The proposal said so at the top and asked for someone to test it in a real session before anything was built on it. A support teammate did the next day. The route worked, and they corrected the address I'd given for it.

**Wrote it as a product proposal**, in the format the company uses for scoping work. It covered who was affected and what they needed, the cheap fixes that shouldn't wait, the larger work behind them, and how we'd know it worked. It included the security view as well: any new way in had to be at least as strong as the check it replaced.

## What changed

- **The proposal was approved** by the support side two days after I opened it.
- **An engineer shipped the fix three days after that.** Both pages now tell customers they can change their email address and link to the form. The page that used to sign people out now shows that option as well.
- **The larger work is on hold for now**, including another way to prove ownership and letting support change an email without an engineer. The team chose to see how tickets change after the fix before scoping more.
- **No ticket of this kind has reached me since the fix went out** — about four weeks, against a rate that had been running to several a month.

## The limits, stated

- **Four weeks of no tickets isn't proof.** These were never high volume, so a quiet month can happen on its own. What I can say is the direction, not the size of the effect.
- **The fix doesn't reach everyone.** A customer who presses the reset button before reading the page still gets signed out. They find the option when they sign back in.
- **This doesn't cover orphaned accounts.** If nobody has the password, the full identity check is still the right process.

## What I'd carry to another team

1. **Look for slow tickets, not just frequent ones.** A small group of tickets that each take days can cost more than a large group that takes minutes.
2. **Check whether the customer is blocked by a rule or by a page.** A page problem is usually a much smaller fix.
3. **Say what you haven't confirmed,** and ask someone to test it before anyone builds on it.
4. **Put the cheap fix first** so it doesn't wait on the bigger project.
5. **Include the security view** so the proposal can't be dismissed as weakening protection.
