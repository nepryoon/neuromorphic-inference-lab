# Roadmap – Neuromorphic Inference Lab

This roadmap is intentionally long term (3–4+ years) and research oriented.  
It is organised along three parallel tracks:

- **Track A – Theory and Reading**
- **Track B – Software and Agents**
- **Track C – Neuromorphic Hardware (later)**

---

## Phase 0 – Foundations (0–6 months)

**Goal:** Build a solid conceptual and practical base.

### Track A – Theory and Reading
- [ ] A0.1: Review core probability theory and Bayesian inference.
- [ ] A0.2: Study spiking neural networks (coding schemes, neuron models, learning rules).
- [ ] A0.3: Study active inference and predictive coding frameworks.
- [ ] A0.4: Maintain `docs/bibliography.md` with key references and concise notes.

### Track B – Software and Agents
- [ ] B0.1: Set up Python environments for SNN simulation (e.g. Brian2, Lava).
- [ ] B0.2: Create minimal examples of single neurons and small SNN circuits in `notebooks/00_snn_basics`.
- [ ] B0.3: Implement small toy generative models / Bayesian models in `notebooks/01_active_inference_toy_models`.

### Track C – Hardware
- [ ] C0.1: Survey available neuromorphic hardware and open simulators.
- [ ] C0.2: Document pros/cons and access conditions in `docs/hardware-landscape.md`.

---

## Phase 1 – Simulated neuromorphic agents (6–12 months)

**Goal:** Build SNN-based agents in simple environments.

### Track A – Theory and Reading
- [ ] A1.1: Review reinforcement learning versus active inference perspectives.
- [ ] A1.2: Study existing work on SNN control and neuromorphic agents.

### Track B – Software and Agents
- [ ] B1.1: Implement a simple environment (1D navigation or gridworld) in `envs/`.
- [ ] B1.2: Build a baseline non-spiking agent (e.g. tabular or simple neural network) for comparison.
- [ ] B1.3: Implement the first SNN-based agent in `src/neuromorphic_inference/agents.py`.
- [ ] B1.4: Package one complete experiment in `experiments/001_snn_spike_response` with a small README and plots.

### Track C – Hardware
- [ ] C1.1: Reproduce one SNN example from the literature on a public simulator or framework.
- [ ] C1.2: Document limitations and next steps.

---

## Phase 2 – Active inference on SNNs (12–24 months)

**Goal:** Prototype active-inference–style agents with spiking architectures.

### Track A – Theory and Reading
- [ ] A2.1: Deep dive into the active inference formalism (generative models, policies, expected free energy).
- [ ] A2.2: Survey any existing work on the intersection between active inference and neuromorphic computing.

### Track B – Software and Agents
- [ ] B2.1: Implement a minimal discrete active inference agent in a toy environment (non-spiking).
- [ ] B2.2: Map key components (belief updates, policy selection) to a spiking-friendly representation.
- [ ] B2.3: Prototype a first “spiking active inference agent” in `experiments/003_snn_active_inference_agent`.
- [ ] B2.4: Compare energy/compute properties versus non-spiking baselines (at least in simulation).

### Track C – Hardware
- [ ] C2.1: Identify a target neuromorphic platform or realistic simulator.
- [ ] C2.2: Port a subset of the spiking active inference agent to that platform.

---

## Phase 3 – Towards neuromorphic hardware (24–36+ months)

**Goal:** Make neuromorphic hardware (or realistic emulation) a first-class target.

### Track A – Theory and Reading
- [ ] A3.1: Follow recent research on learning rules suited to hardware constraints.
- [ ] A3.2: Study work on energy-efficient inference and on-chip learning.

### Track B – Software and Agents
- [ ] B3.1: Refine the software stack into reusable modules (`src/neuromorphic_inference/`).
- [ ] B3.2: Create a clearer API for defining agents, environments and experiments.

### Track C – Hardware
- [ ] C3.1: Run at least one end-to-end agent on neuromorphic hardware or a close simulator.
- [ ] C3.2: Document performance, bottlenecks and lessons learnt.
- [ ] C3.3: Prepare material for blog posts or preprints based on these prototypes.

---

## Phase 4 – Research prototypes and publications (36+ months)

**Goal:** Consolidate the work into research-grade outputs.

- [ ] R4.1: Refine the codebase into a minimal, well-documented toolkit.
- [ ] R4.2: Prepare one or more research-oriented write-ups or preprints.
- [ ] R4.3: Define directions for a deep-tech start-up around neuromorphic agents.
