# Modern Minimalist Novel Reading Website (WordPress) — Step-by-Step Blueprint

## 1) Project Goal (What you are building)
You are building a **premium e-reader style WordPress website** focused on long-form novel reading with:
- Distraction-free design
- Fast mobile experience
- Simple chapter navigation
- Controlled AdSense monetization that does not harm reading retention

---

## 2) Technical Requirements (Recommended Stack)

## Hosting & Core
- **Hosting:** LiteSpeed/VPS managed WordPress hosting with SSD and server-level caching
- **PHP:** 8.2+
- **MySQL/MariaDB:** MySQL 8+ or MariaDB 10.6+
- **HTTPS:** Required (Let’s Encrypt)
- **CDN:** Cloudflare (free plan is enough to start)

## Theme (lightweight)
Use one:
1. **GeneratePress** (excellent performance and typography controls)
2. **Astra** (beginner-friendly and fast)

> If your priority is pure speed and clean reading layout, start with **GeneratePress**.

## Essential Plugins (lightweight set)
- **SEO:** Rank Math *or* Yoast SEO (choose one only)
- **Caching/Performance:** LiteSpeed Cache (if LiteSpeed server) or WP Rocket
- **Image Optimization:** ShortPixel or Imagify
- **Ad Management:** Ad Inserter (for controlled placements)
- **Table of Contents:** Easy Table of Contents (or LuckyWP TOC)
- **Custom Post Type / Fields:** CPT UI + Advanced Custom Fields (ACF)
- **Security:** Wordfence (or lightweight alternative like Solid Security)
- **Backup:** UpdraftPlus

Optional:
- **Perfmatters** (script manager, cleanup)
- **WPCode** (safe place for snippets like progress bar or next/prev logic)

---

## 3) Information Architecture (Best Site Structure)

## Primary Content Model
Create a custom post type: **Novels**

Use taxonomy structure:
- **Genres** (Fantasy, Romance, Thriller, etc.)
- **Authors** (taxonomy or custom field)
- **Novel Series / Novel Title** (taxonomy to group all chapters of one novel)

## Chapter Model (recommended)
For each chapter, store:
- Novel Name (taxonomy term)
- Chapter Number (custom field: integer)
- Reading Time (optional)
- Status (Draft/Published/Premium if needed)

This allows sorting and automation for next/previous chapter buttons.

## Suggested URL Structure
- Novel archive: `/novels/`
- Single novel chapter: `/novels/{novel-name}/chapter-{number}/`
- Genre archive: `/genre/{genre-name}/`
- Author archive: `/author/{author-name}/`

---

## 4) Design System (Modern Minimalist E-Reader Style)

## Visual Rules
- Background: **#FFFFFF** (clean white)
- Text color: **#1A1A1A**
- Link/accent color: your **brand color from logo**
- Container width for reading: **680–760px max**
- Generous line height: **1.7–1.95**
- Paragraph spacing: **1.1–1.4em**
- Minimize visual noise (no heavy shadows, no busy sidebars on chapter pages)

## Typography
- Headings: elegant sans-serif or serif pair
- Body reading font: **Merriweather** or **Lora**
- Fallback stack example:
  - `"Merriweather", Georgia, "Times New Roman", serif`

## Header & Branding
- Place your logo **left-aligned in header**
- Reuse logo brand colors for:
  - links
  - active buttons
  - progress indicators
  - focus states

---

## 5) Reader Experience Features (Implementation Plan)

## A) Dark Mode Toggle (Essential)
Implementation options:
1. Plugin route: lightweight dark mode plugin with schedule + manual toggle
2. Custom route: CSS variables + JS toggle + localStorage

Best practice:
- Toggle should be visible near top-right of reading UI
- Remember user preference with localStorage/cookie
- Dark palette example:
  - Background: `#111111`
  - Text: `#E8E8E8`
  - Muted: `#BDBDBD`

## B) Font Customization (Size + Line Spacing)
Provide quick controls in floating mini-toolbar:
- **A- / A+** for font size
- **Line height +/-** (or preset buttons)

Store preferences in localStorage:
- `reader_font_size`
- `reader_line_height`
- `reader_theme`

## C) Reading Progress Bar
- Sticky thin bar at top of chapter page
- Fill width based on scroll depth
- Should not overlap admin bar/menu on mobile

Implementation approach:
- Add HTML container in template (or via hook)
- JS on scroll updates progress width
- Smooth transition with CSS

---

## 6) Content Management Workflow (WordPress Editorial System)

## Step-by-Step Setup
1. Install WordPress, theme, and core plugins.
2. Create **CPT: Novels** using CPT UI.
3. Create taxonomies:
   - Genre
   - Author
   - Novel (series title / book title)
4. Add ACF fields to Novels CPT:
   - Chapter Number (required)
   - Estimated Reading Time
   - Chapter Subtitle (optional)
5. Build custom single template for novel chapters.
6. Add next/previous chapter logic based on:
   - Same Novel taxonomy term
   - Adjacent chapter number
7. Add TOC block on novel landing page (all chapter links sorted ascending).

