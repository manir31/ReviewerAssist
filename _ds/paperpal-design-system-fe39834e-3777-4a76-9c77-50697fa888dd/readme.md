# Paperpal Design System

An applied design system for **Paperpal** — an AI academic-writing assistant that helps
researchers, students and academics write, edit, check and submit their manuscripts.
Paperpal pairs a live language-and-grammar editor with AI rewriting, citation/research,
translation, plagiarism + submission checks, and *ChatPDF* (chat with research papers).
This system captures the product's visual language as runnable tokens, components and a
high-fidelity editor UI kit.

> **Sources.** Built from the attached Figma file **"Paperpal Edit Components.fig"**
> (mounted read-only). All token values, component specs, the logomark vector and the
> editor layout were transcribed from that file. No live codebase or URL was provided.
> Public references were used only to confirm names, never as a substitute for the file.

---

**Build status:** 104 components (curated + raw kit) across 8 groups · 21 Design-System cards ·
148 tokens · 2 interactive UI kits (Editor, ChatPDF). See the coverage map at the end.

## Index / manifest

| Path | What |
|---|---|
| `styles.css` | Global CSS entry point — `@import`s the token files. Consumers link this. |
| `tokens/fonts.css` | Webfont loading (Google Fonts — see Font note). |
| `tokens/colors.css` | 12-step ramps (Gray, Blue, Green, Yellow, Red) + semantic aliases. |
| `tokens/typography.css` | Font families, weights, type scale. |
| `tokens/layout.css` | Spacing, radius, elevation, motion. |
| `assets/paperpal-logomark.svg` | The Paperpal page logomark (recreated from exact paths). |
| `components/forms/` | Button, IconButton, TextField, Select, Checkbox, Radio, Switch. |
| `components/display/` | Card, Badge, Tag, PromptChip, Avatar, Tooltip, Icon, Shortcut. |
| `components/feedback/` | Dialog, Toast, Callout, Skeleton, Coachmark. |
| `components/navigation/` | Tabs, MenuItem, RailButton. |
| `components/brand/` | Logo, PrimeButton, UsesMeter. |
| `components/editor/` | SuggestionCard, SelectionBar, DocumentTitle, Marker, SaveToNotesButton. |
| `components/chatpdf/` | DocumentCard, ChatInput, ChatMessage, FollowupItem, SegmentedToggle. |
| `components/kit/` | Raw 1:1 Figma extractions of every component family (figma-named). |
| `ui_kits/editor/` | Interactive Paperpal editor recreation (`index.html`). |
| `ui_kits/chatpdf/` | Interactive Paperpal ChatPDF recreation (`index.html`). |
| `guidelines/` | Foundation specimen cards (Colors, Type, Spacing, Brand). |
| `SKILL.md` | Agent-Skill manifest for downstream use. |

The compiler bundles every `components/**/<Name>.jsx` (with a sibling `.d.ts`) into
`_ds_bundle.js` and exposes them on `window.PaperpalDesignSystem_fe3983`.

> **Two tiers.** `components/forms|display|feedback|navigation|brand|editor|chatpdf/` are the
> **curated** primitives — clean, documented, brand-accurate, used by the UI kits. `components/kit/`
> holds **raw 1:1 Figma extractions** of every component family (figma layer names, exact
> geometry) for when you need a pixel match to the source. Where names would clash, the curated
> component wins (Button, Icon, Tag, Tooltip, Marker, SaveToNotesButton).

---

## CONTENT FUNDAMENTALS

Paperpal's voice is **calm, expert and encouraging** — a knowledgeable writing coach, not a
cheerleader. Copy is academic-adjacent but plain.

- **Person & address.** Speaks to the writer as *you* ("Type or paste something",
  "use the sample text", "Chat with PDF"). Paperpal refers to its own capabilities by
  feature name ("Paperpal AI", "ChatPDF"), rarely "I".
- **Casing.** Buttons and features use **Title Case** for product names and primary actions
  ("Get Unlimited", "Write with AI", "Brainstorm Ideas", "Create an Outline",
  "Research | Cite"); sentence case for helper/body text.
- **Verbs first, concise.** Actions are short imperatives: *Accept, Retry, Copy, Discard,
  Rewrite, Make academic, Translate, Insert*. Suggestion notes are one clause
  ("Subject–verb agreement", "More concise phrasing").
- **Domain vocabulary.** Manuscript, abstract, citation, plagiarism, submission, journal,
  academic tone, plain-language summary, study highlights.
- **Tone of guidance.** Suggestions are framed as improvements, never scolding. Limits are
  stated factually with a friendly upsell ("Free Uses 3/10 · Get Unlimited").
