# AXIS PRAXIS — Agent Operating Rules

**Version:** Machine-optimized. Human narrative: `AXIS-PRAXIS.md`. Use `check_section()` for deep reference.
**Last updated:** 2026-03-25
**Override authority:** CEO only.

---

## ⚡ TIER 1 — NEVER FORGET (survives all compaction)

These rules are the most violated and most damaging when broken. If context is shrinking and you remember nothing else, remember these.

### CEO is the decision maker
- No product decisions without CEO approval (UX, features, flows, data changes, tradeoffs)
- No unsolicited code changes — diagnose and recommend, wait for "approved" or "make the change"
- No closing GitHub issues without CEO saying to
- Escalation/strong language from CEO = you went off track. Stop. Re-read. Recalibrate.

### Plan before code — always
- Written plan required before ANY code change: files touched, what it does, impact analysis, risks
- CEO approves plan before implementation begins. No "quick fix" exceptions.
- Blast radius: trace every caller of the function you're fixing. Check for fire-and-forget patterns.

### Build before commit — always
- `npm run build` (or `clode-build`) must pass before every commit
- `git status` clean check before push
- Monitor Vercel deploy until success confirmed
- Post-deploy smoke test before declaring done

### Never use CEO as QA
- Clode does ALL technical verification before saying "ready for UAT"
- QA = does it work (Clode/Quinn). UAT = does it match intent (CEO).
- Present evidence (screenshots, test output), not test steps for CEO to run
- CEO does NOT: run SQL, restart servers, debug in browser console, test on localhost

### DB writes require CEO review
- Show the exact SQL → get CEO thumbs up → then run it
- Applies to: CREATE/ALTER/DROP, INSERT/UPDATE/DELETE, cron.schedule, apply_migration
- SELECT queries: pre-authorized, no approval needed
- Supabase CLI is dead. All DB ops through Supabase MCP.

### One thing at a time
- Never ask CEO multiple questions in one message
- Complete one task before starting another

---

## ⚡ TIER 2 — CORE PROTOCOLS

### Code quality (non-negotiable)
- Ban `.catch(() => {})` — minimum floor is `.catch(console.error)`
- Check `res.ok` before using response data. Always.
- No fire-and-forget mutations — handle every failure
- All queries user-scoped to authenticated user
- No data hacks — fix the code, not the data (backfill only after code fix, with CEO approval)

### Diagnosis — evidence first
- §7.1: Restate action sequence → list ALL symptoms → analyze code → verify hypothesis explains EVERY symptom
- §7.3: Three failed attempts = STOP. Summarize. Escalate to Clai. No more code.
- §7.3b: Never assert runtime behavior from reading code. Run it. Observe output. Then propose fix.
- §7.7 Shainin's Red X: When same inputs produce different results by path → simulate failing path (Observation A) → simulate working path (Observation B) → diff A vs B → THEN read code. No code reading until you have both observations.

### Testing — verify, don't assume
- §5.4: Bug-to-test protocol — write failing test, fix bug, test passes, commit both
- §5.5b: Every fix needs runtime verification. "Build passes" is not a test. Run actual code, observe output, compare before/after.
- Post-fix checkpoint must include REGRESSION TESTS section with PASS/FAIL per test.
- §5.6: Check simulation skills before manual testing
- §5.7: Never use raw Playwright for screenshots — use screenshot skill
- §5.8: Before UI changes: before screenshot → confirm what needs changing → plan → implement → after screenshot → present both
- §5.9: E2E tests against production only (`BASE_URL=https://your-production-url.com`), never localhost
- §5.5: Test data cleanup in afterAll/afterEach — pass or fail

### Critical path protection
| Critical Path | Trigger Files | Required UAT |
|---|---|---|
| *Example: Onboarding* | *`OnboardingFlow.tsx`, `/api/onboarding/*`* | *Full onboarding (fresh user)* |
| *Example: Core workflow* | *`/api/core/*`, `MainClient.tsx`* | *End-to-end workflow test* |

- Define your own critical paths in your project's `CLAUDE.md`. Any commit touching a critical path trigger file requires full end-to-end UAT. Build passing is NOT sufficient.
- 3+ commits touching same flow in a week = treat combined diff as single review with mandatory E2E UAT

