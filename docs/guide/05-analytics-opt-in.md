# 5. Analytics, opt-in only

The kit ships with **no analytics, no tracking and no third-party requests**, and the automated tests fail if any appear in the pages, styles, scripts or artwork. Measuring visits is your decision, and in many places it needs a notice or consent first.

Nothing below is active. It is documentation only.

## If you decide to measure

1. Pick a provider and read its documentation and the privacy rules that apply to your visitors.
2. Update your privacy notice to name the provider and say what is collected.
3. If you need consent, load the script only after the visitor agrees (see the pattern below).
4. Re-test the page and confirm in the browser's network panel that only the requests you expect are made.

## Pattern: load a provider script only after consent

Replace `PROVIDER-SCRIPT-URL` with the script address your provider tells you to use. This is a generic pattern, not an endorsement of any provider.

```html
<!-- Put this at the end of <body> on pages where you want measurement. -->
<script>
  // Call this from your own consent banner when the visitor agrees.
  function loadAnalytics() {
    var s = document.createElement('script');
    s.src = 'PROVIDER-SCRIPT-URL';
    s.defer = true;
    document.head.appendChild(s);
  }
</script>
```

Many privacy-focused providers publish a single `<script defer src="..." data-domain="your-domain.example">` line instead; if you use one and your lawyer confirms no consent is needed for it, paste that line before `</body>` exactly as the provider documents it.

## Measure without a script

If you only need to know whether the page works, your host's server logs (visits) and your form provider's dashboard (sign-ups) need no code on the page.

## After you add anything

The kit's own tests will flag a tracking script. If you copy the test files into your own project, update them deliberately and record why.

Made by The Diamond Empire, https://thedempire.shop/
