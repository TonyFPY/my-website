# Website Structure and Specifications

This document captures the current structure and behavior of the MY-WEBSITE codebase. It is intended as a reference for future refactoring and maintenance.

## Repository Structure

```
.
├── README.md
├── codex.md
├── email.html
├── images/
│   ├── logo.png
│   ├── logo_brown.png
│   ├── logo_cu.png
│   ├── logo_nio.png
│   ├── logo_ucb.png
│   ├── logo_uon.png
│   ├── profile.jpg
│   ├── profile2.jpg
│   ├── zuckerman.webp
│   └── pubs/
│       ├── hmn.jpg
│       └── na_iclr_2026.mp4
├── index.html
└── style.css
```

## Page Structure (index.html)

- Document head
  - Title: "Pinyuan Feng"
  - Meta: `charset="utf-8"`, `viewport="width=1000"`
  - Favicon: `images/logo.png`
  - External scripts:
    - Google Analytics (gtag.js) with ID `G-STGLQW4BJX`
    - jQuery 3.6.1
    - jQuery UI 1.13.2
    - Isotope 3 (layout + filtering)
  - External styles:
    - Google Fonts: "Asap" loaded via `<link>` and `@import`
    - Font Awesome 6.4.0 and 6.5.2
    - Academicons 1.9.4
  - Local stylesheet: `style.css`

- Body
  - `#banner`: full-width top banner image (`images/zuckerman.webp`)
  - `#main`: fixed-width centered content container
    - `#intro`: two-column intro layout
      - `#intro-text`: name, social links directly under the name, biography paragraphs, and institution logos
      - `#intro-image`: profile image (`images/profile.jpg`) with hover swap to `images/profile2.jpg`
    - `#filters`: Isotope filter button group
      - Buttons: News (`.highlight`), Research (`.publication`), Misc (`.misc`)
      - News is marked active in static markup and is also the runtime default
    - `.grid`: Isotope container for list sections
      - `#main-highlights`: news/timeline items
      - `.list-item.publication.description`: research-direction summary
      - `#main-publications`: populated publication list
      - `.list-item.misc`: community memberships and reviewer service
    - `#footer`: template attribution

## Content Inventory

- Intro content
  - Describes the site owner as a PhD student at Columbia University's Zuckerman Mind Brain Behavior Institute working with Prof. Niko Kriegeskorte.
  - Describes prior education at Brown University and the University of Nottingham, plus a Machine Learning Engineer internship at NIO Inc.
  - Lists collaborators and affiliations at Brown, Nottingham, Berkeley DeepDrive, and related institutions.
  - Social links include Google Scholar, LinkedIn, X/Twitter, and email.
  - Institution logos link to Columbia, Brown, Nottingham, UC Berkeley, and NIO.

- News/highlights
  - 2026 items include co-organizing the CCN 2026 Satellite Event: Human Brain Foundation Model Workshop, VSS 2026 presentation, ICML 2026 acceptance, ACL 2026 Findings acceptance, and ICLR 2026 acceptance.
  - 2025 items include Trends in Cognitive Sciences acceptance, NeurIPS 2025 BrainBodyFM Workshop presentation, EMNLP 2025 acceptance, and ICLR 2025 Re-Align Workshop acceptance.
  - Older timeline items include the website launch, starting the PhD at Columbia in 2024, starting the MS at Brown in 2022, starting the NIO internship in 2021, completing the bachelor's degree at Nottingham, and the First Class Honours / High Achievers Award note.

- Research section
  - The summary lists three directions:
    - Multimodal brain encoding and decoding
    - Human-inspired self-supervised representation learning
    - Representational similarity analysis between humans and machines
  - Publication entries currently include:
    - "Towards Interpretable Visual Decoding with Attention to Brain Representations" with an MP4 thumbnail (`images/pubs/na_iclr_2026.mp4`) and links to OpenReview, arXiv, webpage, and code.
    - "Better Artificial Intelligence Does Not Mean Better Models of Biology" with an image thumbnail (`images/pubs/hmn.jpg`) and links to Cell Press, arXiv, video, and code.

- Misc section
  - Mentions membership in the GrowAI community.
  - Mentions membership in Neurotech X Columbia.
  - Mentions reviewer service for IEEE TPAMI, IEEE TBD, NeurIPS, ICLR, CVPR, and CCN.

## Contact Page (email.html)

- Minimal standalone HTML page.
- Title: "Contact"
- Meta: `charset="utf-8"`
- Favicon: `images/logo.png`
- Body uses inline sans-serif styling and displays the obfuscated email text `pf2477 at columbia dot edu`.
- The email page is opened from the envelope social link in `index.html` with `target="_blank"`.

## Layout Structure

- Overall layout
  - Full-width banner at top, followed by a fixed-width content column centered on the page.
- Intro area
  - Two-column row: left text column (`#intro-text`) and right image block (`#intro-image`).
  - Social icons sit directly below the `h1` name and above the biography paragraphs.
- Filter controls
  - Horizontal button row aligned with the content column.
