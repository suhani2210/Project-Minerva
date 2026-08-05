# Pandemic Vaccine Diplomacy – Multi-Agent Simulation

A notebook-based simulation of pandemic response using multiple autonomous countries. Each country must balance domestic survival, vaccine production, diplomacy, and resource management while interacting with other countries through public pledges and private actions.

This project was developed as part of the BCS Summer Project (Week 6) on Agentic AI.

---

## Overview

The simulation models a pandemic spreading across multiple countries. Every round:

1. Countries attempt to contain the outbreak.
2. Failed containment creates new infections.
3. Existing infections eventually lead to deaths if untreated.
4. Vaccine production scales with remaining population.
5. A deterministic ranking identifies the country in greatest need.
6. Other countries publicly pledge vaccine support.
7. Countries privately decide how to allocate vaccines.
8. Public pledges are compared against actual deliveries to detect deception.

Agents can be powered by either:
- Groq LLMs (recommended)
- A heuristic fallback when no API key is available

---

## Environment Model

Each country maintains:

- Population
- Capital
- Vaccine Stockpile
- Infrastructure Rating
- Maximum Production Rate
- Active Infection Queue

Production follows

```
R = R_max × (Current Population / Initial Population)
```

meaning countries that lose population gradually lose manufacturing capacity.

---

## Actions Available

Every round an agent may allocate vaccines toward:

- Cure infected citizens
- Export vaccines
- Gift vaccines
- Sell vaccines for capital

Public pledges are independent from actual allocations, allowing cooperative or deceptive behaviour.

---

## Simulation Flow

```
Containment Roll
        │
        ▼
New Infections
        │
        ▼
Deaths (after D rounds)
        │
        ▼
Production Update
        │
        ▼
Adversity Ranking
        │
        ▼
Public Pledges
        │
        ▼
Private Allocation
        │
        ▼
Resolve Trades & Aid
        │
        ▼
Deception Detection
        │
        ▼
Log Results
```

---

## Configuration

Important parameters can be modified from the configuration section of the notebook.

| Parameter | Description |
|-----------|-------------|
| NUM_ROUNDS | Number of simulation rounds |
| K | New infections after containment failure |
| D | Survival period before untreated infections become deaths |
| RANDOM_SEED | Reproducibility |
| COUNTRIES | Initial country configuration |
| GROQ_MODEL | Groq model used for LLM agents |

---

## Running

### Install dependencies

```bash
pip install -r requirements.txt
```

### (Optional) Configure Groq

Create a `.env` file

```env
GROQ_API_KEY=your_api_key_here
```

If no API key is provided, the simulation automatically falls back to heuristic agents.

---

## Output

The notebook produces

- Round-by-round simulation logs
- Public pledges
- Actual vaccine deliveries
- Deception detection
- Population changes
- Vaccine production updates
- Final simulation history as a Pandas DataFrame

---

## Project Structure

```
.
├── Pandemic_Vaccine_Diplomacy.ipynb
├── requirements.txt
└── README.md
```

---

## Technologies Used

- Python
- Pandas
- Groq API
- python-dotenv
- Jupyter Notebook

---

## Notes

- The simulation is intentionally lightweight and focuses on multi-agent interaction rather than epidemiological realism.
- LLM agents and heuristic agents share the same environment, making behaviour easy to compare.
- All simulation parameters are configurable from the notebook.