# Serenichron Email Signature Generator

A single-file, zero-build web app that generates on-brand HTML email signatures for the
Serenichron team. **Live: https://serenichron.github.io/serenichron-signatures/** — or open
`index.html` in any browser. No server, no install.

Modeled on the [Kontas signature generator](https://github.com/Kontas-Management/kontas-signatures),
restyled to the [Serenichron design system](https://github.com/serenichron) (petrol teal +
signal orange, Montserrat), and extended with **one-click copy/paste into Outlook and Apple Mail**
in addition to HTML export.

## Features

- **Live preview** that updates as you type.
- **Copy signature** — copies rich (formatted) HTML to the clipboard so you can paste straight
  into Apple Mail, Outlook (Mac / new Windows), and Gmail signature editors.
- **Download HTML** — for classic Outlook on Windows and for archiving.
- **CSV batch import** — generate signatures for the whole team at once and download them as a ZIP.
- **Email-client-safe markup** — table-based layout with MSO conditionals, absolute image URLs,
  inline styles. No external CSS, no web fonts (falls back to Arial in mail clients).

## Usage

### Single signature
1. Open `index.html` in a browser.
2. Fill in the fields on the **Single person** tab. Optional fields (photo, address, CTA,
   social links) are omitted from the output when left blank.
3. Click **Copy signature**, then follow the in-app install steps for your email client.
   Or click **Download HTML** to save the file.

### Batch (CSV)
1. Switch to the **CSV import** tab.
2. Prepare a CSV using `signatures_template.csv` as the model. Column order matters; the header
   row is required:

   ```
   FirstName,LastName,Title,Phone,Email,Address,CTAText,CTAUrl,LinkedIn,Facebook,YouTube,Photo
   ```
   Wrap any value containing a comma in double quotes. Leave optional columns empty (keep the commas).
3. Upload the file, click **Process all**, then **Download ZIP archive**.

## Installing the signature per client

| Client | Method |
|---|---|
| **Apple Mail** | Settings → Signatures → add one → uncheck "Always match my default message font" → paste. |
| **Outlook (Mac / new Windows)** | Settings → Signatures → new → paste. |
| **Outlook (classic Windows)** | Download HTML, open in browser, Select-All + Copy, then paste into File → Options → Mail → Signatures. |
| **Gmail** | Settings → Signature → Create new → paste → Save changes. |

The in-app **How to install** section repeats these steps with exact menu paths.

## Brand assets

- **Logo:** `https://serenichron.com/wp-content/uploads/2025/06/Serenichron-logo-01-600x180.png`
  (rendered at 180px wide in the signature).
- **Tagline:** "Business systems, simplified."
- **Colors:** petrol teal `#367883` (name, links, tagline), signal orange `#FD9D58` (UI actions
  only), near-black navy `#040214`. See `DESIGN.md` in the main `serenichron` repo for the full token set.
- **Website:** https://serenichron.com

Images are referenced by absolute HTTPS URL so they render in email. If the logo URL changes,
update `LOGO_URL` in the `<script>` block of `index.html`.

## Notes

- **Social icons:** v1 uses text links (LinkedIn · Facebook · YouTube) for maximum email
  compatibility and zero hosting dependency. To switch to image icons, host brand-colored PNGs at
  a stable HTTPS URL and swap the `social` block in `generateSignatureHTML()`.
- **Clipboard copy** uses the async Clipboard API (`ClipboardItem`) with a `document.execCommand`
  fallback for older browsers. Requires opening the page over `http(s)://` or `file://` in a modern browser.