- Content grid
  - Single-column list items inside the Isotope grid; sections are grouped by category and filtered by buttons.
  - Publication items use left-aligned thumbnails and right-aligned text blocks.
- Footer
  - Positioned at the bottom of the main content container.

## Styles (style.css)

- Global reset
  - Meyer reset styles normalize default browser spacing and display behavior.
- Base typography and color
  - Font family: Asap with roboto/sans-serif fallbacks
  - Primary text color: `#150c21`
  - Muted text color: `#a0a8b0`
  - Link color: `rgb(20, 110, 190)`
  - Text autosizing is explicitly controlled with `text-size-adjust`
- Layout
  - `#main` width: 54em, centered, min height: 100vh
  - `#intro` uses flex
  - `#intro-text` width: 40em
  - `#intro-image` is a fixed 12em square with rounded corners
  - `#banner` uses flex centering, full-width image display, and max height
- Components
  - Filter buttons with hover and active (`.is-checked`) states
  - `.grid` list items for news, publications, and misc content
  - Before Isotope is ready, `.grid:not(.isotope-ready)` hides Research and Misc items so News is the first visible category.
  - Publication thumbnails support both images and videos
  - Social icons use flex layout, large icon sizing, hover color change, and hover scale
  - Institution logos use flex layout, hover scale/opacity, fixed max height, and wrapping
- Responsive rules (max-width 600px)
  - Banner max height increases
  - Social icon spacing and sizing are reduced
  - Institution logos scale down and center

## Scripts and Behaviors (index.html)

- Google Analytics initializes on load with ID `G-STGLQW4BJX`.
- Isotope grid setup:
  - Uses `.list-item` as the item selector.
  - Uses `fitRows` layout.
  - Disables transitions with `transitionDuration: 0`.
  - Starts with `initLayout: false`.
  - Defines sort data for legacy name/symbol/number/category/weight fields, though filtering is the active behavior.
- Filter behavior:
  - Clicking a filter button updates the active `.is-checked` class.
  - Clicking a filter button applies that button's `data-filter` value to the Isotope grid.
  - `update_isotope()` always defaults to `.highlight` (News) on page load.
  - `update_isotope()` adds `.isotope-ready` to `.grid` after applying the default filter.
  - The selected filter is not cached or restored across page loads.
  - The default filter is applied immediately by the bottom script, then the grid is laid out again after full window load.
  - The grid is refreshed on `pageshow` when restored from the browser back/forward cache.
- Hover effect:
  - Profile image swaps from `images/profile.jpg` to `images/profile2.jpg` on hover and restores the original image when the pointer leaves.
- Unused/legacy functions:
  - `toggle_bio()` is defined but no matching active bio toggle markup is present.
  - `toggle_publications()` is defined but the related "more publications" markup/button is not active in the current page.

## Functional Specifications (Current Behavior)

- Single static personal website rendered from `index.html`.
- Separate minimal static contact page rendered from `email.html`.
- Displays a banner image, intro text, social links, institution logos, news, research, misc content, and footer attribution.
- Filters content via Isotope using News, Research, and Misc buttons.
- Defaults to News on each page load.
- Does not persist the last selected filter.
- Swaps the profile image on hover.
- Publication media includes one local MP4 thumbnail and one local image thumbnail.
- Social and publication links open external pages, while the email icon opens `email.html` in a new tab.

## Non-Functional Specifications (Current Characteristics)

- Static site with no build step, package manager config, or backend.
- External CDN dependencies are required for JavaScript, fonts, and icons.
- Analytics are enabled via Google Analytics.
- Layout is fixed-width (`viewport` set to `width=1000`) with limited responsive rules.
- Local assets are loaded from `images/` and `images/pubs/`.
- No lazy loading is configured for images or videos.
- Accessibility support is limited; several images have generic or empty `alt` attributes, and the profile image has no `alt`.
- Performance and privacy depend on third-party CDNs and analytics.

## Version Control Log

- Step 1: Created `WEBSITE_SPEC.md` documenting repository structure, page structure, styles, scripts, and specs.
- Step 2: Added a "Layout Structure" section to describe the page's spatial organization.
- Step 3: Renamed `WEBSITE_SPEC.md` to `codex.md`.
- Step 4: Moved social icons to sit next to the name in `index.html` and added styling for the name/icon row in `style.css`.
- Step 5: Normalized social icon sizing when displayed next to the name in `style.css`.
- Step 6: Right-aligned the social icons within the name row in `style.css`.
- Step 7: Adjusted the name row for mobile by stacking the name and icons and left-aligning them in `style.css`.
- Step 8: Disabled mobile text autosizing to keep grid text consistent after filtering in `style.css`.
- Step 9: Moved social icons back under the name in `index.html` and removed name-row styles in `style.css`.
- Step 10: Updated `codex.md` to reflect the current working-tree implementation, including the populated publication list, 2026 news items, contact page, asset inventory, and runtime filter default behavior.
- Step 11: Changed the grid filter behavior so News is the static and runtime default, and removed cached filter persistence.
- Step 12: Added a pre-Isotope CSS fallback and immediate default filter application to avoid the initial all-category grid flash.
