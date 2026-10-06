# EazyDiner Autonomous Concierge (EAC)

**A retrieval-first restaurant intelligence engine** — the LLM never recalls restaurant facts from memory; it reasons only over retrieved, validated context.

> The working codebase is private (it contains production credentials and partner data). This repository is a public overview of the architecture and results.

## The problem

EazyDiner — one of India's dining platforms — had a silent crisis: **282 NPS detractors at an average 1.0/10**, with the #1 complaint being *discount opacity* — users saw "25% off" but paid far more at the restaurant.

## What EAC does

An agentic concierge layer that:

1. resolves a free-text dining intent (deterministic + LLM-assisted parsing),
2. retrieves candidate restaurants through a layered pipeline,
3. ranks them by **user value** (ADR-010: maximize user value, not platform value),
4. generates a grounded recommendation — every claim traced to retrieved context.

**Pipeline:** intent → deterministic filter → semantic search (pgvector) → graph expansion → candidate assembly → ranking → context assembly → LLM generation.

## Engineering

- **Architecture frozen in ADRs** — 16-table schema, 6 repositories, 10 modules; flat locality hierarchy; explicit user-value principle.
- **Retrieval-first design**: deterministic metadata, semantic knowledge, graph relationships, and LLM generation are independent layers. No LLM recall of facts.
- **Evaluation discipline**: ranking evaluation suites, regression datasets (ambiguous + impossible queries), stress tests, leakage-prevention filters.
- **Production**: Supabase (Postgres + pgvector) data layer, deployed API service, founder-demo runbook.

Also in the family — the live concierge landing experience: 32K-particle GPU hero (Three.js/GLSL), GSAP + Lenis scroll narrative, LLM concierge with offline fallback → **[eazydinerai.netlify.app](https://eazydinerai.netlify.app/)**

## Impact

- Competitive transparency audit (app emulation + web crawls): EazyDiner **0/9** vs District by Zomato 7/9 → fix designed, **projected ≥60% reduction** in the top NPS complaint category (282 → ≤112 in 30 days).
- **Net Effective Price (NEP)**: a 6-layer discount-stacking engine collapsing restaurant + membership + bank card + co-brand + perks into one honest price.

---

Built by [Pratham Sethi](https://github.com/prathamsethiongithub) · [portfolio](https://prathamsethiongithub.github.io/portfolio-samples/)
