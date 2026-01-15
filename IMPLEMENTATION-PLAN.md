# WriteRight Implementation Plan

## Overview

This document outlines the step-by-step implementation plan for WriteRight, a single-page web application that teaches technical writing through a learn-then-practice structure across four levels.

---

## Phase 1: Foundation

### 1.1 HTML Structure Setup

- [ ] Create main `index.html` file with embedded CSS and JS
- [ ] Add Google Fonts imports (IBM Plex Mono, Instrument Serif)
- [ ] Build header with app title and tagline
- [ ] Create level navigation (4 buttons: Sentences, Principles, Sequencing, Architecture)
- [ ] Add Learn/Practice mode toggle
- [ ] Create container sections for each level (8 total: 4 Learn + 4 Practice)

### 1.2 CSS Design System

- [ ] Define CSS custom properties (design tokens):
  - `--bg-primary: #0a0a0a`
  - `--bg-secondary: #141414`
  - `--bg-tertiary: #1a1a1a`
  - `--text-primary: #e8e8e8`
  - `--text-secondary: #888`
  - `--text-muted: #555`
  - `--accent: #f0c040`
  - `--accent-dim: #a08020`
  - `--success: #40c080`
  - `--error: #e05050`
  - `--border: #2a2a2a`
- [ ] Apply base typography styles (IBM Plex Mono body, Instrument Serif headings)
- [ ] Style header and navigation components
- [ ] Add button styles (`.btn-primary`, `.btn-secondary`)
- [ ] Implement responsive layout foundation

### 1.3 Core Navigation JavaScript

- [ ] Implement level switching logic (show/hide level containers)
- [ ] Implement Learn/Practice mode toggle
- [ ] Add active state management for navigation buttons
- [ ] Store current level and mode in application state

---

## Phase 2: Level 1 - Sentence Mechanics

### 2.1 Level 1 Learn Content

Create teaching cards for 5 writing problems, each with:
- Title and source attribution
- Rule explanation
- "Why it matters" explanation
- 2 before/after examples with character count notes

**Content to implement:**

1. **Passive Voice** (Strunk & White)
   - Rule: Use active voice. Make the doer the subject.
   - Examples needed: 2 before/after pairs

2. **Nominalizations / Buried Verbs** (Williams)
   - Rule: Use verbs instead of noun forms.
   - Examples needed: 2 before/after pairs

3. **Expletive Constructions** (Williams)
   - Rule: Avoid "There is/are" and "It is" sentence starters.
   - Examples needed: 2 before/after pairs

4. **Wordy Phrases** (Zinsser)
   - Rule: Replace wordy phrases with concise alternatives.
   - Examples needed: 2 before/after pairs

5. **Redundancy** (Strunk & White)
   - Rule: Eliminate redundant words and phrases.
   - Examples needed: 2 before/after pairs

### 2.2 Level 1 Learn UI Components

- [ ] Build `.learn-card` component structure
- [ ] Style card header (title + source)
- [ ] Style rule callout (left border accent)
- [ ] Style "why it matters" section
- [ ] Style example pairs (before/after with labels)
- [ ] Add example notes (character count reduction)

### 2.3 Level 1 Practice Data

Create 8-10 bloated sentences for practice:

```javascript
const level1Sentences = [
  {
    original: "...",
    ideal: "...",
    tips: ["issue1", "issue2"]
  },
  // ... 7-9 more sentences
];
```

**Sentences should cover:**
- Passive voice examples
- Nominalization examples
- Expletive construction examples
- Wordy phrase examples
- Redundancy examples
- Mixed-issue sentences (multiple problems)

### 2.4 Level 1 Practice UI

- [ ] Build exercise card with original sentence display
- [ ] Add textarea for user revision input
- [ ] Implement live character count (original vs. user input)
- [ ] Show percentage reduction calculation
- [ ] Add "Check Revision" submit button
- [ ] Add "Next Sentence" navigation button
- [ ] Build feedback display component (score + feedback text)
- [ ] Add ideal revision reveal (shown after scoring)

### 2.5 Level 1 Practice Logic

- [ ] Implement sentence cycling (next button functionality)
- [ ] Track current sentence index
- [ ] Handle submission flow:
  1. Disable button, show "Analyzing..."
  2. Call Claude API for scoring
  3. Display score with color coding (good/medium/poor)
  4. Show feedback text
  5. Reveal ideal revision
- [ ] Implement fallback scoring if API fails

---

## Phase 3: Level 2 - Writing Principles

### 3.1 Level 2 Learn Content

Create teaching cards organized by category:

**Information Flow:**
1. Old Before New (Williams)
2. Stress Position (Williams)
3. Subject-Verb Proximity (Williams)

**Clarity:**
4. Positive Form (Strunk & White)
5. Concrete Over Abstract (Zinsser)
6. Cut Qualifiers (Zinsser)

