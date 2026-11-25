# 4. Connect a form

Out of the box the forms are **demo only**. When a visitor submits a valid form, `js/form.js` calls one function, `window.lpkSubmit(data)`, defined in `js/submit-adapter.js`. The included version makes no network request and stores nothing. It shows a message marked "Demo" so nobody thinks sign-ups are being collected.

To go live, replace that one function. Nothing else needs to change.

## The contract

```js
window.lpkSubmit = function (data) { /* ... */ };
```

- Input `data`: an object with `email`, plus `name`, `message` or `consent` when the form has those fields, and `form` (the form's id) and `page` (the file name).
- Return a Promise that resolves to `{ ok: true, message: 'Thanks!' }`. The message is shown to the visitor. Add `demo: true` only for stand-ins.
- Reject, throw, or resolve with `ok` not true to show: "Sorry, something went wrong and nothing was sent. Please try again." The visitor's input is kept.
- `form.js` calls the function once per valid submission and ignores extra clicks while the Promise is pending.

## Example A: JSON POST to a provider endpoint

Most email and form services give you an endpoint URL that accepts a POST. Use the exact URL and format your provider documents.

```js
var LPK_ENDPOINT = 'PASTE-THE-ENDPOINT-YOUR-PROVIDER-GIVES-YOU';
window.lpkSubmit = function (data) {
  return fetch(LPK_ENDPOINT, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
    body: JSON.stringify(data)
  }).then(function (res) {
    if (!res.ok) throw new Error('HTTP ' + res.status);
    return { ok: true, message: 'Thanks! Check your inbox to confirm.' };
  });
};
```

## Example B: form-encoded POST

Many form back ends expect the classic encoding:

```js
window.lpkSubmit = function (data) {
  return fetch(LPK_ENDPOINT, { method: 'POST', body: new URLSearchParams(data) })
    .then(function (res) {
      if (!res.ok) throw new Error('HTTP ' + res.status);
      return { ok: true, message: 'Thanks, you are on the list.' };
    });
};
```

## Example C: mail link, no server

```js
window.lpkSubmit = function (data) {
  window.location.href = 'mailto:you@your-domain.example?subject=Signup&body=' + encodeURIComponent(data.email);
  return Promise.resolve({ ok: true, message: 'Your mail app should open with a prepared message.' });
};
```

Nothing is sent until the visitor presses send in their mail app, and it does not work for people without a mail app set up.

## Example D: redirect to a thank-you page

```js
window.lpkSubmit = function (data) {
  return fetch(LPK_ENDPOINT, { method: 'POST', body: new URLSearchParams(data) }).then(function (res) {
    if (!res.ok) throw new Error('HTTP ' + res.status);
    window.location.href = 'thanks.html';
    return { ok: true, message: 'Thanks! Taking you to the next page.' };
  });
};
```

## Things to settle before you collect real data

- **Cross-origin requests.** If the endpoint is on a different domain, the provider must allow requests from your site (CORS). If it does not, use a provider form action instead, or a small server of your own.
- **Privacy.** Name the provider in your privacy notice, say what you collect and why, and add a consent checkbox where the law of your visitors' country requires one. The consent checkbox pattern is in the webinar page: add `required` to make it mandatory and `data-msg-required` for your own wording.
- **Validate on the server.** The browser checks are a convenience, not a security measure. The receiving service must validate and rate-limit, and should use its own spam protection.
- **Test it.** Submit the live form with a real address you control, with the browser's network panel open, and confirm exactly what is sent and where.
- **Without JavaScript.** The form is `method="post" action="#..."`. For a no-JavaScript fallback, set `action` to your provider's form URL; with JavaScript on, the adapter takes over and the page does not reload.

Made by The Diamond Empire, https://thedempire.shop/
