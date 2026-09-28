# Dynamic Recipe Matching Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Upgrade `05_UseFirst_Product_Prototype.html` with a client-side Dynamic Recipe Matching Engine supporting intelligent ingredient classification, interactive chip toggling, strict `AGENT.md` schema compliance, and batch mark-used actions with undo support.

**Architecture:** Extend the existing zero-dependency Vanilla JavaScript engine inside `05_UseFirst_Product_Prototype.html`. Introduce modular culinary classification dictionaries, combinatorial template selection, reactive selection state, and batch state transitions with reversible snapshots.

**Tech Stack:** HTML5, Vanilla CSS3 (custom properties, flexbox/grid), Vanilla ES6 JavaScript (zero external dependencies).

---

## Global Constraints

- **Single file deliverable:** Modify `d:/usefirst/05_UseFirst_Product_Prototype.html` directly.
- **Zero external dependencies:** No CDN scripts, fonts, or network API calls. 100% offline.
- **Mandatory compliance disclaimer:** Maintain persistent footer disclaimer verbatim.
- **Strict AGENT.md compliance:**
  - Prep and cook time must be under 20 minutes.
  - Universal staples assumed: cooking oil, salt, black pepper, water.
  - No biological freshness guarantees.
  - Exact JSON keys: `recipe_title`, `prep_time_minutes`, `matched_items`, `pantry_staples_assumed`, `instructions`, `safety_reminder`.
- **Design tokens:** Preserve Forest (`#1F4D3A`), Cream (`#F6F1E8`), Lime (`#B8D96C`), Orange (`#F28C45`), Ink (`#193029`), White (`#FFFFFF`).

---

## Task Structure

### Task 1: Classification Matrix & Recipe Generation Engine

**Files:**
- Modify: `d:/usefirst/05_UseFirst_Product_Prototype.html`

**Interfaces:**
- Consumes: `pantryItems` state array (`{ id, name, days }`)
- Produces: `generateRecipe(selectedItems)` returning recipe object conforming to `AGENT.md` schema:
  ```typescript
  interface RecipeOutput {
    recipe_title: string;
    prep_time_minutes: number;
    matched_items: string[];
    pantry_staples_assumed: string[];
    instructions: string[];
    safety_reminder: string;
  }
  ```

- [ ] **Step 1: Define culinary role dictionary and classifier**
  Add the dictionary mapping ingredient keywords to culinary roles (`greens`, `aromatic`, `veg`, `dairy`, `starch`, `protein`, `fruit`).
  ```javascript
  const CULINARY_ROLES = {
    spinach: 'greens', kale: 'greens', lettuce: 'greens', arugula: 'greens', cabbage: 'greens', herbs: 'greens',
    onion: 'aromatic', garlic: 'aromatic', carrot: 'veg', broccoli: 'veg', pepper: 'veg', mushroom: 'veg', zucchini: 'veg', tomato: 'veg',
    milk: 'dairy', yogurt: 'dairy', 'greek yogurt': 'dairy', cream: 'dairy', cheese: 'dairy', butter: 'dairy',
    pasta: 'starch', rice: 'starch', bread: 'starch', potato: 'starch', noodles: 'starch', oats: 'starch',
    eggs: 'protein', egg: 'protein', tofu: 'protein', chicken: 'protein', beef: 'protein', beans: 'protein', fish: 'protein',
    berries: 'fruit', apple: 'fruit', banana: 'fruit', avocado: 'rich_fruit', lemon: 'fruit'
  };

  function classifyItem(name) {
    const clean = name.toLowerCase().trim();
    for (const [key, role] of Object.entries(CULINARY_ROLES)) {
      if (clean.includes(key)) return role;
    }
    return 'veg';
  }
  ```

