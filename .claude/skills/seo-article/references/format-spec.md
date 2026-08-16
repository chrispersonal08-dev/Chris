# Format Spec — hard constraints

Every rule here is binding. The article is not done until §8 passes.

---

## 1. Length

| | Words |
|---|---|
| Target | **2100 - 2500** |
| Hard floor | 2100 |
| Stretch ceiling | **2800** — allowed *only* when SERP coverage forces more than 9 body H2s |

Word count = article body only (intro through the last FAQ answer). Front matter,
headings-as-metadata, and the coverage report do not count.

### Word budget math

```
fixed cost  = intro (~95) + Key Takeaways (~90) + Conclusion (~100) + FAQs (~250)  ≈ 535
body budget = target − 535
per section = body budget ÷ number of body H2s
```

| Body H2s | Target total | Per section |
|---|---|---|
| 7 | 2,400 | ~265 |
| 8 | 2,450 | ~240 |
| 9 | 2,500 | ~220 |
| 10 | 2,650 | ~210 |
| 11 | 2,800 | ~205 |

**Never let a body section fall below ~150 words.** If the math pushes it lower,
merge sections (see `serp-research.md` §4) rather than writing thin ones.

---

## 2. Document order

Fixed. No deviation.

```
1. Intro          — no H2, two paragraphs
2. Key Takeaways  — H2
3. Body sections  — H2, with H3 where earned
4. Conclusion     — H2
5. FAQs           — H2, each question an H3
```

---

## 3. Intro (no heading)

**Exactly two paragraphs.**

- **Paragraph 1 — 60-80 words.** Sets up the background around the primary
  keyword. Opens on the reader's actual situation ("If you are sourcing…",
  "When buyers compare…"), states the direct answer or core tension early, and
  uses the primary keyword naturally within the first two sentences.
- **Paragraph 2 — 25-30 words.** One or two sentences that announce what the
  article covers. Must contain the **primary keyword and at least one secondary
  keyword**. Typical shape: "In this article, we will break down X, how it
  differs from Y, and what Z means for buyers."

Do not put a heading above the intro. Do not exceed two paragraphs.

---

## 4. Key Takeaways (H2)

- Heading is exactly `## Key Takeaways`.
- **5-6 items**, bulleted list.
- **One sentence each.** No sub-bullets, no bold labels, no two-sentence items.
- Each item states a conclusion the article proves — not a topic label.
  - ✅ "Most office chair suppliers set MOQ between 50 and 200 units per model."
  - ❌ "MOQ requirements." / "This article explains MOQ."
- Together they should answer the keyword's core question on their own.

---

## 5. Body sections — the anti-monotony rules

This is the rule most often broken. **Read it twice.**

### 5.1 Forbidden patterns

Across the whole article, all four of these are violations:

- ❌ Every H2 written as plain paragraphs
- ❌ Every H2 written as a bulleted list
- ❌ Every H2 written as a numbered list
- ❌ Every H2 carrying H3s

### 5.2 The five section formats

Assign each body H2 one format in the Step 1 section plan:

| | Format | Shape |
|---|---|---|
| **A** | Prose | 2-4 flowing paragraphs, no list, no H3 |
| **B** | Prose + H3s | Short lead paragraph, then 2-4 H3 subsections |
| **C** | Prose + bulleted list | 1-2 paragraphs, an unordered list, a closing line |
| **D** | Prose + numbered list | Lead-in, then an ordered list — **only** for genuine sequences, steps, or ranked items |
| **E** | Prose + table | Lead-in, a comparison table, then a paragraph reading the table |

### 5.3 Distribution rules

- Use **at least 3 different formats** per article; 4+ is better.
- **No format more than 3 times** in one article.
- **Never two consecutive sections** with the same format.
- **At most half** the body H2s use format B (H3s).
- **At least one** section uses format E (a table) — comparison tables win
  featured snippets in this niche and every strong competitor has one.
- Format D only where order is real. Never number an unordered set.

### 5.4 Heading style

- H2s are **specific and scannable**, 4-9 words. Questions are good when the
  competitor SERP shows question intent.
- H3s only when a section has 2+ genuinely parallel sub-topics. A single H3
  under an H2 is always wrong — promote it or fold it into prose.
- Front-load the keyword or its modifier in the heading; never keyword-stuff.
- No H4s.

### 5.5 Prose quality

- Paragraphs of 2-4 sentences. Never a single 200-word block.
- Concrete over vague: "seat height adjustable 42-52 cm" beats "adjustable
  height". Cite the mechanism, the standard, the tolerance, the trade term.
- Second person for the buyer ("your MOQ", "when you order"), third person for
  the market.
- No hype ("revolutionary", "game-changing"), no filler ("in today's fast-paced
  world"), no "it's important to note that".

---

## 6. Conclusion (H2)

- Heading is `## Conclusion`.
- **One paragraph, ~100 words.** Not two, not a list.
- Must contain the **primary keyword** and deliver an actual conclusion — the
  answer, the recommendation, or the decision rule. Not a summary of what the
  article said.
- May end with one soft CTA line if the brand profile enables it (see
  `office-furniture-b2b.md` §5).

---

## 7. FAQs (H2)

- Heading is `## FAQs`.
- **4-6 questions.** Each question is an **H3**, phrased as a real question with
  a question mark.
- Questions come from the SERP: "People also ask", competitor FAQ blocks, and
  long-tail variants. Prefer questions the body did *not* already answer head-on.
- **Each answer 30-60 words**, 1-3 sentences, answering in the first sentence.
- Collectively the FAQs must contain the primary keyword and at least two
  secondary keywords.

---

## 8. Final self-check

Verify each line before delivering. Report the numbers — do not just assert pass.

```
[ ] Total word count is 2100-2500 (or ≤2800 with >9 body H2s)     → actual: ____
[ ] Body H2 count ≥ 7 AND ≥ N_max                                 → ____ vs ____
[ ] Every competitor H2 topic maps to an H2 or H3 here
[ ] Order is Intro → Key Takeaways → body → Conclusion → FAQs
[ ] Intro is 2 paragraphs, 60-80w and 25-30w
[ ] Intro ¶2 contains primary + a secondary keyword
[ ] Key Takeaways: 5-6 items, one sentence each
[ ] ≥3 distinct section formats used, none used >3 times
[ ] No two consecutive sections share a format
[ ] ≤ half the sections use H3s; no section has exactly one H3
[ ] At least one comparison table
[ ] No section under 150 words
[ ] Conclusion is ONE paragraph ~100w and contains the primary keyword
[ ] FAQs: 4-6 H3 questions, each answer 30-60 words
[ ] Meta Title ≤60 chars, Meta description ≤155 chars w/ primary keyword
[ ] Slug is lowercase-hyphenated and contains the primary keyword
[ ] No fabricated prices, certifications, statistics, or company names
```

### Keyword density

Primary keyword **0.8-1.5%** of total words — roughly 18-35 uses in a 2,300-word
article, counting the title, headings, and meta. Every use must read naturally.
Exact-match in: Title, Meta Title, Meta description, slug, intro ¶1, intro ¶2,
at least two H2s, the Conclusion, and at least one FAQ. Elsewhere prefer
variations and partial matches over exact repetition.
