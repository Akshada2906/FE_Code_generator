# FE Code Generator

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![Framework](https://img.shields.io/badge/framework-CrewAI%20%2F%20AAVA-orange)

## Overview

An AI-powered frontend code generation system built with **AAVA (Autonomous AI Agent Architecture)**.  
Accepts a GitHub repository URL, pulls the source files, analyzes the structure, and generates frontend code using a multi-agent pipeline built on CrewAI.

## Features

- Pulls files from any public GitHub repository (no auth needed)
- Recursive directory cloning into a local workspace
- Auto-detects default branch (main / master / custom)
- AI agent pipeline for code analysis and generation
- Security-hardened tool: path traversal protection, SSRF prevention, atomic writes

## Project Structure

```
FE_Code_generator/
├── github_tool.py       # GitHubPublicRepoCloner — CrewAI tool
├── agent.py             # AAVA agent definitions (crew + tasks)
├── main.py              # Entry point
├── requirements.txt
├── .env.example         # GITHUB_TOKEN (optional)
└── workspace/           # Cloned repo files land here
```

## Quick Start

### 1. Clone this repo

```bash
git clone https://github.com/Akshada2906/FE_Code_generator.git
cd FE_Code_generator
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Set environment variables (optional)

```bash
cp .env.example .env
# Add GITHUB_TOKEN=your_token   ← avoids GitHub rate limits
```

### 4. Run

```bash
python main.py --repo https://github.com/owner/repo
```

## How It Works

1. Agent receives a GitHub repo URL
2. `GitHubPublicRepoCloner` tool fetches all files into `./workspace/`
3. Analyzer agent reads the file structure
4. Code generator agent produces frontend output

## Requirements

```
crewai
requests
pydantic
python-dotenv
```

## Security

- Public repos only — no private repo access
- Path traversal protection on all inputs
- SSRF prevention via domain whitelist
- Atomic file writes (TOCTOU-safe)
- Optional `GITHUB_TOKEN` via env var — never hardcoded

## License

MIT
