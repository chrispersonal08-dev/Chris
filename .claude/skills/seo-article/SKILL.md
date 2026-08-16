---
name: seo-article
description: Write SEO articles for an office-furniture B2B foreign-trade site. Takes one keyword and outputs, in a single pass, the Table of Contents (Title + all H2s) followed by the full 2100-2500 word article in the locked house format (Intro / Key Takeaways / body H2-H3 / Conclusion / FAQs). Use whenever the user gives a keyword and asks for an SEO article, blog post, outline, or TOC — e.g. "写篇文章 office chair supplier", "SEO article for ergonomic office chair wholesale", "给这个关键词写个大纲".
---

# SEO Article Workflow — Office Furniture B2B

Turn one keyword into a ranking article. The format below is **not a suggestion**.
Every rule in `references/format-spec.md` is a hard constraint, and the article is
not finished until the self-check in that file passes.

## The contract

One keyword in, **outline and finished article out in a single response**. Do not
stop to ask for approval between them.

```
INPUT: one keyword
  ↓
PART 1 — SERP research + Table of Contents
  ↓  (continue straight through, no pause)
PART 2 — full article
```

Both parts always ship together. Two exceptions:

- If the user asks for **only an outline / TOC / 大纲**, produce Part 1 and stop.
- If the user's message already contains an outline to write against, skip the
  research and go straight to Part 2 using their outline.

### Input modes

The user may supply more than a keyword. Use whatever they give:

| They give | Do this |
|---|---|
| Keyword only | Full research pass — find competitors via WebSearch, extract per §1.2 |
| Keyword **+ page-1 URLs** | Skip competitor discovery; use their list verbatim as the competitor set. Still extract H2s per §1.2 — a URL does not make WebFetch work if egress is blocked, but it **sharpens Method B**: run one targeted `WebSearch(allowed_domains:[that domain])` to recover the article's exact title, then use that title in the Method B pattern |
| Keyword **+ competitor H2 lists** | Best case. Skip extraction entirely. Use their headings verbatim, mark every competitor `[user-supplied]`, compute N_max exactly, and **drop the +2 search-derived margin** — no padding needed, so each section gets a fuller word budget |

A user-supplied URL list **overrides** your own SERP results — they are looking
at the real localized Google page for their target market; WebSearch is US-only
and is not Google. Do not add competitors they did not list, and do not drop one
because you judge it off-topic — ask instead.

When the user supplies H2 lists in raw pasted form (Ahrefs/Surfer exports,
rough Ctrl+F copies, mixed languages), normalize them yourself: strip
navigation and related-post noise, drop their intro/takeaways/conclusion/FAQ
headings for the like-for-like count, and do not ask the user to reformat.

---

## PART 1 — SERP research and Table of Contents

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
3. Extract each one's H2s. **Try `WebFetch` first; if it fails for a URL, fall
   back to the WebSearch extraction protocol** in `serp-research.md` §3 Method B
   — it works even when outbound egress is blocked. Every competitor gets
   extracted by one method or the other.
4. Build the coverage matrix and compute **N_max** = the largest number of body
   H2s any single competitor has (+2 margin for search-derived counts).

**The coverage rule:** the article's body H2 count must be `>= max(7, N_max)`,
and the union of all competitor H2 topics must be covered — as an H2, or as an
H3 nested under an H2 that subsumes it. Semantically duplicate competitor H2s
merge into one H2 (see `serp-research.md` §4). Nothing gets silently dropped.

**Never abandon the coverage step because WebFetch is blocked** — that is what
Method B is for. Only if *both* methods fail on a URL do you mark it `UNREAD`
and name it. Label each competitor `[fetched]` or `[search-derived]` in the
report. Never invent a competitor outline and never present paraphrased
structure as a verbatim H2 list.

### 1.3 Choose the keywords

From the SERP and the niche file, pick:
- **1 primary keyword** — the user's keyword, used verbatim
- **3-5 secondary keywords** — real variants and co-occurring terms seen in the
  SERP, not synonyms you made up

### 1.4 Output the TOC

Emit exactly this, then continue straight into Part 2 in the same response:

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

---

## PART 2 — Write the article

Write the full article against the outline you just produced, in the same
response. Separate it from Part 1 with a `---` rule and an `## Article` heading
so the outline and the article are visually distinct.

If the research in Part 1 forces a change to the outline while drafting (a
section will not carry its word budget, two sections turn out to overlap), make
the change and note it in one line after the article — do not silently ship an
article that does not match the TOC above it.

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

Output the article body in markdown (`##` / `###`). The front matter was already
emitted in Part 1 — do not repeat it.

## Non-negotiables

- **Never pad to hit the word count.** If a section runs short, add a real
  specification, tolerance, standard, or buyer consideration — not filler prose.
- **Never fabricate** prices, certification numbers, test results, lead times,
  company names, or statistics. Write specifics the reader can act on; if you do
  not know a figure, describe the range or the mechanism instead of inventing a
  number.
- **Never claim SERP coverage you did not verify.** A blocked fetch is reported,
  not papered over.
