# Example Output: Conglomerate Trading Feature

This example shows what the skill produces for a board game trading feature — a real-world use case with game state management, real-time sync, UI interactions, and testing.

## Input Context (from brainstorming)

User brainstormed a trading/negotiation feature for a board game called Conglomerate. Players can propose trades of assets (companies, resources, influence), counter-offer, accept, or reject. Trades execute atomically — both sides swap simultaneously. Real-time updates so both players see trade status changes live.

Tech stack: vanilla JS, Firebase Firestore, Vercel deployment.

---

## Generated /speckit.specify Output

```
/speckit.specify

Conglomerate — Player Trading System

**User Need:**
Players need to negotiate and exchange assets during gameplay to pursue different
strategies. Currently players can only acquire assets through game mechanics (auctions,
events). Trading adds a social negotiation layer that makes the game more dynamic
and strategic.

**Core Functionality:**
1. Players can propose a trade to any other player, selecting assets to offer and request
2. The receiving player can accept, reject, or counter-offer with modified terms
3. Accepted trades execute atomically — both players' inventories update simultaneously
4. All players see real-time trade activity (who's trading, when trades complete)
5. Trade history is recorded for the current game session

**User Flows:**
- Primary: Player A opens trade dialog → selects Player B → picks assets to offer/request → sends proposal → Player B receives notification → reviews terms → accepts → both inventories update → trade logged
- Counter-offer: Player B modifies terms → sends counter → Player A reviews → accepts/rejects/counters again (max 3 rounds)
- Cancellation: Either player can cancel a pending trade before acceptance

**Success Criteria:**
- Trade proposals appear for the other player within 2 seconds
- Accepted trades update both inventories atomically (no partial trades)
- Concurrent trade conflicts are handled (Player B can't accept two trades for the same asset)
- Trade history shows all completed and rejected trades for the session
- Works on mobile and desktop

**Scope:**
In scope: 1-to-1 trades, counter-offers, real-time notifications, trade history, conflict prevention
Out of scope: Multi-party trades (3+ players), automated trade matching, trade templates/presets, cross-game trading

**Assumptions:**
- Players are authenticated via existing Firebase Auth
- Asset data model already exists in Firestore (companies, resources, influence)
- Game state management already handles turn structure
- Maximum 3 counter-offer rounds before trade auto-cancels

---

## Agent Teams Implementation Structure

### Teammate Definitions

**Teammate 1 — Trade Engine**
- **Owns:** src/game/trading/engine/
- **Responsibility:** Core trade logic — state machine (proposed → countered → accepted → executed → rejected), validation rules (player owns offered assets, assets not locked in another trade), trade execution (atomic swap), conflict detection
- **Depends on:** Nothing — this is pure game logic with no external dependencies
- **Wave:** 1

**Teammate 2 — Trade Sync Layer**
- **Owns:** src/game/trading/sync/
- **Responsibility:** Firebase integration — Firestore document structure for trades, real-time listeners for trade status changes, optimistic locking for concurrent trade prevention, transaction batching for atomic execution
- **Depends on:** Teammate 1 (Trade Engine) completing interface contracts for trade state machine and validation functions
- **Wave:** 2

**Teammate 3 — Trade UI**
- **Owns:** src/game/trading/ui/
- **Responsibility:** Trade proposal dialog, counter-offer interface, incoming trade notifications, trade status indicators, trade history panel, asset picker component
- **Depends on:** Teammate 1 (Trade Engine) completing interface contracts for trade data shapes and status enums
- **Wave:** 2

**Teammate 4 — Trade Tests**
- **Owns:** tests/trading/
- **Responsibility:** Unit tests for trade validation logic, integration tests for multi-step trade flows, edge case tests (disconnect mid-trade, concurrent conflicting trades, max counter-offer rounds), state consistency verification after trade execution
- **Depends on:** Teammate 1 (Trade Engine) completing core interfaces; can start writing test shells immediately
- **Wave:** 2

### Dependency Waves

**Wave 1 (spawn first):**
- Teammate 1 (Trade Engine): Produces the core interfaces, data shapes, and validation functions that all other teammates code against. Must complete and message other teammates when interfaces are stable.

**Wave 2 (spawn after Wave 1 completes):**
- Teammates 2, 3, 4 work in parallel:
  - Sync Layer codes against Trade Engine's validation and execution interfaces
  - Trade UI codes against Trade Engine's data shapes and status enums
  - Trade Tests writes test cases against Trade Engine's public API

**Wave 3 — Integration:**
- Lead agent wires Sync Layer ↔ Trade Engine ↔ Trade UI together
- Runs full integration tests
- Verifies real-time updates work end-to-end

### Interface Contracts

**Contract: Trade State Machine**
```
TradeStatus = "proposed" | "countered" | "accepted" | "rejected" | "executed" | "cancelled" | "expired"

