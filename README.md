# ABHA Lab website — abha-lab.in

Hand-written static site: plain HTML and one CSS file. No build step, no JavaScript, no external requests (fonts are self-hosted).

```
index.html          Home: hero, themes, news
research.html       Themes in detail, "Why Bharat", collaborators
people.html         PI + students
publications.html   Full list, grouped by year
join.html           Openings and how to apply
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

- [ ] Set up email forwarding for `join@abha-lab.in` at your registrar (used on every page).
- [ ] People page: replace the "AM" initials with a photo if you want (`assets/abhi.jpg` + an `<img>`), and check the bio.
- [ ] Join page: check the PhD/MTech wording matches IIT Jammu's current admission process.
- [ ] Ask IIT Jammu IT for `abha.iitjammu.ac.in` → CNAME to `abha-lab.github.io` or a redirect to `abha-lab.in`.

## Editing

- **Add news:** copy one `<li>` in the News list in `index.html`; newest first.
- **Add a paper:** copy one `<li>` in `publications.html` under the right year. Wrap your name in `<span class="me">`.
- **Add a student:** copy the `.person` block in `people.html` into the Students section and delete the empty note.
- **New page:** copy `privacy.html`, change the `<title>`, the `aria-current` link and the `<main>` content, then add it to the nav in every page.

Header and footer are repeated in each file on purpose (no build tools). If you change the nav, change it in all pages:
`grep -l 'site-nav' *.html`
