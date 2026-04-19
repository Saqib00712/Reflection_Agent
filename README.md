# Reflection_Agent
Built a self-improving AI agent using LangGraph's graph-based workflow that generates content, critiques its own output, and iteratively refines it through a reflection loop. Applied to a LinkedIn post generator — the agent runs 3 iterations of Generate → Reflect → Regenerate using conditional routing and MessageGraph state management.



# Reflection Agent with LangGraph
> A self-improving AI agent that generates, critiques, and refines its own outputs through iterative feedback loops — built with LangGraph and IBM Granite LLM.

---

## What is Reflection?

Reflection is a prompting strategy where an AI agent **pauses, reviews, and critiques its own output** before finalizing it. This mimics how humans write, review, and improve their work.

Think of it as two systems working together:

| System | Behavior |
|--------|----------|
| **System 1** — Generator | Reactive, produces a quick first draft |
| **System 2** — Reflector | Deliberate, critiques and refines the draft |

The result is higher-quality, more polished AI output through iteration.

---

## Demo

**Task:** Generate a LinkedIn post announcing a job promotion.

**First Draft (System 1):**
```
"Excited to share that I've been promoted to Engineering Manager!"
```

**After Reflection (System 2):**
```
"Thrilled to share that I've been promoted to Engineering Manager at [Company]!
Grateful for the mentorship, team collaboration, and opportunities that led here.
Looking forward to leading new initiatives. #Leadership #CareerGrowth"
```

---

## Workflow

```
User Input
    ↓
[Generate Node] → produces initial draft
    ↓
Should continue?
   ├── YES (< 6 messages) → [Reflect Node] → critique & feedback → back to Generate
   └── NO  (> 6 messages) → Final Output
```

The agent runs **3 full iterations** (generate → reflect → generate → reflect → generate → end), each time improving the output based on the previous critique.

| Iteration | Node | Action |
|-----------|------|--------|
| 1 | Generate | Produces first draft |
| 1 | Reflect | Critiques tone, clarity, engagement |
| 2 | Generate | Revises based on feedback |
| 2 | Reflect | Suggests further improvements |
| 3 | Generate | Produces final polished output → END |

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square)
![LangGraph](https://img.shields.io/badge/LangGraph-0.3.31-teal?style=flat-square)
![LangChain](https://img.shields.io/badge/LangChain-0.3.23-green?style=flat-square)
![IBM Granite](https://img.shields.io/badge/IBM-Granite%20LLM-black?style=flat-square)

- **LangGraph** — `MessageGraph` for stateful agent workflow
- **LangChain** — Prompt templates, message types, chain composition
- **IBM Granite** (`granite-3-2-8b-instruct`) — Core language model via WatsonX
- **ChatWatsonx** — IBM WatsonX LLM integration

---

## Project Structure

```
Reflection-Agent/
│
├── reflection_agent.ipynb    # Full implementation notebook
├── requirements.txt          # All dependencies
├── .env.example              # API key template (for local use)
└── README.md
```

---

## Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/Saqib00712/Building-AI-Agents-and-Agentic-Workflows.git
cd Building-AI-Agents-and-Agentic-Workflows
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up API keys (only needed if running locally outside IBM Skills Network)
```bash
cp .env.example .env
```
Edit `.env` and add your keys:
```
WATSONX_API_KEY=your_watsonx_api_key_here
WATSONX_PROJECT_ID=your_project_id_here
```

### 4. Run the notebook
```bash
jupyter notebook reflection_agent.ipynb
```

> **Note:** If running inside IBM Skills Network JupyterLab, no API keys are needed — the environment is pre-configured.

---

## Key Concepts Covered

- **Reflection prompting** — how agents critique and improve their own outputs
- **MessageGraph** — LangGraph's prebuilt stateful graph for conversational workflows
- **Generation node** — producing an initial AI response from a prompt chain
- **Reflection node** — critiquing output and returning feedback as `HumanMessage`
- **Conditional edges** — routing logic that decides when to stop iterating
- **Chain composition** — linking prompt templates to LLMs using the `|` pipe operator

---

## Why HumanMessage for Reflection?

The reflection node returns feedback as a `HumanMessage` — not an `AIMessage`. This is intentional: the feedback is treated as if it comes from a human reviewer, which tells the generation agent to treat it as a new instruction and revise accordingly. This is what drives the iterative improvement loop.

---

## Example Use Case

**Input:**
```
Write a LinkedIn post on getting a software developer job at IBM under 160 characters.
```

**Final Output after 3 reflection iterations:**
A polished, engagement-optimized LinkedIn post with strong call-to-action, relevant hashtags, and professional tone — significantly better than the first draft.

---

## Related Certifications

Built as part of the IBM **Building AI Agents and Agentic Workflows Specialization** on Coursera.

[![IBM Badge](https://img.shields.io/badge/IBM-AI%20Agents%20Specialization-blue?style=flat-square)](https://www.credly.com/users/muhammad-saqib.361f9b8c)

---

## Author

**Muhammad Saqib**
- GitHub: [@Saqib00712](https://github.com/Saqib00712)
- LinkedIn: [muhammad-saqib](https://www.linkedin.com/in/muhammad-saqib-68b9b3374/)
- Email: saqibkhosa649@gmail.com
- Credly: [15x IBM Certified](https://www.credly.com/users/muhammad-saqib.361f9b8c)
