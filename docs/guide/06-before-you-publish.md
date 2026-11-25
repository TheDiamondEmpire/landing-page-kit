# 6. Before you publish

## Replace the sample content

- [ ] Delete the demo bar (`<aside class="demo-bar">`) on each page.
- [ ] Replace every brand name, headline, price, date, name and address. Search for the word "sample": it marks text you must replace.
- [ ] Replace sample testimonials, customer logos and press mentions with real ones you have permission to use, or delete the section. Do not publish numbers or claims you cannot support.
- [ ] Replace the placeholder footer links (they point at `#top`) with real privacy, terms and contact pages.
- [ ] Replace the hero artwork or keep it. Give every informative image real `alt` text; use `alt=""` only for decoration.

## Page details

- [ ] Write a unique `<title>` (about 50 to 60 characters) and `<meta name="description">` (about 120 to 160 characters) for each page.
- [ ] Open Graph: each page has `og:title`, `og:description` and `og:type`. Social networks also want an absolute image address, so add `<meta property="og:image" content="https://your-domain.example/path/preview.png">` and `<meta property="og:url" content="https://your-domain.example/page">` once you know your domain. They are left out because a relative address does not work there.
- [ ] Add `<link rel="canonical" href="https://your-domain.example/page">` once the final address is known. It is left out on purpose.
- [ ] Update `lang` on the `<html>` tag if your page is not in English.
- [ ] Replace `assets/favicon.svg` with your own icon.

## Forms and privacy

- [ ] Connect the form (guide 4) and test it with a real submission. Until then it shows a "Demo" message and sends nothing.
- [ ] Add a privacy notice that names the services you use. Add consent wording where the law requires it.
- [ ] Add analytics only deliberately (guide 5).

## Test what you built

- [ ] Open each page at phone width, tablet width and a wide screen. Nothing should scroll sideways.
- [ ] Use only the keyboard: Tab through the page, open the menu, open FAQ items, submit the form. Focus must always be visible.
- [ ] Switch your system between light and dark, and press the theme button.
- [ ] Turn on "reduce motion" in your system settings and confirm the page stays usable.
- [ ] Run a contrast checker on any colours you changed (guide 2) and an accessibility scanner of your choice. Automated scanners find only a part of the problems that affect people, so also try a screen reader and ask someone else to try the page.
- [ ] Open the browser's network panel, reload, and confirm only your own files and the services you chose are requested.

## Publishing

Upload the folder to any static host (your web host, an object-storage bucket with website hosting, or a static-site service). No build step and no server software are required. Keep the folder structure so the relative paths keep working.

Made by The Diamond Empire, https://thedempire.shop/
