# 🩺 Bio-Atlas Medical Showcase

![Bio-Atlas Medical Orchestrator](assets/thumbnail.png)

> **Sovereign Biomedical Intelligence, Genomic Variant Screening & 3D Macromolecular Visualizer**  
> *A next-generation clinical decision-support ecosystem engineered by SNORBIK Studio.*  
> *Live Web Workstation: `http://localhost:8529/`*

[![Domain](https://img.shields.io/badge/Domain-Biomedical_%26_Genomics-blue.svg)]()
[![Status](https://img.shields.io/badge/Status-Public_Showcase-emerald.svg)]()
[![Compliance](https://img.shields.io/badge/Privacy-GDPR_Art.9_%26_HIPAA-purple.svg)]()
[![Protocol](https://img.shields.io/badge/Standard-Model_Context_Protocol_(MCP)-orange.svg)]()
[![Architecture](https://img.shields.io/badge/Core-Snorbik_Sovereign_AI-grey.svg)]()

---

## 🎯 1. Why Bio-Atlas Exists & What Real Problem It Solves

In modern clinical oncology and medical genetics, interpreting High-Throughput Genomic Sequencing data (NGS `.vcf` files) and projecting mutations onto protein 3D structures is critical for targeted therapy selection. However, clinicians face three major bottlenecks:

1. **The Cloud Privacy & Legal Barrier :**  
   Under European GDPR (Article 9) and HIPAA regulations, clinicians are strictly forbidden from uploading patient names and genetic sequencing to cloud-based LLMs (e.g. ChatGPT, Claude).
2. **The Lethal Risk of LLM Hallucinations :**  
   Pure probabilistic text models predict words, not atomic stereochemistry. An AI that hallucinates molecular coordinates or drug dosages creates catastrophic medical and liability risks.
3. **The "Prompt Engineering" Rejection :**  
   Doctors do not have the time to copy-paste libraries of 40 complex prompts. The tool must operate deterministically with **zero prompt fatigue**.

**Bio-Atlas solves this** through a sovereign, local "Dual-Brain" architecture:
* **The Semantic Brain (AI Agent) :** Understands clinical intents and orchestrates tools.
* **The Deterministic Core (Sovereign MCP) :** Runs local irreversible anonymization, parses official RCSB PDB files and ClinVar records, and renders interactive 3D structures on a dedicated local web server (`http://localhost:8529/`).

---

## 🛡️ 2. How GDPR & Patient Privacy Are Enforced in Source Code

Patient data protection is not marketing rhetoric; it is physically enforced at the architectural layer:
* **Volatile RAM Destruction :** Upon patient intake, the patient's name (`raw_name`) is consumed into a one-way salted SHA-256 hash. The plain-text name is immediately dropped from memory and never returned in the response entity.
* **Irreversible Pseudonymization :** The system assigns a sealed identifier (`MED-ANON-[UUID8]`).
* **Zero PII Exposure :** Session states (`state.json`), audit logs, and AI context memories contain strictly zero Personally Identifiable Information (PII). No health data ever leaves the local machine.

---

## ⚡ 3. The "Zero-Prompt" Paradigm: How to Command Without Complex Prompts

Clinicians do not write code or multi-paragraph prompt instructions. Bio-Atlas offers 3 frictionless command channels:

* **Channel 1 — Single Clinical Intent (AI Voice / Chat) :**  
  The physician states: *"Run oncological screening on patient Dupont for TP53."*  
  The agent queries the `bio_medic_get_pipelines` compass tool and automatically executes the exact 8-step pipeline without human micromanagement.
* **Channel 2 — 1-Click Laboratory Pipeline (CLI) :**  
  ```bash
  # Execute the 5 gold standard benchmarks and launch the browser immediately
  python run_benchmarks.py --open
  ```
* **Channel 3 — Autonomous Interactive 3D Workstation (`http://localhost:8529/`) :**  
  The local web server starts automatically and opens the default browser. Clinicians interact via mouse controls (3D orbit rotation, wheel zoom onto the mutated residue) while real-time polling (`/api/latest`) updates metrics dynamically without manual reloads.

---

## 🔬 4. Two Real-World Clinical Scenarios

### Scenario 1: Dr. Sarah Benali (Medical Oncologist)
* **Clinical Case :** 42-year-old female patient with high-grade serous ovarian adenocarcinoma and suspected hereditary Li-Fraumeni syndrome.
* **Clinical Challenge :** Rapidly determine whether the *TP53* mutation disrupts the core DNA-binding domain.
* **Execution :** The VCF file is scanned under pseudonym `MED-ANON-705A0D`. Variant `c.742C>T` (`p.Arg248Trp`) is flagged as **Pathogenic** (ClinVar VCV000012347).
* **3D Output :** The official crystallographic structure `1TUP` (5,828 atoms) appears on screen. Mutated residue 248 is illuminated in bright red directly at the DNA major groove contact point, immediately ready for multidisciplinary team (MDT) presentation.

### Scenario 2: Dr. Marc Vanhove (Molecular Geneticist)
* **Clinical Case :** 64-year-old male with stage IV non-small cell lung adenocarcinoma (NSCLC).
* **Clinical Challenge :** Confirm the presence of activating mutation *EGFR L858R* in exon 21 to prescribe 3rd-generation tyrosine kinase inhibitors (Osimertinib).
* **Execution :** Automated background pipeline parses PDB `2ITY` (2,446 atoms) complexed with Gefitinib, mapping the leucine-to-arginine substitution in the activation loop.
* **Output :** Sealed clinical audit report `CLIN-REP-20261112-A99BBC.json` is archived for PACS/EMR integration with zero cloud data transmission.

---

## 📊 5. Gold Standard Clinical Benchmarks Suite (Verified RCSB PDB & ClinVar)

Bio-Atlas includes a deterministic test suite covering 5 landmark oncological mutations verified against official public repositories:

| Benchmark | Gene | Real Mutation (HGVS) | Pathology | PDB ID | Real ATOM Count | Source |
|---|---|---|---|---|---|---|
| **BENCH-01** | TP53 | p.Arg248Trp (c.742C>T) | Li-Fraumeni / Ovarian Cancer | 1TUP | 5,828 atoms | ClinVar VCV000012347 / RCSB |
| **BENCH-02** | BRAF | p.Val600Glu (c.1799T>A) | Metastatic Melanoma | 4MNE | 17,682 atoms | ClinVar VCV000013961 / RCSB |
| **BENCH-03** | EGFR | p.Leu858Arg (c.2573T>G) | NSCLC Lung Adenocarcinoma | 2ITY | 2,446 atoms | ClinVar VCV000016618 / RCSB |
| **BENCH-04** | KRAS | p.Gly12Asp (c.35G>A) | Pancreatic Ductal Adenocarcinoma | 4OBE | 5,725 atoms | ClinVar VCV000012582 / RCSB |
| **BENCH-05** | BRCA1| p.Glu23ValfsTer17 | Hereditary Breast & Ovarian Cancer | 1JNX | 1,660 atoms | ClinVar VCV000017662 / RCSB |

*All macromolecular structures are deterministically parsed from official .pdb files with verified SHA-256 provenance.*

---

## 🔌 6. Model Context Protocol (MCP) Architecture (8 Tools)

1. `bio_medic_get_pipelines` — Navigation compass guiding agent actions.
2. `bio_medic_patient_intake` — GDPR/HIPAA-compliant ingestion & SHA-256 pseudonymization.
3. `bio_medic_vcf_genomic_scan` — Variant filtering and ClinVar clinical impact scoring.
4. `bio_medic_pdb_structure_fetch` — Deterministic PDB parser and macromolecule indexer.
5. `bio_medic_3d_mutation_map` — 3D spatial mapping of mutated residues $(X, Y, Z)$.
6. `bio_medic_telemetry_digest` — Laboratory bench sensors and anomaly alerts.
7. `bio_medic_export_clinical_report` — Sealed diagnostic digest and JSON export.
8. `bio_medic_render_gui` — Dynamic bioStations interactive 3D WebGL workstation viewport (spawns autonomous live HTTP server at `http://localhost:8529/` with real-time polling and auto-browser launch).

---

## 🤖 7. AI Indexing & Machine Readability

This public repository is natively indexed for AI search engines, agents, and web scrapers:
* [**`llms.txt`**](./llms.txt) : Concise machine-readable summary following the LLMs.txt standard.
* [**`llms-full.txt`**](./llms-full.txt) : Exhaustive architectural overview and capability catalog.

---

## 🤝 8. R&D Collaboration & Inquiries

This project illustrates the research, development, and engineering capabilities of **SNORBIK Studio**.

- 🌐 **Portfolio & Case Studies :** [https://tayier.snorbik.com](https://tayier.snorbik.com)
- 📬 **Medical Engineering Inquiries :** contact@snorbik.com

---

© 2026 **SNORBIK Studio** — All rights reserved. Sovereign Biomedical AI Architecture.
