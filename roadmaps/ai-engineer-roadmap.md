# Backend → AI/Agentic Engineer Roadmap

**How this document works:** No calendar dates. Each phase has a **gate** — a specific thing you must be able to do _without help_ before moving on. If a phase takes you 4 days or 4 weeks, that's fine. Don't advance because time passed; advance because you cleared the gate.

---

## The Method (read this before Phase 1)

For every new concept, work in this order:

1. **Attempt it hand-coded first**, even badly. Don't open docs or ask anything before you've tried and failed once. The failure is what makes the next step stick.
2. **Stuck for 15-20 min?** → Check official docs first (Python docs, framework docs, provider API reference). Docs teach you to read docs — a skill you'll need forever.
3. **Docs didn't clarify it?** → Targeted Google search for the specific error or concept. Not "how to build an AI agent," but "pydantic validation error extra fields not permitted."
4. **Still stuck, or the _concept_ itself is unclear (not just syntax)?** → Ask me — but ask for the _concept explained_, not the code written. "Explain why tool calling needs a JSON schema" is good. "Write me the tool calling code" defeats the point.
5. **Videos** → Use only for things that are genuinely spatial/architectural and hard to get from text (e.g. visualizing how an event-driven pipeline flows). Don't use videos to learn syntax or to avoid writing code yourself. Cap it — if you've watched more than you've typed, invert it.

Rule of thumb: the harder something was to get unstuck on, the better you'll remember it. Getting handed the answer immediately is the single biggest way people fake progress on a roadmap like this.

---

## Phase 1 — Python Reboot

**Start here, today.**

**Steps, in order:**

1. Syntax refresh: variables, functions, control flow, lists/dicts/sets, comprehensions — 2-3 days of small scripts, not a course.
2. Classes and modules — build something with 2-3 files that import from each other.
3. Virtual environments + pip (or `uv`) — set up a project properly, not global installs.
4. Exceptions and error handling.
5. Async basics (`async`/`await`) — this matters a lot later for streaming and concurrent tool calls.
6. Build a small FastAPI CRUD API with Pydantic models. This is deliberately chosen because it overlaps your NestJS/Express knowledge — you're learning Python syntax, not backend concepts from scratch.

**Gate — you're done when:**

- You can build the FastAPI CRUD endpoint above with the docs open but without copy-pasting a tutorial's code, and
- You can explain out loud (to me, or to yourself) why Pydantic validation happens where it does, and what `async def` actually buys you over `def` in an endpoint handler.

If you can't explain it, you can still "do" it — that's the gap to close before moving on.

---

## Phase 2 — Talk to an LLM Directly (No Frameworks)

**Ban on LangChain/LangGraph/LlamaIndex for this entire phase.** Use the raw Anthropic or OpenAI Python SDK only. The goal is to understand what frameworks are hiding from you before you use the frameworks.

**Steps, in order:**

1. Basic call: Python script → API → printed response. Nothing else.
2. Structured outputs: force the model to return JSON matching a Pydantic schema you define.
3. Multi-turn conversation: manage the message history array yourself, by hand — see what "context" actually is.
4. Streaming: implement token-by-token streaming to a simple endpoint (you already know SSE from your backend work — reuse that).
5. Tool/function calling: give the model a schema for a fake function (e.g. `get_weather`), watch it decide to call it, and handle the round-trip yourself.

**Gate — you're done when:**

- You can explain, without notes, what actually happens on the wire when "tool calling" occurs — what the model returns, what your code does with it, what gets sent back.
- You could roughly sketch what LangChain is doing under the hood, even if you've never opened its source.

---

## Phase 3 — Build the Core Evolving System

Pick **one** real project (a RAG-based knowledge assistant or a support/billing agent — pick whichever domain interests you, not whichever sounds most impressive).

**Steps, in order:**

1. Set up Postgres + pgvector.
2. Write a background worker (reuse your queue/worker experience) that chunks documents, generates embeddings, stores them.
3. Build the retrieval side: a query comes in, gets embedded, does semantic search, returns relevant chunks.
4. Wire retrieval into the LLM call from Phase 2 — this is your first real RAG loop.
5. Add a proper API layer in front of it (your backend strength does the heavy lifting here).

**Gate — you're done when:**

- You can explain a bad retrieval result and diagnose _why_ it was bad (chunking too coarse? embedding model mismatch? query phrasing?) rather than just re-running it and hoping.
- The system survives you feeding it a deliberately weird or adversarial query without silently breaking.

---

## Phase 4 — Extensions (this is what makes the project worth showing)

**Steps, in order:**

1. Replace ad hoc conditionals with a lightweight agent loop or state machine — this is where LangGraph or a hand-rolled loop finally makes sense to introduce, because you understand what it's replacing.
2. Write an eval script: 15-20 test queries, run them through your system, score outputs (a stronger model as judge, or deterministic checks where possible).
3. Add tracing/observability (LangSmith, Phoenix, or even structured logging you build yourself) — track latency, token spend, where things fail.
4. Only now, if useful: a minimal dashboard/chat UI to demo it (your 10% frontend budget goes here, not before).

**Gate — you're done when:**

- You can walk someone through the eval failures and explain what you'd change, live, in an interview setting.
- You can articulate the reliability trade-offs you made — not just that it works, but why it works _reliably enough_.

---

## Running alongside all phases (not a separate track)

- **DSA:** light and steady early (1 problem every 1-2 days, just to not go cold) — deliberately ramp up once Phase 3 is working and you're a few weeks from applying. Don't front-load this; sharpness before interviews matters more than volume months ahead of them.
- **System design:** a good engineering blog post or write-up a few times a week (ByteByteGo, Netflix/Uber eng blogs) — read for patterns, not memorization.
- **Frontend:** touch only when Phase 4 needs a UI.

---

## Self-assessment checklist (use at every gate, not just phase ends)

Ask yourself these three honestly before moving forward:

1. **Could I rebuild this from scratch in a new empty folder, docs open, without looking at my old code?**
2. **Could I explain a design decision I made to someone skeptical, and defend it?**
3. **If I changed one input (a bad document, a malformed request, an edge case), do I know what would happen — or would I have to run it to find out?**

If any answer is "not really," that's not failure — it's the actual signal for what to spend another few days on before advancing.