**Structure:**
7. Parallel Construction (Strunk & White)
8. Characters as Subjects (Williams)

Each card needs:
- Title and source
- Rule explanation
- 1-2 before/after examples

### 3.2 Level 2 Learn UI

- [ ] Reuse `.learn-card` component from Level 1
- [ ] Add category headers/dividers
- [ ] Style category groupings

### 3.3 Level 2 Practice Data

Define the 8 principles for selection:

```javascript
const writingPrinciples = [
  { id: 'old-new', name: 'Old Before New', desc: '...' },
  { id: 'subject-verb', name: 'Subject-Verb Proximity', desc: '...' },
  // ... 6 more
];
```

Create 12-15 exercises:

```javascript
const level2Exercises = [
  {
    sentence: "...",
    violations: ['principle-id-1', 'principle-id-2'],
    correction: "...",
    explanation: "..."
  },
  // ... 11-14 more
];
```

### 3.4 Level 2 Practice UI

- [ ] Build principle selection grid (8 selectable cards)
- [ ] Style principle option cards with checkbox UI
- [ ] Implement multi-select interaction (click to toggle)
- [ ] Add selected state styling
- [ ] Add correct/incorrect state styling (for after submission)
- [ ] Build streak counter display
- [ ] Add submit button and feedback area

### 3.5 Level 2 Practice Logic

- [ ] Implement principle card selection toggle
- [ ] Track selected principles in state
- [ ] Handle submission:
  1. Compare user selections to correct violations
  2. Mark each principle card as correct/incorrect
  3. Calculate score based on accuracy
  4. Display corrected sentence
  5. Show explanation
- [ ] Implement streak tracking (consecutive correct answers)
- [ ] Add exercise navigation

---

## Phase 4: Level 3 - Logical Sequencing

### 4.1 Level 3 Learn Content

Create teaching cards for 5 ordering principles:

1. **Inverted Pyramid** (journalism)
   - Conclusion/most important information first

2. **Context Before Detail** (Williams)
   - General before specific

3. **Chronology for Events**
   - Timelines in order

4. **Problem Before Solution** (proposal structure)

5. **Action Before Rationale** (runbook/emergency style)

Each needs 1-2 examples showing document section ordering.

### 4.2 Level 3 Learn UI

- [ ] Reuse `.learn-card` component
- [ ] Add visual section flow diagrams if helpful

### 4.3 Level 3 Practice Data

Create 3-4 document exercises:

```javascript
const level3Exercises = [
  {
    title: "Incident Report",
    sections: [
      { id: 'a', text: "Executive Summary: ..." },
      { id: 'b', text: "Timeline: ..." },
      // ... 4-6 sections
    ],
    validOrders: [
      ['a', 'd', 'b', 'c', 'e', 'f'],
      // alternative valid orders
    ],
    explanation: "..."
  },
  // ... 2-3 more documents
];
```

**Document types to include:**
- Incident Report
- Technical Proposal
- Design Document
- Status Update

### 4.4 Level 3 Practice UI

- [ ] Build sortable container
- [ ] Create draggable section cards with numbers
- [ ] Style drag states (dragging, hover)
- [ ] Add grab cursor styling
- [ ] Build submit and feedback area

### 4.5 Level 3 Practice Logic

- [ ] Implement HTML5 drag and drop:
  - `dragstart` - mark element as dragging
  - `dragend` - clear dragging state
  - `dragover` - determine drop position
  - `drop` - reorder elements
- [ ] Auto-update card numbers after reorder
- [ ] Handle submission:
  1. Get current order from DOM
  2. Send to Claude API for evaluation
  3. Display score (1-10)
  4. Show feedback on ordering logic
- [ ] Support multiple valid orderings
- [ ] Implement exercise cycling

---

## Phase 5: Level 4 - Document Architecture

### 5.1 Level 4 Learn Content

Create document type cards for 6 types:

| Document | When to Use | Structure |
|----------|-------------|-----------|
| Incident Report | After something broke | Summary → Impact → Timeline → Root Cause → Remediation → Prevention |
| Technical Proposal | Need approval/resources | Problem → Solution → Cost/Benefit → Implementation |
| Decision Memo | Leadership choosing between options | Context → Options → Analysis → Recommendation |
| Design Document | Before building something complex | Requirements → Architecture → Details → Risks |
| Operational Runbook | On-call procedures | Trigger → Steps → Verification → Escalation |
| Status Update | Recurring project communication | Progress → Blockers → Next Steps → Timeline |

Each card needs:
- Document name
- "When to use" tag
- Purpose (1-2 sentences)
- Standard structure (section flow)

### 5.2 Level 4 Learn UI

- [ ] Build `.doc-type-card` component
- [ ] Style document header (name + when-to-use tag)
- [ ] Style purpose section
- [ ] Style structure flow diagram (arrows between sections)

### 5.3 Level 4 Practice Data

Create 6-8 scenarios:

