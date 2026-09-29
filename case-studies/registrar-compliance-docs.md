---
layout: case-study
title: "Turning registry rules into steps customers can follow"
description: "Turned ICANN, NIS2, and registry changes into steps customers can follow."
tags: ["Compliance", "ICANN", "NIS2"]
---

# Case study: turning registry rules into steps customers can follow

**Stephanie Coulter · DNSimple, an ICANN-accredited domain registrar · October 2025 – September 2026**

Registries and regulators change the rules for domain names regularly: contact verification, registration data, certificate lifetimes. Each change lands on customers as an email they don't understand or a domain that suddenly stops working. I turned those changes into documentation that tells a customer what is happening, what they have to do, and by when, and checked it against how the product actually behaves.

---

## The problem

Registry and regulatory notices are written for registrars, not for the people who own the domains. They describe obligations, deadlines, and consequences in policy language. A customer needs something else: *Does this affect my domain? What do I do? What happens if I don't?*

Getting it wrong has real costs. A missed verification can suspend a domain. A wrong prerequisite sends a customer straight into an error. And for an accredited registrar, documentation that misstates a policy is a compliance problem, not just a support ticket.

## What I did

**1. Read the source, then wrote for the customer.** For each change, I worked from the registry or regulator's own requirements and wrote what applied to a DNSimple customer: the trigger, the action, the deadline, and the consequence.

| Change | Documentation |
|---|---|
| ICANN domain contact validation | Rewrote the [validation article](https://support.dnsimple.com/articles/icann-domain-validation/) |
| DENIC `.DE` contact accuracy under the EU's NIS2 directive | Verification requirements, dates, and consequences, then post-registration holder verification, in the [.DE article](https://support.dnsimple.com/articles/domains-de/) |
| NIS2 contact email verification | A [new article](https://support.dnsimple.com/articles/nis2-contact-verification/) |
| Registration data policy | [WHOIS Privacy explanations](https://support.dnsimple.com/articles/what-is-whois-privacy/) updated |
| Shorter SSL certificate lifetimes | An [announcement](https://support.dnsimple.com/articles/announcement-ssl-certificate-validity-changes/), then corrected [renewal notice windows](https://support.dnsimple.com/articles/expiring-product-email-notifications/) once the change took effect |
| `.IS` transfers, which use contact handles instead of authorization codes | Corrected wording and steps in the [.IS article](https://support.dnsimple.com/articles/domains-is/) |

**2. Checked the documentation against the product.** A policy article can be accurate about the rule and still wrong about the product. When a customer reported that the account ownership article told them to do something that led straight to an error, I traced the behavior to the application code, confirmed the article had the prerequisite backwards, named the exact error they would hit, and gave the three ways around it in the [article](https://support.dnsimple.com/articles/transfer-account-ownership/).

**3. Kept the TLD-specific rules where customers look.** Country-code domains each have their own rules. Those went into the article for that TLD, with the general list of TLDs updated so the difference was visible before a customer started, not after something failed.

## What shipped

Documentation for ICANN, NIS2, DENIC, and certificate authority changes, plus TLD-specific requirements, all live on the [DNSimple help center](https://support.dnsimple.com/).

## Why this background matters

Before support, I worked as a psychiatric nurse aide and in emergency room registration and admissions: documentation where accuracy, protocol, and deadlines have real consequences, with people who are often upset when you meet them. Registrar compliance documentation is the same kind of work. The obligation has a deadline, the evidence has to hold up, and the reader needs to know exactly what to do.

## What I'd carry to another team

- **Translate the obligation into an action.** Trigger, action, deadline, consequence — in that order.
- **Verify against the product, not just the policy.** The rule can be right and the steps still wrong.
- **Put exceptions where readers will meet them,** on the page for that product or TLD, not in a general policy page.
- **Name the exact error message.** It's what customers search for when something goes wrong.
