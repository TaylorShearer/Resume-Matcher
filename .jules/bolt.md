# Bolt's Journal - Critical Learnings Only

## 2025-05-18 - Caching compiled regular expressions in client-side text analysis
**Learning:** In text analysis utilities like `keywordInText` and `calculateMatchStats`, keywords are repeatedly evaluated against resume and job description text. Compiling Unicode-aware regular expressions with boundary lookarounds (`(?:(?<!\w)|(?<=\p{CJK}))term(?:(?!\w)|(?=\p{CJK}))`) on every check causes substantial regex engine compilation overhead (~5x slower in benchmarks).
**Action:** Use a bounded `Map` cache (e.g., 500 entries) for compiled term regexes whenever repeatedly testing discrete terms against text blocks.
