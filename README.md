# SENTINEL — Six-Agent Autonomous Software Reliability

SENTINEL is an architecture for autonomous software reliability: a production failure goes in as raw signal and comes out as a **verified root cause and repair plan**. A Mission Controller dispatches specialist agents, and an Adversarial Verification agent tries to tear every conclusion down before anyone trusts it — *the engineering is in the brakes*.

**Live demo:** deployed on Vercel (static site, no build step) — open `index.html` or visit the project URL.

## The six agents

| # | Agent | Job |
|---|-------|-----|
| 01 | **Mission Controller** | Classifies the failure, assembles incident state, owns routing — forward on confidence, backward on doubt |
| 02 | **Codebase Analyst** | Maps blast radius across services, deploys, and dependencies; seals the evidence pack |
| 03 | **Failure Hypothesis** | Generates ranked candidate causes, each with the observation that would confirm or kill it |
| 04 | **Root-Cause** | Tests hypotheses against logs, metrics, and code paths until one cause explains every symptom |
| 05 | **Repair** | Drafts the smallest safe fix: change, blast radius, rollback path, regression coverage |
| 06 | **Adversarial Verification** | Argues against the root cause and the repair; nothing is verified until the challenge fails to break it |

## Architecture

- **LangGraph state graph** — agents read/write one typed state object (incident, evidence, hypotheses, verdicts), so every conclusion traces to its evidence.
- **Conditional routing** — low-confidence branches loop back for more evidence instead of guessing forward.
- **Verification gates** — regression thinking, edge cases, and output validation applied to every root-cause claim; a failed claim returns to the Hypothesis agent, not to production.
- **Human-in-the-loop** — below the confidence threshold, cases escalate to an engineer with the full evidence trail attached.
- **Auditability by construction** — every agent action is logged against the incident state.

## The demo

The page replays three realistic incidents end to end — a payments retry storm, a checkout deploy regression, and a silently stalling document-verification pipeline — with the agent pipeline visualised live and a final verified incident report.

*Honest note: this repository is an interactive demonstration of the SENTINEL architecture. SENTINEL is an architecture design project by Guru Datha Kandanathi Chittem; the production systems behind the metrics on his résumé are the multi-agent KYC platform and the production RAG pipeline on his portfolio.*

## Run locally

No build, no dependencies — any static server works:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Author

**Guru Datha Kandanathi Chittem** — AI Engineer | Multi-Agent Systems, RAG & LLM Evals
[Portfolio](https://gurudatha-portfolio.vercel.app/) · [LinkedIn](https://www.linkedin.com/in/gurudatha-kandanathi-chittem/) · [Résumé](https://gurudatha-portfolio.vercel.app/gurudatha.pdf)
