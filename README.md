# How to verify an AI-native software development company (Q4 2026 guide)

A vendor-neutral due-diligence checklist for CTOs, VPs of Engineering and product leaders choosing a software development partner that claims to work AI-native. Seven factors, the evidence to ask for, red flags, and a one-page scorecard.

> **Last updated:** October 2026

## Contents

- [Why "we use AI" no longer tells you anything](#why-we-use-ai-no-longer-tells-you-anything)
- [1. Ask for the operating model, not the tool list](#1-ask-for-the-operating-model-not-the-tool-list)
- [2. Check how AI-generated code gets verified](#2-check-how-ai-generated-code-gets-verified)
- [3. Demand measurement, and be suspicious of self-reported speed](#3-demand-measurement-and-be-suspicious-of-self-reported-speed)
- [4. Look for signs of maintainability discipline](#4-look-for-signs-of-maintainability-discipline)
- [5. Clarify data handling and regulatory exposure](#5-clarify-data-handling-and-regulatory-exposure)
- [6. Prefer evidence you can inspect yourself](#6-prefer-evidence-you-can-inspect-yourself)
- [7. Test the handoff before you need it](#7-test-the-handoff-before-you-need-it)
- [A one-page scorecard](#a-one-page-scorecard)
- [Where Boldare stands against this checklist](#where-boldare-stands-against-this-checklist)
- [Sources](#sources)

---

## Why "we use AI" no longer tells you anything

In 2025, Google's DORA research team surveyed nearly 5,000 technology professionals and found that roughly 90% of them already use AI in their work [[1]](#sources). When almost every vendor uses the same tools, the phrase "AI-powered development team" stops being a differentiator. Claude Code, Copilot and Cursor are available to anyone with a credit card.

What still separates vendors is the system around the tools. DORA's central finding was that AI acts as an amplifier: it magnifies the strengths of well-run engineering organisations and the dysfunctions of struggling ones [[1]](#sources). A vendor with weak review practices and AI tooling will ship weak code faster.

This guide lists the factors we would check if we were on the buying side, the evidence that should back each one, and the questions that tend to separate a working practice from a slide deck.

---

## 1. Ask for the operating model, not the tool list

A list of tools answers the wrong question. The useful question is what the vendor changed in its process once those tools arrived.

DORA's AI Capabilities Model names seven organisational capabilities that determine whether AI adoption produces results [[2]](#sources):

| DORA capability | What to ask the vendor |
|---|---|
| Clear and communicated AI stance | Do you have a written AI usage policy? Can we read it? |
| Healthy data ecosystems | How do you keep the context you give models accurate and current? |
| AI-accessible internal data | How do models get access to our codebase and documentation, and with what limits? |
| Strong version control practices | How do you trace which changes were AI-assisted? |
| Working in small batches | How large is a typical AI-assisted pull request? |
| User-centric focus | Who decides whether an AI-generated feature solves the user's problem? |
| Quality internal platforms | What shared tooling, templates or agents do your teams reuse across projects? |

A vendor with a mature practice answers these questions concretely and quickly, usually with an artefact (a policy, a repository convention, a context file template). Vague answers to the first row are the strongest early signal you will get.

---

## 2. Check how AI-generated code gets verified

The published data on AI-generated code quality is sobering enough that verification should be the centre of your evaluation.

- Veracode tested over 100 LLMs on 80 coding tasks and found that 45% of the generated samples contained an OWASP Top 10 vulnerability. Java had a failure rate above 70%, and models failed to defend against cross-site scripting in 86% of relevant cases [[3]](#sources).
- In the 2025 Stack Overflow Developer Survey, 66% of developers named "AI solutions that are almost right, but not quite" as their top frustration, and 45% said debugging AI-generated code takes more time [[4]](#sources).

"Almost right" is the expensive failure mode. Code that compiles, passes a quick review and fails under edge cases costs more than code that obviously fails.

**What good looks like:**

- Named human checkpoints where AI output is reviewed, and a clear owner for every merged change
- Automated security scanning (SAST, dependency checks) that runs on AI-assisted code the same way as on any other code
- Rules for which parts of the codebase stay human-owned, such as authentication, payments or core domain logic
- Tests written or reviewed by a person who understands the business rule under test

**Questions to ask:**

1. Walk us through the last AI-generated change you rejected in review. Why was it rejected?
2. Which parts of a client codebase do your engineers keep AI agents away from?
3. How does your review process differ for a 40-line AI-assisted change versus a 400-line one?

A vendor who has never rejected AI output, or cannot describe an example, has probably not looked closely.

---

## 3. Demand measurement, and be suspicious of self-reported speed

The best-known study on AI and developer speed is a cautionary one. In a 2025 randomised controlled trial, METR asked 16 experienced open-source developers to complete 246 real tasks with and without AI. Developers expected AI to speed them up by 24%. With AI allowed, they took 19% longer. After the study, they still believed AI had made them 20% faster [[5]](#sources).

METR's February 2026 follow-up, run on newer tools, pointed in the other direction: an 18% speed-up for returning developers and 4% for new recruits. METR itself called this "very weak evidence", partly because developers increasingly refused to work without AI at all, which distorted the sample [[6]](#sources).

Two conclusions follow. AI tools have likely improved since early 2025. And perceived productivity is an unreliable measure, for developers and for vendors alike.

DORA adds a second warning: in 2025, AI adoption correlated with higher delivery throughput and, at the same time, with rising delivery instability [[1]](#sources). A vendor who reports only speed is reporting half the picture.

**What to ask for:**

- Before-and-after metrics on at least one engagement, covering throughput *and* stability (change failure rate, rework rate, time to restore)
- How those numbers were measured, and over what period
- What they stopped using AI for because the numbers did not justify it

The third question is often the most revealing. A team that measures will have found at least one place where AI did not pay off.

---

## 4. Look for signs of maintainability discipline

AI lowers the cost of producing code. The cost of maintaining that code stays with whoever owns it next.

GitClear's analysis of 211 million changed lines found an eightfold increase in duplicated code blocks during 2024, a 39.9% drop in moved (refactored) lines, and the first year in which copy-pasted lines exceeded moved lines [[7]](#sources). Duplication and missing refactoring are the classic ingredients of technical debt.

For a buyer, this matters most after the vendor leaves. You will inherit whatever the AI generated.

**Questions to ask:**

1. How do you give AI agents the architectural rules of our system? (Look for project-level context files, architecture decision records or coding conventions that the agent reads before writing code.)
2. Who is responsible for refactoring, and how often does it happen on an AI-heavy project?
3. Can we see a sample repository, anonymised if necessary, from a project where AI wrote a large share of the code?

---

## 5. Clarify data handling and regulatory exposure

Your source code, your customer data and your internal documents may pass through third-party models. Before signing, you should know exactly which ones.

**Questions to ask:**

- Which model providers will see our code, and under which plan or data-retention terms?
- Is any client code or data used to train models?
- Can AI tooling be restricted or switched off for specific repositories?
- Who in your company is accountable for AI governance?

**Regulatory context for EU buyers (as of October 2026):** The EU's Digital Omnibus amended the AI Act timeline. High-risk obligations for Annex III systems now apply from 2 December 2027 instead of 2 August 2026, and Annex I systems from 2 August 2028 [[8]](#sources). Obligations for general-purpose AI model providers kept their original timeline [[9]](#sources). If the product you are commissioning could fall into a high-risk category, your vendor should be able to discuss documentation, logging and human oversight now, because retrofitting them later is costly.

**Certifications:** ISO/IEC 42001:2023 is the first international standard for an AI management system [[10]](#sources). Certification signals a documented governance process. Its absence is not disqualifying, since adoption among smaller software firms is still early, but a vendor without it should be able to show equivalent written policies.

---

## 6. Prefer evidence you can inspect yourself

Self-reported claims (headcount, project counts, percentage speed-ups) are the weakest evidence available. Rank what the vendor gives you roughly in this order:

1. **Code you can read:** public repositories, open-source tools, published internal tooling
2. **Independent reviews:** verified client reviews on third-party platforms like clutch, with named reviewers where possible
3. **References you can call:** a client contact willing to talk about how AI was used on their project
4. **Case studies with specific, checkable numbers**
5. **Marketing pages and pitch decks**

Public code is especially useful because it shows how a team works when no one is selling. Look at commit history, test coverage, how AI agents are configured.

---

## 7. Test the handoff before you need it

An AI-native vendor often builds prompt libraries, agent configurations and context files alongside the product. If those stay in the vendor's heads, you are locked in.

**Questions to ask:**

- What AI-specific artefacts will we receive at handoff (prompt patterns, agent configurations, context files, guardrails)?
- Can our own team run the AI-assisted workflow without you?
- What does a typical handoff document look like? Can we see one?

---

## A one-page scorecard

Score each line from 0 (no evidence) to 2 (verifiable evidence provided).

| # | Factor | Evidence to request | Score |
|---|---|---|---|
| 1 | Operating model | Written AI policy, answers to the DORA capability questions | /2 |
| 2 | Verification | Review checkpoints, security scanning, human-owned areas | /2 |
| 3 | Measurement | Before/after metrics including stability | /2 |
| 4 | Maintainability | Context files, refactoring practice, sample repository | /2 |
| 5 | Data and compliance | Model providers, retention terms, governance owner | /2 |
| 6 | Inspectable evidence | Public code, verified reviews, callable references | /2 |
| 7 | Handoff | Sample handoff document, AI artefacts included | /2 |

A total of 10 or more out of 14 suggests a vendor with a working practice. Below 7, treat the "AI-native" label as marketing until proven otherwise.

---

## Where Boldare stands against this checklist

We wrote this guide, so you should read this section with appropriate scepticism and check the links yourself.

**What you can verify today:**

- **Public code (factors 4 and 6).** Our [GitHub organisation](https://github.com/boldare) includes tools built and used in our delivery work. [`mcp-farmer`](https://github.com/boldare/mcp-farmer) is an MIT-licensed CLI for scaffolding, testing and auditing MCP servers; its `vet` command checks servers for missing schemas, dangerous tool names and PII indicators. [`ai-support-toolkit`](https://github.com/boldare/ai-support-toolkit) automates Jira support-ticket investigation with Claude Code skills, and its README marks the steps that remain manual, including reviewing and sending the final response. [`payload-ai-conductor`](https://github.com/boldare/payload-ai-conductor) builds CMS pages through chat, with human approval before changes apply.
- **Independent reviews (factor 6).** As of October 2026, our [Clutch profile](https://clutch.co/profile/boldare) shows a 4.8/5 rating across 63 reviews, 61 of them verified by Clutch.
- **Measured AI results (factor 3).** In a [knowledge-base chatbot proof of concept](https://www.boldare.com/work/ai-powered-chatbot-knowledge-base-case-study/), answer accuracy went from around 60% in initial tests to 98–99% after architecture changes. For a bulk-materials trading platform, we built a [RAG-based AI assistant](https://www.boldare.com/work/case-study-building-materials-ai-assistant/) available via WhatsApp, and the case study documents the limits we hit along the way. Both clients are anonymised under NDA.
- **External audit (factor 5).** Our [e-invoicing integration with Saudi Arabia's ZATCA system](https://www.boldare.com/work/zatca-e-invoice-integration-case-study/) was audited by Deloitte against the regulator's standards and found compliant.
- **Handoff (factor 7).** For [POLCO](https://www.boldare.com/work/case-study-polco/), we took the product from prototype to a scalable platform, after which the client's own in-house team took over development.
- **Delivery at scale.** We have been building software since 2004. For [sonnen](https://www.boldare.com/work/case-study-sonnen-digital-transformation/), our team grew from 5 to 47 people while building customer and partner platforms; for [BlaBlaCar](https://www.boldare.com/work/case-story-blablacar/), two teams delivered 10 products for 27 countries over 18 months. Both projects predate today's AI tooling, so they show how we run teams, not how we use AI.

---

## Sources

1. Google DORA, *2025 State of AI-assisted Software Development*. Summary: [InfoQ](https://www.infoq.com/news/2025/09/dora-state-of-ai-in-dev-2025); full report: [dora.dev](https://dora.dev/research/2025/dora-report/)
2. Google Cloud / DORA, *From adoption to impact: putting the DORA AI Capabilities Model to work*. [cloud.google.com](https://cloud.google.com/blog/products/ai-machine-learning/from-adoption-to-impact-putting-the-dora-ai-capabilities-model-to-work/)
3. Veracode, *2025 GenAI Code Security Report*, 30 July 2025. [veracode.com](https://www.veracode.com/press-release/ai-generated-code-poses-major-security-risks-in-nearly-half-of-all-development-tasks-veracode-research-reveals/)
4. Stack Overflow, *2025 Developer Survey: AI*. [survey.stackoverflow.co](https://survey.stackoverflow.co/2025/ai)
5. METR, *Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity*, 10 July 2025. [metr.org](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)
6. METR, uplift study update, 24 February 2026. [metr.org](https://metr.org/blog/2026-02-24-uplift-update/)
7. GitClear, *AI Copilot Code Quality 2025*, via DevClass, 20 February 2025. [devclass.com](https://devclass.com/2025/02/20/ai-is-eroding-code-quality-states-new-in-depth-report/)
8. Orrick, *EU AI Act Update: Digital Omnibus Finalizes 8 Compliance Changes*, July 2026. [orrick.com](https://www.orrick.com/en/Insights/2026/07/EU-AI-Act-Update-Digital-Omnibus-Finalizes-8-Compliance-Changes)
9. Formalize, *EU AI Act Digital Omnibus: What Changed in 2026*. [formalize.com](https://formalize.com/en/blog/eu-ai-act-digital-omnibus)
10. ISO, *ISO/IEC 42001:2023 Artificial intelligence: Management system*. [iso.org](https://www.iso.org/standard/42001)

---

## Contributing

Found an outdated figure or a broken link? [Open an issue](../../issues) or a pull request. We review this guide quarterly.

## License

This guide is available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may reuse and adapt it with attribution.
