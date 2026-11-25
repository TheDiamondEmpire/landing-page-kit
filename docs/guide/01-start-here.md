# 1. Start here

## What is in the folder

```text
index.html            gallery of the eight templates (delete it if you only need one page)
pages/                the eight landing pages, one HTML file each
  saas.html  app.html  launch.html  event.html
  waitlist.html  webinar.html  agency.html  pricing.html
css/
  tokens.css          colours, fonts, spacing, shape (edit this to rebrand)
  base.css            reset, type, buttons, form controls, focus, reduced motion
  sections.css        the shared section patterns (hero, features, pricing, FAQ, form, footer)
  pages/<name>.css    the look of one page: its colour tokens and page-only rules
js/
  theme.js            light/dark toggle (loads in <head>)
  menu.js             mobile menu button
  faq.js              optional FAQ behaviour
  form.js             form validation
  submit-adapter.js   what happens when the form is valid (a harmless stand-in)
  billing.js          monthly/yearly switch (pricing page only)
assets/               original SVG artwork and the favicon
docs/guide/           these guides
```

Each page links its own four stylesheets and only the scripts it needs, with relative paths (`../css/...`), so the folder works from the file system, from a sub-folder of a website, or from the root of a domain.

## Your first edit

1. Open `pages/saas.html` (or any page) in a text editor.
2. Change the text between tags. Headings are `h1` (once per page) and `h2` for each section.
3. Save and refresh the browser.

To keep one page, delete the other seven files in `pages/`, their `css/pages/<name>.css` files and the art in `assets/` that only they use. To make a page your home page, copy it to `index.html` in the root and change `../css/` to `css/`, `../js/` to `js/` and `../assets/` to `assets/` in that copy.

## Why the scripts are not ES modules

The kit is meant to work when you double-click a file. Browsers block `<script type="module">` files that are loaded from the file system, so the scripts are small classic scripts that load with `defer`. Each one is wrapped in a function, so nothing leaks into the page except one deliberate global, `window.lpkSubmit` in `js/submit-adapter.js`.

## A local server (optional)

Not needed for editing. If you want to see the pages on `http://127.0.0.1`, any static file server works.

## What the kit does not include

No tracking or analytics, no web fonts, no images from other sites, no cookies. The theme toggle stores the words `light` or `dark` in your browser's local storage on that device only. The email form does not send anywhere until you connect it (guide 4).

Made by The Diamond Empire, https://thedempire.shop/
