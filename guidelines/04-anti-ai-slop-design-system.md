# 04. Anti-AI Slop Design System & Human-Crafted UI Standard

[English](04-anti-ai-slop-design-system.md) | [Bahasa Indonesia](id/04-anti-ai-slop-design-system.md)

---

This document establishes strict rules to eliminate **"AI Slop"**—generic, unreadable, and bot-generated UI patterns. All user interfaces, layouts, components, and styles in this project **must remain consistent, align with existing design tokens, feel authentically human-crafted, and deliver 100% responsive support across all devices (from the smallest iPhone to ultra-wide 4K desktop screens)**.

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
   - Minimum interactive touch targets of **44x44pt** across touchscreens.
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

## 4. Universal Responsive Matrix (From Smallest Mobile to 4K Ultra-Wide)

Interfaces must be meticulously tested and responsive across the entire device spectrum:

| Device Category | Viewport Width | Typical Hardware Target | Layout Strategy |
| :--- | :--- | :--- | :--- |
| **Extra Small (Compact Mobile)** | `320px – 375px` | iPhone SE (1st–3rd Gen), iPhone 12/13 mini | Single column, tight padding (`px-3`), collapse secondary actions into sheets/menus |
| **Standard Mobile** | `390px – 430px` | iPhone 12/13/14/15/16, Pro & Pro Max, Android flagships | Fluid container, full touch targets (44pt+), bottom navigation |
| **Tablet Portrait** | `768px – 834px` | iPad mini, iPad 10.9", iPad Air/Pro 11" | 2-column grids, split views, elevated sheets |
| **Tablet Landscape / Small Laptop**| `1024px – 1280px`| iPad Pro 12.9", MacBook Air 13", compact ultrabooks | Collapsible side navigation, 3-column dashboard grids |
| **Standard Desktop** | `1440px – 1920px`| 1080p monitors, MacBook Pro 16", iMac 24" | Full multi-column dashboard, persistent sidebars |
| **Ultra-Wide & 4K Displays** | `2560px – 3840px+`| 27"-32" 4K displays, 21:9 / 32:9 ultra-wides | **Enforce max-width constraint** (`max-w-7xl` / `1280px–1440px`) to prevent text lines from stretching excessively |

---

## 5. Full iPhone & iOS Ecosystem Ergonomics (Apple HIG Compliance)

When designing web or mobile views, AI assistants must strictly respect iOS-specific constraints:

1. **Dynamic Viewport Heights (`dvh`):**
   - ❌ **DILARANG:** Using `height: 100vh` on full-screen containers (causes bottom controls to be hidden behind the Safari floating URL bar).
   - ✅ **MANDATORY:** Use `min-h-screen min-h-dvh` or `height: 100dvh` so containers adapt fluidly when Safari's address bar collapses or expands.
2. **Safe Area Insets (Notch & Dynamic Island & Home Bar):**
   - Fixed/sticky navigation headers, bottom tab bars, floating action buttons (FAB), and modals **MUST** respect Apple Safe Area Insets:
     ```css
     padding-top: env(safe-area-inset-top);       /* Notch / Dynamic Island */
     padding-bottom: env(safe-area-inset-bottom); /* Home Indicator bar */
     padding-left: env(safe-area-inset-left);
     padding-right: env(safe-area-inset-right);
     ```
   - In Tailwind CSS projects, use utility classes like `pt-safe`, `pb-safe`, or custom CSS variables with `env()`.
3. **Prevent Form Auto-Zooming on iOS Safari:**
   - ❌ iOS Safari automatically zooms in on any `<input>`, `<select>`, or `<textarea>` whose computed `font-size` is smaller than `16px`, breaking user layouts.
   - ✅ Form inputs on mobile viewports **MUST have a minimum font-size of 16px** (`text-base` in Tailwind).
4. **Native-Like Touch & Momentum Scrolling:**
   - Enable hardware-accelerated momentum scrolling on overflow containers:
     ```css
     -webkit-overflow-scrolling: touch;
     overflow-y: auto;
     ```
   - Remove annoying gray tap highlight overlays:
     ```css
     -webkit-tap-highlight-color: transparent;
     ```
5. **Touch Targets (Apple HIG 44x44pt Rule):**
   - Every tappable element (buttons, hamburger icons, tabs, dropdown items) must have an active hit area of at least **44x44pt**, even if the visual icon inside is smaller.

---

## 6. Pre-Completion UI Checklist

- [ ] Does styling 100% respect existing theme tokens and CSS variables?
- [ ] Is the design free of purple-blue neon gradients and generic glassmorphism?
- [ ] Do all spacing and padding values follow the 8-point grid scale?
- [ ] Are Loading (skeleton), Empty, and Error states fully implemented?
- [ ] **Full Responsive Check:** Tested on 320px (iPhone SE) up to 4K ultra-wide (max-width container enforced)?
- [ ] **iPhone & iOS Check:** Uses `100dvh`? Uses `env(safe-area-inset-*)` on fixed bars? Form inputs >= 16px? Touch targets >= 44x44pt?
- [ ] Is copywriting concise, natural, and free of AI marketing fluff?
- [ ] Have accessibility contrast and keyboard focus indicators been verified?
