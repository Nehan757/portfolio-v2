# UI Design System — Nehan Tanwar Portfolio

A reusable design reference for building apps with the same aesthetic language.

---

## Design Philosophy

**Core idea:** A developer's physical workspace rendered digitally. The interface feels *tactile* — things you can pick up, paper you can read, a desk you're sitting at. Information is revealed through interaction rather than laid out flat.

**Guiding principles:**
- Warmth over sterility — dark browns and ambers, not pure black
- Analog textures in a digital medium — ruled paper, wood grain, coffee rings
- Terminal/code aesthetic for technical content, handwriting for personal content
- Everything has physical weight — shadows, depth, layering
- Reveal on interaction — the desk is a scene, not a layout

---

## Mood & Atmosphere

| Attribute | Description |
|-----------|-------------|
| **Tone** | Warm, focused, late-night coding session |
| **Energy** | Calm and confident — not flashy, not cold |
| **Feel** | Like walking into a tidy but lived-in workspace |
| **Metaphor** | A developer's desk: wood surface, coffee, earphones, scattered notes |

---

## Color Palette

```css
:root {
  /* Accent — electric cyan, the only "bright" color */
  --green: #06b6d4;
  --green-dim: rgba(6, 182, 212, 0.12);  /* accent bg tint */

  /* Backgrounds — warm dark, not cold dark */
  --desk:      #110e09;   /* deepest background */
  --modal-bg:  #131110;   /* modal / overlay surfaces */
  --card-bg:   #1a1714;   /* elevated cards */
  --card-hover:#1e1b18;   /* card hover state */

  /* Borders — subtle warm separators */
  --border:    #2a2420;

  /* Text hierarchy */
  --text:      #f5f0ea;   /* primary — warm white */
  --stone:     #a8a29e;   /* secondary */
  --muted:     #78716c;   /* tertiary / captions */

  /* Paper (analog surface) */
  --paper-bg:  #f5ede0;   /* cream notebook paper */
  --paper-line: rgba(150, 120, 90, 0.16);  /* ruled lines */
  --paper-margin: rgba(210, 70, 60, 0.22); /* red margin line */
  --paper-ink:  #3a2a18;  /* handwritten text */
  --paper-dim:  #7a6450;  /* faded handwritten text */
}
```

**Accent color alternatives (swap --green):**
- Cyan (default): `#06b6d4`
- Emerald: `#22c55e`
- Amber: `#f59e0b`
- Violet: `#a855f7`
- Blue: `#3b82f6`
- Red: `#ef4444`

---

## Typography

Three fonts, each with a distinct role:

### Display / UI — Space Grotesk
```
font-family: 'Space Grotesk', sans-serif;
```
- Used for: headings, body text, buttons, all UI chrome
- Weights: 300, 400, 500, 600, 700
- Character: geometric, modern, slightly quirky — not clinical

### Code / Technical — JetBrains Mono
```
font-family: 'JetBrains Mono', monospace;
```
- Used for: labels, tags, badges, timestamps, terminal widgets, file names
- Weights: 300, 400, 500 (italic variants available)
- Character: technical authority without being aggressive

### Handwriting / Personal — Caveat
```
font-family: 'Caveat', cursive;
```
- Used for: paper card content, personal notes, analog surfaces only
- Weights: 400, 600, 700
- Character: casual, human, unpretentious

### Type Scale
```
Hero name:      58px / weight 700 / tracking -0.025em
Section title:  34px / weight 700 / tracking -0.022em
Card title:     22px / weight 700
Body:           14.5px / weight 400 / line-height 1.78
Mono label:     11–12px / weight 400 / tracking 0.03–0.1em
Tag/badge:      10–11px
```

---

## Environment / Scene Design

The desktop view is a **physical scene**, not a layout:

### Background Layer
- Real photo of a wooden desk (`uploads/Gemini_Generated_Image_kdyiq9kdyiq9kdyi.png`)
- Overlaid with radial gradients to darken edges and add depth:
  ```css
  background:
    radial-gradient(ellipse 100% 50% at 50% 100%, rgba(0,0,0,0.5) 0%, transparent 65%),
    radial-gradient(ellipse 70% 35% at 50% 55%, rgba(0,0,0,0.18) 0%, transparent 80%);
  ```

### Ambient Code Snippets
Scattered Python/LangGraph snippets float over the desk at very low opacity (0.07–0.09), rotated slightly, never interactive. They establish context without demanding attention.

```css
position: absolute;
font-family: 'JetBrains Mono';
font-size: 10px;
color: rgba(6, 182, 212, 0.9);
opacity: 0.07–0.09;
transform: rotate(±4–8deg);
pointer-events: none;
```

### Paper Fan
Six notebook cards fanned out from a single pivot point. Each card:
- Cream ruled paper background with repeating-linear-gradient lines
- Red margin line on the left (classic notebook style)
- Handwritten font (Caveat) for content
- Rotates from a bottom-center pivot
- Lifts on hover with spring easing: `cubic-bezier(0.34, 1.56, 0.64, 1)`
- Shadows deepen on hover for physical lift feel

