# WriteRight - Technical Writing Trainer

## Overview

A single-page web app that teaches technical writing through a learn-then-practice structure. Four levels, each with a Learn tab (teaching content with examples) and a Practice tab (interactive exercises scored by AI).

---

## Tech Stack

- Single HTML file with embedded CSS and JS
- Vanilla JS (no frameworks)
- Claude API for scoring (`claude-sonnet-4-20250514`)
- Fonts: IBM Plex Mono, Instrument Serif (Google Fonts)
- Dark theme

---

## Design Tokens

```css
:root {
  --bg-primary: #0a0a0a;
  --bg-secondary: #141414;
  --bg-tertiary: #1a1a1a;
  --text-primary: #e8e8e8;
  --text-secondary: #888;
  --text-muted: #555;
  --accent: #f0c040;
  --accent-dim: #a08020;
  --success: #40c080;
  --error: #e05050;
  --border: #2a2a2a;
}

body {
  font-family: 'IBM Plex Mono', monospace;
  background: var(--bg-primary);
  color: var(--text-primary);
}

h1, h2, .level-title, .learn-card-title {
  font-family: 'Instrument Serif', serif;
}
```

---

## Structure

### Level 1: Sentence Mechanics

#### Learn Tab

Teach these common problems with 2 before/after examples each:

- **Passive voice** (Strunk & White)
- **Nominalizations / buried verbs** (Williams)
- **Expletive constructions** - "There is/are", "It is" (Williams)
- **Wordy phrases** - "due to the fact that" → "because" (Zinsser)
- **Redundancy** (Strunk & White)

#### Practice Tab

- Show a bloated sentence
- User rewrites it in a textarea
- Display character count comparison (original vs revision, show % reduction)
- On submit: call Claude API to score 1-10 with specific feedback
- Show ideal revision after scoring
- "Next" button cycles through 8-10 sentences

---

### Level 2: Writing Principles

#### Learn Tab

Teach these principles organized by category, each with 1-2 before/after examples:

**Information Flow:**
- Old before new (Williams)
- Stress position - emphasis at sentence end (Williams)
- Subject-verb proximity (Williams)

**Clarity:**
- Positive form - state what is, not what isn't (Strunk & White)
- Concrete over abstract (Zinsser)
- Cut qualifiers - "very", "rather", "quite" (Zinsser)

**Structure:**
- Parallel construction (Strunk & White)
- Characters as subjects (Williams)

#### Practice Tab

- Show a problematic sentence
- Display all 8 principles as selectable options (checkbox-style cards)
- User selects which principle(s) are violated (can be multiple)
- On submit: highlight correct/incorrect selections, show score, display corrected version with explanation
- Track streak for motivation
- 12-15 exercises

---

### Level 3: Logical Sequencing

#### Learn Tab

Teach these ordering principles with examples:

- **Inverted pyramid** - conclusion first (journalism)
- **Context before detail** - general before specific (Williams)
- **Chronology for events** - timelines in order
- **Problem before solution** (proposal structure)
- **Action before rationale** (runbook/emergency style)

#### Practice Tab

- Show 5-6 document sections as draggable cards
- User drags to reorder
- On submit: call Claude API to evaluate ordering logic, score 1-10
- Multiple valid orderings acceptable
- 3-4 different document types to practice

---

### Level 4: Document Architecture

#### Learn Tab

Teach 6 document types, each with:

- Name and "when to use" tag
- Purpose (1-2 sentences)
- Standard structure (section flow)

**Document types:**

| Document | When to Use |
|----------|-------------|
| Incident Report | After something broke |
| Technical Proposal | Need approval/resources |
| Decision Memo | Leadership choosing between options |
| Design Document | Before building something complex |
| Operational Runbook | On-call procedures |
| Status Update | Recurring project communication |

#### Practice Tab

- Show a scenario (2-3 sentences describing a situation)
- Display 4 document type options as cards
- User selects the best match
- On submit: call Claude API to explain why correct/incorrect
- 6-8 scenarios

---

## Example UI Components

### Header and Navigation

