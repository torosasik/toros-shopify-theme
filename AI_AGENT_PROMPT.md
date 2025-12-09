# AI Agent Prompt: Shopify Calculator Popup Redesign

## Your Role
You are continuing a Shopify theme development project for American Tile Depot. The previous developer set up the environment and created a modern CSS redesign for the tile calculator popup. Your job is to verify the design, make adjustments based on feedback, and ensure everything works correctly.

## Project Context

**Store:** American Tile Depot (american-tile-depot.myshopify.com)
**Theme Location:** `/Users/torosasik/Downloads/copy-of-toros-new-theme`
**Objective:** Modernize the calculator popup's visual appearance WITHOUT changing any functionality

## Current State

### What's Been Done
1. Shopify CLI local development environment is set up
2. A modern CSS file has been created: `/assets/calculator-popup-modern.css`
3. The CSS is included in `/layout/theme.liquid`
4. Documentation exists in the theme folder (DEVELOPMENT_GUIDE.md, QUICK_REFERENCE.md, PROJECT_STATUS.md)

### What Needs To Be Done
1. Start the dev server and verify the calculator popup appears with the new modern styling
2. Get feedback from the user on what needs adjustment
3. Make CSS adjustments as requested
4. Ensure all calculator functionality still works (calculations, overage options, add to cart)
5. Test mobile responsiveness
6. Push to production when approved

## How To Start

### Step 1: Start the Development Server
```bash
cd /Users/torosasik/Downloads/copy-of-toros-new-theme
shopify theme dev --store american-tile-depot.myshopify.com
```

If you get authentication errors, the user needs to:
1. Go to Shopify Admin → Apps → Theme Access
2. Generate a new password
3. Enter it when prompted

### Step 2: Test the Calculator
1. Open browser to: `http://127.0.0.1:9292`
2. Navigate to: `/products/10x30-alaska-ivory-natural-stone-look-porcelain-wall-tile`
3. Click "How much do I need?" link next to the Quantity field
4. The calculator popup should appear with modern styling

## Key Files

| File | Purpose |
|------|---------|
| `/assets/calculator-popup-modern.css` | **EDIT THIS** - Modern styles for calculator popup |
| `/snippets/product-template.liquid` | Calculator HTML and JavaScript (DO NOT modify functionality) |
| `/layout/theme.liquid` | Where CSS files are included |
| `/DEVELOPMENT_GUIDE.md` | Full project documentation |

## CSS Architecture

The new CSS overrides existing inline styles. Key selectors:

```css
.calc_pop_up              /* Overlay backdrop */
.calc_pop_up-open         /* Added when popup is visible */
.tile-calculator-wrapper  /* Main popup container */
.heading                  /* Blue gradient header */
.calculator-section       /* Content sections */
.calculator-section.footage    /* Square footage input section */
.calculator-section.dimensions /* Length/width input section */
.input-box                /* Input field wrappers */
.calculate_btn            /* Blue "Calculate" buttons */
.btn-calculator           /* Green "Add to Cart" button */
.footer_outcome           /* Green results section */
#overage-selectors        /* Overage radio buttons (10%, 15%, etc.) */
.line-separator           /* "Or" divider between sections */
```

## Design Specifications Applied

- **Popup:** White background, 20px border-radius, drop shadow
- **Header:** Blue gradient (#1a365d → #2c5282), white text
- **Sections:** Light gray background (#f8fafc), 16px border-radius
- **Inputs:** White background, 2px border, 12px border-radius, focus ring
- **Buttons:** Gradient backgrounds with hover effects and shadows
- **Outcome Section:** Light green background with green accents
- **Animation:** Fade-in backdrop, slide-up popup
- **Mobile:** Bottom sheet style, stacked layouts

## Important Rules

1. **DO NOT** modify any JavaScript or calculation logic
2. **DO NOT** change HTML structure in product-template.liquid
3. **ONLY** modify CSS in `/assets/calculator-popup-modern.css`
4. **PRESERVE** all existing class names (JavaScript depends on them)
5. **TEST** that calculations still work after any changes

## Deployment

When the user approves the design:
```bash
shopify theme push --store american-tile-depot.myshopify.com
```

## Troubleshooting

**CSS not appearing?**
- Hard refresh browser (Cmd+Shift+R or Ctrl+Shift+R)
- Verify `/layout/theme.liquid` contains: `{{ 'calculator-popup-modern.css' | asset_url | stylesheet_tag }}`

**Popup won't open?**
- Product must have tag `Tile_calculator`
- Check browser console for JavaScript errors

**Dev server won't start?**
- Run `shopify version` to verify CLI is installed
- Try `shopify auth logout` then restart

## Communication Style

- Ask the user to describe what they see or share screenshots
- Propose specific CSS changes and explain what they'll do
- Make incremental changes rather than rewriting everything
- Confirm functionality works after visual changes

## Read More

For complete details, read the documentation files in the theme folder:
- `/Users/torosasik/Downloads/copy-of-toros-new-theme/DEVELOPMENT_GUIDE.md`
- `/Users/torosasik/Downloads/copy-of-toros-new-theme/QUICK_REFERENCE.md`
- `/Users/torosasik/Downloads/copy-of-toros-new-theme/PROJECT_STATUS.md`
