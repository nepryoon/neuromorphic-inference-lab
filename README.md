# Neuromorphic Inference Lab

> **Website:** [https://www.neuromorphicinference.com/](https://www.neuromorphicinference.com/)
> **Demos:** [https://www.neuromorphicinference.com/demos](https://www.neuromorphicinference.com/demos)
> **Evidence index:** [https://www.neuromorphicinference.com/evidence](https://www.neuromorphicinference.com/evidence)

Neuromorphic Inference Lab is my independent software research initiative, focused on ontology and knowledge-graph architecture and governed AI agents. This repository is its hub: it lists the projects, their status and their code.

---

## Research direction

"Neuromorphic Inference" is the name of my lab and of a research direction: brain-inspired principles for how AI systems activate, connect and update structured knowledge, starting with context-dependent activation and relevance propagation over knowledge graphs. It is software research: no spiking neural networks and no neuromorphic hardware. These mechanisms are not implemented yet; OCOR builds the components they would act on.

---

## Projects

Each project carries its status. None of them is a production system.

* **[OCOR (Operational Causal Ontology Runtime)](https://github.com/nepryoon/ocor)** — in development: a runnable implementation on a synthetic scenario; qualification in progress. A vendor-neutral semantic core. Built so far: an ontology compiler that turns each ontology version into a content-addressed canonical model, a named-query gateway that checks policy before any read, governed agent memory with hybrid retrieval, a causal scenario runtime, and an agent kernel with typed tools, budgets and a kill switch. The W3C boundary (RDF, JSON-LD, SHACL Core and SPARQL on Apache Jena / Fuseki) is a prototype.
* **[Enterprise Code Intelligence](https://github.com/nepryoon/eci)** — runnable proof of concept. Graph-RAG over a codebase: vector and full-text retrieval expanded along graph neighbours and fused by reciprocal rank, with event-driven updates. Services in Python, Go and Rust; Neo4j, Qdrant, OpenSearch, Kafka and Debezium.
* **[Enterprise Sovereign AI Decision Matrix](https://github.com/nepryoon/enterprise-sovereign-ai-matrix)** — proof of concept with a [live demo](https://matrix.neuromorphicinference.com/) on synthetic data and one real routed model call. A governed AI workflow that routes the model call to a provider by data-sovereignty rules, requires human approval, records every decision and tracks latency, token use and cost.
* **[IADF Platform](https://github.com/nepryoon/iadf-platform)** — runnable architecture proof of concept: contract-first schemas, an explicit state machine, model routing and fail-closed controls, with a four-role agent engine (architect, implementer, adversarial reviewer, diagnostician). Not a complete software factory.
* **Agent demos: [HR onboarding orchestrator](https://github.com/nepryoon/hr-onboarding-orchestrator), [hiring panel](https://github.com/nepryoon/hr-hiring-panel), [innovation board](https://github.com/nepryoon/innovation-board)** — live demos on simulated data. In all three, code validates the agents' output and a person decides.
* **[RAG Knowledge Copilot](https://www.neuromorphicinference.com/demos/rag-copilot)** — live public demo, not a production system. Question answering over PDFs with citations: all-MiniLM-L6-v2 embeddings, exact FAISS search, GPT-4o Mini constrained to the retrieved context, and an automatic benchmark with three reference-free metrics.
* **[MV Grid Fault Risk](https://github.com/nepryoon/mv-grid-fault-risk)** — open-source ML application (Apache 2.0): fault-risk scoring for medium-voltage lines with time-based validation, training tracked with MLflow and Docker packaging. Independent project, not an Enel system; the live endpoint is rule-based.
* **Preprint: *Can LLM Agents Care About the World?* (2026)** — theoretical preprint, not peer reviewed, with public [simulation code](https://github.com/nepryoon/ehd-simulations). [ResearchGate, DOI 10.13140/RG.2.2.25820.55685](https://doi.org/10.13140/RG.2.2.25820.55685)

---

## Transparency

The repositories of the lab are public; only some of them carry an open-source licence. I define architectures and specifications, direct AI-assisted implementation with coding agents (Claude, Codex), read and review the code and tests, and remain accountable for validation, limitations and deployment decisions. The repositories demonstrate inspectable patterns, bounded proofs of concept and one implementation in development (OCOR). They are not presented as customer production platforms, validated research frameworks or evidence of years operating autonomous multi-agent runtimes at scale.

---

## Contact

* [GitHub](https://github.com/nepryoon)
* [LinkedIn](https://www.linkedin.com/in/nepryoon)
* [Website](https://www.neuromorphicinference.com)
