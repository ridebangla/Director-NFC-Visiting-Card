# Emon Seddik — NFC Visiting Card (Director) — Build Report

**Status: STAGED ONLY.** Built in `~/workspace/nfc-cards/director/`. Nothing was pushed,
deployed, or written to any live repo. The CEO repo (`ridebangla/CEO-NFC-Visiting-Card-`)
was only read/copied from, never edited. The coordinator creates the GitHub repo, pushes,
and deploys on Vercel after verification.

## Person (only source used: main-website team data, as briefed)

- **Emon Seddik — Co-Founder & Director, Ride Bangla Limited**
- Personal phone / WhatsApp: **+8801885002951** (displayed as +880 1885 002951, same
  grouping style as the CEO card)
- Facebook: https://www.facebook.com/share/14gWYs5XrYE/ (verbatim share URL)
- Instagram: https://www.instagram.com/emonrehman51
- X: none. WeChat: none. Personal email: none on the main site.
- Kept from the CEO card: company phone +8801309587749, company email
  info@ridebangla.bd, company site https://ridebangla.bd, location Faridpur,
  Bangladesh 7803 (Google Maps query unchanged), company tagline, overview, services,
  official links, layout, colours, fonts, logo, icons, service SVGs, `vercel.json`,
  LICENSE and standard files (all byte-identical to the template where the brief
  required copy-as-is).

## Domain

Every `the previous subdomain` self-reference now reads **https://director.ridebangla.bd**:
canonical/OG/Twitter URLs, JSON-LD `url`, manifest `id`/`scope`/`start_url`,
`robots.txt` sitemap URL, `sitemap.xml` loc, README links/badges, and the QR target.

## What changed in `index.html` (scripted replacements, never by hand)

- Name/title everywhere: the previous holder's name / the previous title → Emon Seddik /
  Co-Founder & Director (meta, OG, Twitter, JSON-LD, keywords, front-face name/role,
  portrait alt text, vCard).
- Phones: `tel:the previous personal number` → `tel:+8801885002951`; `wa.me/the previous personal number` →
  `wa.me/8801885002951`; vCard `TEL:+8801885002951`, `N:Seddik;Emon`,
  `TITLE:Co-Founder & Director`; email/URL/ADR kept.
- Download filenames: `Emon-Seddik-RideBangla.vcf`,
  `Emon-Seddik-RideBangla-Card-Front.jpg`, `Emon-Seddik-RideBangla-Card-Back.jpg`.
