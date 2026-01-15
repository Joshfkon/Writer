# WriteRight Implementation Plan

A step-by-step guide to building the WriteRight technical writing trainer.

---

## Phase 1: Foundation

### 1.1 HTML Skeleton

Create the base HTML structure in a single file:

- [x] Document head with Google Fonts (IBM Plex Mono, Instrument Serif)
- [x] Header with logo and tagline
- [x] Level navigation (4 level buttons)
- [x] Mode toggle (Learn/Practice tabs)
- [x] Container sections for each level-mode combination (8 total sections)
- [x] API key input modal (for Claude API)

**Files:** `index.html` (single file approach)

### 1.2 CSS Foundation

Implement design system:

- [x] CSS custom properties (design tokens from spec)
- [x] Base typography styles
- [x] Dark theme background and text colors
- [x] Button styles (primary and secondary)
- [x] Form elements (textarea, inputs)
- [x] Layout utilities (flex, grid)

### 1.3 Core Navigation JS

Build the navigation system:

- [x] Level button click handlers
- [x] Mode toggle (Learn/Practice) handlers
- [x] Show/hide appropriate content sections
- [x] Active state management for buttons
- [ ] URL hash support for direct linking (optional)

---

## Phase 2: Level 1 - Sentence Mechanics

### 2.1 Level 1 Learn Content

Create 5 learn cards teaching:

| Concept | Source | Examples Needed |
|---------|--------|-----------------|
| Passive voice | Strunk & White | 2 before/after |
| Nominalizations/buried verbs | Williams | 2 before/after |
| Expletive constructions | Williams | 2 before/after |
| Wordy phrases | Zinsser | 2 before/after |
| Redundancy | Strunk & White | 2 before/after |

- [x] Implement `.learn-card` component
- [x] Add all 5 cards with content
- [x] Style before/after examples

### 2.2 Level 1 Practice Data

Create exercise dataset:

- [x] Write 8-10 bloated sentences with issues
- [x] Write ideal revision for each
- [x] Document tips/issues for each sentence
- [x] Store in `level1Sentences` array

### 2.3 Level 1 Practice UI

Build the exercise interface:

- [x] Exercise card with original sentence display
- [x] Textarea for user revision
- [x] Character count comparison (original vs revision with % reduction)
- [x] "Check Revision" submit button
- [x] "Next Sentence" button
- [x] Feedback display area (hidden initially)
- [x] Progress indicator (e.g., "3 of 10")

### 2.4 Level 1 Scoring Integration

Implement AI scoring:

- [x] API key storage (localStorage)
- [x] `scoreRevision()` function calling Claude API
- [x] JSON response parsing
- [x] Fallback heuristic scoring (if API fails)
- [x] Loading state on submit button
- [x] Display score (1-10) with color coding
- [x] Show feedback text
- [x] Reveal ideal revision after scoring

---

## Phase 3: Level 2 - Writing Principles

### 3.1 Level 2 Learn Content

Create teaching content for 8 principles organized by category:

**Information Flow:**
- [x] Old before new (Williams)
- [x] Stress position (Williams)
- [x] Subject-verb proximity (Williams)

**Clarity:**
- [x] Positive form (Strunk & White)
- [x] Concrete over abstract (Zinsser)
- [x] Cut qualifiers (Zinsser)

**Structure:**
- [x] Parallel construction (Strunk & White)
- [x] Characters as subjects (Williams)

Each needs 1-2 before/after examples.

### 3.2 Level 2 Practice Data

Create exercise dataset:

- [x] Write 12-15 problematic sentences
- [x] Tag each with violated principles (can be multiple)
- [x] Write correction for each
- [x] Write explanation for each
- [x] Store in `level2Exercises` array

### 3.3 Level 2 Practice UI

Build the selection interface:

- [x] Exercise card showing problematic sentence
- [x] Principle grid (8 selectable cards)
- [x] Checkbox-style selection (multiple allowed)
- [x] Submit button
- [x] Feedback showing correct/incorrect highlights
- [x] Corrected version display with explanation
- [ ] Streak counter display
- [x] Progress indicator

