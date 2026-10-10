# DESIGN CORE

## UI/UX DESIGN RULES

1. Mobile-first, single-column layout unless desktop is explicitly required.

2. Minimal navigation: one primary action per screen. No multi-level menus.

3. Load fast: avoid heavy images, use system fonts, inline critical CSS.

4. Accessibility: sufficient contrast, touch targets ≥ 44px, semantic HTML.

5. No decorative elements (shadows, gradients, animations) unless they serve a functional purpose.

6. Use real icons (SVG or icon fonts) instead of emojis.

7. Forms: minimal fields, inline validation, clear error messages.

8. Color contrast: Normal text must have a contrast ratio of at least 4.5:1 against its background. Large text (≥24px, or ≥18.7px bold) and UI components must have at least 3:1.

9. Color blindness simulation: Every color palette must be tested with a color blindness simulator (protanopia, deuteranopia, tritanopia) before finalizing. Use tools such as Adobe Color Accessibility, Stark, or Coblis.

10. Color independence: Never rely on color alone to convey information (status, error, selection). Pair color with text, icon, pattern, or shape.

11. Color documentation: When a palette is chosen, state the contrast ratios for primary text/background pairs. If a pair fails, state the fallback (darker shade, outline, or icon).

## FOLDER STRUCTURE DESIGN RULES

12. Folder depth:
    a. Prefer 3 levels. Use this for most projects: clear separation without nesting.
    b. Allow 4 levels when features branch (e.g. src/features/auth/login.js) or when test layers exist (e.g. tests/unit/validate.test.js).
    c. Allow 5 levels only for monorepo layouts (e.g. packages/ui/src/components/Button.js). If depth exceeds 5, split the module instead of nesting deeper.

13. Group by feature or domain, not by file type.

14. Use consistent, lowercase, hyphenated naming.

15. No redundant or empty folders.

16. Separate source, tests, and build artifacts clearly.

17. Configuration files at root.

18. Avoid deep nesting beyond the limits in rule 12.

## ALGORITHM DESIGN RULES

19. Aim for optimal time and space complexity. State the Big-O notation.

20. No unnecessary loops, conditionals, or data structures.

21. Use standard, well-known algorithms when applicable. Do not reinvent.

22. Handle edge cases explicitly (empty input, null, overflow).

23. Provide pseudocode or language-agnostic steps before implementation if requested.

24. Ensure logic is testable and traceable.
