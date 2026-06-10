# RaisePoint — marketing site

A small, fast, two-page marketing site for **RaisePoint**. It's plain HTML + CSS with
[Tailwind](https://tailwindcss.com/) loaded from a CDN and a little vanilla JavaScript —
**no build step, no npm, nothing to install.** You can edit every file by hand.

---

## 1. Preview it on your computer

**Double-click `index.html`.** It opens in your browser. That's it.

> ⚠️ Keep an internet connection while previewing — the fonts and the styling library load
> from the web. Everything else is local.

To click between the two pages and have it behave exactly like the live site, you can also
serve the folder locally (optional, needs Python which Macs already have):

```bash
cd raisepoint
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

---

## 2. The files

| File | What it is |
|------|------------|
| `index.html` | The main landing page (hero, about, security, coverage, use cases, who it's for, FAQ, final call-to-action, footer). |
| `request-access.html` | The private "Request access" page with the lead-capture form. |
| `styles.css` | **The one place to change colors and fonts.** Also holds the custom visual effects. |
| `favicon.svg` | The little icon in the browser tab (a placeholder, swap it anytime). |
| `assets/` | Images used by the site. Holds `hero.svg`, the picture on the right of the hero. Replace it with your own (see §3). |
| `reference/` | The design reference (the Intelic BASE screenshot), design notes, and the screenshots used while building. Not part of the live site, so you can delete it before deploying. |

Each section inside the HTML has a **comment above it** (lines that start with `<!--`)
telling you what it is, so you can find and edit the words easily.

---

## 3. Edit the words (copy)

1. Open `index.html` (or `request-access.html`) in any text editor — even TextEdit.
2. Look for the comment banners like `<!-- 2. HERO -->` or `<!-- 4. WHERE WE COVER -->`.
3. Change the text **between** the tags. For example, to change the headline, find:
   ```html
   <h1 ...>Verified intelligence on Ukraine &amp; EU defence-tech, built for the funds backing it.</h1>
   ```
   and edit the sentence. Leave the `<h1 ...>` and `</h1>` parts alone.
4. Save, then refresh the browser.

> ✍️ **Keep the messaging outcome-level.** Describe *what a customer gets*, never *how it's
> produced*: no sourcing methods, no scoring formula, no source lists. (This is baked into
> the current copy on purpose.)

### The hero visual (right of the first screen)
The hero shows a built-in, code-drawn recreation of the RaisePoint terminal (the `<div class="term">…</div>`
block in `index.html`). It needs no image file and stays sharp at any size. To edit the sample rows,
change the text inside the `.term-row` blocks.

**Prefer a real screenshot instead?** Put your image in `assets/` (e.g. `hero.png`) and replace the whole
`<div class="term">…</div>` block in `index.html` with:
```html
<div class="hero-frame"><img src="assets/hero.png" class="hero-img" alt="RaisePoint terminal" /></div>
```
Any size works; the image is cropped to fit the frame.

---

## 4. Recolor the whole site (1 place)

Open `styles.css`. Right at the top there's a block called `:root` with the palette:

```css
--bg:          #171717;  /* page background          */
--surface:     #1e1e1e;  /* cards                    */
--ink:         #fafafa;  /* headings                 */
--muted:       #b3b3b3;  /* body text                */
--accent:      #33c2ff;  /* primary accent (cyan)    */
--accent-deep: #1e6682;  /* deep accent (petrol)     */
```

Change a hex value (e.g. swap `--accent: #33c2ff` for an orange `#ff6d24`) and **the whole
site updates** — buttons, links, glows, the score highlight, everything. Save and refresh.

Fonts: the site uses **Inter** (loaded at the top of each HTML file). To change it, swap the
Google Fonts `<link>` in `index.html` / `request-access.html` and update `font-family` in
`styles.css`.

---

## 5. Make the form actually send you submissions

Right now the form on `request-access.html` **validates and shows a "Thanks" message, but does
not send anything anywhere** (a static site has no server). Pick one of these — all free:

### Option A — Formspree (recommended, ~2 minutes)
1. Go to [formspree.io](https://formspree.io), sign up, create a form. You'll get a URL like
   `https://formspree.io/f/abcdwxyz`.
2. In `request-access.html`, find:
   ```html
   <form id="access-form" action="#" method="POST" novalidate>
   ```
   and change `action="#"` to your Formspree URL:
   ```html
   <form id="access-form" action="https://formspree.io/f/abcdwxyz" method="POST" novalidate>
   ```
3. (Optional, for a nicer experience) In the `<script>` at the bottom of that file, there's a
   commented `fetch(...)` block inside the form handler. Follow the comment there to submit
   without leaving the page. If you skip this, the form still works — it just opens Formspree's
   own thank-you page.

### Option B — Tally or Google Forms (no code)
Create the form on [tally.so](https://tally.so) or Google Forms and replace the form card in
`request-access.html` with their embed code.

### Option C — mailto fallback (zero setup, least reliable)
Change the form tag to:
```html
<form id="access-form" action="mailto:hello@raisepoint.nl" method="POST" enctype="text/plain">
```
This opens the visitor's email app with the details pre-filled.

---

## 6. Put it online for free

Both options take a folder and give you a live URL. No account-wide setup, no command line.

### Cloudflare Pages
1. Go to **dash.cloudflare.com → Workers & Pages → Create → Pages → Upload assets**.
2. Drag the `raisepoint` folder (or a zip of it) onto the page.
3. Click deploy. You get a `*.pages.dev` URL. Add your own domain later in the dashboard.

### Netlify (drag-and-drop)
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the `raisepoint` folder onto the page.
3. You get a live `*.netlify.app` URL instantly.

> Tip: you can delete the `reference/` folder before deploying — it isn't used by the site.

---

## 7. Placeholders to replace before launch

Search the project for these and swap in real values:

- `hello@raisepoint.nl` — your real contact email (appears in both footers + the form page).
- `raisepoint.nl` — your real domain (in the `<link rel="canonical">` and meta tags).
- `favicon.svg` — replace with your own icon if you have one.
- `reference/social-card-placeholder.png` — add a 1200×630 image for nice link previews, or
  remove the `og:image` line in `index.html`.

---

Built as a static site so it stays fast, cheap to host, and fully under your control.
