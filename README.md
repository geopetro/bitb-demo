# Browser-in-the-Browser (BitB) Simulation

This repository demonstrates the Browser-in-the-Browser technique first documented by
[mr.d0x (2022)](https://mrd0x.com/browser-in-the-browser-phishing-attack/).

It's a single self-contained HTML page that draws a fake browser popup window on top of a blurred background document, with
a working Microsoft-style sign-in form inside it. The fake address bar can show a trusted-looking
URL even though nothing has actually navigated anywhere.

Built as a personal learning project to explore the BitB technique and for awareness testing.

> Authorized use only. This is for security awareness training, red-team labs, and defender
> exercises. Don't use it against anyone you aren't explicitly allowed to test.

## Files

- `Microsoft_BitB.demo.html` — the self-contained page.

## Picking the background

Set `data-lure` on the `<body>` tag to choose the blurred document behind the popup:

- `1` Excel (current default)
- `2` Word
- `3` PowerPoint
- `4` OneNote 
- `5` Visio

The tab title and icon change to match.

## The form

The sign-in form is real page DOM (not an iframe). In this build the form's `action` is `#`;
operators point it at their own capture endpoint when wiring it up.

### Sign-in flow

Three sliding steps, mirroring the real Microsoft sign-in:

1. **Email** — type an address, click **Next**. Nothing is sent; the panel slides to the
   password step. The address shown above the password field has a `←` back button to return.
2. **Password** — enter a password, click **Sign in**. Nothing is sent yet; the panel slides
   to the "Stay signed in?" step.
3. **Stay signed in?** — click **No** or **Yes**. *This* step POSTs the full form (email +
   password + a `stay=no|yes` field) to whatever `action` is set to. There's also a
   "Don't show this again" checkbox, submitted alongside.

## Disclaimer

For education and authorized testing only. Don't misuse it.
