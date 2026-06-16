# NinetySix Studios — WordPress Website

> A static HTML/CSS website deployed inside WordPress using **Custom HTML Blocks** and **Additional CSS**. Originally prototyped as a React project, but WordPress does not natively support React in page content without heavy plugin overhead. The solution: self-contained HTML/CSS/JS blocks pasted directly into the WordPress block editor.

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [How It Works](#how-it-works)
3. [Prerequisite — Google Fonts](#prerequisite--google-fonts)
4. [Custom HTML Blocks in WordPress](#custom-html-blocks-in-wordpress)
5. [Additional CSS in WordPress](#additional-css-in-wordpress)
6. [Page 1 — Landing Page (`page-id-1336`)](#page-1--landing-page-page-id-1336)
7. [Page 2 — Blog Posts (`page-id-1583`)](#page-2--blog-posts-page-id-1583)
8. [Page 3 — Press Kit (`page-id-1664`)](#page-3--press-kit-page-id-1664)
9. [Shared Header Component](#shared-header-component)
10. [Troubleshooting](#troubleshooting)

---

## Project Structure

```
Website-VS-Code/
├── Home page/
│   ├── Header.html          ← Shared header (logo, nav, social icons)
│   ├── Header.css           ← Header styles
│   ├── Home page.html       ← Landing page HTML
│   ├── Home page.css        ← Landing page styles (→ Additional CSS)
│   └── ui/
│       └── assets/          ← Images used on landing page
│
├── Blog-Posts/
│   ├── blog.html            ← Blog page (3 blocks: Header, Query Loop, Footer)
│   ├── blog-wordpress.html  ← Legacy static version (no longer used)
│   ├── press-kit.html       ← Press Kit page (4 blocks)
│   ├── style.css            ← Legacy stylesheet (no longer used)
│   └── assets/              ← Blog & Press Kit images
│
├── About Us/
│   ├── About Us.html
│   └── About Us.css
│
└── Press-Kit/
    └── assets/
```

---

## How It Works

Each WordPress page is composed of multiple **Custom HTML Blocks** pasted in order. Each block is self-contained — it carries its own `<style>` tag (or inline styles), its own HTML, and optionally a `<script>` tag.

### Why Not React?

The project was originally built as a React application. However, WordPress page content runs through the block editor and PHP renderer. React components cannot run inside native WordPress page content without:
- A headless WordPress setup (REST API + separate React frontend)
- A plugin like ReactPress or WP React

**The pragmatic solution:** Convert React components into plain HTML with inline CSS/JS, and deliver them via WordPress's built-in **Custom HTML block**.

---

## Prerequisite — Google Fonts

Before pasting any blocks, make sure these fonts are available. Each page's header block already includes the `@import` declarations:

```css
@import url('https://fonts.googleapis.com/css2?family=Special+Elite&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');
```

---

## Custom HTML Blocks in WordPress

### What Is a Custom HTML Block?

The Custom HTML block lets you write raw HTML, CSS, and JavaScript directly in the WordPress block editor. It renders as-is without WordPress adding paragraph tags or block wrappers (mostly).

### How to Add One

1. Open any page in the **WordPress Block Editor**
2. Click the **+** (Add Block) button
3. Search for **"Custom HTML"**
4. Select it
5. Paste your code into the block
6. Click **Preview** (or the block toolbar's "Preview" tab) to see it rendered

> **Screenshot Placeholder:** `docs/screenshots/add-custom-html-block.png`
> _(Shows the + button, search for "Custom HTML", and the block being added.)_

### Code Editor View (for Block Patterns)

Some blocks use WordPress block syntax (comments like `<!-- wp:query -->`). These must be pasted in **Code Editor** mode:

1. Click the **three-dot menu** (⋮) in the top-right toolbar
2. Select **Code Editor** (or press `Ctrl+Shift+Alt+M`)
3. Paste the block pattern
4. Switch back to **Visual Editor** to see it rendered

> **Screenshot Placeholder:** `docs/screenshots/code-editor-view.png`
> _(Shows the three-dot menu and the "Code Editor" option.)_

---

## Additional CSS in WordPress

### Where Is It?

**Appearance → Customize → Additional CSS**

> **Screenshot Placeholder:** `docs/screenshots/additional-css-location-1.png`
> _(Shows the WordPress admin sidebar: Appearance → Customize.)_

> **Screenshot Placeholder:** `docs/screenshots/additional-css-location-2.png`
> _(Shows the Customizer with the "Additional CSS" tab open and code entered.)_

### What Goes Here?

CSS that targets the entire page — things that can't live inside a single Custom HTML block:
- **Hiding the theme's header/footer** (because we provide our own)
- **Stripping theme wrapper margins/padding** (to go edge-to-edge)
- **Styling WordPress dynamic blocks** like the Query Loop (which generates its own HTML that we can't wrap in a `<style>` tag inline)

Each page has its own section of Additional CSS prefixed with `.page-id-XXX` to avoid conflicts.

---

## Page 1 — Landing Page (`page-id-1336`)

### Files
| File | Role |
|------|------|
| `Home page/Home page.html` | Main landing page content (hero, CTA, cards, trailer, footer) |
| `Home page/Home page.css` | All landing page styles (→ paste into Additional CSS) |

### Setup Steps

1. **Create a WordPress page** at the desired URL
2. Note the page ID from the URL (`post=1336`)
3. Paste the entire contents of `Home page.html` into a **Custom HTML block**
4. Go to **Appearance → Customize → Additional CSS** and paste the contents of `Home page.css`
5. Wrap all CSS rules with `body.page-id-1336` prefix (already done in the file)
6. **Publish**

### What It Contains
- Full-screen background image
- Hero section with game cover art
- CTA section with Steam wishlist button
- Game card carousel
- Trailer card with play button overlay
- Press Kit link with pointing hand animation
- Custom footer with logo

---

## Page 2 — Blog Posts (`page-id-1583`)

### Files
| File | Role |
|------|------|
| `Blog-Posts/blog.html` | 3 WordPress blocks (copy/paste each block separately) |

### Setup Steps

**Step 1 — Create the page**

1. Create a WordPress page at `/blog-posts/`
2. Note the page ID (`1583`)

**Step 2 — Paste Block 1 (Header)**

1. Add a **Custom HTML block**
2. Copy everything from `<!-- ⏬ CUSTOM HTML — HEADER ⏬ -->` to `<!-- ⏹ END HEADER ⏹ -->` in `blog.html`
3. Paste into the block

**Step 3 — Paste Block 2 (Query Loop)**

This is the dynamic blog post list. It uses WordPress block syntax.

1. Click the **three-dot menu → Code Editor**
2. Copy everything from `BLOCK 2: Paste this in the Code Editor` to `END BLOCK 2` in `blog.html`
3. Paste into the Code Editor
4. Switch back to **Visual Editor**

> **Important:** The Query Loop filters posts by category IDs `[18841228, 770389608]`. Change these to match your own category IDs.
>
> Also, each blog post needs a **Featured Image** set in Posts → Edit → Featured Image.

**Step 4 — Paste Block 3 (Footer)**

1. Add another **Custom HTML block** below the Query Loop
2. Copy everything from `<!-- ⏬ CUSTOM HTML — FOOTER ⏬ -->` to `<!-- ⏹ END FOOTER ⏹ -->`
3. Paste into the block

**Step 5 — Additional CSS**

Go to **Appearance → Customize → Additional CSS** and add (see the Blogpost CSS section already in Additional CSS):

```css
/* ── Hide theme footer ── */
.page-id-1583 footer,
.page-id-1583 #footer,
.page-id-1583 #colophon,
.page-id-1583 [class*="footer"] {
  display: none !important;
}
.page-id-1583 .blog-custom-footer {
  display: flex !important;
}

/* ── Hide block theme header ── */
.page-id-1583 header.wp-block-template-part {
  display: none !important;
}

/* ── Strip block theme wrappers ── */
.page-id-1583 .wp-site-blocks,
.page-id-1583 .wp-block-post-content,
.page-id-1583 .entry-content,
.page-id-1583 main {
  margin: 0 !important;
  padding: 0 !important;
  max-width: 100% !important;
}

/* ── Featured image ── */
.page-id-1583 .wp-block-post-featured-image {
  flex: 0 0 700px !important;
  max-width: 700px !important;
  position: relative !important;
}
.page-id-1583 .wp-block-post-featured-image img {
  border-radius: 12px !important;
  filter: drop-shadow(0 6px 18px rgba(0,0,0,0.22)) drop-shadow(0 2px 5px rgba(0,0,0,0.12)) !important;
  display: block !important;
}

/* ── Content column ── */
.page-id-1583 .wp-block-post-template .wp-block-column.is-vertically-aligned-center {
  flex: 1 !important;
  max-width: 550px !important;
}

/* ── Query Loop layout ── */
.page-id-1583 .wp-block-post-template .wp-block-columns {
  display: flex !important;
  gap: 10px !important;
  margin-bottom: 60px !important;
  align-items: flex-start !important;
  justify-content: center !important;
}

/* ── Post date ── */
.page-id-1583 .wp-block-post-date time {
  font-family: 'Poppins', sans-serif !important;
  font-size: 1.1rem !important;
  color: #777 !important;
}

/* ── Post title link ── */
.page-id-1583 .wp-block-post-title a {
  display: inline-block !important;
  background-color: #1f345c !important;
  color: #fff !important;
  font-family: 'Poppins', sans-serif !important;
  font-weight: 700 !important;
  font-size: 1.4rem !important;
  padding: 12px 22px !important;
  border-radius: 14px !important;
  line-height: 1.4 !important;
  text-decoration: none !important;
}
.page-id-1583 .wp-block-post-title a:hover {
  background-color: #2a4478 !important;
}

/* ── Post excerpt ── */
.page-id-1583 .wp-block-post-excerpt__excerpt {
  font-family: 'Poppins', sans-serif !important;
  font-size: 1.1rem !important;
  color: #000 !important;
  line-height: 1.7 !important;
  margin-bottom: 18px !important;
}

/* ── Read more link ── */
.page-id-1583 .wp-block-post-excerpt__more-link {
  font-family: 'Poppins', sans-serif !important;
  color: #bf9c3b !important;
  font-weight: 600 !important;
  font-size: 1.1rem !important;
  text-decoration: none !important;
}
.page-id-1583 .wp-block-post-excerpt__more-link:hover {
  color: #a5832e !important;
}

/* ── Kill top gap ── */
.page-id-1583,
.page-id-1583 body {
  padding: 0 !important;
  margin: 0 !important;
}
.page-id-1583 .wp-site-blocks,
.page-id-1583 .entry-content,
.page-id-1583 .wp-block-post-content,
.page-id-1583 article,
.page-id-1583 .has-global-padding,
.page-id-1583 #page,
.page-id-1583 #content,
.page-id-1583 .site {
  padding-top: 0 !important;
  margin-top: 0 !important;
  margin-block-start: 0 !important;
}

/* ── Responsive ── */
@media (max-width: 700px) {
  .page-id-1583 .wp-block-post-template .wp-block-columns {
    flex-direction: column !important;
  }
  .page-id-1583 .wp-block-post-featured-image {
    flex: 0 0 auto !important;
    max-width: 100% !important;
  }
}
```

### What It Contains
- Custom header with logo, navigation (Home, Blogs, Free, Press, About Us), and social media icons
- Dynamic blog post list powered by WordPress Query Loop (auto-updates when you publish new posts)
- Each post shows: featured image (left), date, title badge, excerpt, "Read more" link
- Custom footer with background image and copyright overlay

---

## Page 3 — Press Kit (`page-id-1664`)

### Files
| File | Role |
|------|------|
| `Blog-Posts/press-kit.html` | 4 WordPress blocks (copy/paste each block separately) |

### Setup Steps

**Step 1 — Create the page**

1. Create a WordPress page at `/press/`
2. Note the page ID (`1664`)

**Step 2 — Paste Block 1 (Header + Page CSS)**

1. Add a **Custom HTML block**
2. Copy everything from `<!-- ⏬ CUSTOM HTML — HEADER ⏬ -->` to `<!-- ⏹ END HEADER ⏹ -->` in `press-kit.html`
3. Paste into the block

> This block includes: header HTML, header CSS, full-page background, theme hiding, and wrapper stripping.

**Step 3 — Paste Block 2 (Intro + Download)**

1. Add another **Custom HTML block** below Block 1
2. Copy everything from `<!-- ⏬ CUSTOM HTML — PRESS KIT INTRO ⏬ -->` to `<!-- ⏹ END PRESS KIT INTRO ⏹ -->`
3. Paste into the block

**Step 4 — Paste Block 3 (Developer / Socials)**

This block uses **only inline styles** (no `<style>` tag) to avoid WordPress stripping issues.

1. Add another **Custom HTML block** below Block 2
2. Copy everything between `<!-- BLOCK 3: Custom HTML — Developer / Socials -->` and `<!-- END BLOCK 3 -->`
3. Paste into the block

**Step 5 — Paste Block 4 (Footer)**

1. Add another **Custom HTML block** below Block 3
2. Copy everything from `<!-- ⏬ CUSTOM HTML — FOOTER ⏬ -->` to `<!-- ⏹ END FOOTER ⏹ -->`
3. Paste into the block

**Step 6 — Additional CSS**

Go to **Appearance → Customize → Additional CSS** and add:

```css
/* Press-kit */
.page-id-1664 .press-footer-col * {
  color: #000 !important;
  display: block !important;
  visibility: visible !important;
}
```

> **Note:** Most press page CSS is already inline inside Block 1's `<style>` tag (background, theme hiding, wrapper stripping) and Block 2's `<style>` tag (intro content styling). The Additional CSS rule above is a safety override for the Developer/Socials section.

### What It Contains
- Custom header (same as blog page)
- Full-page background image
- Game cover art with rounded corners and drop shadow
- Title ("Langit Lupa: Office Series") in Special Elite font
- Body sections: Short Description, About this Game, Key Features (bold keywords), Closing
- Download Assets button (links to Google Drive, scales on hover)
- 3-column section: Logo (left), Developer info (center), Social links (right)

---

## Shared Header Component

The header is used across multiple pages: **Blog** and **Press Kit**. It lives in:

```
Home page/Header.html   ← HTML structure
Home page/Header.css    ← CSS styles
```

### Header Features
- Logo on the left (links to home)
- Navigation links with pipe `|` separators: Home, Blogs, Free, Press, About Us
- Social media icons on the right (Facebook, Instagram, Twitter/X, LinkedIn, TikTok, YouTube)
- Social icons scale up and brighten on hover
- `#1F345C` dark blue background

### Updating the Header Across Pages

If you change the header (e.g., add a new nav link), update these files:
1. `Home page/Header.html` — the source template
2. Blog page's Block 1 (`blog.html`)
3. Press Kit page's Block 1 (`press-kit.html`)

---

## Troubleshooting

### "My custom footer is hidden"

WordPress theme CSS may hide all `<footer>` elements. Ensure your Additional CSS has:
```css
.page-id-XXXX .blog-custom-footer {
  display: flex !important;
}
```

### "Content shows in the editor but not on the live page"

1. **Clear all caches** — WP Rocket, Cloudflare, browser (Ctrl+Shift+R)
2. **Check View Page Source** (Ctrl+U) — search for your content. If missing, WordPress stripped it.
3. **wpautop** — WordPress auto-wraps lines in `<p>` tags. This can inject `<p>` into `<style>` blocks. Try using inline styles instead of `<style>` tags.
4. **Security plugins** — WordFence or Sucuri may block `<style>` in Custom HTML. Temporarily disable to test.

### "I added a new page but the CSS doesn't apply"

Your CSS rules must use the correct page ID. Find it from the page editor URL (`post=XXXX`). Replace `XXXX` in all `.page-id-XXXX` selectors.

### "The Query Loop doesn't show my posts"

- Ensure your posts have **Featured Images** set
- Check the category IDs in the Query Loop match your blog posts' categories
- Ensure the Query Loop block was pasted in **Code Editor** mode, not as Custom HTML

### "There's a gap at the top of the page"

Add to Additional CSS for that page ID:
```css
.page-id-XXXX .wp-site-blocks,
.page-id-XXXX .entry-content,
.page-id-XXXX .has-global-padding {
  padding-top: 0 !important;
  margin-top: 0 !important;
}
```

---

## Notes

- **All images** must be uploaded to the WordPress Media Library and their URLs updated in the HTML if you change hosts or domains
- **Page IDs** may change if you recreate a page. Always verify the ID
- **The `Additional CSS` box** has no version control — keep a backup of your final CSS in a separate file
- **Custom HTML blocks** don't support WordPress shortcodes — use raw HTML/CSS/JS only

---

> **Project origination:** This site was initially prototyped as a React single-page application. WordPress does not support embedding React components into its page content natively. The solution is self-contained Custom HTML blocks with inline CSS/JS, which provide the same visual result without requiring a Node.js build pipeline or headless WordPress setup.
