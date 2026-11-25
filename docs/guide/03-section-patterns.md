# 3. Section patterns

Every page is built from the same documented patterns, styled in `css/sections.css`. Copy a block from one page into another and it will look right, because the page's colours come from its tokens. Page-only components (agenda, specs, timeline, speakers, gallery, switch) are styled in that page's own CSS file.

General rules: one `h1` per page (in the hero), `h2` for each section, `h3` inside cards. Every `<section>` that has a heading uses `aria-labelledby` pointing at that heading's `id`.

## Page frame

```html
<body class="page-saas">
<a class="skip-link" href="#main">Skip to main content</a>
<aside class="demo-bar" aria-label="Template notice">...</aside>   <!-- delete before publishing -->
<header class="site-header">...</header>
<main id="main" tabindex="-1">...sections...</main>
<footer class="site-footer">...</footer>
```

The `page-<name>` class on `<body>` lets the page's CSS file target only that page. Keep the skip link first and keep `id="main"` on `<main>`.

## Header and navigation

```html
<header class="site-header">
  <div class="container site-header__inner">
    <a class="brand" href="#top"><svg class="icon" ...></svg> Brand</a>
    <div class="header-actions">
      <button class="icon-btn" type="button" data-theme-toggle aria-pressed="false" aria-label="Dark theme">...</button>
      <button class="icon-btn menu-toggle" type="button" data-menu-toggle aria-expanded="false" aria-controls="site-nav" aria-label="Menu">...</button>
    </div>
    <nav id="site-nav" class="nav" aria-label="Primary"><ul>
      <li><a href="#features">Features</a></li>
      <li><a class="btn btn--small nav-cta" href="#signup">Start free</a></li>
    </ul></nav>
  </div>
</header>
```

Without JavaScript the navigation is simply visible. With JavaScript, below 48em the menu button opens and closes it (`js/menu.js`); Escape closes it. Remove the two buttons if you do not want a theme toggle or a menu.

## Hero

```html
<section class="hero hero--split" id="top" aria-labelledby="hero-title">
  <div class="container hero__grid">
    <div>
      <p class="eyebrow">Short label</p>
      <h1 id="hero-title">One clear promise</h1>
      <p class="hero__lede">One or two sentences.</p>
      <div class="hero__actions"><a class="btn" href="#signup">Main action</a><a class="btn btn--ghost" href="#features">Second action</a></div>
      <p class="hero__note">Reassurance</p>
    </div>
    <img class="hero__art" src="../assets/hero-saas.svg" width="640" height="480" alt="...">
  </div>
</section>
```

Variants: `hero--split` (text and image side by side from 56em) and `hero--center` (centred). Colours come from `--hero-bg`, `--hero-text`, `--hero-muted`.

## Proof (logo strip)

```html
<section class="proof" aria-labelledby="proof-title"><div class="container">
  <p class="proof__title" id="proof-title">Used by teams at</p>
  <ul class="logos"><li>Name</li>...</ul>
</div></section>
```

The marks are drawn in CSS. Replace the list items with `<li><img src="../assets/logo.svg" alt="Company name" height="28"></li>` for real logos you have permission to use. Only claim customers you really have.

## Features

```html
<section class="section" id="features" aria-labelledby="features-title"><div class="container">
  <div class="section__head section__head--center"><h2 id="features-title">...</h2><p class="section__lede">...</p></div>
  <div class="feature-grid">
    <article class="feature"><span class="feature__icon"><svg class="icon" viewBox="0 0 24 24" aria-hidden="true">...</svg></span><h3>...</h3><p>...</p></article>
  </div>
</div></section>
```

Related: `split` (text beside an image, add `split--reverse` to flip), `checklist`, `steps` (an ordered list that numbers itself), `quote-grid` with `quote`, and `section--surface` for a tinted band.

## Pricing

```html
<div class="plans">
  <article class="plan plan--featured">
    <h3 class="plan__name">Team <span class="badge">Most popular</span></h3>
    <p class="plan__desc">...</p>
    <p class="plan__price">$12 <small>per person, per month</small></p>
    <ul class="checklist"><li>...</li></ul>
    <a class="btn btn--block" href="#signup">Start free</a>
  </article>
</div>
```

The pricing page adds a monthly/yearly switch: price elements carry `data-monthly` and `data-yearly`, and `js/billing.js` swaps the text. A comparison table sits in `<section class="table-wrap" aria-label="..." tabindex="0">` so keyboard users can scroll it; keep a `<caption>`, `scope` attributes and visually hidden text for tick marks.

## FAQ

```html
<div class="faq" data-faq data-faq-exclusive>
  <details><summary>Question?</summary><p>Answer.</p></details>
</div>
```

Native `<details>` works with keyboard and screen readers and needs no JavaScript. `data-faq-exclusive` (optional, `js/faq.js`) closes the other answers when one opens.

## Form

```html
<div class="form-card">
  <form class="form" id="signup-form" data-lpk-form method="post" action="#signup">
    <div class="field">
      <label for="signup-email">Work email</label>
      <input id="signup-email" name="email" type="email" autocomplete="email" inputmode="email" required
             aria-describedby="signup-email-hint signup-email-error">
      <p class="field__hint" id="signup-email-hint">Helper text</p>
      <p class="field__error" id="signup-email-error" hidden></p>
    </div>
    <button class="btn btn--block" type="submit">Create free workspace</button>
    <div class="form-status" data-form-status role="status" aria-live="polite"></div>
  </form>
</div>
```

The contract `js/form.js` relies on: the form has `data-lpk-form`; every control has an `id` and a `<label for>`; the error element has the id `<control id>-error`; the status area has `data-form-status`. Optional attributes on a control: `data-msg-required`, `data-msg-email`, `data-msg-minlength` replace the default message wording; `minlength` and `required` work as in HTML. Supported controls: `input` (text, email), `textarea`, checkbox. Always keep the form inside `.form-card` (or another surface) so the error colour keeps its contrast. See guide 4 for sending the data.

## Footer

```html
<footer class="site-footer"><div class="container">
  <div class="footer-grid">
    <div><p class="footer-title">Brand</p><p>One sentence.</p></div>
    <nav aria-label="Product"><p class="footer-title">Product</p><ul class="footer-list"><li><a href="#features">Features</a></li></ul></nav>
  </div>
  <p class="footer-legal">Copyright line and legal links.</p>
</div></footer>
```

Give every `<nav>` its own unique `aria-label`. The placeholder footer links point at `#top`: replace them with your real pages.

Made by The Diamond Empire, https://thedempire.shop/
