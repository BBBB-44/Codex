---
---

## 1. Core Problem-Solving Workflow

### A. Problem Definition (Before touching code)
- **State the gap** in one sentence: *“Expected X happens, but actual Y happens.”*
- **Write down what “fixed” looks like** – this prevents over-engineering.
- **Name the impact** (e.g., data loss, UI freeze, wrong calculation) – this prioritizes urgency.

### B. Expected vs. Current Output
- **Compare side‑by‑side** – highlight the exact difference (character, value, timestamp, order).
- **Simplify inputs** – use the smallest, simplest input that still reproduces the difference.
- **Test with a known correct case** – sanity‑check your expectation first.

### C. Related Field / Context
- **Tag the area** – e.g., auth, caching, DB query, network, rendering.
- **List recent changes** in that field (your code, libs, configs, data).
- **Check if the same field behaves correctly elsewhere** – that isolates the problem.

---

## 2. Must‑Have Debugging Habits

### Learn to read the error message (really)
- **First line** = exception type (e.g., `TypeError`, `KeyError`).
- **Last line** = actual failure (often in a stack trace).
- **Look for file names & line numbers** – go there immediately.
- **Copy the error into a search engine** – you’re not the first to see it.

### When did it start?
- **Find the first occurrence** – ask users, check deployment logs, or run older commits.
- **Correlate with a change** – commit, dependency update, config push, data change.
- **If unknown**: binary search `git bisect` or manual test between two dates.

### Can you reproduce it consistently?
- **If yes** → you can debug properly.
- **If no** → note the conditions (time, data volume, user role, environment). Flaky bugs need logging + hypothesis testing.

### Narrow the scope: frontend or backend?
- **Frontend**: browser console, network tab, device/OS, user action sequence.
- **Backend**: request logs, DB queries, environment variables, background jobs.
- **Hybrid**: check API request/response – often the boundary reveals the lie.

### Use logs
- **Log at entry and exit** of suspect functions + key variables.
- **Add unique markers** (e.g., `[DEBUG-123]`) so you can grep.
- **Log the unexpected** – not just errors; log “impossible” branches.

---

## 3. Speed Multipliers (How to Be Faster)

### Jump to the right layer quickly
- **Ask**: “What’s the minimal system that must work for this to succeed?” → go there.
- **Mental layer map** (example for a web app):
  - UI → Event handler → API client → Network → Backend route → Service → DB.
- **Check the layer that changed most recently first** – probability heuristic.

### Eliminate wrong assumptions early (and catch them)
- **Write down your top 3 assumptions** explicitly. Then falsify each with a simple test.
- **Common wrong assumptions**:
  - “The data is clean.”
  - “This function never returns null.”
  - “The config in prod is the same as in dev.”
  - “The user didn’t click twice.”
- **Catch them by**: asserting in code, printing, or writing a tiny unit test.

### Don’t trash randomly (no shotgunning)
- **One intentional change at a time** – log what you changed and why.
- **Before changing anything**, ask: “Will this test a specific hypothesis?”
- **If you feel like guessing** → stop, go back to logs or reproduction steps.
- **Keep a “what I tried” list** – avoids repeating dead ends.

---

### 4. Check the trivial things first (seriously)
Experienced engineers skip these. Fast engineers check them in 10 seconds and move on.

Is it plugged in / running? (Service up? Container healthy?)

Did the config file actually reload?

Is there a typo in a variable name? (Case sensitivity)

Is the environment pointing to the right database/API URL?

Did you clear the cache? (Browser, Redis, CDN, opcache)

These account for ~15% of "mysterious" bugs.

---

### 5. Add checkpoints
Instead of vague logging, add pass/fail checkpoints along the execution path.

python
# Bad: log("got here")
# Good:
assert user_id is not None, "Checkpoint 1 failed: user_id missing"
assert balance > 0, "Checkpoint 2 failed: balance zero or negative"
When a checkpoint fails → you know exactly which step broke, no guessing.

---

### 6. Know when to escalate or reset
Speed isn't always solving it yourself.

After 45–60 minutes with zero progress → stop. Write down what you tried. Ask someone else (fresh eyes see what you're blind to).

Reset your environment → fresh clone, clear caches, restart services. Sometimes the bug is in state, not code.

Stubbornness is the enemy of efficiency.

---

## 7. Quick Cheat Sheet

| When you see...                     | Do this first...                              |
|-------------------------------------|-----------------------------------------------|
| An error message                    | Read line 1 + last line. Go to file:line.    |
| “It worked yesterday”               | Find what changed (git diff, deploy log).    |
| “Sometimes it fails”                | Log conditions + reproduce 5x in a row.      |
| No error, wrong output              | Compare expected vs actual at smallest step. |
| UI issue                            | Open devtools → network & console.           |
| Backend crash                       | Check logs near the timestamp.                |
| You’re about to change random files | Stop. Write a hypothesis first.               |

---

Final rule: **Speed comes from reducing the search space, not from increasing change velocity.** Every minute spent sharpening the problem definition saves an hour of random “fixing.”
