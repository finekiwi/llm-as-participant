# LLM-as-Participant

**Can LLM-generated synthetic personas replace real users in UX research?** A comparative study analyzing pain point alignment, severity judgment, and blind spots between 8 LLM personas and 5-8 real participants on a Korean welfare policy chatbot.

---

## Research Question

Do LLM synthetic personas catch the same usability issues as real users when given identical questionnaires on the same service? What do they miss, and what do they fabricate?

## Study Design

| | LLM Personas | Real Users (Developer) | Real Users (Non-developer) |
|---|---|---|---|
| **N** | 8 | 3-4 | 3-4 |
| **Method** | Backstory-driven prompting | Usability testing + Think-aloud + Post-interview | Same |
| **Service** | 복지나침반 v2 (Welfare Compass — Korean youth welfare policy RAG chatbot) |
| **Questionnaire** | Identical across all groups |

### Three-Way Comparison Framework

```
Developer ─────── structured, architecture-aware feedback
                          ↕ How similar?
LLM Persona ───── logical, pattern-based feedback
                          ↕ How different?
Non-developer ─── embodied, emotional, context-dependent feedback
```

## Analysis Framework

Each pain point is classified into one of three categories:

| Category | Definition |
|----------|-----------|
| ✅ **Match** | Both LLM and real users identified the issue |
| ❌ **LLM Blind Spot** | Only real users found it — LLM missed it |
| ⚠️ **LLM Hallucination** | Only LLM reported it — real users didn't mention it |

### Analysis Dimensions
- Pain point match rate
- Severity judgment distortion (direction TBD — overestimate vs underestimate)
- Expression style differences (analytical vs emotional)
- Blind spot typology (embodied experience, context-dependent behavior, emotional response, unexpected usage)
- Three-group comparative analysis

## Hypotheses

| # | Hypothesis | Literature Basis |
|---|-----------|-----------------|
| H1 | LLM catches general pain points but misses context-dependent ones | Blind spot #4: inability to simulate real-world irrationality |
| H2 | LLM severity judgments are distorted — narrow distribution, unstable direction | Emporia study: positive bias + herd mentality in LLM responses |
| H3 | LLM feedback is more similar to developer group than non-developer | Szymanski et al. (2024): three-group qualitative divergence |
| H4 | LLM's biggest limitation is emotional context | Blind spot #1: absence of embodied experience |

## Research Gaps Addressed

1. **Korean-language validation** — Most LLM persona studies are English/WEIRD-centric. No deep UX comparison exists for Korean services.
2. **Public welfare domain** — Existing studies focus on low-risk commercial apps. Welfare services involve administrative burdens, stigma, and emotional distress that LLMs may fail to simulate.
3. **Three-way comparison** — Prior work is binary (LLM vs user). Developer vs non-developer vs LLM triangulation is novel.

## Key References

- Kapania et al. (2025). *Simulacrum of Stories.* CHI 2025. — Backstory-driven prompting outperforms demography-only
- Papangelis (2025). *The Synthetic Persona Fallacy.* ACM Interactions. — "Epistemic freeloading" critique
- Szymanski et al. (2024). *Comparing Criteria Development Across Domain Experts, Lay Users, and Models.* ArXiv. — Three-way comparison precedent
- Pang et al. (2025). *Understanding the LLM-ification of CHI.* CHI 2025. — Systematic review of LLM roles in HCI
- Truss et al. (2026). *PersonaCite.* AAMAS 2026. — Evidence-bounded persona system

## Repository Structure

```
llm-as-participant/
├── README.md
├── LICENSE
├── personas/              # 8 persona profiles + prompts
├── responses/
│   ├── llm/              # LLM persona responses (primary model)
│   ├── pilot/            # Pilot comparison: Claude vs GPT vs Gemini
│   └── real/             # Real user interview data (anonymized)
├── analysis/
│   ├── pilot_model_comparison.md
│   ├── pain_points.md    # Pain point matching analysis
│   ├── comparison.py     # Analysis scripts
│   └── visualizations/   # Charts, heatmaps, diagrams
├── interview/
│   ├── questionnaire.md  # Interview questionnaires
│   └── protocol.md       # Interview protocol
└── paper/                # Paper draft (optional)
```

## Tools & Methodology

**Model Selection:** A pilot test was conducted with 2 personas across three LLMs (Claude Opus, GPT-4o, Gemini Pro) to compare response diversity, persona consistency, and backstory adherence. The primary model was selected based on pilot results; full pilot comparison is documented in `analysis/pilot_model_comparison.md`.

Persona prompt design, analysis framework, and interpretation were performed by the researcher. LLMs were used as **research instruments**, not co-authors.

All prompts are published in this repository for full reproducibility.

## Status

🔄 **In Progress**

- [x] Research design & literature review
- [x] Persona profiles designed (8 personas)
- [ ] Pilot: multi-model comparison (Claude vs GPT vs Gemini)
- [ ] Primary model selected + justification documented
- [ ] LLM simulation responses collected
- [ ] Real user interviews conducted
- [ ] Comparative analysis
- [ ] Portfolio case study
- [ ] Paper draft

## Target Service

**복지나침반 (Welfare Compass)** — AI-powered welfare policy recommendation chatbot for Seoul youth (ages 19-39), matching users to 342 municipal welfare policies via a hybrid architecture: rule-based eligibility filtering + RAG chatbot with ReAct agent.

## Author

**Yuna Sim** — MS in AI (Computer Vision), LLM Engineer & UX Research Lead

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt this material with appropriate attribution.