### 3.4 Level 2 Scoring Logic

Implement local scoring:

- [x] Compare user selections to correct answers
- [x] Calculate score (correct matches vs total)
- [x] Apply `.correct` / `.incorrect` classes to options
- [ ] Track and display streak
- [x] Store progress in localStorage (optional)

---

## Phase 4: Level 3 - Logical Sequencing

### 4.1 Level 3 Learn Content

Create teaching content for 5 ordering principles:

- [x] Inverted pyramid - conclusion first
- [x] Context before detail - general before specific
- [x] Chronology for events - timelines in order
- [x] Problem before solution - proposal structure
- [x] Action before rationale - runbook/emergency style

Each needs clear examples demonstrating the principle.

### 4.2 Level 3 Practice Data

Create exercise dataset:

- [x] 3-4 different document types
- [x] Each with 5-6 sections as shuffled cards
- [x] Define valid orderings for each (can be multiple)
- [x] Write explanations for each
- [x] Store in `level3Exercises` array

**Document types to include:**
1. Incident Report
2. Technical Proposal
3. Decision Memo
4. Status Update

### 4.3 Level 3 Practice UI

Build the drag-drop interface:

- [x] Sortable container
- [x] Draggable card component with number indicator
- [x] Visual feedback during drag (opacity, border)
- [x] Exercise title display
- [x] Submit button
- [x] Feedback area

### 4.4 Level 3 Drag-Drop JS

Implement drag functionality:

- [x] `handleDragStart()` - set dragged element, add class
- [x] `handleDragEnd()` - cleanup, update numbers
- [x] `handleDragOver()` - reposition logic
- [x] `getDragAfterElement()` - determine drop position
- [x] `updateCardNumbers()` - renumber after reorder
- [x] Attach event listeners to all cards

### 4.5 Level 3 Scoring Integration

Implement AI scoring:

- [x] Collect current order on submit
- [x] Check against valid orderings (local match)
- [x] If no local match, call Claude API to evaluate
- [x] Display score (1-10) and explanation
- [x] Accept multiple valid orderings

---

## Phase 5: Level 4 - Document Architecture

### 5.1 Level 4 Learn Content

Create cards for 6 document types:

| Document | When to Use |
|----------|-------------|
| Incident Report | After something broke |
| Technical Proposal | Need approval/resources |
| Decision Memo | Leadership choosing between options |
| Design Document | Before building something complex |
| Operational Runbook | On-call procedures |
| Status Update | Recurring project communication |

Each card needs:
- [x] Name and "when to use" tag
- [x] Purpose (1-2 sentences)
- [x] Standard structure (section flow)

### 5.2 Level 4 Practice Data

Create scenario dataset:

- [x] Write 6-8 scenarios (2-3 sentences each)
- [x] Define 4 document type options per scenario
- [x] Mark correct answer
- [x] Write explanation for each
- [x] Store in `level4Scenarios` array

### 5.3 Level 4 Practice UI

Build the selection interface:

- [x] Scenario card with situation description
- [x] 2x2 grid of document type options
- [x] Single-select behavior (radio-style)
- [x] Submit button
- [x] Feedback area

### 5.4 Level 4 Scoring Integration

Implement scoring:

- [x] Check selection against correct answer
- [x] Call Claude API for explanation (why correct/incorrect)
- [x] Display result and explanation
- [x] Progress indicator

---

## Phase 6: Polish & Refinement

### 6.1 Loading States

- [x] Submit button disabled state with "Analyzing..." text
- [ ] Skeleton loading for API responses (optional)
- [x] Prevent double-submission

### 6.2 Error Handling

- [x] API error graceful fallback
- [x] Invalid API key detection
- [x] Network error messages
- [x] Empty input validation

### 6.3 Responsive Design

- [x] Mobile breakpoint (< 768px)
- [x] Stack template grid on mobile
- [x] Touch-friendly drag-drop (or simplified mobile alternative)
- [x] Readable font sizes on all screens