- Portrait: the page's single `data:image/jpeg;base64` portrait was replaced wholesale
  with Emon's photo, square-cropped (975×1254 → 975×975, top offset 40px so the head
  keeps headroom) and resized to 640×640, JPEG quality 85 (45,574 bytes vs the
  original's 33,703 — same order of magnitude). Repo `photo.png` is the same crop as
  PNG 640×640.
- QR: the brief's "if runtime-derived" branch does **not** apply — the QR is
  **hardcoded**: `q.addData` with the previous subdomain in the page script. It was
  swapped to `q.addData('https://director.ridebangla.bd/')` (qrcode-generator 1.4.4,
  error correction H, same as before).

## Back-side buttons — final set (5, not 6)

| Button | Target |
|---|---|
| Website | https://ridebangla.bd (kept) |
| WhatsApp | https://wa.me/8801885002951 |
| Facebook | https://www.facebook.com/share/14gWYs5XrYE/ |
| Instagram | https://www.instagram.com/emonrehman51 (NEW) |
| Location | Faridpur, Bangladesh 7803 map link (kept) |

- The CEO card truly had **no Instagram slot** (0 mentions in the template) — confirmed,
  so one Instagram button was added in the exact same button style/class and geometry
  as the removed WeChat button (`--x:50;--y:930;--w:312;--h:148`, first column, row 2).
- X and WeChat buttons were **removed entirely** (anchor + WeChat copy-to-clipboard JS),
  never replaced with invented links. The middle slot of row 2 is therefore empty;
  Website/WhatsApp/Facebook (row 1) and Location (row 2, third column) keep their exact
  original positions.
- `sameAs` in JSON-LD is now the Facebook share URL + the Instagram URL (the only two
  personal social URLs that exist for Emon).
- Note: `x.com/ridebangla` still appears in the README's "Follow Ride Bangla
  everywhere" company section. That is the **company** account, kept verbatim with the
  other official links — it is not Emon's personal X, and no X button exists on the card.

## Docs images — the previous holder material deliberately NOT reused

- Template `docs/images/card-back.png` shows the CEO back face (WeChat/X tiles, CEO QR)
  and `docs/screenshots/card-desktop.png` shows the previous holder's face, name and phone. Both
  were **deleted from this tree, not copied**.
- The template README's hero reference (`docs/images/card-front.png`) pointed at a file
  that does not exist in the template tree — flagged here, not silently carried over.
- New `docs/images/card-front.png` and `docs/images/card-back.png` are fresh renders
  of **this** card (see Verification). The empty `docs/screenshots/` directory was
  removed. The README's "live card" wording was corrected to "rendered locally …
  refresh after the live deploy", and the CEO card's "final, as confirmed by the owner"
  sentence was **not** carried over (this card is staged, not owner-confirmed).

## Blank card frames

`card-front.jpg` / `card-back.jpg` are reused as-is (byte-identical). They are blank
dark-green + gold frames (empty photo circle, empty boxes, QR frame) with no name,
photo or text — they leak nothing. This report does not claim they show any person.

## Verification (honest, multi-angle)

1. **Leak grep on the full output tree (text files):** `the previous holder`, `the previous handle`,
   `the previous personal number`, `previous-subdomain`, `the previous title`, `chat-app deep link`, `WeChat` → **0
   matches**. Positive checks pass: `Emon Seddik` ×16, `Co-Founder & Director` ×8,
   `director.ridebangla.bd` ×12, `+8801885002951`, `wa.me/8801885002951`, Facebook
   share URL ×3, Instagram URL ×2, `Emon-Seddik-RideBangla` ×7 in `index.html`.
2. **Headless Chromium render (Playwright, phone 390px primary + desktop):**
   - First pass over `file://` failed to load CDN/fonts (sandbox proxy tunnel errors)
     and a centre-click landed on a phone hit-area link, so the card did not flip
     (the page correctly ignores clicks on links for flipping). Both are sandbox /
     test-method artefacts, not page defects — see below.
   - Second pass served the tree over local HTTP with the QR library vendored
     locally. The vendored `qrcode.min.js` SHA-384 matches the page's SRI pin
     exactly, so it is byte-identical to the shipped pinned library; the shipped
     page still loads it from cdnjs with the SRI pin (no local file was added to
     this repo). Google Fonts were likewise vendored for the render only.
   - Front face verified visually: Emon's portrait, "Emon Seddik", "Co-Founder &
     Director", +880 1885 002951, info@ridebangla.bd, ridebangla.bd, Faridpur.
   - Back face verified visually after a neutral-corner click (flip class toggles
     `inner` → `inner flipped` → `inner`): QR renders, five buttons in the set above,
     About Us kept. Company panel / services section verified on desktop: all 8
     services, overview, official links, company phone.
3. **QR target proven, not assumed:** the page-rendered QR SVG module path is
   byte-identical to a fresh qrcode-generator 1.4.4 encoding of
   `https://director.ridebangla.bd/` and differs from the CEO-URL encoding.
4. **vCard download tested:** clicking "Save Contact to Phone" in the headless
   browser downloaded `Emon-Seddik-RideBangla.vcf` with exactly the fields listed
   above (N, FN, ORG, TITLE, TEL +8801885002951, EMAIL info@ridebangla.bd,
   URL ridebangla.bd, ADR Faridpur 7803 Bangladesh).
5. **Manifest / robots / sitemap** carry the new domain (verified by reading them).
   **README** carries Emon's details, the new domain, five-tile wording, the
   Instagram row (X/WeChat rows removed), and only the new card renders.
6. **Unverified / owed to the coordinator's live check:** live behaviour on the real
   `director.ridebangla.bd` URL after Vercel deploy (CDN + fonts from the public
   internet, NFC tap, phone rendering on a real device, QR scan to the live URL).
   The sandbox renders used fallback-then-real fonts and a local server; the
   coordinator's live verification after deploy is still required before this is
   called done.

## Push-back / corrections to the brief (with evidence)

- **QR is hardcoded, not runtime-derived** — the brief's conditional is resolved:
  the swap was made in source (`q.addData`), not left to runtime behaviour.
- **No Instagram slot existed** — confirmed (0 mentions); the button is a genuine
  addition in the WeChat slot, not a relabel.
- **Template README hero image was already broken** (referenced a missing
  `docs/images/card-front.png`); this tree supplies real renders instead.
- **Display-phone grouping** (+880 1885 002951) is inferred from the CEO card's
  grouping pattern (+880 1626 633316), not from team data — it is formatting only;
  the dialled number is the briefed +8801885002951 verbatim.

## Files

- Repo tree: `~/workspace/nfc-cards/director/` (complete: `index.html`, `photo.png`,
  `logo.png`, icons, `card-front.jpg`, `card-back.jpg`, `assets/services/*.svg`,
  `manifest.json`, `robots.txt`, `sitemap.xml`, `vercel.json`, LICENSE,
  CODE_OF_CONDUCT.md, CONTRIBUTING.md, SECURITY.md, CLIENT-LICENSE-TEMPLATE.txt,
  `.gitignore`, README.md, `docs/images/card-front.png`,
  `docs/images/card-back.png`)
- This report: `~/workspace/nfc-cards/director/REPORT.md`
- No secrets, no invented copy, no invented links anywhere in the tree or this report.

---

# VERIFIER SECTION — independent verification, 2026-10-27 (separate team)

**Scope note:** this section was written by the independent verifier, not the builder.
Nothing was pushed, deployed, or written to any live repo or to the CEO repo. The
only file changed in this tree by the verifier is `sitemap.xml` (lastmod, below).
`index.html` and all docs images are UNCHANGED by the verifier, for the reason in
§V3. Leak-sensitive identifiers are deliberately NOT spelled out in this section
(the builder's report does the same): writing them here would itself make a future
leak grep over this tree match. Counts below are for the previous holder's name,
handle, personal number, subdomain, and title, each searched separately.

## V1. Leak grep — PASS (0 matches)

- `grep -R -a` over the WHOLE tree (text + binary files, including PNG/JPG bytes):
  previous holder's name: 0; previous handle: 0; previous personal number: 0;
  previous subdomain: 0; previous title (the CEO-form title): 0.
- A loose substring search for "ceo" hits only incidental letter sequences inside
  the base64 portrait blob — not a domain, link, or name — and is not a leak.
- Re-run after the sitemap edit: still 0 on every term.

## V2. Positive checks — PASS

- `index.html`: Emon Seddik ×13, "Co-Founder & Director" ×7,
  director.ridebangla.bd ×7, +8801885002951 ×4, wa.me/8801885002951 ×1,
  Facebook share URL ×3, Instagram URL ×2, company phone +8801309587749 ×1,
  info@ridebangla.bd ×7, Faridpur ×7, 7803 ×7, Emon-Seddik-RideBangla ×7.
- Canonical + OG + Twitter URLs, JSON-LD `url`, manifest `id`/`scope`/`start_url`,
  `robots.txt` sitemap URL, `sitemap.xml` loc, README links, and QR data
  (`q.addData('https://director.ridebangla.bd/')`) all carry director.ridebangla.bd.
  JSON-LD `sameAs` = Facebook share URL + Instagram URL only.
- vCard (JS-generated, lines ~242–252): `N:Seddik;Emon;;;`, `FN:Emon Seddik`,
  `ORG:Ride Bangla Limited`, `TITLE:Co-Founder & Director`,
  `TEL;TYPE=CELL,VOICE:+8801885002951`, `EMAIL:info@ridebangla.bd`,
  `URL:https://ridebangla.bd`, `ADR:;;;Faridpur;;7803;Bangladesh`. Correct.
- Download filenames in source: `Emon-Seddik-RideBangla.vcf` (×1),
  `Emon-Seddik-RideBangla-Card-Front.jpg` (×3),
  `Emon-Seddik-RideBangla-Card-Back.jpg` (×3). No previous-holder filename remains.
- Back buttons (verified in source AND in live rendered geometry, phone 390px):
  Website → https://ridebangla.bd; WhatsApp → https://wa.me/8801885002951;
  Facebook → https://www.facebook.com/share/14gWYs5XrYE/;
  Instagram → https://www.instagram.com/emonrehman51;
  Location → https://www.google.com/maps/search/?api=1&query=Faridpur%2C%20Bangladesh%207803.
  Rendered positions (phone): row 1 y≈290 — Website x≈31, WhatsApp x≈145,
  Facebook x≈252; row 2 y≈348 — Instagram x≈31, Location x≈252, middle slot
  (x≈145) has NO button. See §V3.
- No X button, no WeChat button, no dead links in `index.html`: "WeChat" 0,
  "x.com" 0, "twitter.com" 0, `href="#"` 0, `href=""` 0, no TODO/FIXME/placeholder
  anchors. The only remaining share-code is the legitimate vCard/download logic
  (no WeChat copy-to-clipboard JS remains; a generic `copyText` helper exists but
  is not wired to any removed button — verify at apply time that it is unused or
  retained only if the template used it elsewhere).
- Nuance, NOT a failure: the README's "Follow Ride Bangla everywhere" COMPANY
  section still links the company's X account (x.com/ridebangla), kept verbatim
  with the other official company links. That is the company account, not a
  personal X button on the card, and no X button exists on the card itself.
  If the coordinator wants zero "x.com" strings anywhere including the README,
  that is a separate decision, not a card defect.
- README: carries Emon's details + director.ridebangla.bd only for the person/domain
  (7 director-domain mentions, no previous-subdomain string). Every docs/ reference
  in the README resolves to an existing file: `docs/images/card-front.png` and
  `docs/images/card-back.png` both exist; `manifest.json`, `vercel.json`,
  `SECURITY.md`, `LICENSE`, `card-front.jpg`, `card-back.jpg` all exist.
  (A scripted "mailto:…" hit is a mailto link, not a missing file.)

## V3. KNOWN DEFECT — REPRODUCED, FIX *NOT* APPLIED (STOP clause invoked)

- **Reproduced independently:** the back face renders an EMPTY gold box in the
  middle of row 2 (row 1: Website/WhatsApp/Facebook; row 2: Instagram / EMPTY /
  Location). Confirmed in the verifier's own headless-Chromium render (§V5) and
  in the shipped `docs/images/card-back.png`, which shows the same empty box.
- **Why a button reflow alone CANNOT fix it (this is the key finding):**
  the `.btn` elements have `background:transparent; border:0` — they are invisible
  hit-areas with an icon + label. The six gold boxes are BAKED INTO the
  background artwork `card-back.jpg` (verified visually: the blank frame alone
  shows 3 boxes in row 1 and 3 in row 2), and that file is byte-identical to the
  template. Reassigning button placements only MOVES the empty box: putting
  Location in the middle slot leaves the right-hand baked box empty; widening a
  row-2 button does not paint over a baked outline and would mis-centre its icon.
  No placement of 2 buttons over 3 baked boxes yields "no empty box".
- **Action taken per the task's STOP clause: NO redesign, NO button move,
  NO docs-image replacement.** Moving buttons without fixing the artwork would
  have produced a still-empty box in a new position and a misleading "fixed"
  screenshot. The current `docs/images/card-back.png` therefore still accurately
  depicts the current (defective) state and was deliberately left in place.
- **Exactly what is needed (for the parent/owner to approve):** ONE of —
  (a) a new `card-back.jpg` variant whose artwork has FIVE button boxes
  (3 in row 1, 2 in row 2 — reflowed/centred as the owner prefers), with the
  5 buttons re-placed onto the new boxes; or (b) the same frame with the middle
  row-2 outline cleanly inpainted to the frame's dark-green texture, keeping the
  other 5 boxes, with buttons left exactly where they are. Either option breaks
  the current byte-identical `card-back.jpg` and is a design-asset change, so it
  needs an explicit owner/coordinator decision — it is NOT covered by "reflow
  only, do not restyle anything else". After either option, re-render the back
  face and replace `docs/images/card-back.png` (front is unaffected).
- **Not a defect:** the front face is clean and unchanged; no front-image
  replacement is needed.

## V4. Kept-as-is items — PASS with one explained exception

- Byte-identical to the template (cmp): `logo.png`, all icons
  (`apple-touch-icon.png`, `favicon.ico`, `icon-192.png`, `icon-512.png`,
  `icon-maskable-512.png`), `card-front.jpg`, `card-back.jpg`, `vercel.json`,
  `LICENSE`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SECURITY.md`,
  `CLIENT-LICENSE-TEMPLATE.txt`, and all 8 `assets/services/*.svg` files.
- `.gitignore` differs in exactly ONE word: its comment says "Director" where the
  template says "CEO". That is the correct renaming, not a drift.
- Company overview / services / tagline / official-links wording: the 8 services
  (ride-share, food, parcel-delivery, courier, marketplace, medicine, it-services,
  ride-bangla-pay) match the template; taglines "Together We Move" / "A Better
  Tomorrow", the About Us text, and the company panel are carried over.
  `photo.png` correctly DIFFERS from the template (it is Emon's portrait).
- File-set vs template: director adds this REPORT.md and supplies
  `docs/images/card-front.png` (missing in the template); the template's
  `docs/screenshots/card-desktop.png` (previous holder's face) is correctly absent.

## V5. Render check — Chromium claim CONFIRMED, with sandbox caveats

- The builder's "used headless Chromium successfully" claim is credible: this
  verifier ran headless Chromium itself (`/opt/meta-chromium/chrome` via
  Playwright, phone 390×844 + desktop 1280×900). Layout, flip state
  (`.inner` → `.inner.flipped`), front face (Emon's portrait, name, title,
  +880 1885 002951, info@ridebangla.bd, ridebangla.bd, Faridpur 7803), back face
  (QR, 5 buttons, About Us), and the 8-service company panel all rendered.
- Sandbox caveats (same class as the builder's first pass): direct `file://`
  load failed to fetch Google Fonts and the cdnjs QR/html2canvas libraries
  (proxy tunnel errors), so QR was empty on the first pass. Second pass used a
  render-only `/tmp` copy with the QR library vendored locally; the vendored
  file's SHA-384 matches the page's SRI pin exactly
  (`sha384-mZT2gIty7ZDdOGkxfP6joZcYdMW1Jvj9dRlfpTmaJAKKXTqzygtB22k7FLe+KZC1`),
  so it is byte-identical to the shipped pinned library — no file was added to
  this tree. With that, QR rendered (innerHTML length 14,843, both viewports).
  Fonts fell back in the sandbox; live fonts/CDN behaviour still needs the
  post-deploy live check (§V6). Verifier renders were kept in `/tmp` only and
  were NOT copied into `docs/` (see §V3).
- Services section: verified on the rendered page (all 8 services, overview,
  official links, company phone) — matches the builder's claim.

## V6. Fix applied by the verifier (the only tree change)

- `sitemap.xml`: `<lastmod>2026-10-20</lastmod>` → `<lastmod>2026-10-27</lastmod>`.
  Stale-date defect fixed as authorised. Re-grep after this edit: still 0 leaks.

## V7. Still UNVERIFIED (owed, not claimed)

- Live behaviour on the real director.ridebangla.bd URL after Vercel deploy:
  CDN + Google Fonts from the public internet, NFC tap, rendering on a real
  phone, QR scan landing on the live URL, and vCard download on a real device.
- Identity of the portrait (face-matching Emon) beyond the builder's statement
  that it came from main-website team data — the verifier confirmed the photo
  differs from the template and renders correctly, not the person's identity.
- The empty-box artwork fix (§V3) — deliberately NOT done, awaiting decision.

## Verifier verdict

- Tree is LEAK-CLEAN and all positive/identity/domain/button/vCard/README/
  byte-identity checks PASS.
- The tree is NOT ready to be called visually final until the §V3 artwork
  decision is made and the back face is re-rendered. Do not push a "fixed"
  claim on a button reflow alone — it would still show an empty box.

- No secrets, no invented copy, no invented links anywhere in the tree or this report.
