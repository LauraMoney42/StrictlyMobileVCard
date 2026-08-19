# Project Overview: StrictlyMobileVCard

## Purpose

A digital business card for Ryan Ross, owner of Strictly Mobile Massage (a mobile
massage practice). The page is distributed by an NFC tag: a client taps the tag,
the card opens in their browser, and one button adds Ryan to their contacts.

Because distribution is physical rather than search-driven, the two things that
matter most are that the page loads fast on mobile data and that the contact
download actually imports on both iOS and Android.

## Technology

Plain HTML, CSS, and vanilla JavaScript in a single file. No framework, no build
tooling, no package manager, no runtime dependencies. Hosted on GitHub Pages from
the `main` branch, root folder.

## Architecture

Everything is `index.html`. It contains three parts:

1. **`<style>`**: all CSS, including the mobile breakpoint at 480 px.
2. **`<body>`**: header with photo and Add Contact button, bio, Book and Pay
   buttons, payment menu, contact rows, social links, services and pricing,
   modalities, and a corporate note.
3. **`<script>`**: the vCard string and download function, a payment menu
   toggle, a click rate limiter on payment links, and a right-click blocker.

Supporting files are `ryan-photo.jpg` (the profile image) and `robots.txt`.

## Key component: the vCard

The `Add Contact` button is the reason the project exists.

`const vCardData` is a JavaScript template literal holding a complete vCard 3.0
record. `downloadVCard()` wraps it in a `Blob` with type `text/vcard` and triggers
a download of `ryan_ross_strictly_mobile_massage.vcf`. This is fully client side.

Fields: `FN`, `N`, `ORG`, `TEL;TYPE=CELL`, `EMAIL`, `URL`, and an embedded
base64 `PHOTO`.

Two constraints are easy to break and worth stating plainly:

- **Line folding.** RFC 2426 caps lines at 75 octets. The base64 photo is folded
  across many lines, each continuation beginning with exactly one space. Because
  the data sits in a template literal, whitespace is preserved literally, so any
  stray indentation becomes part of the base64 payload and corrupts the image.
- **Size.** Many contact apps reject or stall on multi-megabyte `.vcf` files. The
  embedded photo is deliberately a small 300x300 JPEG.

## Known characteristics

- The page photo and the vCard photo are two separate images and must be updated
  separately.
- The right-click blocker is cosmetic only, it does not protect anything.
- Payment links are plain outbound links; no payment is processed on this site.
