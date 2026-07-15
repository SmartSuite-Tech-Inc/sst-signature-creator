# SST Signature Creator

Internal tool for **SmartSuite Tech** — generates consistent, email-client-safe
HTML signatures for the whole team.

**Live tool:** https://smartsuite-tech-inc.github.io/sst-signature-creator/

## How the team uses it

1. Open the tool in a browser.
2. Fill in your **name, title, email, website, and phone**.
3. Pick the logo that matches your email background (light or dark).
4. Copy your signature:
   - **Copy signature** — copies the *rendered* signature (formatting + logo).
     Use this for most mail clients.
   - **Copy HTML code** — copies the raw HTML. Use this for Outlook on the web
     or anywhere that accepts pasted HTML source.
5. Paste into your mail client:
   - **Apple Mail:** Mail → Settings → Signatures → **+** to add a signature →
     **uncheck "Always match my default message font"** (otherwise Mail strips
     the formatting) → select the placeholder text and paste (⌘V). The logo
     often shows as a broken/blank box *inside Settings* — that's normal;
     send yourself a test email and it renders in real messages.
   - **Outlook:** Settings → Mail → Signatures → paste.

The signatures are **table-based HTML with inline styles** — required because
most email clients strip modern CSS. Don't "modernize" `buildSig()` in
`index.html`.

## Updating the logos

The two logo files live in [`/assets/`](assets/):

| File | Used for |
|---|---|
| `assets/logo-black.png` | Light email backgrounds (black logo) |
| `assets/logo-white.png` | Dark email backgrounds (white logo) |

To update a logo, **replace the PNG with the same filename**, commit, and push.
Existing signatures in people's mail clients keep working because they point at
these hosted URLs — updating the file updates everyone's logo (may take a few
minutes for GitHub Pages + email-client caches to refresh).

> ⚠️ Don't rename or move these files — every signature already copied by the
> team embeds their full URL. Renaming breaks the logo in previously created
> signatures.

Editing brand colors or logo paths: see the maintenance comment block at the
top of [`index.html`](index.html).

## Hosting notes

- Pure static HTML/CSS/JS — no build step, no server-side code.
- Logo paths are stored relative (`assets/…`) but converted to **absolute URLs**
  at runtime, so copied signatures always reference the hosted logo files.
  This means signatures should be created from the **GitHub Pages URL**, not
  from a local copy of the file (a local copy would embed `file://` paths that
  no one else can load).

## Enabling GitHub Pages

Repo → **Settings → Pages** → Source: *Deploy from a branch* →
Branch: `main`, folder `/ (root)` → Save. The tool will be live at
`https://<username-or-org>.github.io/sst-signature-creator/` within a minute or two.
