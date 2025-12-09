# Tile Calculator Update Summary - December 7, 2025

## Objective
Achieve a "premium", "ultra-compact", and "pixel-perfect" UI/UX for the Tile Calculator popup, ensuring seamless functionality and a specific 2-step user flow (Calculator -> Overage Reminder).

## Achievements & Verification

### 1. Functional Logic (Verified)
*   **Dimensions Sync:** Typing `10` x `10` in the dimensions section automatically populates the "Enter Your Area" box with `100` (Verified via test).
*   **Exclusive Inputs:** Typing in the "Area" box allows manual override and clears dimension inputs to avoid confusion.
*   **2-Step Flow:** Clicking "Add to Cart" inside the calculator:
    1.  Closes the Calculator.
    2.  Immediately opens the **Overage Reminder** popup (Verified via test).
    3.  User selects an overage amount (e.g., 15%), which then adds the total quantity to the cart.
*   **Dynamic Wording:** The logic correctly checks the product's unit type (Box, Sheet, Piece) and updates labels in both the Calculator ("Boxes Needed") and the Overage Popup ("You are adding X Boxes...").

### 2. Visual Design
*   **Ultra-Compact Layout:** All vertical scrolling has been eliminated. Padding reduced to `10px`, margins tightened.
*   **Premium Styling:** Soft shadows, rounded corners, "New York" serif font for headers (`17px`), and clean sans-serif for inputs. Number spinners removed for a cleaner look.

## Deployment Guide

### Files to Upload
To deploy this to your live theme, update these two files with the code from your local environment:
1.  **`snippets/product-template.liquid`**: Contains all HTML, JavaScript logic, and Liquid conditions.
2.  **`assets/calculator-popup-modern.css`**: Contains all the styling rules.

### Configuration & Triggers
For the calculator to appear on a product, ensure the following:

#### 1. Activation Tag
Add the tag **`Tile_calculator`** to the product in Shopify Admin.
*   *Note:* This single tag now activates **BOTH** the "How much do I need?" calculator link AND the "Overage Reminder" popup. You no longer need separate overage tags.

#### 2. Dynamic Units (Metafields)
To ensure the calculator says "Boxes", "Sheets", or "Pieces" correctly, set the following Product Metafield:
*   **Namespace/Key:** `measuringunitsatd.measuring_units_atd`
*   **Values:**
    *   `Box`
    *   `Sheet`
    *   `Piece`
    *   *(If left empty, it defaults to pluralizing the value or "Boxes" as fallback)*

## Technical Details
*   **Logic:** The JavaScript uses independent calculations for Top (Area) and Bottom (Dimensions) sections but syncs them intelligently.
*   **Overage Trigger:** The "Add to Cart" button in the calculator manually triggers the `#ovg-popup` opening class before closing itself, ensuring a smooth transition without relying on hidden overlays.
