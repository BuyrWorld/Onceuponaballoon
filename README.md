# Once Upon a Balloon

Static single-page site. No build step, no dependencies, no framework.

```
/
├── index.html      ← the entire site
├── vercel.json     ← static config
└── README.md
```

Push to `main` → Vercel redeploys. Framework Preset **Other**, no build command,
no output directory.

---

## Design system

Tokens live in one `:root` block at the top of the `<style>`. Change a colour
there and it propagates everywhere. CSS is numbered 01–20, JS 01–12.

### Colour

| Token | Value | Use |
|---|---|---|
| `--ivory` | `#F8F5EF` | primary ground |
| `--stone` | `#F1ECE4` | alternating sections |
| `--pure` | `#FFFDF9` | cards, form |
| `--charcoal` | `#171715` | buttons, footer |
| `--deep` | `#11110F` | statement section |
| `--ink` | `#191816` | body text — 16.3:1 |
| `--ink-2` | `#6D6861` | secondary — 5.1:1 |
| `--gold` | `#B9914A` | DECORATIVE ONLY — 2.7:1 on ivory, fails as text |
| `--gold-soft` | `#D2B77B` | gold text on dark grounds — 9.7:1 |
| `--gold-ink` | `#7E5C1E` | gold text on light grounds — 5.6:1 |
| `--blush` `--sage` | | palette accents |

`.on-dark` remaps `--bg / --fg / --fg-2 / --accent-tx / --rule`, so any section
flips dark by adding the class — no per-component overrides.

### Type
- **DM Serif Display** — headings only, never below ~1.15rem
- **Manrope** — everything else
- All sizes via `clamp()`; zero hardcoded px font sizes

### Radii
`0`, `2px`, `50%`. Nothing else.

---

## Before you publish

Search for `[` — every placeholder is bracketed:
`[Your number]` · `[Your town]` · `[X] miles` · `[£X] per mile` ·
`[Company details]` · `[Confirm your own terms before publishing.]`

Also: `hello@onceuponaballoon.co.uk`, the three `Placeholder —` testimonials,
and the social `href="#"` links.

## Making the form send

Inputs already carry `name` attributes, so it's a one-line change:

```html
<form class="enq-form" id="enq" action="https://formspree.io/f/YOUR_ID" method="POST">
```

Then delete the submit handler in JS section 11. (Or add `netlify` to the tag
if hosting there instead.)

## Dropping in real photography

Each editorial slot is a `.frame` with a generated `<svg>` inside:

```html
<div class="item" data-art="arch">
  <div class="frame frame--r34"></div>
</div>
```

Replace with:

```html
<div class="item">
  <div class="frame frame--r34"><img src="/img/arch.jpg" alt="…" loading="lazy"></div>
</div>
```

Remove the `data-art` attribute and the generator skips it. Grain, vignette and
hover-scale all apply to `<img>` identically. Ratios available:
`--r45` (4:5) · `--r34` (3:4) · `--r11` (1:1) · `--r1610` (16:10) · `--r219` (21:9).

Hero photography: put the `<img>` inside `.hero-stage` behind `.orbfield`.
The orbs float over it.
