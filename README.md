# Once Upon a Balloon

Static single-page site. No build step, no dependencies, no framework.

```
/
├── index.html      ← the entire site
├── vercel.json     ← static config
└── README.md
```

## Deploying

1. New GitHub repo, e.g. `once-upon-a-balloon`.
2. Put `index.html` and `vercel.json` in the **root** — not in a subfolder.
3. Push.
4. Vercel → Add New → Project → import the repo.
5. Framework Preset: **Other**. Root Directory: `./`. Build Command: leave empty. Output Directory: leave empty.
6. Deploy.

Vercel serves `index.html` at `/` automatically. Every push to `main` redeploys.

### Local preview on Windows
Open `index.html` in a browser directly, or from the repo folder:
```
python -m http.server 8000
```
then visit `http://localhost:8000`.

### Domain
Vercel → Project → Settings → Domains → add `onceuponaballoon.co.uk` and `www`.
At the registrar: `A` record for the apex to `76.76.21.21`, and a `CNAME`
for `www` to `cname.vercel-dns.com`. Vercel shows the exact values to use —
follow those rather than these if they differ.

---

## Before you publish — placeholders to replace

Search `index.html` for square brackets. All of them:

| Placeholder | Where |
|---|---|
| `[Your number]` | Enquiry section |
| `[Your town]` | Enquiry section, footer |
| `[X] miles` | Investment, FAQ, Enquiry |
| `[£X] per mile` | FAQ |
| `[Confirm your own terms before publishing.]` | Investment |
| `[Company details]` | Footer |
| `hello@onceuponaballoon.co.uk` | Nav-adjacent, Enquiry, Footer (×3) |
| Instagram / Pinterest / TikTok `href="#"` | Footer |

Also replace the three testimonials marked **Placeholder** with real ones.

## Making the enquiry form actually send

Right now it validates and shows a confirmation, but emails nobody.

**Formspree** (fastest): sign up, create a form, then change
```html
<form id="enq" novalidate>
```
to
```html
<form id="enq" action="https://formspree.io/f/YOUR_ID" method="POST">
```
Add a `name` attribute to each input matching its `id` (Formspree reads `name`,
not `id`), and delete the submit handler at the very bottom of the `<script>`.

**Netlify**: add `netlify` to the `<form>` tag instead, and host there.

## Notes

- Fonts load from Google Fonts (Newsreader + Manrope). Everything else is inline.
- Every balloon is drawn in SVG at runtime — no image files.
- Portfolio tiles are 4:5, the Instagram portrait ratio. Swap the generated
  SVGs for `<img>` tags when you have real photographs.
- Respects `prefers-reduced-motion`; all text passes WCAG AA contrast.