```html
<header>
  <h1>Write<span class="accent">Right</span></h1>
  <p class="tagline">Technical writing trainer — structure, clarity, precision</p>
</header>

<nav class="level-nav">
  <button class="level-btn active" data-level="1">Level 1: Sentences</button>
  <button class="level-btn" data-level="2">Level 2: Principles</button>
  <button class="level-btn" data-level="3">Level 3: Sequencing</button>
  <button class="level-btn" data-level="4">Level 4: Architecture</button>
</nav>

<div class="mode-toggle">
  <button class="mode-btn active" data-mode="learn">Learn</button>
  <button class="mode-btn" data-mode="practice">Practice</button>
</div>
```

---

### Learn Card (for teaching principles)

```html
<div class="learn-card">
  <div class="learn-card-header">
    <div class="learn-card-title">Passive Voice</div>
    <div class="learn-card-source">Strunk & White</div>
  </div>
  <div class="learn-card-rule">
    Use active voice. Make the doer the subject of the sentence.
  </div>
  <div class="learn-card-why">
    Passive voice hides responsibility and adds words. "Mistakes were made" vs 
    "We made mistakes"—one is accountable, the other is evasive.
  </div>
  <div class="example-pair">
    <div class="example-label before">Before</div>
    <div class="example-text before">The report was written by the team.</div>
  </div>
  <div class="example-pair">
    <div class="example-label after">After</div>
    <div class="example-text after">The team wrote the report.</div>
    <div class="example-note">6 words → 5 words. Clearer actor.</div>
  </div>
</div>
```

```css
.learn-card {
  background: var(--bg-secondary);
  border: 1px solid var(--border);
  padding: 1.75rem;
  margin-bottom: 1.5rem;
}

.learn-card-header {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  margin-bottom: 1rem;
}

.learn-card-title {
  font-family: 'Instrument Serif', serif;
  font-size: 1.15rem;
}

.learn-card-source {
  font-size: 0.7rem;
  color: var(--text-muted);
  font-style: italic;
}

.learn-card-rule {
  font-size: 0.9rem;
  color: var(--text-secondary);
  margin-bottom: 1rem;
  padding-left: 1rem;
  border-left: 2px solid var(--accent-dim);
}

.example-pair {
  background: var(--bg-tertiary);
  padding: 1rem 1.25rem;
  margin-bottom: 0.75rem;
}

.example-label {
  font-size: 0.65rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 0.35rem;
}

.example-label.before { color: var(--error); }
.example-label.after { color: var(--success); }

.example-text.before { color: var(--text-muted); }
.example-text.after { color: var(--text-primary); }

.example-note {
  font-size: 0.75rem;
  color: var(--text-muted);
  margin-top: 0.5rem;
  font-style: italic;
}
```

---

### Practice Card with Textarea (Level 1)

```html
<div class="exercise-card">
  <div class="exercise-type">Edit Mode</div>
  <p class="exercise-prompt">Rewrite this sentence to be clearer and more concise:</p>
  <div class="original-text" id="l1-original">
    It was decided by the committee that the implementation should be postponed.
  </div>
  <textarea id="l1-input" placeholder="Your revision..."></textarea>
  <div class="btn-row">
    <button class="btn-primary" id="l1-submit">Check Revision</button>
    <button class="btn-secondary" id="l1-next">Next Sentence</button>
    <span class="char-count">Original: 78 chars</span>
  </div>
  <div class="feedback" id="l1-feedback">
    <div class="feedback-header">
      <span class="score good">8</span>
      <span class="score-label">/ 10</span>
    </div>
    <div class="feedback-text">
      Good compression! You eliminated the passive voice and cut the nominalization...
    </div>
  </div>
</div>
```