- [ ] **Step 2: Implement combinatorial recipe template selector**
  Implement `generateRecipe(selectedItems)` evaluating present roles and producing structured steps:
  - If `greens` + `dairy` + `starch`: "Creamy Greens & Pasta Toss" (15 min)
  - If `protein` + any `veg`/`greens`: "Quick Farmhouse Scramble" (12 min)
  - If `starch` + any `veg`/`protein`: "Savory Pantry Sauté Bowl" (14 min)
  - If `dairy` + `fruit` or `oats`: "Fresh Pantry Parfait" (8 min)
  - If `greens`/`veg` + any item: "Garlic-Herb Pan Skillet" (10 min)
  - Fallback: "Chef's Pantry Medley" (15 min)
  Ensure all outputs include `safety_reminder` and `pantry_staples_assumed`.

---

### Task 2: Ingredient Selection UI & Chip Controls

**Files:**
- Modify: `d:/usefirst/05_UseFirst_Product_Prototype.html`

**Interfaces:**
- Consumes: `pantryItems`, `selectedItemIds` set
- Produces: `renderCookScreen()`, `toggleItemSelection(id)`

- [ ] **Step 1: Add HTML markup for chip selection container**
  Update `#screen-cook` inner HTML to include:
  - Subhead: "Dynamic meal ideas from your perishables"
  - Ingredient chip container: `<div class="ingredient-chips-wrap" id="cook-ingredient-chips"></div>`
  - Helper copy: "Tap items to pair (1 to 4 items):"
  - Recipe card container with dynamic instruction list (`<ol class="recipe-step-list" id="recipe-instructions"></ol>`)

- [ ] **Step 2: Add styles for chips and step items**
  Add CSS for `.ingredient-chips-wrap`, `.chip-btn`, `.chip-btn.active`, `.recipe-step-list`, and `.recipe-step-item`.

- [ ] **Step 3: Implement selection state management**
  Maintain `selectedItemIds` array. When `switchTab('cook')` is called:
  - If `selectedItemIds` is empty, auto-select top 2 items from `pantryItems`.
  - Filter out any `selectedItemIds` that no longer exist in `pantryItems`.
  - Provide `toggleItemSelection(id)` to add/remove and re-trigger recipe rendering.

---

### Task 3: Batch Mark Used & Undo Toast Notification

**Files:**
- Modify: `d:/usefirst/05_UseFirst_Product_Prototype.html`

**Interfaces:**
- Consumes: `currentRecipe.matched_items`, `pantryItems`
- Produces: `handleBatchMarkUsed()`, `handleUndoLastAction()`

- [ ] **Step 1: Implement batch removal logic with state snapshot**
  Create `lastRemovedItems` cache. When user clicks `Mark [N] items used`:
  - Find all pantry items whose names match `currentRecipe.matched_items`.
  - Save to `lastRemovedItems`.
  - Remove from `pantryItems`.
  - Clear `selectedItemIds`.
  - Update `render()` and telemetry.

- [ ] **Step 2: Implement undo toast banner**
  Add banner container: `<div class="undo-toast" id="undo-toast" role="status"></div>`.
  When batch used executes:
  - Display: `"[N] items marked used. <button type='button' class='btn-toast-undo' onclick='handleUndoLastAction()'>Undo</button>"`.
  - Auto-hide after 5000ms.
  - Clicking undo restores `lastRemovedItems` to `pantryItems` and refreshes UI.

---

### Task 4: End-to-End Verification

**Files:**
- Verify: `d:/usefirst/05_UseFirst_Product_Prototype.html`

- [ ] **Step 1: Run browser subagent validation**
  - Verify initial load displays top 2 items auto-selected in Cook tab.
  - Verify tapping a third chip updates recipe dynamically.
  - Verify clicking `Mark [N] items used` clears items from pantry and updates telemetry.
  - Verify clicking `Undo` restores items and telemetry accurately.
  - Verify zero console errors and persistent footer disclaimer intact.

- [ ] **Step 2: Update walkthrough artifact**
  Update `walkthrough.md` with verification results, before/after comparison, and recording.