### Content search, not filename search
- §7.2: When checking "is function X called anywhere?" — search file CONTENTS. Read files, grep them.
- Declaring code "dead" or "never called" based on filename search is a hallucination.

---

## ⚡ TIER 3 — OPERATIONAL RULES

### Context exhaustion protocol
- At ~75% context: STOP new tasks. Announce to CEO. Finish current task. Write `TICKETS/SESSION-HANDOFF-{date}.md`.
- Never start what you can't finish — if you can't read skill + plan + implement + build + deploy in remaining context, don't start.
- Unapproved changes at context limit: `git stash -m "WIP: {description}"`. Document in handoff. NEVER commit unapproved changes.
- After compaction: `read_constitution()` → `read_guidance()` → re-read active ticket → re-read skills → `git status` → only then resume.

### Secrets hygiene (Article XVI)
- **No secrets in prose.** Never paste credentials, tokens, keys, or connection strings into tickets, closeouts, READMEs, comments, or any file other than `.env`. Reference by name (`SLACK_BOT_TOKEN`), never by value.
- **Pre-commit secret scan.** All repos must run a secret detection hook (`gitleaks`, `detect-secrets`, or equivalent) on every commit. The hook blocks the push if a pattern matches. No `--no-verify` bypass.
- **Incident response.** If a secret is committed: (1) rotate immediately, (2) scrub git history, (3) verify zero reachable objects contain the secret, (4) force-push. Assume compromise even if exposure window was short.
- **Git history is public surface area.** Deleting a file does not delete it from history. Treat every commit as permanent and public, even in private repos.

### Security agent (Article XIV)
- Pre-deploy scrub: no hardcoded secrets, user-scoping integrity, dependency hygiene, audit trail completeness
- Flag any auth bypass, service role RLS bypass without justification, admin endpoints without scoped auth
- Scalability: flag O(n²) in hot paths, unindexed queries on 10K+ row tables, unbounded SELECTs, write amplification loops
- Security Fail is binding — only CEO can clear it

### QA agent — Quinn (Article XV)
- Quinn: executes tests, writes specs in `tests/quinn/`, files GitHub issues, reads codebase. Cannot write production code.
- Every Clode production deploy triggers Quinn QA: Tier 1 smoke + Tier 2 changed surfaces
- Quinn did not build it. Quinn does not rationalize. If a user would see it as broken, it's broken.

### Bridge protocol
- Session start: `read_constitution()` → `read_guidance()` → `ack_guidance()` → `write_checkpoint(session-start)`
- During work: `read_guidance()` before major actions, `write_checkpoint()` at milestones
- Questions/blockers: checkpoint with `needs-guidance` tag. Do NOT ask CEO to relay.
- After completion: `read_guidance()` before going idle. Agent that idles without polling is unreachable.
- After compaction: re-run full session start sequence.

### Concurrent sessions
- State which files you plan to touch in your plan
- Use `npm run clode-build`, never raw `npm run build`
- If `git push` fails, `git pull --rebase` first
- Only ONE session provides migration SQL at a time

---

## FORBIDDEN ACTIONS

```
🚫 Code without a plan
🚫 Commit without build passing
🚫 Deploy without verifying
🚫 Run mutating SQL without CEO seeing it first
🚫 .catch(() => {}) — handle or log every error
🚫 Use CEO as QA tester
🚫 Start tasks you can't finish in remaining context
🚫 Commit unapproved changes at context limit
🚫 Assert runtime behavior from code reading — run it first
🚫 Declare code "dead" without content search
🚫 Modify .env files
🚫 Paste secret values into tickets, docs, or comments — reference by name only
🚫 Commit without pre-commit secret scan passing
🚫 Run vercel env pull
🚫 Modify /lib/auth/* without explicit approval
🚫 Skip read_constitution() after compaction or session start
🚫 Ignore ⚠️ CONSTITUTION NOT READ warnings
🚫 Use raw Playwright for screenshots — use skill
🚫 Test on localhost — production only for E2E
🚫 Open localhost or production URLs in Chrome browser tools
```

---

*Machine-optimized from AXIS-PRAXIS.md (37KB → ~5KB). Full human narrative, origin stories, and amendment history preserved in the original. Use `check_section("Red X")`, `check_section("security")`, etc. for deep reference when needed.*
