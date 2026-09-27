# Ramesh Kumar L

I spent about 14 years building Android and OEM platform software at Samsung — the kind of work where a bug ships to millions of devices and "it worked on my machine" means nothing. That standard for correctness is the one I'm now trying to hold AI agents to.

The question I keep coming back to: how much context does an agent actually need before its decision holds up? My hunch is far less than people hand it — the right evidence, not all of it — but a hunch isn't worth much, so most of what I build here is aimed at measuring it. The repos below are the front-to-back version of that idea: decide what an agent should know, prove whether it helped, make the judgment repeatable, and give it somewhere durable to remember.

These are active engineering projects, not products. Where something is proven I show the number; where it isn't, I say so — that's the part I'd want a reviewer to check first.

## The stack, in the order it makes sense to read it

**[engineering_context_compiler](https://github.com/ramesh-kumar-l/engineering_context_compiler)** (ECC) compiles a messy engineering task into the smallest evidence-backed context package an agent needs to act — ranked, trust-labeled, and honest about what it left out. It's fully deterministic: no LLM call anywhere, every ranking decision is a rule you can inspect. 202 tests across 46 files, CI on every push. In its own benchmark against a keyword-matching baseline it reached 100% evidence recall on roughly 63% fewer tokens — measured on its own codebase.

**[engineering_evaluation_platform](https://github.com/ramesh-kumar-l/engineering_evaluation_platform)** (EEP) is where the claims get tested — baseline-vs-treatment comparisons over real fixture tasks with confidence intervals and effect sizes. 353 tests, CI on every push, and a zero-credential `npm run reproduce:smoke` so anyone can re-run the pipeline. Its first live pilot came back statistically inconclusive at n=3, and I've left it reported that way. A tool that only produces flattering results isn't an evaluation tool.

**[agentic_engineering_skills_platform](https://github.com/ramesh-kumar-l/agentic_engineering_skills_platform)** (AESP) is the reliability layer: reusable skills and verification workflows so an agent's judgment is repeatable across runs instead of re-improvised each time.

**[semantic_control_plane](https://github.com/ramesh-kumar-l/semantic_control_plane)** (SCP) is the plumbing underneath — memory, a knowledge graph, trust scoring, governance, and a flight recorder for replay. Built to a real bar: ports/adapters throughout, ~63 behavioral tests, strict typing, and eight decision records covering the trade-offs. No live validation result yet, and the README says so.

Two smaller, self-contained ones: **[scp-memory-core](https://github.com/ramesh-kumar-l/scp-memory-core)**, persistent memory for agents, and **[sqlite_diffx](https://github.com/ramesh-kumar-l/sqlite_diffx)** — a Git-style diff and migration tool for SQLite you can `pip install` and use today.

## How I work

Habits from platform engineering: decision records for anything non-obvious, benchmarks where I have them, failure analysis when things break, and explicit trade-offs instead of hand-waving. I'm not trying to prove AI is always better — I'm trying to find out when it helps, and to build the instruments that can tell the difference.

Currently going deep on context engineering, evaluation, and the reliability of agentic software work.