```javascript
const level4Scenarios = [
  {
    scenario: "Your deployment broke production at 3 AM...",
    options: [
      { id: 'incident', name: 'Incident Report', desc: '...' },
      { id: 'proposal', name: 'Technical Proposal', desc: '...' },
      // 2 more options
    ],
    correct: 'incident',
    explanation: "..."
  },
  // ... 5-7 more
];
```

**Scenarios should cover all 6 document types.**

### 5.4 Level 4 Practice UI

- [ ] Build scenario display
- [ ] Create 2x2 template selection grid
- [ ] Style template option cards
- [ ] Implement single-select interaction (radio behavior)
- [ ] Add selected state styling
- [ ] Build feedback area

### 5.5 Level 4 Practice Logic

- [ ] Implement single-select card interaction
- [ ] Handle submission:
  1. Get selected document type
  2. Call Claude API for evaluation
  3. Explain why correct/incorrect
- [ ] Track progress through scenarios

---

## Phase 6: API Integration

### 6.1 Claude API Setup

- [ ] Create API configuration section
- [ ] Add API key input UI (stored in localStorage)
- [ ] Implement secure key storage

### 6.2 API Scoring Functions

- [ ] `scoreRevision(original, revision, ideal, tips)` - Level 1
  - Prompt Claude to score 1-10
  - Return score + feedback JSON

- [ ] `evaluateOrdering(sections, currentOrder)` - Level 3
  - Prompt Claude to evaluate logical flow
  - Return score + feedback

- [ ] `evaluateDocumentChoice(scenario, selected, correct)` - Level 4
  - Prompt Claude to explain choice
  - Return explanation

### 6.3 Fallback Scoring

- [ ] Level 1 fallback: Character reduction heuristics
- [ ] Level 2: Direct comparison (no API needed)
- [ ] Level 3 fallback: Check against validOrders array
- [ ] Level 4 fallback: Direct comparison

### 6.4 Error Handling

- [ ] Add loading states for all API calls
- [ ] Implement retry logic for transient failures
- [ ] Show user-friendly error messages
- [ ] Gracefully degrade to fallback scoring

---

## Phase 7: Polish and Refinement

### 7.1 Loading States

- [ ] Add button loading state ("Analyzing...")
- [ ] Add skeleton loaders if needed
- [ ] Disable interactions during API calls

### 7.2 Progress Tracking

- [ ] Track completed exercises per level
- [ ] Show progress indicators
- [ ] Persist progress in localStorage

### 7.3 Responsive Design

- [ ] Test and fix mobile layout
- [ ] Adjust grid layouts for smaller screens
- [ ] Ensure touch-friendly drag-drop on mobile
- [ ] Test tablet layouts

### 7.4 Accessibility

- [ ] Add ARIA labels to interactive elements
- [ ] Ensure keyboard navigation works
- [ ] Add focus states
- [ ] Test with screen reader

### 7.5 Final Testing

- [ ] Test all 4 levels (Learn + Practice)
- [ ] Test API integration end-to-end
- [ ] Test fallback scoring
- [ ] Cross-browser testing
- [ ] Performance optimization

---

## File Structure

```
Writer/
├── index.html          # Main application (HTML + embedded CSS + JS)
├── writeright-spec.md  # Original specification
└── IMPLEMENTATION-PLAN.md  # This file
```

---

## Content Creation Checklist

### Level 1 Learn Content
- [ ] 2 passive voice examples
- [ ] 2 nominalization examples
- [ ] 2 expletive construction examples
- [ ] 2 wordy phrase examples
- [ ] 2 redundancy examples

### Level 1 Practice Sentences
- [ ] 8-10 bloated sentences with ideal revisions

### Level 2 Learn Content
- [ ] 8 writing principles with examples

### Level 2 Practice Exercises
- [ ] 12-15 sentences with tagged violations

### Level 3 Learn Content
- [ ] 5 ordering principles with examples

### Level 3 Practice Documents
- [ ] 3-4 scrambled documents (5-6 sections each)

### Level 4 Learn Content
- [ ] 6 document type descriptions

### Level 4 Practice Scenarios
- [ ] 6-8 workplace scenarios

---

## Implementation Order Summary

1. **Foundation** - HTML structure, CSS design system, navigation JS
2. **Level 1** - Learn cards, practice textarea + API scoring
3. **Level 2** - Learn cards, checkbox selection logic
4. **Level 3** - Learn cards, drag-drop implementation
5. **Level 4** - Learn cards, single-select grid
6. **API Integration** - Connect all scoring to Claude
7. **Polish** - Loading states, progress, responsive, accessibility

---

## Notes

- All CSS and JS should be embedded in the single `index.html` file
- Use `claude-sonnet-4-20250514` model for API calls
- Design tokens ensure consistent theming throughout
- Fallback scoring ensures app works without API access
- Progress should persist across sessions via localStorage