- **Emoji.** Not used in product UI. Iconography carries meaning instead.
- **Numerals.** Used sparingly and meaningfully — credit counts, suggestion counts,
  word counts. Avoid decorative stats.

---

## VISUAL FOUNDATIONS

**Overall vibe.** Clean, bright, document-first. The manuscript is the hero on a near-white
canvas; chrome recedes. A single confident brand blue, a deep-navy chrome accent, and a gold
"Prime" gradient for upgrade moments. Restrained, trustworthy, academic.

- **Color.** A Radix-style **12-step** system. The neutral **Gray ramp is blue-tinted**
  (cool, not warm). **Blue is the brand**: `--blue-9 #0062FF` is the solid primary fill,
  `--blue-10 #0054F1` the hover/active, `--blue-11 #1C4DC0` brand text, `--blue-12 #051E57`
  the deep navy used for headings and the right-hand feature rail. Green/Yellow/Red are
  the status ramps. Steps 1–2 = backgrounds, 3–4 = hover/selected surfaces, 6 = border,
  9 = solid fill, 11–12 = text. *(Accent steps 5–8 were interpolated — see Caveats.)*
- **Type.** Three roles: **IBM Plex Serif** for display/marketing headings, **IBM Plex Sans**
  for all product UI and body, and **Inter** for the *manuscript/editor document text*
  (16–17px, 1.75 line-height) — this separation of UI vs document font is intentional.
  IBM Plex Mono for code/shortcuts. Scale runs 12 → 56px (H1 45/56, H2 30/40, H3 24/32).
- **Backgrounds.** Flat, near-white (`--gray-2 #F8F9FD` app, `#FFF` cards). No photographic
  or textured backgrounds in-product. Gradients appear only as brand accents: the blue
  header gradient (`#1C4DC0 → #0062FF`) and the gold Prime gradient (`#ECB441 → #FFF1D6`).
- **Corner radii.** 5px (editor frame), **6px** (buttons, cards, suggestion popovers),
  **12px** (prompt chips, dropdown surfaces, dialogs), 20px (callout banners),
  pill (badges, the floating suggestions Tag, avatars).
- **Cards & elevation.** Cards are white with **6px** radius. The signature shadow is
  **Elevation 1**: `4px 4px 16px rgba(0,0,0,.08), 16px 8px 32px 16px rgba(0,0,0,.02)` — a
  soft, slightly down-right offset. Popovers add a `0 0 0 .5px` hairline. Nav bars use a
  flatter `0 4px 8px rgba(0,0,0,.08)`. Borders are the cool grays (6–8).
- **Buttons.** Primary = solid `#0062FF`, white text, 6px radius, IBM Plex Sans 500.
  Secondary = transparent with a 1px inset blue border + blue text. Tertiary = text only.
  Small = 32px tall / 14px / pad 4×16; Medium = 40px / 16px / pad 8×24.
- **Suggestions.** Inline language issues are marked with a **wavy underline** colored by
  category (red = grammar, amber = clarity, blue = language). Clicking opens a small white
  SuggestionCard showing the rewrite (original struck in red, suggestion in green) with
  **Accept** / **Discard**.
- **Motion.** Subtle and fast — 120–260ms, `cubic-bezier(0.4,0,0.2,1)`. Popovers and panels
  fade-and-rise ~4px. No bounce, no decorative looping animation on content.
- **Hover / press.** Hover = a step-darker fill (primary → `--blue-10`) or a soft tint
  (`--blue-3`) for low-emphasis controls; ghost icons get a `--gray-3` wash. The navy rail
  uses translucent white overlays on hover/active. Focus = blue ring (1px inset border +
  3px `--blue-4` halo). No shrink-on-press.
- **Layout.** The editor is a centered document column (~760px) on the app canvas, a fixed
  white top toolbar, an optional right-side feature panel, and a fixed **navy vertical rail**
  (72px) pinned to the right edge with the feature icons + Prime + bell/help.
- **Transparency & blur.** Used lightly — translucent white overlays on the navy rail and a
  40% black modal backdrop. No heavy glassmorphism.

---

## ICONOGRAPHY

- **System.** Paperpal's icons are **Font Awesome** (the file notes "a high quality selection
  available in Font Awesome Icons (official)", and uses *Font Awesome 6 Pro Solid*). This
  system uses **Font Awesome 6 Free** via CDN as the substitute — same metrics and glyph
  language; a handful of Pro-only glyphs may differ. *(See Caveats — flagged substitution.)*
  Load it with:
  `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css">`
