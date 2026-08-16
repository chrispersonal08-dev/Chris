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

Two methods. **Always try Method A first; fall back to Method B per URL.**
Never skip a competitor — every page-1 article gets its headings extracted by
one method or the other.

### Method A — WebFetch (preferred, verbatim)

```
WebFetch(url, "List every H2 heading on this page, verbatim and in order.
Exclude navigation, sidebar, footer, and related-post headings — body content
only. Then give the approximate word count of the article body.")
```

Gives exact, verbatim, complete headings. Use it whenever it works.

### Method B — WebSearch heading extraction (fallback, validated)

WebSearch runs on different infrastructure from WebFetch and **keeps working
when outbound egress is blocked** (sandboxes, restricted corporate proxies,
403-on-CONNECT policy denials). The search backend reads the page body, so it
can return the section structure even when you cannot fetch the URL yourself.

**The query pattern that works** — all three parts matter:

```
WebSearch(
  query: "<the article's EXACT title words> headings sections table of contents",
  allowed_domains: ["<competitor domain>"]
)
```

Rules learned from testing this pattern:

- **Use the article's exact title** from the SERP result. Generic queries
  ("list every H2 on this page", the bare URL) return site boilerplate and
  company blurbs instead of structure — they fail.
- **`allowed_domains` is required.** Without it the results scatter across
  other sites and the backend summarizes the wrong page.
- **Never paste the raw URL as the query.** That returns Trustpilot reviews and
  "about us" copy, not the article.

**Run 2-3 queries per competitor**, each angled differently, then union the
results:

1. `<exact title> headings sections table of contents`
2. `<exact title> what does the article cover main points`
3. `<primary keyword> <a topic you expect deep in the article>` — pulls
   sections the first two queries truncated

### Method B's known limitation — and the margin it requires

The search backend **paraphrases and compresses**. It returns the section
structure faithfully but not always verbatim, and it under-reports: long
articles come back with the tail sections missing.

Therefore, when a competitor's headings came from Method B:

- Treat the recovered headings as **topics, not verbatim H2s**.
- **Add a +2 safety margin** to that competitor's H2 count before computing
  `N_max`. Under-reporting is the failure mode, so bias upward.
- Label the source in the coverage report: `[fetched]` vs `[search-derived +2]`.

### Reporting honestly

State in the Part 1 output which method produced each competitor's headings.
Say `[search-derived]` where it applies — do not present paraphrased structure
as a verbatim H2 list. If both methods fail for a URL, mark it `UNREAD`, name
it, and say coverage is verified against the rest.

Count **body** H2s the way this workflow counts them: exclude a competitor's own
intro, key-takeaways, conclusion, and FAQ headings so the comparison is
like-for-like.

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
per competitor:  count = body H2s found
                 count += 2  if the headings were search-derived (Method B)

N_max          = highest adjusted count among competitors
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