createTradeOffer(offer: TradeOffer): { tradeId: string, status: TradeStatus }
validateTradeOffer(offer: TradeOffer): { valid: boolean, errors: string[] }
submitCounterOffer(tradeId: string, counter: CounterOffer): { status: TradeStatus }
acceptTrade(tradeId: string, playerId: string): { success: boolean, newState: GameState }
rejectTrade(tradeId: string, playerId: string): { status: TradeStatus }
cancelTrade(tradeId: string, playerId: string): { status: TradeStatus }
```

**Contract: Trade Data Shapes**
```
TradeOffer = {
  fromPlayerId: string,
  toPlayerId: string,
  offering: Asset[],
  requesting: Asset[],
  message?: string,          // optional note to other player
  counterRound: number       // 0 for initial, increments with counters, max 3
}

Asset = {
  type: "company" | "resource" | "influence",
  id: string,
  name: string,
  value: number              // for display purposes
}

TradeRecord = {
  tradeId: string,
  status: TradeStatus,
  fromPlayer: { id: string, name: string },
  toPlayer: { id: string, name: string },
  currentOffer: TradeOffer,
  history: TradeOffer[],     // all previous offers/counters
  createdAt: timestamp,
  updatedAt: timestamp,
  resolvedAt?: timestamp
}
```

**Contract: Firestore Trade Documents**
```
Collection: games/{gameId}/trades/{tradeId}
- Maps directly to TradeRecord shape above
- Use Firestore transactions for atomic execution
- Index on: status + updatedAt (for active trade queries)
- Index on: fromPlayerId, toPlayerId (for player-specific queries)
```

**Contract: Trade Events (for UI updates)**
```
Events emitted by Sync Layer, consumed by Trade UI:
- "trade:received"  — payload: TradeRecord (new trade proposed to this player)
- "trade:updated"   — payload: TradeRecord (status changed on an existing trade)
- "trade:executed"   — payload: { tradeId, updatedAssets: Asset[] } (trade completed, refresh inventory)
```

### Spawn Prompt Blueprints

**Teammate 1 — Trade Engine:**
"You are implementing the core trade engine for the Conglomerate board game. Your files are in src/game/trading/engine/. Do NOT modify files outside this directory.

Your responsibilities:
1. Implement the trade state machine (proposed → countered → accepted → executed flow)
2. Write validation functions (player owns assets, assets not locked, counter-round limits)
3. Implement trade execution logic (atomic swap of assets between players)
4. Export all public interfaces matching the Trade State Machine and Trade Data Shapes contracts in the spec

Follow the interface contracts exactly — other teammates will code against your exports.

Acceptance criteria:
- All TradeStatus transitions are valid (no skipping states)
- Validation catches: trading assets you don't own, assets locked in another trade, exceeding 3 counter-rounds
- Trade execution is atomic (both sides update or neither does)
- All functions match the contract signatures exactly

When complete: Mark tasks done. Message Sync Layer, Trade UI, and Trade Tests teammates that interfaces are ready."

**Teammate 2 — Trade Sync Layer:**
"You are implementing Firebase sync for the Conglomerate trading system. Your files are in src/game/trading/sync/. Do NOT modify files outside this directory.

Your responsibilities:
1. Create Firestore document structure matching the Trade Documents contract
2. Implement real-time listeners for trade status changes
3. Use Firestore transactions for atomic trade execution
4. Implement optimistic locking to prevent concurrent conflicting trades
5. Emit Trade Events for the UI layer to consume

Dependencies: Trade Engine interfaces must be complete before you begin (Wave 2).

Follow the Firestore Trade Documents and Trade Events contracts exactly.

Acceptance criteria:
- Trade documents match the contract schema
- Real-time listeners fire within 2 seconds of status change
- Concurrent trades for the same asset are prevented
- Trade execution uses Firestore transactions (no partial updates)

When complete: Mark tasks done. Message Lead that sync layer is ready for integration."

**Teammate 3 — Trade UI:**
"You are implementing the trading user interface for the Conglomerate board game. Your files are in src/game/trading/ui/. Do NOT modify files outside this directory.

Your responsibilities:
1. Trade proposal dialog (select player, pick assets to offer/request, send)
2. Incoming trade notification component
3. Counter-offer interface (modify terms, send counter)
4. Trade status indicators (pending, accepted, etc.)
5. Trade history panel (completed and rejected trades)
6. Asset picker component (reusable for offer and request sides)

Dependencies: Trade Engine data shapes must be complete before you begin (Wave 2).

Follow the Trade Data Shapes and Trade Events contracts for all data structures.

Acceptance criteria:
- Trade dialog shows only assets the player actually owns
- Counter-offer UI pre-fills current terms for modification
- Status updates appear in real-time (driven by Trade Events)
- Works on mobile (responsive) and desktop
- Asset picker supports all asset types (company, resource, influence)

When complete: Mark tasks done. Message Lead that UI is ready for integration."

**Teammate 4 — Trade Tests:**
"You are writing tests for the Conglomerate trading system. Your files are in tests/trading/. Do NOT modify files outside this directory.

Your responsibilities:
1. Unit tests for trade validation (valid offers, invalid offers, edge cases)
2. State machine tests (all valid transitions, invalid transition attempts)
3. Integration test shells for multi-step flows (propose → counter → accept → execute)
4. Edge case tests: disconnect mid-trade, concurrent conflicting trades, max counter-rounds reached, trading last asset
5. State consistency tests: verify game state is correct after trade execution

Dependencies: Trade Engine interfaces should be complete before writing detailed tests, but you can start writing test shells and edge case definitions immediately.

Acceptance criteria:
- Every validation rule has at least one positive and one negative test
- Every state transition is tested
- Edge cases cover: concurrent conflicts, disconnection, counter-round limits
- Integration tests verify end-to-end trade flow

When complete: Mark tasks done. Message Lead with test coverage summary."

---

## Execution Directive

After processing this specification, follow these steps:

**Planning constraint:** When generating the plan via /speckit.plan, use the
file structure and directory ownership defined in the Teammate Definitions above.
Do not reorganize files into a different structure — the teammate assignments
depend on these exact directory boundaries. If the plan suggests a different
architecture, reconcile it with the teammate ownership map before proceeding.

**Execution steps — run automatically after /speckit.plan and /speckit.tasks:**

1. Enable delegate mode — coordinate only, do not implement tasks yourself
2. Create an agent team based on the Teammate Definitions above
3. Spawn Teammate 1 (Trade Engine) using their Spawn Prompt Blueprint — this is Wave 1
4. Wait for Wave 1 to complete and confirm interfaces are ready
5. Spawn Teammates 2, 3, and 4 simultaneously using their Spawn Prompt Blueprints — this is Wave 2
6. Assign each teammate ONLY the files/directories listed in their "Owns" field
7. Monitor teammate progress and redirect if any teammate drifts from scope
8. After all teammates complete, run Wave 3 integration: wire Sync Layer ↔ Trade Engine ↔ Trade UI together, run full integration tests, verify real-time updates end-to-end
9. Run a final review against the Success Criteria before marking complete
```

---

## Notes on This Example

This example demonstrates several key patterns:

1. **Wave 1 is small and focused** — only the Trade Engine, which produces interfaces others need
2. **Wave 2 teammates are truly independent** — Sync, UI, and Tests all code against the Engine's contracts but don't depend on each other
3. **Interface contracts are specific** — exact function signatures, data shapes, and event names, not vague descriptions
4. **Spawn prompts include everything** — a teammate reading only their spawn prompt knows exactly what to build, where to put it, and how to know when they're done
5. **File ownership is non-overlapping** — each teammate has their own subdirectory under src/game/trading/
