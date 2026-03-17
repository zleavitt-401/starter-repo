# Agent Teams Additions to Spec Kit Prompts

This reference covers what Agent Teams specs need beyond standard Spec Kit output. These additions ensure multiple Claude Code instances can work in parallel without conflicts.

## Why Standard Specs Aren't Enough

A standard `/speckit.specify` output assumes one agent reads the spec, plans tasks, and implements them sequentially. The context carries forward naturally in a single conversation.

Agent Teams breaks this assumption because each teammate starts with zero conversation history. Everything the teammate needs must be in the spec, the CLAUDE.md, or the spawn prompt. The additions below bridge this gap.

## Addition 1: Teammate Definitions

Each teammate needs a clear role with explicit file ownership.

**Required fields per teammate:**
- **Name/Role** — descriptive label (e.g., "Trade State Machine", not "Worker 1")
- **Owns** — exact directory paths this teammate can modify
- **Responsibility** — 1-2 sentences on what they build
- **Depends on** — which other teammates must finish first (or "None")
- **Wave** — which spawn wave they belong to (1, 2, or 3)

**Sizing guidance:**
- Each teammate should have 5-6 tasks worth of work
- If a teammate has fewer than 3 tasks, merge them with another
- If more than 8 tasks, split into two teammates

## Addition 2: Dependency Waves

Waves determine spawn order. Getting this wrong means teammates wait idle or code against interfaces that don't exist yet.

**Wave 1 — Foundation:**
Work that other teammates depend on. Typically: data models, authentication, shared utilities, core business logic interfaces. Spawn these first, wait for completion.

**Wave 2 — Parallel Features:**
Independent feature work that builds on Wave 1 output. All Wave 2 teammates spawn simultaneously. This is where the parallelism payoff happens.

**Wave 3 — Integration (optional):**
Wiring modules together, running cross-module tests, fixing integration issues. Often handled by the lead agent rather than a dedicated teammate.

**Rules:**
- Wave 1 should be 1-2 teammates maximum (if foundation is large, you need a different decomposition)
- Wave 2 should be 2-4 teammates (the bulk of parallel work)
- Wave 3 is optional and usually the lead handles it
- A teammate in Wave 2 should NEVER depend on another Wave 2 teammate

## Addition 3: Interface Contracts

The most critical addition. When two teammates' code must interoperate, define the boundary explicitly in a **centralized Interface Contracts section** of the spec.

**CRITICAL: Contracts must be centralized, not scattered.** Every contract lives in one dedicated section of the spec. Spawn prompts reference contracts by name — they do NOT duplicate contract details. This ensures a single source of truth that the coordinator agent can reconcile against during integration.

**Each contract must include:**
- **Name** — descriptive (e.g., "Trade Validation API", not "Contract 1")
- **Produced by** — which teammate creates/exports this interface
- **Consumed by** — which teammates code against it
- **Ready signal** — how the producer notifies consumers it's done

**What to include in contract definitions:**

For function-based interfaces:
```
Contract: Trade Validation API
Produced by: Teammate 1 (Trade Engine)
Consumed by: Teammates 2 (Sync Layer), 3 (Trade UI)

- validateTradeOffer(offer: TradeOffer): { valid: boolean, errors: string[] }
- executeTradeSwap(tradeId: string): { success: boolean, newState: GameState }

TradeOffer shape:
{
  fromPlayerId: string,
  toPlayerId: string,
  offering: Asset[],
  requesting: Asset[],
  timestamp: number
}
```

For event/callback interfaces:
```
Contract: Chat-to-Trade Bridge
Produced by: Teammate 1 (Messaging)
Consumed by: Teammate 3 (Trade Builder UI)

- onOpenTrade(otherPlayerId: string): void
  Emitted when user clicks "Open Trade" in private chat.
  Trade Builder UI listens for this callback to open the trade modal.
```

For database/document interfaces:
```
Contract: Firestore Trade Documents
Produced by: Teammate 2 (Sync Layer)
Consumed by: Teammates 3 (Trade UI), 4 (Tests)

Collection: trades/{tradeId}
Fields:
  - status: "pending" | "countered" | "accepted" | "rejected" | "executed"
  - fromPlayer: string (user ID)
  - toPlayer: string (user ID)
  - offers: array of Asset objects
  - requests: array of Asset objects
  - createdAt: Firestore timestamp
  - updatedAt: Firestore timestamp
```

**Rules:**
- Every point where Teammate A's code calls Teammate B's code needs a contract
- Contracts live in the centralized Interface Contracts section — NOT in spawn prompts
- Spawn prompts say "Follow the [Contract Name] contract in the Interface Contracts section"
- Both producer and consumer must code against the contract exactly
- If a contract needs to change mid-implementation, it must go through the lead/coordinator
- The coordinator uses the centralized contracts as a checklist during integration

## Addition 4: Spawn Prompt Blueprints

Pre-written descriptions that become the initial prompt for each teammate when spawned.

**Effective spawn prompt structure:**
```
You are implementing [ROLE] for [PROJECT/FEATURE].

Your assigned files: [EXACT DIRECTORY PATHS]
Do NOT modify files outside these directories.

Your responsibilities:
1. [Specific task 1]
2. [Specific task 2]
3. [Specific task 3]

You PRODUCE these interface contracts (export exactly as defined in
the Interface Contracts section of the spec):
- [Contract name]

You CONSUME these interface contracts (follow exactly as defined in
the Interface Contracts section of the spec):
- [Contract name]

Dependencies:
- [What must exist before you start / "None — you are Wave 1"]

Acceptance criteria:
- [Specific, testable criterion 1]
- [Specific, testable criterion 2]

When complete:
- Mark tasks done
- Message [teammate names] that your interfaces are ready
```

**Key rules for spawn prompts:**
- Reference contracts by name — NEVER duplicate contract details in the prompt
- Say "as defined in the Interface Contracts section" to point the agent to the single source of truth
- Distinguish between PRODUCE (this agent creates the interface) and CONSUME (this agent codes against it)
- Specific directory paths (not "the frontend code")
- Clear "when complete" actions including who to notify
- Acceptance criteria that map to the spec's success criteria
- No assumption of prior conversation context — the agent starts cold

## Addition 5: CLAUDE.md Recommendations

The spec should include guidance for what to add to the project's CLAUDE.md, since all teammates load it automatically:

- Project architecture overview
- File/directory ownership map
- Interface contract locations (if stored as separate files)
- Coding conventions and patterns
- Reference to spec files by path
- "Do not modify files outside your assigned directories" as a global rule

## Checklist: Is the Spec Agent Teams-Ready?

- [ ] Every teammate has explicit, non-overlapping file ownership
- [ ] Dependency waves are defined (no circular dependencies)
- [ ] Soft foundations identified — any teammate whose types/interfaces are consumed by 2+ others is Wave 1
- [ ] If a Wave 1 teammate is also a large feature builder, split types from implementation
- [ ] Interface contracts are ALL in one centralized section (not scattered in spawn prompts)
- [ ] Every contract has Produced by / Consumed by / Ready signal metadata
- [ ] Spawn prompts reference contracts by name, never duplicate contract details
- [ ] Spawn prompts distinguish PRODUCE vs CONSUME for each contract
- [ ] Spawn prompts are complete enough for a cold-start agent
- [ ] Wave 2 teammates don't depend on each other
- [ ] No teammate has more than 8 or fewer than 3 tasks
- [ ] CLAUDE.md additions are specified
- [ ] Success criteria map to specific teammates' acceptance criteria
