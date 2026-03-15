# Structuring AI — Correctness Loop POC

**Bank of America Global Markets · Structured Products · Phase 1**

A proof-of-concept demonstrating the core correctness loop for AI-assisted structured product pricing and verification.

## What this demonstrates

The four-step loop Gbenga described:

1. **Attempt** — System receives an RFQ, proposes pricing, flags novelty level
2. **Verify** — Confidence score built from three signals: rules rationale, precedent fit, feedback history — plus regime check
3. **Record** — Human reviewer signs off with weighted authority (0.5× associate → 1.4× MD). Commentary absorbed into knowledge graph.
4. **Improve** — System shows what it learned. Next similar trade gets higher confidence. One negative triggers regime review flag — asymmetric by design.

## Three scenarios included

| Scenario | Structure | Novelty | Confidence |
|----------|-----------|---------|------------|
| SCN-001 | Capital-Protected Equity Note (SPX) | Familiar — 18 precedents | 82% · Proceed |
| SCN-002 | Autocall Worst-of (SPX/SX5E/HSCEI) | Partial — HSCEI leg novel | 54% · Caution |
| SCN-003 | FX Barrier Note + Memory Feature | Novel — zero precedents | 12% · Stop |

## Key design principles

- **"I do not know"** — SCN-003 shows the system refusing to hallucinate a price when it has no precedent
- **Asymmetric feedback** — one negative does not subtract 4%. It triggers a regime review flag.
- **Reviewer weighting** — seniority and deal history determine how much a sign-off moves the confidence needle
- **Regime awareness** — current rate environment compared against precedent set, impact quantified
- **No rules pre-coded** — system learns through attempt → verify → record → improve. Same as how a junior structurer learns.

## Run it

Open `poc/correctness-loop/index.html` in any browser. No server, no dependencies, no API keys.

## Roadmap

- [ ] Connect to real trade database (CSV / API)
- [ ] Add QIS Strategies scenario (SCN-004)
- [ ] Add Custom Baskets scenario (SCN-005)
- [ ] Wire reviewer commentary to actual vector store
- [ ] Build confidence drift detection (regime shift alert)
- [ ] Deploy to GitHub Pages

---

*Built by Bolaji Olatoye · Altitude AI Consulting · March 2026*
