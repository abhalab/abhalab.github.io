# ABHA Lab website — abha-lab.in

Hand-written static site: plain HTML and one CSS file. No build step, no JavaScript, no external requests (fonts are self-hosted).

```
index.html          Home: hero, venue strip, theme cards, latest news, selected papers, recruiting banner
research.html       Approach, "Why Bharat", themes with representative papers, collaborating institutions
people.html         PI profile, student slots, collaborators
publications.html   Full list by year, topic filter (CSS only), jump-to-year sidebar
news.html           Full news archive, grouped by year
join.html           Openings, how to apply, FAQ
privacy.html        What the site does (and doesn't) collect
404.html            Not-found page
CNAME               abha-lab.in (tells GitHub Pages your domain)
.nojekyll           Serve files as-is, skip Jekyll
assets/style.css    All styling; colours are tokens at the top
assets/fonts/       Mukta (Latin + Devanagari), SIL Open Font License
assets/favicon.svg
```

## Deploy

1. Create a GitHub organisation, e.g. `abha-lab`, and a repo inside it called `abha-lab.github.io`.
2. Push these files to the `main` branch:
   ```
   git init && git add . && git commit -m "Initial site"
   git branch -M main
   git remote add origin git@github.com:abha-lab/abha-lab.github.io.git
   git push -u origin main
   ```
3. Repo → Settings → Pages: Source = "Deploy from a branch", branch `main`, folder `/ (root)`.
4. At your registrar, set DNS for `abha-lab.in`:
   - `A` records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` for `www` → `abha-lab.github.io`
5. Repo → Settings → Pages → Custom domain = `abha-lab.in`. Tick **Enforce HTTPS** once the certificate is issued (can take up to an hour).
6. Org → Settings → Pages → add `abha-lab.in` as a verified domain (prevents domain takeover).

If you use a different org name, change `abha-lab.github.io` in steps 1, 2 and 4.

## Before going live

- [ ] People page: check the bio.
- [ ] People page: check the collaborators' affiliations are current.
- [ ] Join page: check the PhD/MTech wording matches IIT Jammu's current admission process.
- [ ] Ask IIT Jammu IT for `abha.iitjammu.ac.in` → CNAME to `abha-lab.github.io` or a redirect to `abha-lab.in`.

## Editing

- **Add news:** copy one `<li>` in `news.html` (newest first). If it belongs on the home page, copy it into the "Latest news" list in `index.html` too and drop the oldest one (keep about five). Tags are `<span class="pill">Paper</span>`; use `pill pill-glow` for lab announcements.
- **Add a paper:** copy one `<li class="pub ...">` in `publications.html` under the right year, and give it a unique `id`. Topic classes drive the filter: `t-mob` (mobility), `t-wl` (wireless), `t-anon` (anonymisation), `t-net` (network & IoT); add matching `<span class="pill">` tags. Wrap your name in `<span class="me">`. Update the counts in the filter chips, the year sidebar and the total.
- **Add a student:** in `people.html`, copy the commented member-card template into the `.members` list. Remove an "Open" card once that position is filled.
- **Add a photo:** put it in `assets/` and replace the initials inside `.hexavatar` with `<img src="assets/name.jpg" alt="">`.
- **New page:** copy `privacy.html`, change the `<title>`, the `aria-current` link and the `<main>` content, then add it to the nav in every page.

Header and footer are repeated in each file on purpose (no build tools). If you change the nav, change it in all pages:
`grep -l 'site-nav' *.html`
