# Off-Plan Desk with Josh — landing page

Single-page landing site for Joshua Packer's personalized Dubai and Abu Dhabi
property consulting offer. Plain HTML, CSS and vanilla JS. No build step,
no dependencies, no framework.

## Run it

Open `index.html` directly, or serve the folder:

```
cd site
python3 -m http.server 8000
# http://localhost:8000
```

Fonts (Bricolage Grotesque, Figtree) load from Google Fonts, so the page needs
network access to render with the intended typography. It degrades to system-ui
cleanly offline.

## Files

```
site/
  index.html     the whole page (markup, styles, script inline)
  images/        19 assets copied from the research pack
  README.md      this file
  CONTENT.md     every subject-specific fact on the page and its source tag
```

## Placeholders to swap before launch

Every placeholder is written as a literal bracketed token in `index.html` and
renders on the page as an orange monospace chip, so nothing can ship unnoticed.

| Token | Occurrences | What it is | Status |
|---|---|---|---|
| ~~`[APPLICATION_URL]`~~ | 0 | Primary CTA target. | **Done**, set to `https://cal.com/lvrgd/call` |
| `[PROGRAM_PRICE]` | 1 | Price of the seat. Offer block. | **Required** |
| `[PROGRAM_DURATION]` | 3 | How long the seat runs. Offer block, commitments list, FAQ. | **Required** |
| `[CALL_CADENCE]` | 4 | How often calls happen. Do not invent a number. | **Required** |
| `[MESSAGING_SLA]` | 5 | Reply-time commitment for messaging. Do not invent one. | **Required** |

Swap them all at once:

```
cd site
sed -i '' 's|\[PROGRAM_PRICE\]|AED 00,000|g' index.html
sed -i '' 's|\[PROGRAM_DURATION\]|12 weeks|g' index.html
sed -i '' 's|\[CALL_CADENCE\]|fortnightly|g' index.html
sed -i '' 's|\[MESSAGING_SLA\]|within one working day|g' index.html
```

After swapping, drop the `.ph` chip styling if you no longer want the values
visually highlighted (search for `class="ph"` and `class="ph light-ph"`).

Check nothing was missed:

```
grep -o '\[[A-Z_]*\]' index.html | sort -u
```

## Program name

`[PROGRAM_NAME]` is resolved in the markup as **"Off-Plan Desk with Josh"**.
This is an **assumed working title** from the brief, not something Josh has
published. If he or Felix picks a different name, find and replace
`Off-Plan Desk` across `index.html` (it appears in the title tag, nav, CTAs,
offer block, FAQ and footer).

## Page structure

1. Sticky nav with single Apply CTA
2. Hero, headshot, primary CTA, three soft trust pills
3. Proof strip on a night band, four sourced items with soft labels
4. Problem, six named failure modes
5. Who he is, origin, direct site quote, four fact cards
6. Desk band, poster frame from his site
7. What you get, calls and messaging as the two lead cards, coverage themes, process commitments
8. For and not for, two blunt columns
9. How he works in public, three named-work cards plus eight real video titles
10. Offer block, placeholders, included list, CTA, side door to the free routes
11. FAQ, eight items
12. Final CTA
13. Footer with the required risk line

## Content rules this page was built to

These were hard requirements in the brief and are worth preserving on edit.

- **No invented proof.** No testimonials, no student results, no deal sheets,
  no ROI figures, no follower counts used as vanity proof, no awards claimed as
  personal consulting proof. Every factual claim traces to `CONTENT.md`.
- **Process guarantees only.** The page promises review, calls, messaging and an
  honest fit check. It never promises a yield, a valuation or a resale price.
- **Numbers are framed by type.** License, employer, positioning, channel. Never
  as audited AUM or as anyone's expected outcome.
- **Punctuation.** No em dashes, no en dashes, no semicolons in visible copy.
  Verified clean.
- **Corporate filler banned.** leverage, streamline, seamless, robust, empower,
  elevate, unlock, supercharge, cutting-edge, best-in-class, game-changing,
  revolutionary, world-class, boasts, serves as, stands as. Verified absent.
- **One primary CTA.** Every button points at `https://cal.com/lvrgd/call`. All booking links
  on the page, including the side door and footer, now resolve to that same
  destination. Josh's own free 15 minute brokerage call is no longer linked.
- **No WhatsApp in the hero.** His published numbers exist but are deliberately
  not on this page, per the brief.

### One brief conflict, and how it was resolved

The brief asks for an FAQ entry answering "Is this group coaching?" while also
instructing, three separate times, never to mention group coaching anywhere on
the page. Those cannot both hold literally.

The FAQ now reads **"Is this one to one, or am I sharing the calls with other
people?"** This answers the same buyer worry (am I getting personal attention)
and confirms the seat is one to one, without the phrase appearing on the page.
If you would rather have the literal question, it is one edit in the FAQ block.

## Images

19 assets in `images/`, copied from the research pack. 11 are used.

Unused and why: `05` is the secondary-channel avatar (`01` is the primary face),
`09`, `14`, `15` and `17` are extra video thumbs held back to keep the strip to
eight, and `18` and `19` are developer marketing renders kept off the page so
nothing reads as a property case study.

Caption honesty is load-bearing. `03` uses his own site caption. `04` is labelled
as a poster frame from his site. Video thumbs carry a note that titles are
channel titles, not audited figures. Keep those captions if you move the images.

Note on `04`: Equity top-performer certificates are visible in the frame. That is
his real photo and it stays, but no award claim is made anywhere in the copy,
per the brief's rule about not using firm awards as personal consulting proof.

## Accessibility and performance

- Single request for HTML, one Google Fonts stylesheet, images served locally
- Semantic headings, `details`/`summary` FAQ that works without JS
- Visible focus rings on all interactive elements
- `prefers-reduced-motion` disables the scroll animation and smooth scrolling
- JS is progressive only. With JS off, all content renders and the FAQ still opens
- Verified no horizontal overflow at 375px

## Known gaps

Carried over from the research pack, not solvable in the build:

- Price, duration, call cadence and messaging SLA are unknown, hence placeholders
- No consulting testimonials exist yet, and none were invented
- No application URL yet
