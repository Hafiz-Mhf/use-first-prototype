# UseFirst — Prototype Project Planning

## 1. Objective & Scope
- **Sprint Duration:** 8-Hour Classroom Prototype Implementation[cite: 1, 2].
- **Core Problem:** Household food waste driven by visual neglect of items behind front shelves.
- **Core JTBD:** "When I plan a meal or shopping trip, help me see which food at home needs attention first, so I can choose a practical next action."
- **Deliverable:** A single-file, client-side, zero-dependency HTML/CSS/JavaScript web prototype demonstrating the core pantry prioritization queue[cite: 3, 5].

---

## 2. Technical Requirements
- **Runtime Environment:** Modern web browsers (Chrome, Edge, Safari, Firefox).
- **Architecture:** Client-side only (HTML5, Vanilla CSS3, Vanilla ES6+ JavaScript).
- **Dependencies:** Zero external CDNs, zero third-party JavaScript libraries, zero network API calls[cite: 5].
- **Storage:** Ephemeral in-memory state or local browser storage (`localStorage`)[cite: 3, 5].
- **Responsive Viewport:** Mobile-first layout (optimized for 375px–430px smartphone widths)[cite: 3, 5].

---

## 3. Work Breakdown Structure (WBS)
| Phase | Task | Deliverable | Status |
| :--- | :--- | :--- | :--- |
| **Phase 1** | Layout scaffolding & brand color variables | Base responsive container (`Trebuchet MS`, `Calibri`)[cite: 2] | Completed |
| **Phase 2** | Dynamic date queue & sorting algorithms | Ascending sort by days remaining | Completed |
| **Phase 3** | Quick item entry modal / form | Validated input fields (Item Name, Date) | Completed |
| **Phase 4** | Culinary match logic ("Cook Now") | Context-aware 3-ingredient recipe card | Completed |
| **Phase 5** | Governance, safety disclaimers & accessibility | WCAG high contrast, aria labels, disclaimer banner[cite: 2, 3, 5] | Completed |

---

## 4. Feature Implementation Boundaries
- **In-Scope (MVP Prototype):**
  - Add item with target use-first date.
  - Real-time ascending sort (closest date surfaces at the top)[cite: 3].
  - Mark item as "Used" (immediate removal from queue)[cite: 3].
  - Static 3-ingredient recipe suggestion ("Creamy Spinach Pasta") using listed items[cite: 3].
  - Prominent "Classroom Concept" disclaimer[cite: 2, 5].
- **Out-of-Scope (Deferred to Phase 2 / Research):**
  - Barcode scanning and OCR receipt parsing[cite: 3].
  - Multi-user / shared household synchronization[cite: 3].
  - Push notifications and automated SMS/email alerts[cite: 3].
  - Dynamic LLM API integrations[cite: 3, 5].

---

## 5. Go/No-Go Decision Gate
- **Pass Criteria:** A user can add 3 perishable staples and view a sorted priority list within 60 seconds[cite: 3].
- **Failure Trigger:** If manual data entry takes >30 seconds per item or if testers misinterpret "use-first date" as an absolute food safety indicator, halt feature expansion and redesign entry flow[cite: 3].