```css
.exercise-card {
  background: var(--bg-secondary);
  border: 1px solid var(--border);
  padding: 2rem;
  margin-bottom: 2rem;
}

.exercise-type {
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--accent);
  margin-bottom: 1rem;
}

.original-text {
  background: var(--bg-tertiary);
  border-left: 2px solid var(--border);
  padding: 1rem 1.25rem;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
  color: var(--text-secondary);
}

textarea {
  width: 100%;
  background: var(--bg-primary);
  border: 1px solid var(--border);
  color: var(--text-primary);
  font-family: inherit;
  font-size: 0.9rem;
  padding: 1rem;
  resize: vertical;
  min-height: 100px;
}

textarea:focus {
  outline: none;
  border-color: var(--accent-dim);
}

.btn-row {
  display: flex;
  gap: 1rem;
  align-items: center;
  flex-wrap: wrap;
}

.btn-primary {
  background: var(--accent);
  color: var(--bg-primary);
  border: none;
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  font-size: 0.8rem;
  font-weight: 500;
  cursor: pointer;
}

.btn-secondary {
  background: transparent;
  color: var(--text-secondary);
  border: 1px solid var(--border);
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  font-size: 0.8rem;
  cursor: pointer;
}

.feedback {
  background: var(--bg-tertiary);
  border: 1px solid var(--border);
  padding: 1.5rem;
  margin-top: 1.5rem;
  display: none;
}

.feedback.visible {
  display: block;
}

.score {
  font-size: 1.5rem;
  font-weight: 600;
}

.score.good { color: var(--success); }
.score.medium { color: var(--accent); }
.score.poor { color: var(--error); }
```

---

### Selectable Principle Cards (Level 2)

```html
<div class="principle-grid">
  <div class="principle-option selected" data-id="active-voice">
    <div class="principle-checkbox"></div>
    <div class="principle-content">
      <div class="principle-name">Active Over Passive</div>
      <div class="principle-desc">Prefer active voice</div>
    </div>
  </div>
  <div class="principle-option" data-id="nominalization">
    <div class="principle-checkbox"></div>
    <div class="principle-content">
      <div class="principle-name">Verbs Over Nominalizations</div>
      <div class="principle-desc">Use verbs instead of noun forms</div>
    </div>
  </div>
  <!-- more options... -->
</div>
```

```css
.principle-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.principle-option {
  background: var(--bg-tertiary);
  border: 1px solid var(--border);
  padding: 0.875rem 1rem;
  cursor: pointer;
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  transition: all 0.15s ease;
}

.principle-option:hover {
  border-color: var(--text-muted);
}

.principle-option.selected {
  border-color: var(--accent);
  background: rgba(240, 192, 64, 0.05);
}

.principle-option.correct {
  border-color: var(--success);
  background: rgba(64, 192, 128, 0.1);
}

.principle-option.incorrect {
  border-color: var(--error);
  background: rgba(224, 80, 80, 0.1);
}

.principle-checkbox {
  width: 16px;
  height: 16px;
  border: 1px solid var(--text-muted);
  border-radius: 2px;
  flex-shrink: 0;
}

.principle-option.selected .principle-checkbox {
  border-color: var(--accent);
  background: var(--accent);
}

.principle-option.selected .principle-checkbox::after {
  content: '✓';
  color: var(--bg-primary);
  font-size: 0.7rem;
  display: flex;
  justify-content: center;
}

.principle-name {
  font-size: 0.85rem;
  font-weight: 500;
}

.principle-desc {
  font-size: 0.75rem;
  color: var(--text-muted);
}
```

---

### Draggable Cards (Level 3)

```html
<div class="sortable-container" id="l3-sortable">
  <div class="sortable-card" draggable="true" data-id="a">
    <span class="card-number">1.</span>
    Executive Summary: Database outage affected 2,400 users for 47 minutes.
  </div>
  <div class="sortable-card" draggable="true" data-id="b">
    <span class="card-number">2.</span>
    Timeline: 14:23 - Alert triggered. 14:31 - Team engaged.
  </div>
  <!-- more cards... -->
</div>
```

```css
.sortable-card {
  background: var(--bg-tertiary);
  border: 1px solid var(--border);
  padding: 1rem 1.25rem;
  margin-bottom: 0.5rem;
  cursor: grab;
  font-size: 0.85rem;
  transition: all 0.15s ease;
}

.sortable-card:hover {
  border-color: var(--text-muted);
}

.sortable-card.dragging {
  opacity: 0.5;
  border-color: var(--accent);
}

.sortable-card .card-number {
  display: inline-block;
  width: 1.5rem;
  color: var(--text-muted);
  font-size: 0.75rem;
}
```

