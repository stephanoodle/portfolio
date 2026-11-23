---
layout: case-study
title: "Measuring whether documentation answers correctly"
description: "Built an evaluation from real customer questions, and let the data correct my conclusions twice."
image: /assets/og/measuring-answer-quality.png
tags: ["Evaluation", "Search", "AI retrieval"]
---

# Case study: measuring whether documentation answers correctly

**Stephanie Coulter · DNSimple, a domain registrar · July – November 2026**

Nothing measured whether the help center gave people the right answer, whether the reader was a customer typing into the search box or an AI assistant looking something up. I built an evaluation from real customer questions, measured the live site search, and read six months of search analytics nobody had opened. The measurement proved two of my own conclusions wrong before it produced one worth reporting, and it stopped a plausible search change from shipping. In October I used it to predict a fix before shipping it, and to change how the site search ranks multi-word searches, tested against a year of real searches.

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

**5. Checked the queries against real traffic, and corrected myself again.** My test queries averaged four words. Six months of search analytics showed real searches average under two, most of them one word. On realistic queries, the summary-field change was flat to slightly negative. So the pull request for it stayed in draft and was never merged.

The analytics had their own problems: about a third of the logged "searches" weren't searches at all, but page paths and half-typed words. Anyone reading that dashboard would have drawn the wrong conclusions about what customers look for.

## What it found

- **The search box works for how people actually use it.** Short queries find the right article.
- **Full-sentence questions, the way people ask AI assistants, retrieved about an order of magnitude worse** on the same content with the same configuration. The gap is in natural-language retrieval, not in the search box.
- **Policy-sensitive questions didn't move with any configuration change.** That segment needed terminology work, not a setting. That work is the follow-up case study: [Matching the help center to the words customers use](controlled-vocabulary.md), which moved it.
- **A repeating pattern:** a correct decision, written down, that nothing downstream uses. The unsearched summary field, pins that rarely fire, analytics nobody read.

## October: using the measurement to make changes

**6. Built question sets from tickets and from real searches.** I added five topics from tagged support tickets: expiry, certificates, contacts, transfer lock and propagation. I also built a set from the most-typed searches in a year of search analytics, weighted by how often each one was searched. Every one of the five topics scored well below the one the [terminology work](controlled-vocabulary.md) had already fixed.

**7. Read the analytics again, and found the help widget searching by itself.** When someone opens help from a page in the app, the widget runs a search for that page: *invoice* from the account page, *record editor* from the DNS page. Those automatic searches were logged the same way as typed ones, and they were about a third of the cleaned searches. *Invoice*, which had looked like the most common search, was mostly the widget. With the automatic searches filtered out, I re-tested the August summary-field change on what people actually type. It still made no difference, so the pull request stayed unmerged.

**8. Predicted a fix before shipping it.** Propagation and certificate questions failed partly because the articles never used the words the app shows: the name of the dialog that checks whether a domain resolves, and the exact error customers see when a certificate can't be issued. I rewrote two articles to quote the app, scored the change on a patched copy of the search index before opening the pull request, and re-ran the evaluation on the live site after it deployed. Both topics moved by exactly the predicted amount, and no other question set moved.

**9. Changed how the search ranks multi-word searches.** The site search matched a whole search as one fuzzy pattern. About 60 pages for individual domain extensions (.NL, .CO.UK and so on) have short titles ending in *Domains*, so a two-word search like *unlock domain* returned extension pages first. Three obvious fixes failed: rewording the article, pushing the extension pages down, and matching each word separately, which helped one topic and hurt real traffic. I compared five ranking strategies on every question set. The one that held averages the whole-phrase score with the word-by-word score for searches of two or more words, and leaves one-word searches alone. It improved every set, real typed traffic included.

**10. Tested the new ranking on every real search, not only the labeled ones.** I ran the old and new search on all of the roughly 1,200 distinct typed searches from the year. Most kept the same first result. For the searches whose first result changed, I judged the most-searched ones by hand, plus a random sample of the rest. In both groups, better outnumbered worse about three to one. That check also found a regression no question set contained: *delete account* now went to the article on deleting a domain. Pinned results fixed it before the change shipped.

**11. Caught my own measurement out of date, in November.** The evaluation used a hand-made copy of the site's search code, and that copy missed the new ranking. For four weeks, every live-search run scored a ranking customers no longer got. The evaluation now loads the site's own search code, and stops with an error if that code changes shape. Re-scored on the real ranking, typed traffic came out better than the October projection. Two small topics came out two or three questions lower. That's worth watching, but not proven.

## What October found

- **On the most-typed searches, the right article now comes first about seven times in ten,** up from about two in three, and appears in the top three nearly nine times in ten.
- **Some failures are wording, and some are ranking.** Quoting the app fixed propagation and certificate searches. No wording could fix *unlock domain*. That needed the ranking change.
- **The question sets missed what real traffic caught.** Half of real typed searches are more than one word, far more than the top searches suggested, and the worst regression wasn't in any set.

## What the measurement can't tell you

Retrieval is the floor, not the answer. If the right article doesn't surface, no assistant can answer from it. But an article surfacing doesn't prove the answer built from it is correct. That needs a separate test of the answers themselves.

The October topic sets are small, 12 to 32 questions each, so two or three questions move them visibly. Their correct answers are a first review, not yet checked a second time.

## What I'd carry to another team

- **Real questions, human-checked labels, a holdout set.** Each one closes a specific way to fool yourself.
- **Test changes one at a time.** The thorough-looking bundle was worse than the one-line change.
- **Match the test to the traffic.** A search box and an AI assistant get differently shaped questions, and scoring one with the other's produces a confident, meaningless number.
- **Read the analytics before trusting them.** A third of these weren't searches.
- **Keep the corrections in the record.** A number that survived two rounds of being wrong is worth more than one reported the first time.
- **Predict, then measure.** Scoring a change on a patched copy before shipping it turns the live re-run into a check rather than a hope.
- **Test on all the traffic, not only the labeled set.** The worst regression wasn't in any question set.
- **Check the measurement against production.** A hand-made copy of the search code drifted, and a month of numbers measured the wrong ranking.
- **Re-run after each batch of changes.** With a month of edits between runs, working out which change caused what took an afternoon.
