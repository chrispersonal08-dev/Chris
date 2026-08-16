# SERP Research — competitor H2 coverage

The coverage rule is the core of this workflow: **the article must have at least
as many body H2s as the page-1 competitor with the most H2s, and must cover the
union of every competitor's H2 topics.**

Example: page 1 has 4 articles with 5, 6, 7, and 8 H2s → the article needs
**at least 8 body H2s** (excluding Intro, Key Takeaways, Conclusion, FAQs), and
must cover topics from all four outlines.

---

## 1. Search

```
WebSearch: "<exact keyword>"
```

Run one or two supporting searches when the intent is unclear:
- `<keyword>` — the ranking set
- `<keyword> guide` or `<keyword> vs` — surfaces the article-shaped results

Note the "People also ask" style questions in the results — they feed the FAQs.

## 2. Select competitors

Keep page-1 results that are **articles**: blog posts, guides, comparisons,
buyer's guides.

Drop:
- Marketplaces and retail listings (Amazon, Alibaba SERP pages, eBay)
- Pure product or category pages with no editorial body
- Forums, Reddit, Quora, video-only results
- PDFs and login-walled pages

Normal yield: **4-8 usable competitors**. If fewer than 3 survive, say so and
widen with one more search rather than proceeding on a thin sample.

## 3. Extract H2s

For each competitor:

```
WebFetch(url, "List every H2 heading on this page, verbatim and in order.
Exclude navigation, sidebar, footer, and related-post headings — body content
only. Then give the approximate word count of the article body.")
```

Record verbatim. Count **body** H2s the way this workflow counts them: exclude a
competitor's own intro, key-takeaways, conclusion, and FAQ headings so the
comparison is like-for-like.

**When a fetch fails** (egress blocked, 403, JS-only page): try once more, then
record it as `UNREAD` and continue. In the Part 1 output, name every UNREAD URL
and state that coverage is verified against the pages actually read. Never
substitute a guess.

**When WebFetch is blocked for everything** (as in some sandboxed environments),
stop and tell the user: coverage cannot be guaranteed, and offer the two real
options — run the skill where network access is open, or paste the competitor H2
outlines in directly.

## 4. Build the coverage matrix

Lay every competitor H2 into a topic table:

| Topic | Comp A | Comp B | Comp C | Comp D | Priority |
|---|---|---|---|---|---|
| MOQ requirements | ✓ | ✓ | ✓ | | High |
| Certification (BIFMA/EN) | ✓ | | ✓ | ✓ | High |
| Shipping and container loading | | ✓ | | | Low |

**Priority = how many competitors cover it.** A topic on 3+ outlines is
table-stakes and gets its own H2. A topic on 1 outline can become an H3 under a
broader H2 — but it still has to appear.

### Merging duplicates

Competitors phrase the same topic differently. Merge when the *search intent* is
identical, not just when the words overlap:

- "How much does an office chair cost?" + "Office chair price range" +
  "Budgeting for office seating" → one H2: **Office Chair Pricing and What
  Drives Cost**
- Do **not** merge "How to choose a supplier" with "Top 10 suppliers" — one is
  criteria, the other is a list. Different intent, different sections.

When merging, the merged H2's subtopics become H3s or list items so nothing in
the union is lost.

### Adding differentiators

After covering the union, add **1-2 H2s no competitor has** — this is where a
B2B trade site outranks generic content. Draw them from
`office-furniture-b2b.md` §3: MOQ and OEM/ODM terms, container loading and
freight math, certification for the destination market, QC and inspection,
lead-time planning. Count these toward the H2 total.

## 5. Compute the target

```
N_max          = highest body-H2 count among competitors read
body H2 target = max(7, N_max)   [+1-2 differentiator H2s]
```

If `body H2 target > 9`, apply the merge pass in §4 first. If it is still >9
after merging, the length ceiling rises to 2,800 words per `format-spec.md` §1 —
coverage wins over word count, and thin sections are never the answer.

## 6. Also harvest from the SERP

- **FAQ questions** — from "People also ask" and competitor FAQ blocks
- **Secondary keywords** — recurring phrases in competitor titles and H2s
- **Content gaps** — what every competitor states vaguely and you can state
  concretely (specs, standards, tolerances, trade terms)
- **Format signals** — if 3 of 5 competitors use a comparison table, the article
  needs one