```
Card size:      484 × 400px
Rotation range: -34° to +29° (6 cards spread)
Z-index:        60 (front) to 10 (back)
Hover lift:     translateY(-200px)
```

---

## Component Patterns

### Badges / Status Pills
```css
background: var(--green-dim);
border: 1px solid rgba(6, 182, 212, 0.28);
border-radius: 20px;
padding: 4px 14px 4px 10px;
font-family: var(--mono);
font-size: 11px;
```
Always include a pulsing dot for "live" status:
```css
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50%       { opacity: 0.35; transform: scale(0.8); }
}
```

### Cards (Dark Surface)
```css
background: #1a1714;
border: 1px solid #2a2420;
border-radius: 12–14px;
/* hover */
border-color: rgba(6, 182, 212, 0.4);
background: #1e1b18;
transition: all 0.18s;
```

### Modal / Overlay
```css
/* Overlay */
background: rgba(6, 5, 4, 0.88);
backdrop-filter: blur(6px);

/* Modal */
background: #131110;
border: 1px solid #2a2420;
border-radius: 16px;
width: min(820px, 94vw);
max-height: 88vh;

/* Entry animation */
@keyframes modalIn {
  from { opacity: 0; transform: scale(0.75) translateY(16px); }
  to   { opacity: 1; transform: scale(1) translateY(0); }
}
animation: modalIn 0.38s cubic-bezier(0.34, 1.56, 0.64, 1);
```

### Skill / Tech Tags
```css
background: #1e1c18;
border: 1px solid #2e2c28;
color: #a8a29e;
border-radius: 4px;
padding: 3px 10px;
font-family: var(--mono);
font-size: 10.5px;
```

### Timeline
```css
/* Vertical line */
border-left: 1px solid;
background: linear-gradient(to bottom, var(--green), transparent);

/* Node dot */
width: 10px; height: 10px;
border-radius: 50%;
background: var(--green);
box-shadow: 0 0 10px rgba(6, 182, 212, 0.45);
```

### Terminal Widget
A floating monospace block that mimics a terminal prompt:
```css
background: #0a0807;
border: 1px solid #2a2420;
border-radius: 8px;
font-family: var(--mono);
font-size: 11.5px;
line-height: 2;
```
Lines prefixed with `❯` in accent color. Blinking cursor via:
```css
@keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }
animation: blink 1.1s step-end infinite;
```

### Buttons
```css
/* Primary */
background: var(--green);
color: #0a0807;
border-radius: 8px;
padding: 10px 24px;
font-weight: 600;
/* hover: filter: brightness(1.1); transform: translateY(-2px); */

/* Secondary */
background: transparent;
border: 1px solid #2a2420;
color: var(--text);
/* hover: border-color: var(--green); color: var(--green); */
```

---

## Animation Principles

| Interaction | Easing | Duration |
|-------------|--------|----------|
| Modal open | `cubic-bezier(0.34, 1.56, 0.64, 1)` — spring | 380ms |
| Card hover lift | `cubic-bezier(0.34, 1.56, 0.64, 1)` — spring | 320ms |
| Button hover | `ease` | 180ms |
| Card hover brightness | `ease` | 200ms |
| Overlay fade | `ease` | 220ms |
| Pulse (dot) | `ease-in-out` | 2000ms infinite |
| Steam rise | `ease-in-out` | 2500ms infinite |

**Rule:** Spring easing (`cubic-bezier(0.34, 1.56, 0.64, 1)`) for things that have physical mass. Linear/ease for color and opacity transitions.

---

## Responsive Strategy

**Desktop (>768px):** Full scene — photo background, paper fan, ambient code snippets. Immersive and unconventional.

**Mobile (≤768px):** Switch to a clean scrollable layout. Same dark warm palette, same fonts, but structured vertically:
- Hero header with name, role, stats, CTAs
- Tappable section cards that open the same modals
- No desk metaphor — too complex for touch

```js
const isMobile = window.innerWidth <= 768;
```

Modals adapt on mobile:
```css
@media (max-width: 768px) {
  .sec { padding: 28px 20px; }
  .hero-name { font-size: 38px; }
  .hero-term { display: none; }
  .skills-grid { grid-template-columns: 1fr; }
  .proj-tabs { overflow-x: auto; }
  .about-illus { display: none; }
}
```

---

## Reuse Checklist

When building a new app with this system:

- [ ] Import the three fonts (Space Grotesk, JetBrains Mono, Caveat)
- [ ] Set CSS variables from the color palette section
- [ ] Use warm dark backgrounds — never pure `#000` or cold grays
- [ ] Accent color drives all interactive states (borders, text, glows)
- [ ] JetBrains Mono for any label, tag, timestamp, or code-adjacent content
- [ ] Spring easing for anything that moves with "mass"
- [ ] Cards always have `#1a1714` bg + `#2a2420` border — hover shifts both slightly lighter + accent border
- [ ] Overlays always use `backdrop-filter: blur(6px)` + `rgba(6,5,4,0.88)`
- [ ] Pulsing dot = "live" or "active" status indicator
- [ ] `rgba(6,182,212,0.12)` as background tint wherever accent color applies to a surface
