---
name: seo-article
description: Write SEO articles for an office-furniture B2B foreign-trade site. Takes one keyword and produces a Table of Contents (Title + all H2s) for approval, then the full 2100-2500 word article in the locked house format (Intro / Key Takeaways / body H2-H3 / Conclusion / FAQs). Use whenever the user gives a keyword and asks for an SEO article, blog post, outline, or TOC — e.g. "写篇文章 office chair supplier", "SEO article for ergonomic office chair wholesale", "给这个关键词写个大纲".
---

# SEO Article Workflow — Office Furniture B2B

Turn one keyword into a ranking article. The format below is **not a suggestion**.
Every rule in `references/format-spec.md` is a hard constraint, and the article is
not finished until the self-check in that file passes.

## The two-step contract

This skill runs in **two steps with a stop in between**. Never merge them.

```
INPUT: one keyword
  ↓
STEP 1 — SERP research + Table of Contents  →  STOP, wait for user approval
  ↓
STEP 2 — full article
```

If the user's message contains an approved or edited outline, they are asking for
Step 2 — skip Step 1 and write the article against that outline.
If the user explicitly says "一次性" / "one shot" / "don't stop", run both steps
in one response.

---

## STEP 1 — SERP research and Table of Contents

### 1.1 Read the references first

Read all four before writing anything:

| File | What it locks down |
|---|---|
| `references/format-spec.md` | Every structural rule + the final self-check |
| `references/serp-research.md` | How to harvest and merge competitor H2s |
| `references/office-furniture-b2b.md` | Brand profile, buyer personas, trade angles |
| `references/example-article.md` | The gold-standard exemplar to imitate |

### 1.2 Harvest competitor H2s

Follow `references/serp-research.md` exactly. In short:

1. `WebSearch` the exact keyword.
2. Pick the page-1 **article/blog** results (skip Amazon, marketplaces, pure
   category/product pages) — normally 4-8 of them.
3. `WebFetch` each one for its verbatim H2 list and word count.
4. Build the coverage matrix and compute **N_max** = the largest number of body
   H2s any single competitor has.

**The coverage rule:** the article's body H2 count must be `>= max(7, N_max)`,
and the union of all competitor H2 topics must be covered — as an H2, or as an
H3 nested under an H2 that subsumes it. Semantically duplicate competitor H2s
merge into one H2 (see `serp-research.md` §4). Nothing gets silently dropped.

If WebFetch is blocked or a page fails, say so explicitly and name the pages you
could not read. Never invent a competitor outline and never claim coverage you
did not verify.

### 1.3 Choose the keywords

From the SERP and the niche file, pick:
- **1 primary keyword** — the user's keyword, used verbatim
- **3-5 secondary keywords** — real variants and co-occurring terms seen in the
  SERP, not synonyms you made up

### 1.4 Output the TOC

Emit exactly this, then **stop and ask for approval**:

```
## SERP Coverage
Competitors analyzed: N   |   Highest competitor H2 count: N_max   |   This outline: X body H2s
[one line per competitor: domain — H2 count — word count]
[any URL you could not fetch, flagged]

## Article Front Matter
Title: ...
Primary keyword: ...
Secondary keywords: ..., ..., ...
Meta Title: ...            (≤60 characters)
Meta description: ...      (≤155 characters, contains the primary keyword)
URL slug: ...              (lowercase, hyphenated, contains the primary keyword)
Target length: ~X,XXX words

## Table of Contents
Intro (no H2)
H2: Key Takeaways
H2: ...
  H3: ...
H2: ...
...
H2: Conclusion
H2: FAQs
  H3: [question 1]
  ...

## Section Plan
[H2 → assigned format A-E → word budget → which competitor H2s it covers]

## Coverage Check
[every competitor H2 topic → where it lands in this outline]
```

Then: "确认大纲后我开始写正文。要改哪个 H2 直接说。"

---

## STEP 2 — Write the article

Write the full article against the approved outline.

1. Follow the **section format plan** — the anti-monotony rules in
   `format-spec.md` §5 are the single most common failure. Vary the shape of
   every section.
2. Hit the word budget per section so the total lands in range.
3. Weave in the B2B trade angles from `references/office-furniture-b2b.md`
   (MOQ, OEM/ODM, lead time, FOB/CIF, container loading, BIFMA/EN certification,
   samples) where they genuinely fit the section — a buyer-intent article needs
   them, a pure "what is ergonomics" section does not.
4. Run the self-check in `format-spec.md` §8. Report the real word count, the
   body H2 count vs N_max, and any rule you had to bend and why.

Output the front matter block, then the article body in markdown (`##` / `###`).

## Non-negotiables

- **Never pad to hit the word count.** If a section runs short, add a real
  specification, tolerance, standard, or buyer consideration — not filler prose.
- **Never fabricate** prices, certification numbers, test results, lead times,
  company names, or statistics. Write specifics the reader can act on; if you do
  not know a figure, describe the range or the mechanism instead of inventing a
  number.
- **Never claim SERP coverage you did not verify.** A blocked fetch is reported,
  not papered over.