```javascript
// Drag and drop logic
let draggedElement = null;

function handleDragStart(e) {
  draggedElement = this;
  this.classList.add('dragging');
}

function handleDragEnd(e) {
  this.classList.remove('dragging');
  draggedElement = null;
  updateCardNumbers();
}

function handleDragOver(e) {
  e.preventDefault();
  const container = document.getElementById('l3-sortable');
  const afterElement = getDragAfterElement(container, e.clientY);
  if (afterElement == null) {
    container.appendChild(draggedElement);
  } else {
    container.insertBefore(draggedElement, afterElement);
  }
}

function getDragAfterElement(container, y) {
  const draggables = [...container.querySelectorAll('.sortable-card:not(.dragging)')];
  return draggables.reduce((closest, child) => {
    const box = child.getBoundingClientRect();
    const offset = y - box.top - box.height / 2;
    if (offset < 0 && offset > closest.offset) {
      return { offset, element: child };
    }
    return closest;
  }, { offset: Number.NEGATIVE_INFINITY }).element;
}

function updateCardNumbers() {
  const cards = document.querySelectorAll('.sortable-card');
  cards.forEach((card, i) => {
    card.querySelector('.card-number').textContent = `${i + 1}.`;
  });
}
```

---

### Document Type Cards (Level 4 Learn)

```html
<div class="doc-type-card">
  <div class="doc-type-header">
    <div class="doc-type-name">Incident Report</div>
    <div class="doc-type-when">After something broke</div>
  </div>
  <div class="doc-type-purpose">
    Explains what happened, why, and how to prevent recurrence.
    For both leadership (summary/impact) and engineers (root cause/fixes).
  </div>
  <div class="doc-type-structure">
    <div class="doc-type-structure-label">Standard Structure</div>
    <div class="doc-type-sections">
      <strong>Summary</strong> → <strong>Impact</strong> → <strong>Timeline</strong> →
      <strong>Root Cause</strong> → <strong>Remediation</strong> → <strong>Prevention</strong>
    </div>
  </div>
</div>
```

---

### Template Selection Grid (Level 4 Practice)

```html
<div class="template-grid">
  <div class="template-option selected" data-id="incident">
    <div class="template-name">Incident Report</div>
    <div class="template-desc">Summary → Impact → Timeline → Root Cause → Remediation</div>
  </div>
  <div class="template-option" data-id="proposal">
    <div class="template-name">Technical Proposal</div>
    <div class="template-desc">Problem → Solution → Cost/Benefit → Implementation</div>
  </div>
  <!-- more options... -->
</div>
```

```css
.template-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.template-option {
  background: var(--bg-tertiary);
  border: 1px solid var(--border);
  padding: 1.25rem;
  cursor: pointer;
  transition: all 0.15s ease;
}

.template-option:hover {
  border-color: var(--text-muted);
}

.template-option.selected {
  border-color: var(--accent);
  background: rgba(240, 192, 64, 0.05);
}

.template-name {
  font-size: 0.85rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.template-desc {
  font-size: 0.75rem;
  color: var(--text-muted);
}
```

---

## API Integration Example

```javascript
async function scoreRevision(original, revision, ideal, tips) {
  const btn = document.getElementById('l1-submit');
  btn.disabled = true;
  btn.textContent = 'Analyzing...';

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{
          role: 'user',
          content: `You are a technical writing instructor. Score this revision 1-10.

ORIGINAL: "${original}"
STUDENT REVISION: "${revision}"
IDEAL (reference): "${ideal}"

KEY ISSUES: ${tips.join('; ')}

Respond in JSON:
{
  "score": <number 1-10>,
  "feedback": "<2-3 sentences: what worked, what could improve>"
}

Score 7+ = solid. 10 = as good or better than ideal.`
        }]
      })
    });

    const data = await response.json();
    const result = JSON.parse(data.content[0].text);
    showFeedback(result.score, result.feedback);
  } catch (e) {
    // Fallback: simple heuristic scoring
    const reduction = (original.length - revision.length) / original.length;
    let score = 5;
    if (reduction > 0.3) score += 2;
    if (reduction > 0.5) score += 1;
    if (!revision.toLowerCase().includes('was ')) score += 1;
    showFeedback(
      Math.min(10, score), 
      `Reduced by ${Math.round(reduction * 100)}%. Compare with ideal: "${ideal}"`
    );
  }

  btn.disabled = false;
  btn.textContent = 'Check Revision';
}
```

