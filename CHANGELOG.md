# Changelog

## 2026-08-19 12:30
- Fixed dead website URL in the vCard: `strictlymobilemassage.netlify.app` returned
  HTTP 404, changed to `https://strictlymobilemassage.com` (verified HTTP 200)
- Resized `ryan-photo.jpg` from 2268x4032 (1.9 MB) to 450x800 (64 KB) and stripped
  all EXIF metadata, which had included the camera make and model (Samsung
  SM-N970U1), firmware version, and a capture timestamp, before publishing publicly
- Rebuilt the embedded vCard `PHOTO`: replaced a single unfolded 2,538,572 character
  line with a 300x300 head-and-shoulders JPEG, base64 encoded and folded to RFC 2426
  75 octet lines. The generated `.vcf` went from about 2.5 MB to 21.2 KB, and
  `index.html` from 2,566,431 bytes to 49,315 bytes
- Verified the folded photo: all lines 75 characters or fewer, every continuation
  line starts with exactly one space, and the unfolded base64 decodes to a valid
  JPEG (FFD8 header, FFD9 trailer) that is byte identical to the source
- Removed `vcard.html`, an exact byte for byte duplicate of `index.html`
- Removed `create-enhanced-vcard.html`, a leftover generator scratch file
- Added `README.md`, `PROJECT_OVERVIEW.md`, and `CHANGELOG.md`
- Files affected: `index.html`, `ryan-photo.jpg`, `vcard.html` (deleted),
  `create-enhanced-vcard.html` (deleted), `README.md`, `PROJECT_OVERVIEW.md`,
  `CHANGELOG.md`
