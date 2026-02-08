MULTI-AGENT ORCHESTRATION
Agent Guidelines
Your Fitness Buddy — Claude Code Development
Quick Reference for Session Management, Agent Boundaries & Handoff Protocol
February 2026 | Companion to PRD v2.0 + TechGuide v2.0
1. THE 7 GOLDEN RULES
These rules are inviolable. Breaking any one causes cascading problems across the project.
ONE ROLE PER SESSION. Every Claude Code session has exactly one agent role. Declare it at session start. Never switch mid-session.
READ CLAUDE.md FIRST. Every session starts by reading the repo's CLAUDE.md file. This is the agent's instruction manual.
STAY IN YOUR LANE. Agents only modify files they own. Frontend never writes SQL. Backend never touches React. AI Agent never writes code.
COMMIT WITH CONTRACTS. When creating something another agent consumes (API endpoint, DB table, output schema), document the contract in the commit message.
END WITH A HANDOFF. Every session ends by appending to SESSION_LOGS.md. The next agent reads this for context.
SEQUENTIAL BY DEFAULT. For MVP, run sessions one at a time. Only go parallel when features are independent and in separate repos.
NEVER HARDCODE SECRETS. All API keys in env vars. All AI calls through Edge Functions. Never expose secrets to frontend.
2. AGENT QUICK REFERENCE CARDS
2.1 Frontend Agent
2.2 Backend Agent
2.3 AI Agent
2.4 Integration Agent
2.5 Full-Stack Agent
2.6 DevOps Agent
3. SESSION LIFECYCLE
3.1 Starting a Session
Copy this template every time:
You are the [ROLE] Agent for Your Fitness Buddy. Read CLAUDE.md.
Context from previous session ([DATE], [ROLE]):
- Completed: [what was built, files modified]
- API contracts: [endpoints/schemas created]
- Known issues: [bugs, workarounds, incomplete work]
Task: [specific, scoped task for this session]
If this is the first session on a repo, skip the context block and just declare the role + task.
3.2 During a Session
Work ONLY within your file ownership scope.
Commit frequently with descriptive messages.
If creating an API endpoint or component interface, document the contract in the commit message.
If you need something from another agent's domain, note it as a blocker in your handoff — do NOT cross boundaries.
If you discover a bug in another agent's code, document it in SESSION_LOGS.md — do NOT fix it yourself.
3.3 Ending a Session (MANDATORY)
Append this to SESSION_LOGS.md before closing:
## Session [N]: [DATE] - [AGENT ROLE]
Duration: [X]h | Commits: [hashes] | Branch: main
### Completed
- [What was built/fixed, files created/modified]
### Interface Contracts
- [METHOD] /path — Request: { schema } → Response: { schema }
- Component: Name — Props: { interface }
- Table: name — Columns: [list], RLS: [policy summary]
### Known Issues
- [Bugs found, workarounds, tech debt created]
### Next Session
- Agent: [recommended role]
- Strategy: Sequential after this / Can parallel with [X]
- Tasks: 1) [task] 2) [task] 3) [task]
### Handoff Notes
- [Gotchas, why decisions were made, what next agent needs to know]
4. CONTRACT-FIRST DEVELOPMENT
Agents never communicate directly. They communicate through contracts documented in git commits and SESSION_LOGS.md.
4.1 API Contract Template (Backend → Frontend)
Every new endpoint commit MUST include:
feat: add plan generation API endpoint
Contract:
POST /functions/v1/generate-plan
Headers: Authorization: Bearer <user_jwt>
Body: {
  quiz_profile: {
    user_id: string,
    goals: string[],
    injuries: string[],
    equipment: string[],
    experience_level: string
  }
}
Response 200: { plan_id: string, status: 'generating' | 'complete', estimated_time_seconds: number }
Response 400: { error: 'Invalid quiz profile', details: string }
Response 401: { error: 'Unauthorized' }
Response 500: { error: 'AI generation failed' }
4.2 Schema Contract Template (AI → Backend)
Output schemas define the EXACT JSON structure Claude API must return:
// output-schema.json
{
  "plan_name": "string",
  "phases": [{
    "phase_number": "number",
    "name": "string",
    "weeks": "number",
    "sessions": [{
      "session_type": "A | B | C",
      "exercises": [{ "name": "string", "sets": "number", ... }]
    }]
  }]
}
Backend Edge Functions parse Claude API responses against these schemas with Zod. If the response doesn't match, the function retries or returns an error.
4.3 Type Sync Protocol
When a shared type changes, propagate in this order:
Frontend Agent updates TypeScript interface in yfb-frontend/src/types/.
Backend Agent updates equivalent Zod schema in the relevant Edge Function.
AI Agent updates output-schema.json in yfb-ai-prompts/ (if applicable).
All three agents document the change in their SESSION_LOGS.md.
5. SESSION STRATEGY DECISION TREE
Use this to decide your approach for each new feature:
Q1: Does this feature touch multiple layers (UI + API + DB)?
YES and interfaces are well-defined → Sequential sessions (can parallel if experienced)
YES and interfaces are NOT defined → Sequential sessions (define contracts first)
NO → Single agent, single session
Q2: Does this feature depend on incomplete work from another agent?
YES → Wait for dependency to be committed, then start your session with context from their handoff
NO → Start immediately
Q3: How complex is this feature?
HIGH (8+ hours) → Break into 2-3 sequential sessions with the same agent role
MEDIUM (4-8 hours) → Single long session or two short ones
LOW (under 4 hours) → Single session
Q4: Is this debugging or building new?
DEBUGGING → Single focused session with the same agent role that built the feature
BUILDING NEW → Follow complexity guidelines above
6. DANGEROUS PATTERNS TO AVOID
7. RECOMMENDED DAILY WORKFLOW
For a 6-8 hour solo dev day:
Morning (2-3 hours): Start with Backend Agent session. Build data layer + API endpoints. Commit with contracts.
Mid-day (1 hour): AI Agent session if needed. Write/refine prompts for the feature being built. Commit.
Afternoon (2-3 hours): Frontend Agent session. Build UI consuming the API contracts from the morning. Commit.
End of day (30 min): Review all SESSION_LOGS.md entries. Plan tomorrow's sessions.
Alternative: Single feature deep-dive (4-6 hours)
For complex features, spend the full day on one agent role. Break into 2-3 sessions with commits between them. This gives deeper context but slower cross-layer progress.
Weekly integration check:
Every Friday, run a Full-Stack Agent session to verify all layers work together. Fix any contract mismatches. Run the full test suite.
8. FILE OWNERSHIP QUICK-LOOK TABLE
