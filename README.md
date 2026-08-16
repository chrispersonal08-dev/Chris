# SEO Article Workflow — Office Furniture B2B

A Claude Code skill that turns one keyword into a ranking SEO article for an
office-furniture foreign-trade B2B site.

## Usage

In Claude Code, from this repo:

```
/seo-article ergonomic office chair wholesale
```

or just say: `写一篇 SEO 文章，关键词 office chair supplier`

### How it runs

One pass, no approval stop. A single run outputs:

1. **Research + outline.** Searches Google for the keyword, fetches the page-1
   article competitors, extracts their H2s, and outputs the front matter
   (Title / keywords / meta / slug), the full Table of Contents, a per-section
   format and word plan, and a coverage check.
2. **The article.** Immediately after, the complete 2100-2500 word article, plus
   the self-check numbers.

Ask for "只要大纲" / "outline only" if you want to stop after step 1, or paste
your own outline to skip straight to the article.

## Files

```
.claude/skills/seo-article/
├── SKILL.md                          the workflow
└── references/
    ├── format-spec.md                hard format rules + final self-check
    ├── serp-research.md              competitor H2 harvesting and coverage
    ├── office-furniture-b2b.md       brand profile, personas, trade angles
    └── example-article.md            the gold-standard exemplar
```

## Before first use

Fill in the brand profile block at the top of
`.claude/skills/seo-article/references/office-furniture-b2b.md` — company name,
markets, real certifications, MOQ, lead time, product lines, CTA style. Until it
is filled, articles are written brand-neutral with no CTA, and the skill will
not invent company facts.

## Network requirement

The H2-coverage guarantee depends on fetching page-1 competitor pages. Run this
skill in an environment with open outbound network access (a local Claude Code
session). In sandboxes where egress is restricted, WebFetch is blocked, the skill
will say so, and you can paste competitor H2 outlines in manually instead.
