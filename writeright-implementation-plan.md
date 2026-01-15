# WriteRight Implementation Plan

A step-by-step guide to building the WriteRight technical writing trainer.

---

## Phase 1: Foundation

### 1.1 HTML Skeleton

Create the base HTML structure in a single file:

- [ ] Document head with Google Fonts (IBM Plex Mono, Instrument Serif)
- [ ] Header with logo and tagline
- [ ] Level navigation (4 level buttons)
- [ ] Mode toggle (Learn/Practice tabs)
- [ ] Container sections for each level-mode combination (8 total sections)
- [ ] API key input modal (for Claude API)

**Files:** `index.html` (single file approach)

### 1.2 CSS Foundation

Implement design system:

- [ ] CSS custom properties (design tokens from spec)
- [ ] Base typography styles
- [ ] Dark theme background and text colors
- [ ] Button styles (primary and secondary)
- [ ] Form elements (textarea, inputs)
- [ ] Layout utilities (flex, grid)

### 1.3 Core Navigation JS

Build the navigation system:

- [ ] Level button click handlers
- [ ] Mode toggle (Learn/Practice) handlers
- [ ] Show/hide appropriate content sections
- [ ] Active state management for buttons
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

- [ ] Implement `.learn-card` component
- [ ] Add all 5 cards with content
- [ ] Style before/after examples

### 2.2 Level 1 Practice Data

Create exercise dataset:

- [ ] Write 8-10 bloated sentences with issues
- [ ] Write ideal revision for each
- [ ] Document tips/issues for each sentence
- [ ] Store in `level1Sentences` array

### 2.3 Level 1 Practice UI

Build the exercise interface:

- [ ] Exercise card with original sentence display
- [ ] Textarea for user revision
- [ ] Character count comparison (original vs revision with % reduction)
- [ ] "Check Revision" submit button
- [ ] "Next Sentence" button
- [ ] Feedback display area (hidden initially)
- [ ] Progress indicator (e.g., "3 of 10")

### 2.4 Level 1 Scoring Integration

Implement AI scoring:

- [ ] API key storage (localStorage)
- [ ] `scoreRevision()` function calling Claude API
- [ ] JSON response parsing
- [ ] Fallback heuristic scoring (if API fails)
- [ ] Loading state on submit button
- [ ] Display score (1-10) with color coding
- [ ] Show feedback text
- [ ] Reveal ideal revision after scoring

---

## Phase 3: Level 2 - Writing Principles

### 3.1 Level 2 Learn Content

Create teaching content for 8 principles organized by category:

**Information Flow:**
- [ ] Old before new (Williams)
- [ ] Stress position (Williams)
- [ ] Subject-verb proximity (Williams)

**Clarity:**
- [ ] Positive form (Strunk & White)
- [ ] Concrete over abstract (Zinsser)
- [ ] Cut qualifiers (Zinsser)

**Structure:**
- [ ] Parallel construction (Strunk & White)
- [ ] Characters as subjects (Williams)

Each needs 1-2 before/after examples.

### 3.2 Level 2 Practice Data

Create exercise dataset:

- [ ] Write 12-15 problematic sentences
- [ ] Tag each with violated principles (can be multiple)
- [ ] Write correction for each
- [ ] Write explanation for each
- [ ] Store in `level2Exercises` array

### 3.3 Level 2 Practice UI

Build the selection interface:

- [ ] Exercise card showing problematic sentence
- [ ] Principle grid (8 selectable cards)
- [ ] Checkbox-style selection (multiple allowed)
- [ ] Submit button
- [ ] Feedback showing correct/incorrect highlights
- [ ] Corrected version display with explanation
- [ ] Streak counter display
- [ ] Progress indicator

### 3.4 Level 2 Scoring Logic

Implement local scoring:

- [ ] Compare user selections to correct answers
- [ ] Calculate score (correct matches vs total)
- [ ] Apply `.correct` / `.incorrect` classes to options
- [ ] Track and display streak
- [ ] Store progress in localStorage (optional)

---

## Phase 4: Level 3 - Logical Sequencing

### 4.1 Level 3 Learn Content

Create teaching content for 5 ordering principles:

- [ ] Inverted pyramid - conclusion first
- [ ] Context before detail - general before specific
- [ ] Chronology for events - timelines in order
- [ ] Problem before solution - proposal structure
- [ ] Action before rationale - runbook/emergency style

Each needs clear examples demonstrating the principle.

