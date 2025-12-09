# American Tile Depot - Shopify Theme Development Guide

## Project Overview

**Client:** American Tile Depot (americantiledepot.com)
**Objective:** Modernize the Shopify theme's visual design while preserving all existing functionality
**Current Focus:** Redesigning the Tile Calculator popup on product pages

---

## Development Environment Setup

### Store Information
- **Store URL:** american-tile-depot.myshopify.com
- **Live Site:** https://www.americantiledepot.com
- **Local Dev Server:** http://127.0.0.1:9292

### Theme Being Modified
- **Theme Name:** `copy-of-toros-new-theme` (safe working copy)
- **Theme Location:** `/Users/torosasik/Downloads/copy-of-toros-new-theme`

### Tools Installed

#### 1. Shopify CLI
- **Purpose:** Local theme development with hot-reload capability
- **Installation:** Via npm (requires admin privileges)
- **Command to start dev server:**
  ```bash
  cd /Users/torosasik/Downloads/copy-of-toros-new-theme
  shopify theme dev --store american-tile-depot.myshopify.com
  ```

#### 2. Theme Access App (Shopify)
- **Purpose:** Authentication for Shopify CLI when standard login fails
- **How it works:** Generates a password (format: `shptka_[32-character-hex]`) that bypasses OAuth issues
- **Setup:** Install "Theme Access" app from Shopify App Store → Generate password → Use when CLI prompts for authentication

#### 3. Node.js & npm
- **Purpose:** Required for Shopify CLI
- **Note:** On Mac, may need explicit PATH configuration after installation

---

## Project Architecture

### Key Theme Files

#### Calculator-Related Files
```
/snippets/product-template.liquid          # Main calculator HTML + inline CSS (starts ~line 589)
/snippets/product_details_calculator_main.liquid
/snippets/product_details_calculator_popup.liquid
/snippets/snippet_product-epc_popup_calculator.liquid
```

#### Layout Files
```
/layout/theme.liquid                       # Main theme layout, CSS includes
```

#### Assets (CSS/JS)
```
/assets/calculator-popup-modern.css        # NEW - Modern calculator styles (created by us)
/assets/custom.css                         # Existing custom styles
/assets/theme.css                          # Main theme styles
```

### How CSS is Loaded
In `/layout/theme.liquid` around line 98-100:
```liquid
{% liquid
  echo 'custom.css' | asset_url | stylesheet_tag: preload: true
%}
{{ 'calculator-popup-modern.css' | asset_url | stylesheet_tag }}
```

---

## Current Task: Calculator Popup Redesign

### What is the Calculator?
When customers visit a tile product page (products with tag `Tile_calculator`), they see:
1. A quantity section with "SQ. FT" and "Boxes" inputs
2. A "How much do I need?" link that opens a popup calculator
3. The popup helps customers calculate how many tiles/boxes they need based on:
   - Direct square footage input, OR
   - Room dimensions (length × width in feet/inches)
4. Includes overage options (10%, 15%, manual, none)

### Product Page Example
URL: `http://127.0.0.1:9292/products/10x30-alaska-ivory-natural-stone-look-porcelain-wall-tile`

### Design Goals
- **DO:** Update visual appearance (colors, typography, spacing, animations, rounded corners)
- **DO NOT:** Change any functionality, calculations, or JavaScript behavior

### Current Status
1. ✅ Created `/assets/calculator-popup-modern.css` with modern styles
2. ✅ Added CSS include to `/layout/theme.liquid`
3. ⏳ Need to verify the design and make adjustments

### CSS Design Features Implemented
- Backdrop blur overlay
- Rounded corners (20px border-radius)
- Gradient header (dark blue)
- Smooth slide-up animation
- Modern input styling with focus states
- Pill-style overage selector buttons
- Green "Outcome" section for results
- Mobile-responsive design
- Custom scrollbar styling

---

## How to Continue Development

### Starting the Dev Server
```bash
cd /Users/torosasik/Downloads/copy-of-toros-new-theme
shopify theme dev --store american-tile-depot.myshopify.com
```

If authentication issues occur:
1. Go to Shopify Admin → Apps → Theme Access
2. Generate new password
3. Use password when CLI prompts

### Testing Changes
1. Open browser to `http://127.0.0.1:9292`
2. Navigate to a tile product (e.g., `/products/10x30-alaska-ivory-natural-stone-look-porcelain-wall-tile`)
3. Click "How much do I need?" to open calculator popup
4. Changes to CSS files should hot-reload automatically

### Making CSS Adjustments
Edit `/assets/calculator-popup-modern.css` and save - changes appear instantly in browser.

### Key CSS Classes to Know
```css
.calc_pop_up              /* Overlay/backdrop */
.calc_pop_up-open         /* Class added when popup is visible */
.tile-calculator-wrapper  /* Main popup container */
.heading                  /* Popup header/title */
.calculator-section       /* Each section (footage, dimensions, outcome) */
.input-box                /* Input field containers */
.calculate_btn            /* Calculate buttons */
.btn-calculator           /* Add to Cart button */
.footer_outcome           /* Results section */
#overage-selectors        /* Overage radio button group */
```

### Product Metafields Used by Calculator
```liquid
product.metafields.my_fields.box_area              # Square footage per box
product.metafields.my_fields.tiles_per_box         # Tiles per box
product.metafields.measuringunitsatd.measuring_units_atd  # "Box", "Sheet", or "Piece"
```

---

## Deployment

### Pushing Changes to Live Theme
Once changes are tested and approved:
```bash
shopify theme push --store american-tile-depot.myshopify.com
```

**CAUTION:** Always push to the development/copy theme first, not the live theme.

---

## Troubleshooting

### Dev Server Won't Start
- Check Node.js is installed: `node --version`
- Check Shopify CLI is installed: `shopify version`
- Try re-authenticating with Theme Access password

### CSS Changes Not Appearing
- Hard refresh browser (Cmd+Shift+R)
- Check CSS file is saved
- Verify CSS include exists in theme.liquid
- Check browser dev tools for CSS loading errors

### Calculator Popup Won't Open
- Check browser console for JavaScript errors
- The popup requires the product to have tag `Tile_calculator`
- JavaScript that controls popup is inline in product-template.liquid

---

## Files Created/Modified in This Project

### Created
- `/assets/calculator-popup-modern.css` - New modern styles for calculator popup

### Modified  
- `/layout/theme.liquid` - Added CSS include for new stylesheet (line ~100)

---

## Alternative Verification Methods (Without Browser MCP)

Since Browser MCP has daily limits and can be slow:

1. **Manual Testing:** Open the dev server URL in your browser and test directly
2. **Screenshot Sharing:** User takes screenshots and shares with AI for feedback
3. **Standalone Preview:** Create an HTML file with the popup styles for quick preview without dev server

---

## Contact & Resources

- **Shopify CLI Docs:** https://shopify.dev/docs/themes/tools/cli
- **Theme Access App:** Available in Shopify App Store
- **Liquid Reference:** https://shopify.dev/docs/api/liquid

---

## Session Notes

**Last Session Date:** November 30, 2025

**What Was Done:**
1. Analyzed calculator popup structure in product-template.liquid
2. Created modern CSS redesign (calculator-popup-modern.css)
3. Added CSS to theme.liquid
4. Attempted to verify with Browser MCP (hit daily limits)

**Next Steps:**
1. Manually verify the calculator popup appearance
2. Adjust CSS based on visual feedback
3. Test on mobile viewport
4. Test all calculator functionality still works
5. Push to staging/production when approved
