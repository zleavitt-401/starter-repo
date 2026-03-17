# Specify Prompt Guide

The /specify command creates a feature specification that defines WHAT to build and WHY, without specifying HOW.

## Core Principles

### Focus on WHAT & WHY (Not HOW)
- ✅ "Users need real-time updates of their data"
- ❌ "Implement using WebSockets with Socket.io"

The specification should remain stable even if implementation technologies change.

### Be Concrete and Testable
Every requirement should be specific enough to test. Avoid vague language:
- ❌ "The system should be fast"
- ✅ "Page load time under 2 seconds on 3G networks"

### Use User Stories Format
Structure around user value:
```
As a [user type]
I want to [action]
So that [benefit/value]
```

## Essential Components

### 1. Feature Overview
- What problem does this solve?
- Who benefits from this feature?
- What's the business value?

### 2. User Stories
- Clear actor, action, and outcome
- Each story should be independently testable
- Include acceptance criteria

### 3. Functional Requirements
- Numbered, testable requirements (FR-001, FR-002, etc.)
- Use MUST/SHOULD/MAY language
- Focus on behavior, not implementation

### 4. Success Criteria
- Measurable metrics
- User satisfaction indicators
- Business outcomes
- Performance targets

### 5. Scope Boundaries
**Explicitly state what's IN and OUT of scope:**
- In scope: "Users can create, edit, and delete items"
- Out of scope: "Bulk import/export (future phase)"

### 6. Assumptions
Document reasonable defaults rather than leaving everything vague:
- "Authentication uses email/password (standard approach)"
- "Data retained for 90 days (industry standard)"

## Quality Checklist

A good specification should:
- [ ] Focus on user needs (WHAT), not implementation (HOW)
- [ ] Be testable and unambiguous
- [ ] Include concrete acceptance criteria
- [ ] Define clear scope boundaries
- [ ] Document assumptions made
- [ ] Avoid speculative "nice to have" features
- [ ] Trace every feature to a user story

## Clarification Strategy

Limit [NEEDS CLARIFICATION] markers to maximum 3. Only use for:
- Critical scope decisions
- Security/privacy requirements
- Multiple valid interpretations with different implications

For everything else, make informed assumptions and document them.

## Example Specify Prompt Structure

```
I want to build [feature name].

**User Need:**
[What problem this solves and why users need it]

**Core Functionality:**
1. [Key capability 1]
2. [Key capability 2]
3. [Key capability 3]

**User Flows:**
- [Primary user journey]
- [Secondary user journey]

**Success Looks Like:**
- [Measurable outcome 1]
- [Measurable outcome 2]

**Constraints:**
- [Any known limitations or requirements]

**Out of Scope:**
- [What this feature won't do]
```

## Common Pitfalls to Avoid

1. **Too implementation-focused** - Don't specify tech stack, APIs, or database schemas
2. **Vague requirements** - "User-friendly interface" isn't testable
3. **Missing acceptance criteria** - How do you know when it's done?
4. **Scope creep** - Every feature must trace to a user story
5. **Underspecified** - Avoid excessive [NEEDS CLARIFICATION] markers; make informed assumptions