### 4.2 Level 3 Practice Data

Create exercise dataset:

- [ ] 3-4 different document types
- [ ] Each with 5-6 sections as shuffled cards
- [ ] Define valid orderings for each (can be multiple)
- [ ] Write explanations for each
- [ ] Store in `level3Exercises` array

**Document types to include:**
1. Incident Report
2. Technical Proposal
3. Decision Memo
4. Status Update

### 4.3 Level 3 Practice UI

Build the drag-drop interface:

- [ ] Sortable container
- [ ] Draggable card component with number indicator
- [ ] Visual feedback during drag (opacity, border)
- [ ] Exercise title display
- [ ] Submit button
- [ ] Feedback area

### 4.4 Level 3 Drag-Drop JS

Implement drag functionality:

- [ ] `handleDragStart()` - set dragged element, add class
- [ ] `handleDragEnd()` - cleanup, update numbers
- [ ] `handleDragOver()` - reposition logic
- [ ] `getDragAfterElement()` - determine drop position
- [ ] `updateCardNumbers()` - renumber after reorder
- [ ] Attach event listeners to all cards

### 4.5 Level 3 Scoring Integration

Implement AI scoring:

- [ ] Collect current order on submit
- [ ] Check against valid orderings (local match)
- [ ] If no local match, call Claude API to evaluate
- [ ] Display score (1-10) and explanation
- [ ] Accept multiple valid orderings

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
- [ ] Name and "when to use" tag
- [ ] Purpose (1-2 sentences)
- [ ] Standard structure (section flow)

### 5.2 Level 4 Practice Data

Create scenario dataset:

- [ ] Write 6-8 scenarios (2-3 sentences each)
- [ ] Define 4 document type options per scenario
- [ ] Mark correct answer
- [ ] Write explanation for each
- [ ] Store in `level4Scenarios` array

### 5.3 Level 4 Practice UI

Build the selection interface:

- [ ] Scenario card with situation description
- [ ] 2x2 grid of document type options
- [ ] Single-select behavior (radio-style)
- [ ] Submit button
- [ ] Feedback area

### 5.4 Level 4 Scoring Integration

Implement scoring:

- [ ] Check selection against correct answer
- [ ] Call Claude API for explanation (why correct/incorrect)
- [ ] Display result and explanation
- [ ] Progress indicator

---

## Phase 6: Polish & Refinement

### 6.1 Loading States

- [ ] Submit button disabled state with "Analyzing..." text
- [ ] Skeleton loading for API responses (optional)
- [ ] Prevent double-submission

### 6.2 Error Handling

- [ ] API error graceful fallback
- [ ] Invalid API key detection
- [ ] Network error messages
- [ ] Empty input validation

### 6.3 Responsive Design

- [ ] Mobile breakpoint (< 768px)
- [ ] Stack template grid on mobile
- [ ] Touch-friendly drag-drop (or simplified mobile alternative)
- [ ] Readable font sizes on all screens

### 6.4 Accessibility

- [ ] Keyboard navigation for selections
- [ ] Focus states on interactive elements
- [ ] ARIA labels where needed
- [ ] Color contrast verification

### 6.5 Progress Persistence (Optional)

- [ ] localStorage for completed exercises
- [ ] Track best scores per exercise
- [ ] Visual progress indicators per level

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
- [ ] All 4 levels load correctly
- [ ] Learn/Practice toggle works on each level
- [ ] Level 1: Textarea accepts input, API scoring works
- [ ] Level 2: Multiple selections work, scoring correct
- [ ] Level 3: Drag-drop reordering works, numbers update
- [ ] Level 4: Single selection works, feedback displays
- [ ] API fallback works when API unavailable
- [ ] Next buttons cycle through all exercises

### Visual Tests
- [ ] Dark theme renders correctly
- [ ] Fonts load (IBM Plex Mono, Instrument Serif)
- [ ] Before/after examples styled correctly
- [ ] Score colors correct (good=green, medium=yellow, poor=red)
- [ ] Responsive layout on mobile

### Edge Cases
- [ ] Empty textarea submission handled
- [ ] Very long user input handled
- [ ] Invalid API key handled
- [ ] Network timeout handled
- [ ] Rapid clicking prevented

---

## Notes

- Single HTML file keeps deployment simple
- Claude API key should be entered by user (not hardcoded)
- Consider rate limiting API calls to prevent abuse
- Fallback scoring ensures app works without API access
