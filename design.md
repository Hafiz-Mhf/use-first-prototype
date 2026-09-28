# UseFirst — Interactive Prototype Design System & UI Specifications

## 1. Visual & Architectural Philosophy
The UseFirst prototype employs a split-screen desktop showcase layout pairing an active mobile device simulator on the left with product context and interactive telemetry on the right[cite: 34, 35]. The interface reinforces a calm, practical tone using earthy greens and warm creams to reduce anxiety around household food waste[cite: 2, 34].

---

## 2. Color Palette & Design Tokens

| Token Name | Hex Code | RGB | Interface Function / Role |
| :--- | :--- | :--- | :--- |
| `--color-forest` | `#1F4D3A` | `rgb(31, 77, 58)` | Active tab pills, step card backgrounds, primary action buttons ("Add food", "Save item")[cite: 2, 34, 35]. |
| `--color-cream` | `#F6F1E8` | `rgb(246, 241, 232)` | Full-page desktop backdrop and mobile device chassis background[cite: 2, 34]. |
| `--color-lime` | `#B8D96C` | `rgb(184, 217, 108)` | Accent recipe header card fill, freshness indicators[cite: 2, 36]. |
| `--color-orange` | `#F28C45` | `rgb(242, 140, 69)` | High-urgency indicator bar on perishables ($\le 2$ days), primary culinary action CTA ("Mark spinach used")[cite: 2, 34, 36]. |
| `--color-ink` | `#193029` | `rgb(25, 48, 41)` | Display headings, body typography, active tab text[cite: 2, 34]. |
| `--color-white` | `#FFFFFF` | `rgb(255, 255, 255)` | Internal card fill surfaces, stat counter cards, input boxes[cite: 34, 35]. |
| `--color-border` | `rgba(25, 48, 41, 0.08)` | — | Subtle borders for stat cards and input form fields[cite: 34, 35]. |

---

## 3. Typography & Text Hierarchy

- **Display Headings (H1, H2, Hero):** Bold Serif (Georgia / 'Times New Roman' / Serif alternative)[cite: 34]
  - Hero Headline: `38px` | Weight: `700` | Line-height: `1.15` ("Start dinner with what is already at home.")[cite: 34]
  - Section Headline: `24px` | Weight: `700` ("How the concept works")[cite: 34]
  - Mobile App Header: `24px` | Weight: `700` ("My pantry", "Add food", "Cook now")[cite: 34, 35, 36]
- **Interface & Operational Text:** Clean Sans-Serif (Calibri / -apple-system / Arial)[cite: 2, 34]
  - Body Description: `15px` | Weight: `400` | Color: `#193029`[cite: 34]
  - Stat Numbers: `32px` | Weight: `700`[cite: 34]
  - Badges & Sub-labels: `12px` | Weight: `600` | Letter-spacing: `0.5px` (Uppercase)[cite: 34]

---

## 4. Layout Architecture: Split-Screen Desktop Showcase

The application layout consists of a fixed top bar and a responsive two-column grid[cite: 34]:

### 4.1. Global Header
- **Left:** UseFirst circular mark + wordmark + tagline (*"Eat what you have. Waste less."*)[cite: 2, 34].
- **Right Pill Badge:** White rounded pill with dark ink border: `FICTIONAL CLASSROOM PROTOTYPE`[cite: 34].

### 4.2. Left Column: The Mobile Device Chassis
- **Container:** Dark smartphone frame (`border-radius: 40px`, bezel padding `16px`) with integrated camera speaker notch at top[cite: 34].
- **Inner Canvas:** `#F6F1E8` fill containing screen view, sub-header question, 3-tab navigation bar, and view content[cite: 34].
- **Internal Tab Switcher:** Segmented controls with pills for `Pantry`, `Add`, and `Cook`[cite: 34]. Active state uses Forest Green fill (`#1F4D3A`) with white text[cite: 34, 35, 36].

### 4.3. Right Column: Hero, Telemetry & Onboarding Logic
- **Top Badge:** `PRODUCT CONCEPT` pill[cite: 34].
- **Headline:** *"Start dinner with what is already at home."*[cite: 34]
- **Value Proposition Body:** Explains the core coach philosophy: prioritizing the nearest date to avoid forgotten food rather than demanding perfect tracking[cite: 34].
- **Real-Time Telemetry Cards (3-Column Grid):**
  1. *Total Sample Items:* Dynamically reflects count (e.g., `4` or `3` items)[cite: 34, 36].
  2. *Items to Use Soon:* Counts items due within $\le 2$ days (e.g., `1` or `0` items)[cite: 34, 36].
  3. *Prototype Actions:* Indicates available interactive workflows (`3`)[cite: 34].
- **Process Guide ("How the concept works"):**
  - Three dark forest-green rounded cards (`#1F4D3A`):
    - `01 · ADD` — **Capture food:** Enter an item and a use-first date[cite: 34].
    - `02 · PRIORITIZE` — **See what matters:** The closest date appears first[cite: 34].
    - `03 · ACT` — **Cook or mark used:** Choose a recipe idea or clear the item[cite: 34].

---

## 5. Mobile Screen Interaction States

### Screen 1: "My Pantry" (Priority Queue)
- **Sub-Header:** *"What should I use first?"*[cite: 34]
- **Queue Cards:** White rounded surfaces with item name, days remaining, and trailing `Used` button[cite: 34].
- **Urgency Indicator:** Items with $\le 2$ days remaining display an accent orange border tag on the left edge (e.g., Spinach · 2 days)[cite: 34].
- **Bottom CTA:** Solid forest green button: `Add food`[cite: 34].

### Screen 2: "Add food" (Quick Entry)
- **Sub-Header:** *"Fast manual entry"*[cite: 35]
- **Form Fields:** 
  - Text input: `Food name` (e.g., placeholder "Yogurt")[cite: 35].
  - Number/date input: `Days until use-first date` (e.g., placeholder "6")[cite: 35].
- **Action CTA:** Solid forest green button: `Save item`[cite: 35].
- **Microcopy Footnote:** *"The production idea may support barcode or receipt scanning. This prototype uses a form only."*[cite: 35]

### Screen 3: "Cook now" (Culinary Match)
- **Sub-Header:** *"One idea from your sample pantry"*[cite: 36]
- **Recipe Recommendation Card:** Light lime container (`#E3EED0` / `#B8D96C` tint)[cite: 2, 36]:
  - Overline Badge: `COOK FIRST`[cite: 36]
  - Recipe Title: *"Creamy spinach pasta"*[cite: 36]
  - Ingredient Manifest: *"Uses spinach, milk and pasta from the sample pantry."*[cite: 36]
- **Action CTA:** Full-width warm orange button: `Mark spinach used`[cite: 36].
- **Feedback Microcopy:** *"Spinach was removed from the sample pantry."*[cite: 36]

---

## 6. Mandatory Compliance & Scope Note

Every screen view and export must render the persistent footer disclaimer verbatim[cite: 34, 35, 36]:
> *"Scope note: This is an interactive concept for coursework. It does not scan real barcodes, identify food, calculate verified savings, or provide food-safety advice."*[cite: 34, 35, 36]