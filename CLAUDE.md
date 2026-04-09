# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page website for **Skårsskolans Föräldraförening (SSFF)**. Plain HTML + CSS, no build step. Hosted on GitHub Pages at `https://dpontes.github.io/SSFF-website/`. Content is in **Swedish**.

## Files

- `index.html` — full single-page site
- `style.css` — all styles
- `tack.html` — thank-you page shown after contact form submission (auto-redirects to index after 5s)
- `Images/` — activity photos and Swish QR code

## Page Sections (in order)

1. **Hero** — tagline, "Bli medlem" button, Instagram and Facebook branded buttons
2. **Om oss** — description, bullet points, stats grid (42 families, 8 events/year, 8 board members, founded 2009)
3. **Senaste aktiviteter** — 3 activity cards with photos (skridskor, luciafika, julbazar)
4. **Kommande aktiviteter** — upcoming event list; each event has a date badge, time, and description
5. **Bli medlem** — membership info, Swish number `123-3587516`, QR code (desktop/tablet) or Swish deep-link button (phone only)
6. **Kontakt** — contact form submitting to `dpontes@protonmail.com` via FormSubmit AJAX

## Key Implementation Details

**Fonts:** Inter (400 + 700) from Google Fonts. Body: 16px, line-height 1.5. Headings: bold (700). Body text: normal (400).

**Responsive breakpoints:**
- General layout: `max-width: 800px` (single column, stacked nav)
- Phone-only elements (`.mobile-only`): `max-width: 767px` AND `pointer: coarse` — this intentionally excludes tablets (iPads are ≥768px) so they see the QR code instead of the Swish button

**Swish integration:**
- Desktop/tablet: shows QR code image (`Images/Medlemsvgift_swish-QR-small.png`)
- Phone: shows "Öppna i Swish" button built via JS using `https://app.swish.nu/1/p/sw/` with pre-filled payee (`1233587516`), amount (250 SEK, editable), and locked message (`Medlemsavgift`)

**Contact form:** Uses [FormSubmit](https://formsubmit.co) AJAX endpoint (`/ajax/dpontes@protonmail.com`). Submitted via `fetch` with `Accept: application/json`. On success, redirects to `tack.html` in the same tab. The FormSubmit address must be confirmed via email before forms are delivered.

**Scroll animations:** `IntersectionObserver` adds `.visible` to elements with `.reveal` class as they enter the viewport (threshold 0.12). Cards, stats, and events stagger by 80ms each.

## Adding a New Upcoming Event

Duplicate the `<li class="event">` block in the **Kommande aktiviteter** section of `index.html` and update the day, month, title, time, and description.

## Deployment

Push to `main` — GitHub Pages deploys automatically. No build step needed.
