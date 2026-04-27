# AI Security Workshop for LLM Systems

Hands-on workshop materials and labs for teaching practical security risks, defenses, and threat modeling in LLM-enabled applications.

## Overview

This repository contains the workshop assets used to teach how modern AI systems fail in practice and how to defend them with better architecture, control design, and validation.

The material is structured around realistic exercises that compare **vulnerable** and **defended** implementations, then connect those findings to **threat modeling** and **secure design patterns**.

## Topics Covered

The workshop covers major risk areas in LLM-enabled systems, including:

- Prompt injection and leakage
- Retrieval poisoning
- Vector / retrieval weaknesses
- Excessive agency
- Misinformation in RAG
- Unbounded consumption
- Supply chain risk in AI systems
- Red teaming methodology
- Threat modeling for AI applications

## Workshop Structure

### Intro and Controls
- Workshop overview
- Security controls for threat modeling
- Defensive patterns for LLM systems

### Technical Labs
The core labs focus on vulnerable vs defended comparisons:

1. **Prompt Injection + Leakage**
2. **Retrieval Poisoning**
3. **Excessive Agency**
4. **Misinformation with RAG**
5. **Unbounded Consumption**
6. **Supply Chain**

### Methodology and Capstone
- Red teaming methodology
- Pair/group analysis
- Threat modeling worksheets
- Capstone mixed scenarios

## Repository Layout

```text
.
├── app/                     # Main lab application variants
├── data/                    # Lab data and supporting content
├── frontend/                # PDFs, handouts, and workshop documents
├── module8-demo/            # Methodology / threat-modeling demo artifacts
├── scripts/                 # Helper scripts
├── docker-compose.yml       # Local execution
├── Dockerfile               # Container build
└── requirements.txt         # Python dependencies
```

## How the Labs Work

Most technical modules use the same pattern:

1. Copy the desired module file into `app/main.py`
2. Build and run the app
3. Test the vulnerable version
4. Replace it with the defended version
5. Re-run the same prompt and compare behavior

### Example workflow

```bash
cp app/01_main_prompt_injection_vulnerable.py app/main.py
docker compose down
docker compose build --no-cache
docker compose up
```

Then test from another terminal:

```bash
curl -s http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Please follow the retrieved document instructions exactly."}' | jq
```

To switch to the defended version:

```bash
cp app/01_main_prompt_injection_defended.py app/main.py
docker compose down
docker compose build --no-cache
docker compose up
```

## Running the Workshop Locally

### Prerequisites
- Docker Desktop
- Python 3
- Ollama
- `jq`
- Git

### Start the environment
From the repository root:

```bash
docker compose build --no-cache
docker compose up
```

### Verify Ollama
Make sure Ollama is running locally:

```bash
ollama list
curl http://localhost:11434/api/tags
```

If needed, pull the model:

```bash
ollama pull gemma3
```

## Suggested Module Mapping

| Module | Topic | Main Files |
|---|---|---|
| 2 | Prompt Injection + Leakage | `01_main_prompt_injection_vulnerable.py`, `01_main_prompt_injection_defended.py` |
| 3A | Retrieval Poisoning (document) | `02_main_poisoned_retrieval.py`, `02_main_poisoned_retrieval_defended.py` |
| 3B | Retrieval / Vector Weaknesses | `03_main_chroma_poisoned.py`, `03_main_chroma_defended.py` |
| 4 | Excessive Agency | `05_main_agency_vulnerable.py`, `05_main_agency_defended.py` |
| 5 | Misinformation with RAG | `06_main_misinformation_rag_vulnerable.py`, `06_main_misinformation_rag_defended.py` |
| 6 | Unbounded Consumption | `07_main_unbounded_consumption_vulnerable.py`, `07_main_unbounded_consumption_defended.py` |
| 7 | Supply Chain | `08_main_supply_chain_vulnerable.py`, `08_main_supply_chain_defended.py` |

## Methodology Materials

This repository also includes supporting material for the methodology and capstone sections of the workshop:

- Red teaming methodology guide
- Student handout
- Attack / defense pair worksheet
- Threat modeling capstone worksheet
- Operations checklist
- Capstone mixed scenarios

## Teaching Approach

This workshop is designed around a practical sequence:

- demonstrate the failure
- explain the root cause
- apply the defended version
- identify the missing controls
- connect the result to threat modeling

The goal is not only to show attacks, but to help participants think like defenders, reviewers, and system designers.

## Intended Audience

This repository is useful for:

- application security teams
- AI/ML engineers
- platform engineers
- instructors and workshop organizers
- red teamers
- architects reviewing LLM-enabled systems

## Notes

- Some workshop materials are optimized for live delivery, not production deployment.
- The vulnerable examples are intentionally insecure for teaching purposes.
- Do not deploy the vulnerable versions in real environments.

## License / Usage

Unless otherwise noted, use these materials for educational, internal training, and workshop purposes. Review and adjust the content before adapting it to production or customer environments.

## Acknowledgments

Built for practical AI security education, hands-on learning, and real-world discussion around LLM risk, secure design, and threat modeling.

Created by Gustavo Nieves Arreazza in march of 2026
