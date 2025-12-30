# Website Structure and Specifications

This document captures the current structure and behavior of the MY-WEBSITE codebase. It is intended as a reference for future refactoring.

## Repository Structure

```
.
├── README.md
├── email.html
├── images/
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
    - Google Fonts: "Asap" (loaded via `<link>` and `@import`)
    - Font Awesome (6.4.0 and 6.5.2)
    - Academicons 1.9.4
  - Local stylesheet: `style.css`

- Body
  - `#banner`: top banner image (`images/zuckerman.webp`)
  - `#main`: fixed-width content container
    - `#intro`: two-column intro layout
      - `#intro-text`: name, bio paragraphs, social links, institution logos
      - `#intro-image`: profile image (`images/profile.jpg`) with hover swap
    - `#filters`: button group for Isotope filtering
      - Buttons: News, Research (default), Misc
    - `.grid`: Isotope container
      - `#main-highlights`: list of highlight items (news/timeline)
      - Publications section
        - `.list-item.publication.description`: research summary
        - `#main-publications`: currently empty list area
      - `.list-item.misc`: misc community memberships
    - `#footer`: attribution text

## Layout Structure

- Overall layout
  - Full-width banner at top, followed by a fixed-width content column centered on the page.
- Intro area
  - Two-column row: left text column (`#intro-text`) and right image block (`#intro-image`).
- Filter controls
  - Horizontal button row aligned with the content column.
- Content grid
  - Single-column list items inside the Isotope grid; sections grouped by category and filtered by buttons.
- Footer
  - Positioned at the bottom of the main content container.

## Styles (style.css)

- Global reset (Meyer reset)
- Base typography and color
  - Font family: Asap with roboto/sans-serif fallbacks
  - Primary text color: `#150c21`
  - Link color: `rgb(20, 110, 190)`
- Layout
  - `#main` width: 54em, centered, min height: 100vh
  - `#intro` uses flex; image is fixed 12em square with rounded corners
  - `#banner` uses flex centering and a max height
- Components
  - Filter buttons with active state (`.is-checked`)
  - `.grid` list items for news/publications/misc
  - Social icons with hover scale
  - Institution logos with hover scale and responsive sizing
- Responsive rules (max-width 600px)
  - Banner max height increases
  - Social icon sizing and spacing
  - Institution logos scale down and center

## Scripts and Behaviors (index.html)

- Google Analytics initialized on load.
- Isotope grid setup:
  - `fitRows` layout
  - Filters items by `data-category` via buttons in `#filters`
  - Persists last filter selection in `localStorage` under `filterValue`
  - Restores filter and button state on load (`update_isotope`)
- Hover effect:
  - Profile image swaps from `images/profile.jpg` to `images/profile2.jpg` on hover
- Unused/legacy functions exist:
  - `toggle_bio()` and `toggle_publications()` are defined but not used in the current markup.

## Functional Specifications (Current Behavior)

- Single static page rendered from `index.html`
- Displays a banner image, intro text, social links, and institution logos
- Filters content list via Isotope (News, Research, Misc)
- Persists the last filter selection using `localStorage`
- Swaps profile image on hover
- Social/email links open external pages (email opens `email.html` in a new tab)
- Footer attribution is always visible at the bottom of the content area

## Non-Functional Specifications (Current Characteristics)

- Static site with no build step or backend
- External CDN dependencies required for JS/CSS and icons
- Analytics enabled via Google Analytics (gtag)
- Fixed-width layout with limited mobile responsiveness
- Local assets loaded from `images/` (no lazy loading)
- No explicit accessibility metadata (e.g., ARIA landmarks); some images lack `alt`
- Performance and privacy depend on third-party CDNs and analytics

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
