# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This is a hands-on prep workspace for the **CCA-F (Claude Certified Architect — Foundations)** certification. Scripts, exercises, and notes are organized to support working through the [official Anthropic API course](https://anthropic.skilljar.com/claude-with-the-anthropic-api).

## Environment Setup

Python 3.12.4 venv is already created at `venv/`. Activate it before running scripts:

```powershell
# Windows PowerShell
.\venv\Scripts\Activate.ps1

# Verify
python src/test_env.py
```

Key packages already installed: `anthropic==0.86.0`, `python-dotenv`, `httpx`, `pydantic`, Jupyter stack.

To add new packages:
```powershell
pip install <package>
```

## Running Scripts

```powershell
# Run a script
python src/<script>.py

# Launch Jupyter for notebook exercises
jupyter notebook
```

## API Key Setup

Scripts use `python-dotenv` to load a `.env` file (gitignored). Create one at the repo root:

```
ANTHROPIC_API_KEY=sk-ant-...
```

## Exam Topic Areas (for organizing exercises)

1. Agentic Architecture & Orchestration (27%)
2. Prompt Engineering & Structured Output (20%)
3. Claude Code Configuration & Workflows (20%)
4. Tool Design & MCP Integration (18%)
5. Context Management & Reliability (15%)

New exercises go in `exercises/`, reusable helpers in `src/`, generated outputs in `outputs/`.
