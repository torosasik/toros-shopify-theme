# Quick Reference Cheat Sheet

## Start Development
```bash
cd /Users/torosasik/Downloads/copy-of-toros-new-theme
shopify theme dev --store american-tile-depot.myshopify.com
```

## Test URL
http://127.0.0.1:9292/products/10x30-alaska-ivory-natural-stone-look-porcelain-wall-tile

## Key Files
| Purpose | File Path |
|---------|-----------|
| Calculator Styles (NEW) | `/assets/calculator-popup-modern.css` |
| Calculator HTML/JS | `/snippets/product-template.liquid` (line ~589) |
| CSS Includes | `/layout/theme.liquid` (line ~100) |

## CSS Classes
```
.calc_pop_up              → Backdrop overlay
.tile-calculator-wrapper  → Popup container  
.heading                  → Title bar
.calculator-section       → Content sections
.input-box               → Input fields
.calculate_btn           → Blue calculate button
.btn-calculator          → Green add-to-cart button
.footer_outcome          → Results section
```

## Auth Issues?
1. Shopify Admin → Apps → Theme Access
2. Generate password
3. Use when CLI prompts

## Push to Shopify
```bash
shopify theme push --store american-tile-depot.myshopify.com
```
