# Greek InterVarsity at SDSU — website

**Live at [greekivsdsu.org](https://greekivsdsu.org)** — hosted free on GitHub
Pages, with DNS managed by Cloudflare.

A self-contained static rebuild of [greekivatsdsu.org](https://www.greekivatsdsu.org)
(the old Wix site), recreated as plain HTML and CSS.

No build step, no framework, no Wix. Open `index.html` in a browser and it works.
Every photo is stored in `images/`, so nothing depends on Wix's servers staying up.

## Running it locally

Any static file server works. The simplest:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. (Opening the `.html` files directly from Finder
also works — there is nothing that requires a server.)

## What's in here

```
index.html            Home
programs.html         Programs — Chapter Ministries, Gatherings, Retreats
students.html         Students — Start Here, GroupMe, chapter list, exec team
alumni.html           Alumni — newsletter, happy hour, memory wall
partner-with-us.html  Partner With Us — contacts, the need, funding goals, giving
blog.html             Blog (no posts published yet)
reunion.html          20 Year Reunion event page
css/styles.css        All styling, with the brand colors defined at the top
js/nav.js             Mobile menu toggle (the only JavaScript on the site)
images/               All 21 photos, downloaded at 2x for sharp retina display
```

### Original page addresses

The Wix site used some legacy slugs that don't describe their pages. The rebuild
uses readable filenames instead:

| Original Wix URL   | This repo              |
| ------------------ | ---------------------- |
| `/`                | `index.html`           |
| `/memory-wall`     | `programs.html`        |
| `/today-s-students`| `students.html`        |
| `/blank`           | `alumni.html`          |
| `/partner-with-us` | `partner-with-us.html` |
| `/blog`            | `blog.html`            |
| `/events/greek-iv-at-sdsu-20-year-reunion` | `reunion.html` |

If you ever point the real domain at this site, add redirects from the old
addresses so existing links keep working.

## Brand colors

Defined once as CSS variables at the top of `css/styles.css` — change them there
and they update everywhere:

| Color  | Value     | Used for                                  |
| ------ | --------- | ----------------------------------------- |
| Navy   | `#0B3C61` | Hero panel, headings, nav, buttons        |
| Lime   | `#95C93D` | Callout panels, buttons                   |
| Orange | `#E76127` | Alumni panel, sub-headings, buttons       |
| Ink    | `#2F2E2E` | Body text                                 |

## Fonts

The original uses two licensed fonts that can't be redistributed in a public
repo — Wix's **Horizon** for the big all-caps headings and **Avenir LT Heavy**
for body text. This rebuild substitutes the closest freely licensed equivalents
from Google Fonts:

- **Archivo** (weight 900, widest cut) in place of Horizon
- **Nunito Sans** in place of Avenir

They read almost identically. Headings are about 6% narrower than the original.
If the ministry has a license for the real fonts, swap the two `--font-*`
variables in `css/styles.css` and drop the Google Fonts `<link>` from each page.

## Intentional differences from the live site

Three small things were changed rather than copied:

1. **"Powered and secured by Wix"** was removed from the footer — it is no longer
   true and it linked to Wix's marketing site.
2. **The "Give Here" button** sat *below* the footer on the live site, escaped
   from the panel it belongs to. Here it sits directly under the "Will you join
   us in this vision" line, where it was clearly meant to go.
3. **The giving link** points straight at `give.intervarsity.org` instead of the
   Outlook safe-links wrapper the original used. Same destination, shorter URL.

Everything else — text, photos, colors, layout, and all outbound links (Google
Forms, GroupMe, Facebook, Instagram, the giving page) — matches the live site.

## Editing

The pages are ordinary HTML. Each one repeats the same header and footer markup,
so if you change a nav link, change it in all seven files.

Content that will need updating over time:

- Chapter ministry times and student leaders — `students.html`
- Event dates for the reunion and alumni happy hour — `index.html`, `alumni.html`
- Funding goal figures and charts — `partner-with-us.html`, `images/funding-*.jpg`
- The copyright year in the footer of every page

## Hosting

The site is served by **GitHub Pages** from the `main` branch. Any push to `main`
redeploys it automatically, usually within a minute.

The `CNAME` file in the repository root holds the custom domain. Don't delete it —
GitHub reads that file to know which domain to serve, and removing it takes the
site off `greekivsdsu.org`.

### DNS (Cloudflare)

`greekivsdsu.org` is registered at Cloudflare and points at GitHub's servers:

| Type  | Name  | Value                         | Proxy    |
| ----- | ----- | ----------------------------- | -------- |
| A     | `@`   | `185.199.108.153`             | DNS only |
| A     | `@`   | `185.199.109.153`             | DNS only |
| A     | `@`   | `185.199.110.153`             | DNS only |
| A     | `@`   | `185.199.111.153`             | DNS only |
| CNAME | `www` | `cornertocity-boop.github.io` | DNS only |

**Leave these on "DNS only" (grey cloud), not "Proxied" (orange cloud).** With
Cloudflare's proxy switched on, GitHub can't renew the HTTPS certificate and the
site eventually starts showing security warnings. Cloudflare will keep
recommending you enable proxying — ignore it, or the site will break at renewal
time.

The old Wix domain, `greekivatsdsu.org`, is untouched and still serves the Wix
site. Point it here (or redirect it) whenever you're ready to retire Wix.

## Photos

All photographs are Greek InterVarsity at SDSU's own and show real students.
Keep that in mind before making this repository public or reusing the images
anywhere else.
