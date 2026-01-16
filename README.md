# Neuromorphic Inference Lab

> **Live portfolio:** [https://www.neuromorphicinference.com/](https://www.neuromorphicinference.com/)
> **Demos hub:** [https://www.neuromorphicinference.com/demos](https://www.neuromorphicinference.com/demos)
> **Evidence index (skills → proof):** [https://www.neuromorphicinference.com/evidence](https://www.neuromorphicinference.com/evidence)

Neuromorphic Inference Lab is my personal **applied AI systems** portfolio.
“Neuromorphic” is the signature: I care about **efficient, robust, operable inference** (latency/cost/traceability), not just model accuracy.

This repo is the **hub**: it explains the philosophy and points to **live demos** + the **exact source code** for each system.

---

## How to evaluate (2-minute audit)

1. Open the **Demos hub**: [https://www.neuromorphicinference.com/demos](https://www.neuromorphicinference.com/demos)
2. Pick a demo and check:

   * the **live documentation** on the domain
   * the **source repository** linked on the page
3. Use the **Evidence index** to map skills → proofs: [https://www.neuromorphicinference.com/evidence](https://www.neuromorphicinference.com/evidence)

**Rule:** no “skills list” without a clickable proof.

---

## Applied demos (live docs + code)

Each demo has:

* **Live docs** (domain page)
* **Code** (GitHub repo)

Current catalog (authoritative list is on the website):

* **EdgePulse** — end-to-end operational AI loop (ingest → store → score → alert → dashboard)

  * Live: [https://www.neuromorphicinference.com/demos/edgepulse](https://www.neuromorphicinference.com/demos/edgepulse)
  * Code: [https://github.com/nepryoon/edgepulse](https://github.com/nepryoon/edgepulse)

* **RAG Copilot** — RAG chatbot with citations, eval, guardrails (in progress)

  * Live: [https://www.neuromorphicinference.com/demos/rag-copilot](https://www.neuromorphicinference.com/demos/rag-copilot)
  * Code: [https://github.com/nepryoon/nil-rag-copilot](https://github.com/nepryoon/nil-rag-copilot)

* **Forecast Studio** — backtesting + scheduled forecasts + reporting (in progress)

  * Live: [https://www.neuromorphicinference.com/demos/forecast-studio](https://www.neuromorphicinference.com/demos/forecast-studio)
  * Code: [https://github.com/nepryoon/nil-forecast-studio](https://github.com/nepryoon/nil-forecast-studio)

* **Tabular Risk / Churn** — scoring + explainability + data quality + drift (in progress)

  * Live: [https://www.neuromorphicinference.com/demos/tabular-risk](https://www.neuromorphicinference.com/demos/tabular-risk)
  * Code: [https://github.com/nepryoon/nil-tabular-risk](https://github.com/nepryoon/nil-tabular-risk)

* **Visual Inspector** — image classification + explainability + inference packaging (in progress)

  * Live: [https://www.neuromorphicinference.com/demos/visual-inspector](https://www.neuromorphicinference.com/demos/visual-inspector)
  * Code: [https://github.com/nepryoon/nil-visual-inspector](https://github.com/nepryoon/nil-visual-inspector)

* **ML Infra Template** — reusable repo template for Docker/CI/provenance (in progress)

  * Live: [https://www.neuromorphicinference.com/demos/infra-template](https://www.neuromorphicinference.com/demos/infra-template)
  * Code: [https://github.com/nepryoon/nil-infra-template](https://github.com/nepryoon/nil-infra-template)

---

## Research archive (kept for continuity)

I keep an archive of neuromorphic/SNN experiments and notes, but it’s intentionally **secondary** to applied demos:

* Live archive: [https://www.neuromorphicinference.com/research](https://www.neuromorphicinference.com/research)

---

## What “neuromorphic” means here

Not “SNN-only”. It means:

* **Efficiency-first inference:** latency/cost budgets are explicit
* **Robustness:** behavior under imperfect data and failure modes
* **Operability:** reproducibility, monitoring hooks, auditability
* **Clarity:** architecture and trade-offs explained in plain language

---

## Portfolio infrastructure

The website is operated like a product:

* stable URLs under `/demos/*`
* an evidence map under `/evidence#*` (CV-friendly anchors)
* build provenance exposed via `/api/build` on the domain (commit + branch)

---

## Contact

GitHub: [https://github.com/nepryoon](https://github.com/nepryoon)
