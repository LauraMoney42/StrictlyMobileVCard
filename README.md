# Strictly Mobile Massage: Digital Business Card

A single-page digital business card for Ryan Ross of Strictly Mobile Massage.
The page is designed to be opened by tapping an NFC tag, and its main action is
an "Add Contact" button that saves Ryan's details straight to the visitor's phone.

## What is in the repo

| File | Purpose |
| --- | --- |
| `index.html` | The entire site: markup, CSS, and JavaScript in one file. No build step, no dependencies. |
| `ryan-photo.jpg` | Profile photo shown at the top of the card. |
| `robots.txt` | Crawl rules (slows down general crawlers, blocks several SEO bots). |

## Hosting

Served by GitHub Pages from the `main` branch, root (`/`) folder.

Live URL: https://lauramoney42.github.io/StrictlyMobileVCard/

There is nothing to build or compile. Pushing to `main` publishes the change.

## The "Add Contact" button

The button generates a vCard 3.0 (`.vcf`) file entirely in the browser. No server
or third party is involved.

The card data lives in a JavaScript template literal in `index.html` (search for
`const vCardData`). It is turned into a Blob and downloaded as
`ryan_ross_strictly_mobile_massage.vcf`.

The vCard includes name, organization, cell number, email, website, and an
embedded photo.

### Editing the vCard, please read first

Two rules matter for the file to import correctly on iOS and Android:

1. **Every line must be 75 characters or fewer.** RFC 2426 requires long values
   to be split ("folded") across multiple lines. The embedded `PHOTO` is already
   folded this way.
2. **Each continuation line of the photo starts with exactly one space**, at
   column 0, with no HTML indentation in front of it. The surrounding template
   literal preserves whitespace literally, so an accidental indent corrupts the
   photo data.

Keep the embedded photo small. Contact apps can reject or hang on very large
`.vcf` files, so the current photo is a 300x300 JPEG and the whole `.vcf` is
about 21 KB.

## Updating the profile photo

Replace `ryan-photo.jpg`, keeping the same filename so the `<img>` tag keeps
working. Before committing, resize it (800 px on the long edge is plenty) and
strip the EXIF metadata. Phone camera originals carry the device model and a
timestamp, which should not go into a public repo.

Note that the photo on the page and the photo inside the vCard are separate.
Changing `ryan-photo.jpg` does not change the contact-card photo; that one is
the base64 `PHOTO` block described above.

## Updating pricing and content

Pricing, services, bio, social links, and payment handles are all plain HTML in
`index.html`. Session prices sit under the "Services & Pricing" heading, in
elements with the class `price-main`.

## Payment links

The "Pay" button opens a menu with Venmo, Zelle, and Cash App links. These are
ordinary outbound links to each provider. No payments are processed by this site.