- **Style.** Predominantly **solid** (`fa-solid`) glyphs at 12–18px, in `--text-muted` for
  idle chrome and `--brand` for active/feature icons. Line icons (`fa-regular`) appear for
  bell/help.
- **Brand glyphs.** The Paperpal **logomark** (blue page + folded corner + white smile) is a
  custom vector — use `assets/paperpal-logomark.svg` or the `Logo` component, never redraw.
  Writing-task icons in the source (Paraphrase, Summarize, Make academic, Abstract…) are
  represented here with the closest Font Awesome equivalents.
- **Emoji / unicode.** Not used as iconography. Keyboard shortcuts use unicode (⌘, ↵).

---

## Caveats & substitutions

- **Accent ramp steps 5–8** (Blue/Green/Yellow/Red) were *interpolated* — the Figma color
  guide only published steps 1–4, 9, 11, 12 for the accents. Gray is exact (1–12), and all
  brand-critical blues (9/10/11/12) are exact. Marked `/* interpolated */` in `colors.css`.
- **Icons** are Font Awesome 6 **Free** standing in for the source's FA6 **Pro**.
- **Fonts** load from Google Fonts (the real families: IBM Plex Sans/Serif/Mono, Inter), so
  no visual substitution — but no font binaries ship in the project.
- **Component coverage.** The Figma file enumerates **112 component families**. They are
  delivered in two tiers: a **curated** set of ~36 clean, documented, brand-accurate primitives
  (used by the UI kits), plus a **raw `components/kit/`** tier holding 1:1 figma-named extractions
  of every family for pixel-exact matching. Together they implement **104 of 112** families; the
  remaining handful are Figma-tooling artifacts or pure specimen frames (see “Intentionally
  skipped” below). The table below maps the major families onto the curated primitives.

### Component coverage map (112 Figma families → 36 components)

| Figma families (states/variants) | Implemented as |
|---|---|
| Button, Buttons ×2, Button Template, Actions, Component 1/7/8, Primary/Secondary/Tertiary Idle·Hover·Active·Disabled | **Button** (+ variants/sizes), **IconButton** |
| Input fields, ONBOARDING FIELDS, ICONS/LISTING/FIELDS | **TextField**, **Select** |
| Radio button (4 states) | **Radio** |
| (toggle states) | **Switch**, **Checkbox** |
| Chip component, Prompt, Prompt chips, Chips | **PromptChip**, **Tag**, **Badge** |
| Tooltip | **Tooltip** |
| Toast | **Toast** |
| dialog box with prompts, Discard/Error pop up, Overlays | **Dialog**, **Callout** |
| Tutorial, guide, help and support | **Coachmark** |
| Editor / Editor2, Selection Bar/Editor ×2, AI suggestion, Listing Dropdown, dialog box with prompts | **SuggestionCard**, **SelectionBar**, **MenuItem**, **Marker** |
| Header/Editor ×3, Header iPad/Mobile, Document Title, File name, RHS top navbar | **DocumentTitle**, **UsesMeter** ("Free uses"/"Uses"), editor UI kit |
| SideBar ×3, LHS Menu, LHS/RHS PANEL, RHS NOTCH, Navigation-Bars, Header/Options | **RailButton**, **Tabs**, editor UI kit |
| Save to notes button | **SaveToNotesButton** |
| ChatPDF, ChatPDF/Document Card·Kebab·Library Card·Listing·Followup·Toggle Bar·Toggle Menu·Question, ChatPDF Icons/Listing | **DocumentCard**, **ChatInput**, **ChatMessage**, **FollowupItem**, **SegmentedToggle**, ChatPDF UI kit |
| Icon ×4 (48/49/32/49), ICONS (122), Icons (20), ChatPDF Icons, Drop Down Icons, Skyward-Icons (53), ICONS/LISTING/heavy icons (Paraphrase, Summarize, Abstract, Make academic, …) | **Icon** (Font Awesome wrapper) + the documented FA substitution |
| Shortcuts | **Shortcut** |
| Paperpal Logo, Paperpal AI, Paperpal Animation | **Logo** + `assets/paperpal-logomark.svg` |
| Free uses ×2, Uses ×2, Free credit limit | **UsesMeter** |
| (loading) Explainer Lottie, LoadingPopUp, LoadingCitation | **Skeleton** |

**Intentionally skipped** (Figma-tooling artifacts or non-UI): `App extension`,
`Frame Repalcement`, `Rectangle 3464302–305`, `Scroll` (native scrollbar), `Cursor`
(collaborative caret — out of scope), and the pure specimen frames (`Colors`, `Typography`,
`Elevations`, color guides) which are represented as foundation cards instead.
