# 04. Anti-AI Slop Design System & Human-Crafted UI Standard

[English](04-anti-ai-slop-design-system.md) | [Bahasa Indonesia](id/04-anti-ai-slop-design-system.md)

---

This document establishes strict rules to eliminate **"AI Slop"**—generic, unreadable, and bot-generated UI patterns. All user interfaces, layouts, components, and styles in this project **must remain consistent, align with existing design tokens, and feel authentically human-crafted**.

---

## 1. What is "AI Slop" in UI/UX Design? (STRICTLY PROHIBITED)

AI coding assistants often exhibit biases toward tired, unrealistic design tropes. **STRICTLY PROHIBITED** patterns include:

| AI Slop Anti-Pattern | Why It Is Banned | Human-Crafted Solution |
| :--- | :--- | :--- |
| **Generic Purple-Blue Neon Gradients** (`from-purple-600 to-blue-500` on buttons and cards) | Looks like an amateur 2021 crypto scam template | Use curated brand tokens; prioritize solid neutrals with purposeful accents |
| **Excessive Glassmorphism** (`backdrop-blur-xl bg-white/10` everywhere) | Poor text contrast, GPU lag, unreadable on mobile | Use solid or subtly elevated surfaces with crisp 1px borders (`border-border bg-card`) |
| **Meaningless Floating Icon Pills** (Circular icons beside every sentence) | Clutters layout with meaningless decorative noise | Use icons strictly for navigational affordance or semantic status indicators |
| **Haphazard Spacing** (arbitrary margins like 13px, 27px) | Results in sloppy, amateur alignment | **Strictly follow the 8-Point Grid** (4px, 8px, 12px, 16px, 24px, 32px, 48px, 64px) |
| **Hyperbolic Marketing Fluff** ("Unleash limitless potential with groundbreaking synergy") | Confuses users and feels robotic | Write clear, concise, actionable human copy focused on real user intent |
| **Ignoring Existing Design Tokens** (Adding random hex codes or new font families) | Breaks design consistency across the product | **Reuse existing CSS variables / Tailwind tokens** defined in the project |

---

## 2. Golden Rules of Design Consistency

1. **Token Adherence (Never Break Existing Design Tokens):**
   - Always inspect `tailwind.config.js`, `theme.css`, or design token files before styling.
   - Never hardcode arbitrary hex values (e.g., `#1a2b3c`). Use semantic tokens (e.g., `bg-primary`, `text-muted-foreground`, `border-border`).
2. **Intentional Typography Scale:**
   - Enforce a disciplined typographic hierarchy:
     - **Page Title / H1:** Bold, balanced line-height.
     - **Section Title / H2:** Clear thematic separation.
     - **Body Text:** 14px–16px with `line-height: 1.5 - 1.6` for optimal readability.
     - **Caption / Label:** 12px–13px for metadata, maintaining WCAG AA contrast.
3. **Ergonomics & Accessibility (WCAG AA):**
   - Minimum interactive touch targets of **44x44px** on mobile devices.
   - Visible keyboard navigation indicators (`focus-visible` rings).
   - Minimum text contrast ratio of **4.5:1** against backgrounds.

---

## 3. Mandatory 5 UI States (Complete State Handling)

Real-world applications require complete state management. AI assistants **MUST** implement all 5 states, never just the "happy path":

1. **Default / Resting State:** Standard presentation when data is populated.
2. **Loading State:** Smooth skeleton loaders that mirror the actual layout structure, rather than a generic centered spinner.
3. **Empty State:** Subtle icon/illustration, clear message explaining why data is absent, and a primary CTA to create or get started.
4. **Error State:** Human-friendly error explanation and an actionable retry mechanism.
5. **Disabled State:** Clearly dimmed element with `aria-disabled="true"` to communicate non-interactivity.

---

## 4. Human-Crafted Aesthetic Principles

- **Subtlety over Loudness:** Modern polish comes from restrained details: crisp 1px neutral borders (`border-slate-200 dark:border-slate-800`), layered subtle drop shadows, and uniform border-radii across components.
- **Natural Micro-Interactions:**
  - Snappy, purposeful transitions (`transition-colors duration-150 ease-out`).
  - Animations must never impede user task completion (keep durations under 200ms).
- **Responsive by Design:**
  - Zero accidental horizontal scroll on mobile viewports.
  - Test responsive behaviors for tables and complex grids (collapsing to cards or intentional scrolling containers).

---

## 5. Pre-Completion UI Checklist

- [ ] Does styling 100% respect existing theme tokens and CSS variables?
- [ ] Is the design free of purple-blue neon gradients and generic glassmorphism?
- [ ] Do all spacing and padding values follow the 8-point grid scale?
- [ ] Are Loading (skeleton), Empty, and Error states fully implemented?
- [ ] Is copywriting concise, natural, and free of AI marketing fluff?
- [ ] Have accessibility contrast and keyboard focus indicators been verified?
