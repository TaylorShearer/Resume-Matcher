# Bolt's Journal

Critical performance learnings and codebase-specific patterns.

## 2026-10-29 - Repeated RegExp compilation in keyword matching loops
**Learning:** `keywordInText()` in `apps/frontend/lib/utils/keyword-matcher.ts` is invoked in hot loops during client-side ATS scoring and JD keyword comparison (`calculateMatchStats`, keyword filtering in tailoring). Because the Unicode regex structure (`TERM_START` and `TERM_END` lookarounds) is relatively complex, dynamic recompilation of the same regex string inside iterations incurred measurable V8 bytecode compilation overhead.
**Action:** When performing whole-word regex matching against recurring token sets, cache compiled `RegExp` instances in a bounded map (with an upper size limit to avoid memory leaks) rather than re-instantiating `new RegExp(...)` per match check.
