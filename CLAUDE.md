# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single static, self-contained web page for **GABU COVE** (ガブコブ), a private rental villa in Okinawa, Japan. The page (`amenities.html`) lists the property's amenities/equipment (アメニティ・備品) and a packing checklist for guests. All content is in Japanese.

There is no build system, package manager, test suite, or backend. The deliverable is the HTML file itself.

## Working with it

- **Preview:** open `amenities.html` directly in a browser, or serve the directory (`python3 -m http.server`) and visit it. No build/compile step exists.
- **Tailwind** is loaded from the CDN (`https://cdn.tailwindcss.com`) at runtime — there is no Tailwind config, PostCSS, or compiled CSS. Utility classes work out of the box; custom styles live in the inline `<style>` block in `<head>`.
- The page is fully self-contained: fonts (Noto Sans JP via Google Fonts), images (hosted on `gabucove.com`), and the Booking.com reservation CTA are all external URLs. Editing is just editing one HTML file.

## Structure of `amenities.html`

Everything is in one file, organized as:

1. `<head>` — meta/OG tags, Tailwind CDN, Google Fonts, and an inline `<style>` block defining all the custom component classes.
2. Hero header, intro, and an "室内のものについて" (about the items inside) note.
3. Amenity sections grouped by location, each introduced by a `.section-heading` containing a `.floor-label`:
   - `f1` — 1F ガレージ兼リビング
   - `f1o` — 1F外 ウッドデッキ・屋外
   - `rf` — 屋上 ルーフデッキ
   - `f2` — 2F 寝室・バスルーム
4. A packing checklist (`.checklist-grid` / `.checklist-block`), a notes/「ご注意」 block, the Booking.com CTA, and the footer.
5. A small inline `<script>` at the bottom using `IntersectionObserver` to add the `.visible` class to `.fade-in` elements as they scroll into view.

### Component conventions (defined in the inline `<style>`)

- `.category-block` / `.category-header` / `.category-body` — a titled card listing items. Each amenity is an `.item-row` (item name + availability badge).
- `.badge-yes` (available, green) / `.badge-no` (not available, grey). Use `.item-name.unavailable` to grey out an unavailable item's text.
- `.subgroup-label` and `.footnote` for sub-headings and small print within a card.
- `.floor-label` color is set by the location modifier class (`f1`, `f1o`, `f2`, `rf`) — keep these in sync with the section's location.
- `.free-card` — the highlighted (dashed gold) callout card.
- Every visually-animated block carries the `.fade-in` class so the IntersectionObserver reveals it.

When adding amenities, follow the existing card → row → badge pattern rather than introducing new markup, and add `.fade-in` to new top-level blocks for consistent scroll-in behavior.

## Notes / known discrepancies

- `README.md` refers to the page as `アメニティ.html`, but the actual file is `amenities.html`. Treat `amenities.html` as canonical.
- README also records ownership: owner `chipacopter-dot`, editor `sano040771-blip`.
