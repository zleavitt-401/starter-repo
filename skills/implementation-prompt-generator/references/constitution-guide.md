# Constitution Prompt Guide

The constitution defines non-negotiable principles for your project. It establishes the foundation before any specification work begins.

## Key Elements for Strong Constitutions

### Tech Stack & Architecture
- Specify exact technologies (e.g., "vanilla JavaScript with ES6+ modules")
- Define deployment targets (e.g., "Vercel for hosting, Firebase for backend")
- State architectural patterns (e.g., "single-page architecture", "CDN-based dependencies")
- Clarify build requirements (e.g., "zero-build workflow" vs "Webpack/Vite")

### Code Quality & Style
- Testing approach (e.g., "test-driven development", "integration tests required")
- Code organization patterns (e.g., "feature-based folder structure")
- Naming conventions
- Documentation standards

### Project Constraints
- Browser support requirements
- Performance targets
- Accessibility standards (WCAG level)
- Security requirements

### Development Workflow
- Version control practices
- Branching strategy
- Code review requirements
- Deployment process

## What Makes an Effective Constitution

**DO:**
- Be specific and prescriptive
- Focus on what's truly non-negotiable
- Include rationale for key decisions
- Align with organizational/team standards

**DON'T:**
- Include feature-specific details (those go in specs)
- Make it too restrictive (balance guidance with flexibility)
- Duplicate what's in the specification templates
- Include implementation details for specific features

## Example Constitution Elements

### For a lightweight web app:
```
- Use vanilla JavaScript with ES6+ modules (no build step)
- All dependencies loaded via CDN (unpkg or cdnjs)
- Deploy to Vercel with automatic previews
- Firebase Firestore for database
- Progressive enhancement approach
- Mobile-first responsive design
```

### For quality standards:
```
- Every user-facing feature must have error handling
- All forms must validate input client-side
- Loading states required for async operations
- Accessibility: minimum WCAG 2.1 AA compliance
```
