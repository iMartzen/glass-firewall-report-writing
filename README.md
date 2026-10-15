# Write reports people can act on

<p align="center">
  <img src="assets/glassfirewall.png" alt="Glass Firewall Conference 2026: Breaking Bytes and Barriers" width="320">
</p>

Material from the *Report Writing* workshop at the Glass Firewall Conference: Breaking Bytes and Barriers (2026).

> Personal workshop material. All examples are fictional.

---

## The three questions every report must answer

1. **What is it?** (title and summary)
2. **How do I see it myself?** (steps to reproduce)
3. **Why does it matter?** (impact)

## The test: own every sentence

You can use AI (or a colleague, or a template) to help you write. The measure is simple:

> **Can you explain and defend every sentence if the triager calls you?**

If the answer is no, the sentence does not belong in your report. Fix it, check it, or delete it.

**AI can review. Only you can verify.**

<!--
Maintainer note: the review criteria live in two tiers.

Behavior tier (the AI reads these as instructions, so they must agree):
  - plugins/report-review/skills/report-review/SKILL.md  (the Claude Code skill)
  - prompt/report-review-prompt.md                        (the plain prompt)
A CI check (.github/workflows/validate.yml) asserts the key guardrail phrases
appear in both. If you change a guardrail, change it in both or CI fails.

Human tier (paraphrase freely, no sync required):
  - this README (the "A good report" and "A report to avoid" lists below)
  - assets/examples.md                                    (the worked examples)
These are for people to read. They may word things differently from the behavior
tier on purpose; do not treat small differences as drift.
-->

## A good report

- [ ] **Specific title:** *[Vulnerability type] in [component] allows [impact]*
- [ ] **Short summary** of 2 to 3 sentences
- [ ] **Numbered steps** a stranger can follow, with accounts, full URLs and exact values
- [ ] **Expected versus actual** behavior
- [ ] **Evidence with an explanation** (screenshot, video or request, and what to look at)
- [ ] **Impact in plain language:** who is affected and what can happen
- [ ] **Realistic severity** that you can justify
- [ ] **One finding** per report
- [ ] **Calm, professional tone**
- [ ] **In scope**, using only your own test accounts

## A report to avoid

- Dramatic titles and urgency ("CRITICAL!!!")
- "I think", "maybe", "somewhere around" instead of facts
- Steps that skip things the reader cannot know
- Several findings mixed together
- Unvalidated scanner output
- Text you have not checked, including text from any writing tool
- Inflated severity, bounty pressure or threats to publish
- "See attachment" without an attachment
- Testing on real users or out of scope

For the findings that are usually closed as invalid, and the severity mistakes that cost people credibility, see [`common-pitfalls.md`](assets/common-pitfalls.md).

## Template

Copy this and fill it in with what you **saw yourself**.

```
Title:
[Vulnerability type] in [component] allows [impact]

Summary:
(2 to 3 sentences)

Steps to reproduce:
1.
2.
3.

Expected behavior:
Actual behavior:

Impact:
(Who is affected? What can happen?)

Evidence:
(Screenshot, video, request, with explanation)

Environment:
(Browser, version, account, time)

Recommendation (optional):
```

## Get your report reviewed with AI

How you run it depends on your tool:

- **Any AI tool** (ChatGPT, Gemini, Copilot, Claude and so on)? Use the plain prompt (Option 1).
- **On Claude Code?** Install the plugin (Option 2) or download the skill (Option 3).

### Option 1: Use the plain prompt (any AI tool)

Copy the prompt from [`prompt/report-review-prompt.md`](prompt/report-review-prompt.md) and paste your draft underneath it. This works in any AI tool, and is the best option if you do not use Claude Code.

This plugin ships prompt text only. There are no hooks, scripts or executables, so nothing runs on your machine when you install it. It cannot read files or run commands on its own; it only guides the AI you are already talking to.

### Option 2: Install it as a plugin (Claude Code)

```
/plugin marketplace add iMartzen/glass-firewall-report-writing
/plugin install report-review@glass-firewall-report-writing
```

If the install summary says `Run /reload-plugins to activate.`, run that command. Then use it with:

```
/report-review:report-review
```

and paste your draft. Plugin skills are namespaced with the plugin name, which is why the command is written twice. To update later, run `/plugin marketplace update`. Updating pulls the latest version of this repo, so you get fixes automatically but you are trusting whatever is in the repo at that moment. If you would rather pin a copy you have read yourself, use Option 3.

### Option 3: Download just the skill (Claude Code, no marketplace)

Prefer to pin a copy you control? Download [`SKILL.md`](plugins/report-review/skills/report-review/SKILL.md) and save it in a folder called `report-review` inside your skills folder:

- **For all your projects:** `~/.claude/skills/report-review/SKILL.md`
- **For one project only:** `.claude/skills/report-review/SKILL.md`

Then use it with `/report-review` and paste your draft. This copy does not update by itself, which also means it cannot change under you: it stays exactly as you downloaded it until you replace it. The frontmatter at the top of `SKILL.md` carries a `metadata.version` you can compare against the copy in this repo, so you can tell when yours is behind and download it again.

**How to use it**

1. Add the skill (or paste the prompt) into your AI tool.
2. Paste your **draft** report.
3. Answer the questions it asks, using only what you **observed yourself**.
4. If your honest answer is "I do not know", that is the sentence to fix or delete.

**What the reviewer does:** it reads your report like a triager, gives a verdict, lists the three biggest improvements, and asks questions.
**What it does not do:** it does not invent URLs, endpoints, parameters, versions or severity scores. If it did, you would be defending a sentence you did not write.

### Before you paste anything

- Check the **program's policy** on AI tools and on sharing report details.
- Check your tool's **data handling**.
- Remove **credentials** and **real customer data**.

## Examples

Three reports about the same fictional bug (a polished one, a dramatic one and a strong one): [`examples.md`](assets/examples.md)

Want to try the reviewer live? Each report is also a standalone file you can paste straight in: [`report-1-polished.md`](assets/drafts/report-1-polished.md), [`report-2-dramatic.md`](assets/drafts/report-2-dramatic.md), [`report-3-strong.md`](assets/drafts/report-3-strong.md).

## Further reading

Two common ways a report fails: it describes a finding that triagers routinely close as invalid, or it claims a severity the author cannot defend. [`common-pitfalls.md`](assets/common-pitfalls.md) distills both into portable principles. If you report on HackerOne, the authoritative and current source is HackerOne's own [core ineligible findings](https://docs.hackerone.com/en/articles/8494488-core-ineligible-findings) and [detailed platform standards](https://docs.hackerone.com/en/articles/8369826-detailed-platform-standards).

## Pro tips

- Write for someone who is tired and has 50 reports in the queue.
- Test your steps in an incognito window with a fresh account.
- Hand your steps to a colleague or friend and ask them to follow them literally. Every question they ask is a gap in your report.
- Use help as an editor, not a witness. You found the bug, so you provide the facts.

---

*Made for the Glass Firewall Conference 2026. Questions or ideas? Open an issue.*
