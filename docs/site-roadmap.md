# DStorm Digital — Site Roadmap

## CRITICAL (pre-launch blocker)

### Contact form silently drops leads in browsers without configured mail clients
The contact form on `contact.html` uses a `mailto:` link as its submission mechanism. On modern
mobile devices and most Windows machines without a configured mail client, submitting the form does
nothing — no email is sent, no error is shown. The success screen still fires ("Message sent!"),
so the visitor believes their inquiry was delivered when it was not.

**Fix:** Replace with [Web3Forms](https://web3forms.com) (free tier: 250 submissions/month, no
backend required, GDPR-compliant, delivers to any email address). Drop-in replacement — swap the
form's submit handler for a `fetch` POST to `https://api.web3forms.com/submit` and add a hidden
`<input name="access_key" value="YOUR_KEY">` field.

---

## Follow-up Work

### Favicon
No favicon is defined on any page. Add a text-based inline SVG favicon (no image file needed) to
the `<head>` of all four pages. A simple "D" or "DS" monogram in navy/gold matches the brand.

### Open Graph & Twitter card meta tags
No social sharing metadata exists. When the site URL is pasted into LinkedIn, iMessage, or
Twitter/X the preview is blank. Add `og:title`, `og:description`, `og:url`, and `og:image` to
all four page `<head>` sections, plus `twitter:card` summary tags.

### Mobile nav hamburger → X animation
The hamburger button has no visual state change when the mobile nav is open. Add a CSS transition
that morphs the three bars into an X (`aria-expanded` toggle + transform on the `<span>` elements)
so users know how to close the menu.

### Canonical URL consistency
`vercel.json` sets `"cleanUrls": true` so `/services`, `/portfolio`, etc. are the canonical URLs.
All internal `href` attributes still use `.html` extensions (`services.html`, `portfolio.html`).
Both forms resolve correctly, but `<link rel="canonical">` tags pointing to the clean URLs would
signal the preferred form to search engines.