## Best Practice for Long Novels
For each novel create:
- One **Novel Landing Page** (synopsis + full chapter list/TOC)
- Multiple **Chapter Posts** under Novels CPT

Novel landing page includes:
- Cover image
- Description
- Genre + author meta
- “Start Reading” button (goes to chapter 1)
- Full chapter TOC

## Next/Previous Navigation Rules
At chapter bottom show:
- **Previous Chapter** (if exists)
- **Next Chapter** (if exists)
- “Back to Novel TOC” link (always visible)

This improves session time and reduces bounce.

---

## 7) Table of Contents Strategy

## Per Novel TOC (mandatory)
Use either:
- Gutenberg list block manually (simple)
- Dynamic TOC generated from chapter posts in same Novel taxonomy (scalable)

For scale, dynamic method is better:
- Query all chapters where `novel = current novel`
- Sort by `chapter_number`
- Render links automatically

## In-Chapter TOC (optional)
If a chapter is very long and has subheadings, use Easy TOC for heading-based section jumps.

---

## 8) AdSense Optimization (without killing retention)

## Golden Rule
**Reader trust > short-term ad clicks**

## Recommended Ad Placements
1. **After Chapter Intro** (only once, subtle)
2. **Mid-content** (only for long chapters, one ad after ~35–45% content)
3. **Between chapters** (best for monetization, low frustration)
4. **End of chapter** (before next/prev buttons)
5. Sidebar ads only on desktop archive pages, not heavy on mobile chapter pages

Avoid:
- Sticky ads covering text
- Popups during reading
- Too many in-article blocks

## Ad Inserter Setup Suggestion
- Create separate blocks for desktop and mobile
- Use paragraph-based insertion rules (e.g., after paragraph 4 and 14)
- Add exclusion for very short chapters (<700 words)

---

## 9) SEO + Performance Requirements

## SEO
- Schema: Article/BlogPosting on chapters
- Unique title format:
  - `Chapter X - Novel Name | Site Name`
- Meta description with chapter hook
- Internal links:
  - previous chapter
  - next chapter
  - novel TOC
  - genre page

## Performance Targets
- Mobile LCP < 2.5s
- CLS < 0.1
- INP < 200ms (as practical)

Checklist:
- WebP images
- Local font hosting/preload main font
- Minify CSS/JS
- Delay non-critical scripts
- Disable unnecessary plugins/features

---

## 10) Mobile-First UX Rules (critical)
- Body font size: 18–20px on mobile reading pages
- Tap targets 44px+
- Keep chapter navigation fixed at bottom only if it does not obstruct text
- Ensure ad units are responsive and not intrusive
- Avoid sidebars on single chapter pages

Given your audience behavior, optimize chapter template for mobile first, desktop second.

---

## 11) Practical Publishing Workflow (Easy Novel Upload System)

## Workflow Template
When adding a new novel:
1. Create Novel term (e.g., `The Silent Crown`)
2. Assign Genre + Author
3. Create landing page with synopsis and auto chapter list shortcode/template
4. Publish Chapter 1 with chapter number field = 1
5. Continue adding chapters sequentially
6. Use scheduled publishing for consistency

## SOP for each new chapter
- Add title: `Chapter 12: The Hidden Gate`
- Assign Novel, Genre, Author
- Set chapter number field
- Add featured image (optional minimal)
- Insert ad slots (if chapter long enough)
- Verify next/prev links
- Test on mobile before publish

---

## 12) Recommended Initial Build Order (Week 1 Plan)

Day 1:
- Hosting, SSL, WordPress install, theme install

Day 2:
- CPT + taxonomies + ACF fields
- Create chapter template

Day 3:
- Add dark mode, reading toolbar (font controls), progress bar

Day 4:
- AdSense + Ad Inserter controlled placements

Day 5:
- Speed optimization + SEO basics + analytics

Day 6:
- Upload first novel with 5–10 chapters

Day 7:
- QA on mobile, fix UX friction, submit sitemap to Google Search Console

---

## 13) Final Stack Recommendation (Simple + Effective)
- Theme: **GeneratePress**
- Builder: Native Gutenberg (avoid heavy builders for speed)
- CPT/Fields: CPT UI + ACF
- TOC: Easy TOC + dynamic novel chapter list
- Ads: Ad Inserter + AdSense Auto Ads (limited)
- Performance: LiteSpeed Cache + Cloudflare + ShortPixel
- SEO: Rank Math

This setup is lightweight, scalable, and ideal for long-form reading + monetization.

---

## 14) Quick Success Tips (Aapke “Zaroori Mashwaray” ka action version)
- **Custom Post Types:** Bilkul zaroori — “Novels” section alag rakhein.
- **Mobile First:** Pehle mobile chapter UX perfect karein, phir desktop polish karein.
- **Ad Balance:** Ads ko chapters ke darmiyan smartly place karein, overdo na karein.
- **Logo Integration:** Header mein left logo + brand colors ko links/buttons/progress mein consistent rakhein.
- **Retention Focus:** Reader ko chapter-se-chapter smoothly le jana hi real growth engine hai.