---

## Data Structure Examples

### Level 1 Sentences

```javascript
const level1Sentences = [
  {
    original: "It was decided by the committee that the implementation of the new system should be postponed until such time as additional resources become available.",
    ideal: "The committee postponed the new system until more resources are available.",
    tips: ["Passive voice", "Wordy: 'until such time as'", "Nominalization: 'implementation'"]
  },
  // ... 7-9 more
];
```

### Writing Principles

```javascript
const writingPrinciples = [
  { id: 'old-new', name: 'Old Before New', desc: 'Put familiar information before new information' },
  { id: 'subject-verb', name: 'Subject-Verb Proximity', desc: 'Keep subjects and verbs close together' },
  { id: 'nominalization', name: 'Verbs Over Nominalizations', desc: 'Use verbs instead of noun forms' },
  { id: 'stress-position', name: 'Stress Position', desc: 'Put emphasis-worthy content at sentence end' },
  { id: 'active-voice', name: 'Active Over Passive', desc: 'Prefer active voice' },
  { id: 'positive-form', name: 'Positive Form', desc: "State what is, not what isn't" },
  { id: 'parallel', name: 'Parallel Construction', desc: 'Use consistent structure for parallel ideas' },
  { id: 'concrete', name: 'Concrete Over Abstract', desc: 'Prefer specific, tangible language' }
];
```

### Level 2 Exercises

```javascript
const level2Exercises = [
  {
    sentence: "The decision was made by management to implement the changes.",
    violations: ['active-voice', 'nominalization'],
    correction: "Management decided to implement the changes.",
    explanation: "Passive voice hides the actor. 'Made the decision' is a nominalization."
  },
  // ... 11-14 more
];
```

### Level 3 Exercises

```javascript
const level3Exercises = [
  {
    title: "Incident Report",
    sections: [
      { id: 'a', text: "Executive Summary: Database outage affected 2,400 users for 47 minutes." },
      { id: 'b', text: "Timeline: 14:23 - Alert. 14:31 - Team engaged. 15:10 - Restored." },
      { id: 'c', text: "Root Cause: Connection pool exhaustion from timeout misconfiguration." },
      { id: 'd', text: "Impact: Dashboard unavailable. No data loss. 12 support tickets." },
      { id: 'e', text: "Remediation: Timeout increased. Monitoring threshold lowered." },
      { id: 'f', text: "Prevention: Quarterly audits. Load testing before config changes." }
    ],
    validOrders: [
      ['a', 'd', 'b', 'c', 'e', 'f'],
      ['a', 'b', 'd', 'c', 'e', 'f']
    ],
    explanation: "Summary first, then impact/timeline, then root cause, then fixes."
  },
  // ... 2-3 more
];
```

### Level 4 Scenarios

```javascript
const level4Scenarios = [
  {
    scenario: "Your deployment broke production at 3 AM. Service down for 2 hours. Leadership wants to know what happened and how to prevent recurrence.",
    options: [
      { id: 'incident', name: 'Incident Report', desc: 'Summary → Impact → Timeline → Root Cause → Remediation' },
      { id: 'proposal', name: 'Technical Proposal', desc: 'Problem → Solution → Cost/Benefit → Plan' },
      { id: 'status', name: 'Status Update', desc: 'Progress → Blockers → Next Steps' },
      { id: 'design', name: 'Design Document', desc: 'Requirements → Architecture → Details' }
    ],
    correct: 'incident',
    explanation: "Incident reports are purpose-built for post-mortems."
  },
  // ... 5-7 more
];
```

---

## Build Order Suggestion

1. HTML structure with all sections (learn/practice for each level)
2. CSS styling (can largely copy from examples above)
3. Level navigation and mode toggle JS
4. Level 1 practice functionality (textarea + API scoring)
5. Level 1 learn content (populate the teaching cards)
6. Level 2 practice (checkbox selection + scoring logic)
7. Level 2 learn content
8. Level 3 practice (drag-drop)
9. Level 3 learn content
10. Level 4 practice (single-select grid)
11. Level 4 learn content
12. Polish: loading states, error handling, mobile responsiveness
