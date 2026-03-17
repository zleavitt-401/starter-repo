# CC Quick Prompt Guide

Reference for generating direct Claude Code prompts (Path A). Use for simple-to-medium tasks that don't need Spec Kit's planning overhead.

## Tech Stack Defaults

Include these unless the user specifies otherwise:

**Frontend:** Vanilla JavaScript ES6+, React 18 via CDN (no JSX — use `React.createElement`), no bundlers/transpilers/build steps.

**Backend:** Firebase (Firestore for data, Auth for users, Storage for files). Cross-browser sync via Firebase real-time listeners.

**Deployment:** Vercel for hosting, automatic preview deployments per GitHub branch, production deploy from `main` branch.

**Development:** VS Code with Claude Code extension, Git workflow (feature branches → PR → merge).

## Zero-Build Constraints

When the user's project uses a zero-build philosophy, include:

```
- No npm build scripts (only npm install for dev dependencies if needed)
- No webpack, vite, or bundlers
- No TypeScript compilation (unless explicitly migrating to TS)
- No JSX transformation
- Load all libraries via CDN (unpkg, jsdelivr, cdnjs)
- Pure HTML/CSS/JS that runs directly in browser
```

## Security Context

For features involving user data or payments, add:

```
## Security Requirements
- Validate all user input client-side AND server-side
- Use Firebase Security Rules for data access control
- Never expose API keys in client-side code
- Sanitize user-generated content before display
- [Feature-specific security concerns]
```

## Common Integration Patterns

### Firebase Projects
```
- Use existing Firebase config (check firebase-config.js)
- Follow existing Firestore collection structure
- Implement offline persistence if user expects it
- Handle auth state changes properly
```

### UI Components
```
- Match existing visual style
- Use consistent spacing, colors, typography
- Mobile-first responsive design
- Accessibility: keyboard navigation, focus states, ARIA labels
```

### Chrome Extensions
```
- Manifest V3 requirements
- Content Security Policy restrictions
- Message passing between content scripts and background
- Storage API limits (sync storage: 100KB)
```

## Prompt Types and When to Use Full vs Simple

**Simple template** (just file + change + expected result):
- 1 file, obvious change, no ambiguity

**Full CC template** (Task + Context + Requirements + Tech Stack + Files + Success Criteria):
- Multiple approaches possible
- Claude needs architectural context
- Performance or security implications
- Touches 2-3 files but doesn't need Spec Kit's planning

**Upgrade to Spec Kit** (Path B) when:
- Claude would ask many clarifying questions
- Feature needs user stories and acceptance criteria
- Architecture decisions involved
- Multiple user flows to define

## Token Optimization

- Reference existing patterns instead of explaining them ("Use existing Firestore collection structure" vs explaining what Firestore is)
- Link to docs instead of pasting them
- Use bullet points over paragraphs
- Include only context relevant to this specific task
- Assume Claude knows common technologies — just specify how you're using them

## Example: Simple Template

```
Change button styling in CheckoutForm.js:
- Change submit button color from green (#4CAF50) to blue (#2196F3)
- Increase button padding from 10px to 12px

File: src/components/CheckoutForm.js

Expected result: Blue button with slightly more padding
```

## Example: Full CC Template

```
## Task
Add a voting system to Fauxbituaries where users can upvote their favorite obituaries.

## Context
Fauxbituaries generates random humorous obituaries with glassmorphism design.
Obituaries stored in Firestore with fields: id, text, character, timestamp, userId.

## Requirements
- Users can click an upvote button on each obituary
- Vote count displays next to upvote button
- Users can only vote once per obituary (tracked by userId)
- Votes persist in Firestore
- Sort obituaries by vote count (highest first)

## Tech Stack & Constraints
- No build tools — Vanilla JavaScript with CDN React
- Backend: Firebase Firestore for vote storage
- Deployment: Vercel

## File Structure
Modify: src/components/ObituaryCard.js, src/utils/firebase.js
Create: src/components/VoteButton.js

## Success Criteria
- [ ] Vote button visible on each obituary card
- [ ] Click increments vote count
- [ ] Second click shows "already voted" message
- [ ] Votes persist across page refreshes
- [ ] Obituaries sorted by vote count
- [ ] No console errors
```
