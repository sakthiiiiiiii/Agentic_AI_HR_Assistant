# HR Assistant

An agentic AI HR assistant built with LangGraph, Retrieval-Augmented Generation (RAG), and tool calling to answer HR policy questions, validate leave and reimbursement requests, calculate allowances, and explain decisions using employee handbook context.

## Overview

This project provides an HR assistant that can:

- Answer employee questions using the company handbook as the source of truth
- Route questions to the right workflow: policy lookup, HR actions, or out-of-scope requests
- Use tool-based validation for leave requests, reimbursement claims, payroll deadlines, probation dates, and allowance calculations
- Explain decisions using handbook references and policy logic
- Trace runs with LangSmith when enabled

## Features

- RAG-powered policy Q&A grounded in the employee handbook PDF
- LangGraph workflow for routing and multi-step reasoning
- Tool calling for operational HR checks and calculations
- Deterministic answers for policy and validation scenarios
- Support for LangSmith tracing and session tracking

## Repository structure

```text
.
├── app.py                     # CLI entry point for the HR assistant
├── langgraph.json            # LangGraph app configuration
├── pyproject.toml            # Python project metadata and dependencies
├── requirements.txt          # Core install requirements
├── data/
│   └── PROITBRIDGE_Employee_Handbook_2026_1.pdf
├── src/
│   ├── __init__.py
│   ├── assistant.py          # Assistant wrapper around the LangGraph app
│   ├── config.py             # Environment variables and application settings
│   ├── edges.py              # Routing and decision logic between graph steps
│   ├── graph.py              # LangGraph workflow definition
│   ├── nodes.py              # Graph nodes for retrieval, tool use, and responses
│   ├── prompts.py            # LLM prompts used by the assistant
│   ├── rag.py                # Retrieval and embedding logic
│   ├── state.py              # LangGraph state schema
│   └── tools.py              # HR validation and calculation tools
├── .env.example              # Example environment variables (if present in your local setup)
├── .gitignore
├── .python-version
├── README.md
└── uv.lock
```

## Tech stack

- Python 3.11+
- LangGraph
- LangChain
- LangSmith
- OpenAI API
- pypdf for handbook ingestion

## Prerequisites

Before running the app, you need:

- Python 3.11 or newer
- An OpenAI API key
- Access to the employee handbook PDF in `data/PROITBRIDGE_Employee_Handbook_2026_1.pdf`

## Setup

1. Clone the repository:

```bash
git clone https://github.com/sakthiiiiiiii/Agentic_AI_HR_Assistant.git
cd Agentic_AI_HR_Assistant
```

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate   # Linux/macOS
# .venv\Scripts\activate    # Windows
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

Or using uv:

```bash
uv sync
```

4. Create a `.env` file in the project root with your credentials:

```env
OPENAI_API_KEY=your_openai_api_key
LANGSMITH_TRACING=false
LANGSMITH_API_KEY=your_langsmith_key_if_needed
LANGSMITH_PROJECT=default
```

## Run the app

```bash
python app.py
```

The app will prompt you with questions like:

- Can I take 4 days of casual leave in a row?
- How much earned leave will I accrue after 6 months?
- When does my probation end if I joined 2026-01-01?
- What is my remote-first internet allowance?
- Is my reimbursement claim valid if I submitted it 12 days after returning?

## Example workflows

### Policy question

The assistant reads from the employee handbook and answers grounded policy questions such as:

- What is the casual leave policy?
- What are the travel reimbursement rules?
- What is the payroll cut-off date?

### HR action validation

The assistant invokes tools to validate concrete employee requests, for example:

- leave request approval or rejection
- reimbursement claim validity
- earned leave accrual calculation
- payroll deadline checks
- travel allowance calculations

## LangGraph configuration

The project includes a `langgraph.json` file so it can be run with the LangGraph tooling:

```bash
langgraph dev
```

or

```bash
langgraph up
```

## Notes

- The assistant is built to be grounded in the employee handbook PDF, not to answer from memory alone.
- For accurate results, keep the handbook file in `data/` and ensure the `.env` file contains the required API keys.
- LangSmith tracing is optional and can be enabled by setting `LANGSMITH_TRACING=true`.

## License

This project is provided as-is for educational and demonstration purposes.

## Author

Built for PROITBRIDGE HR use cases and designed to showcase an agentic AI HR assistant using LangGraph and RAG.
