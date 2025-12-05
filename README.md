# Neuromorphic Inference Lab

> Brain-inspired agents that reason under uncertainty on neuromorphic hardware.

---

## Vision

Neuromorphic Inference Lab is a long-term research initiative exploring how
**brain-inspired architectures** and **spiking neural networks (SNNs)** can support
**autonomous agents that reason and act under uncertainty**.

The project focuses on:

- Neuromorphic hardware and realistic simulators  
- Probabilistic and active-inference–based algorithms  
- Methods for using neuromorphic processors as **first-class computational substrates**
  for learning, prediction and decision-making in real-world scenarios

This repository is not a polished product. It is a **living research notebook** that will
evolve over several years.

---

## Goals (and non-goals)

**Goals**

- Build and document a personal research path in neuromorphic inference.
- Prototype simple SNN-based agents in toy environments.
- Explore how active inference and related probabilistic frameworks can be mapped to spiking architectures.
- Move progressively closer to real neuromorphic hardware and energy-aware computation.

**Non-goals (for now)**

- Providing a production-ready library.
- Covering all possible SNN frameworks or neuromorphic platforms.
- Offering plug-and-play solutions for industrial use.

---

## Roadmap (high level)

See [`ROADMAP.md`](./ROADMAP.md) for details.  
At a glance:

- [ ] **Phase 0 — Foundations**  
  Build core understanding of SNNs, generative models and active inference.

- [ ] **Phase 1 — Simulated neuromorphic agents**  
  Implement simple SNN-based agents in small environments.

- [ ] **Phase 2 — Active inference on SNNs**  
  Prototype active-inference–style agents with spiking architectures.

- [ ] **Phase 3 — Towards neuromorphic hardware**  
  Explore deployment on neuromorphic platforms or realistic simulators.

- [ ] **Phase 4 — Research prototypes and publications**  
  Consolidate into a minimal open-source stack and research-grade experiments.

Progress will be tracked through GitHub issues and experiments in the
[`experiments/`](./experiments) and [`notebooks/`](./notebooks) folders.

---

## Repository structure

```text
.
├── README.md          # This file
├── ROADMAP.md         # Long-term roadmap
├── docs/              # Vision, research notes, bibliography, design docs
├── notebooks/         # Jupyter notebooks for exploratory work
├── src/
│   └── neuromorphic_inference/
│       ├── snn_models.py
│       ├── active_inference.py
│       ├── agents.py
│       └── utils.py
├── experiments/       # Reproducible experiments (one per folder)
├── envs/              # Simple environments / MDPs / gridworlds
├── hardware/          # Configs and scripts for neuromorphic platforms
├── requirements.txt
└── pyproject.toml     # (Optional) Packaging configuration
