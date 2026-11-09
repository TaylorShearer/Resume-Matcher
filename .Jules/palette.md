# Palette's Journal

## 2026-04-18 - Dialog Description Accessibility Pattern
**Learning:** In the Swiss design system, modal dialogs define `aria-labelledby` referencing `DialogTitle`, but subheadings and contextual instructions wrapped in `DialogDescription` were disconnected from the dialog root. Connecting `aria-describedby` dynamically via context registration allows screen readers to announce modal context upon open without requiring manual ID wiring across every modal instance.
**Action:** When creating compound dialog components, provide automatic ID and presence tracking in context so accessible descriptions are announced automatically.