### 6.4 Accessibility

- [x] Keyboard navigation for selections
- [x] Focus states on interactive elements
- [x] ARIA labels where needed
- [x] Color contrast verification

### 6.5 Progress Persistence (Optional)

- [x] localStorage for completed exercises
- [x] Track best scores per exercise
- [x] Visual progress indicators per level

---

## Component Reference

### CSS Classes to Implement

```
Base:
- .btn-primary, .btn-secondary
- .btn-row

Learn:
- .learn-card, .learn-card-header, .learn-card-title
- .learn-card-source, .learn-card-rule, .learn-card-why
- .example-pair, .example-label, .example-text, .example-note

Practice:
- .exercise-card, .exercise-type, .exercise-prompt
- .original-text
- .feedback, .feedback-header, .feedback-text
- .score, .score.good/.medium/.poor
- .char-count

Level 2:
- .principle-grid, .principle-option
- .principle-checkbox, .principle-name, .principle-desc
- .principle-option.selected/.correct/.incorrect

Level 3:
- .sortable-container, .sortable-card
- .card-number
- .sortable-card.dragging

Level 4:
- .doc-type-card, .doc-type-header, .doc-type-name
- .doc-type-when, .doc-type-purpose, .doc-type-structure
- .template-grid, .template-option
- .template-name, .template-desc
```

### JS Functions to Implement

```javascript
// Navigation
initNavigation()
showLevel(levelNum)
showMode(mode)

// Level 1
loadL1Exercise(index)
scoreRevision(original, revision, ideal, tips)
showL1Feedback(score, feedback, ideal)
nextL1Exercise()

// Level 2
loadL2Exercise(index)
togglePrincipleSelection(id)
checkL2Answers()
showL2Feedback(correct, incorrect, explanation)
nextL2Exercise()

// Level 3
loadL3Exercise(index)
initDragDrop()
handleDragStart(e)
handleDragEnd(e)
handleDragOver(e)
getDragAfterElement(container, y)
updateCardNumbers()
scoreL3Order()
nextL3Exercise()

// Level 4
loadL4Scenario(index)
selectTemplate(id)
checkL4Answer()
nextL4Scenario()

// API
callClaudeAPI(prompt)
getApiKey()
setApiKey(key)

// Utils
showFeedback(elementId, score, text)
hideFeedback(elementId)
updateProgress(level, current, total)
```

---

## Data Files Structure

All data can be embedded in the single HTML file within `<script>` tags:

```javascript
// Embedded in index.html
const level1Sentences = [...];      // 8-10 items
const writingPrinciples = [...];    // 8 items
const level2Exercises = [...];      // 12-15 items
const level3Exercises = [...];      // 3-4 items
const level4Scenarios = [...];      // 6-8 items
const documentTypes = [...];        // 6 items (for learn content)
```

---

## Testing Checklist

### Functional Tests
- [x] All 4 levels load correctly
- [x] Learn/Practice toggle works on each level
- [x] Level 1: Textarea accepts input, API scoring works
- [x] Level 2: Multiple selections work, scoring correct
- [x] Level 3: Drag-drop reordering works, numbers update
- [x] Level 4: Single selection works, feedback displays
- [x] API fallback works when API unavailable
- [x] Next buttons cycle through all exercises

### Visual Tests
- [x] Dark theme renders correctly
- [x] Fonts load (IBM Plex Mono, Instrument Serif)
- [x] Before/after examples styled correctly
- [x] Score colors correct (good=green, medium=yellow, poor=red)
- [x] Responsive layout on mobile

### Edge Cases
- [x] Empty textarea submission handled
- [x] Very long user input handled
- [x] Invalid API key handled
- [x] Network timeout handled
- [x] Rapid clicking prevented

---

## Notes

- Single HTML file keeps deployment simple
- Claude API key should be entered by user (not hardcoded)
- Consider rate limiting API calls to prevent abuse
- Fallback scoring ensures app works without API access
