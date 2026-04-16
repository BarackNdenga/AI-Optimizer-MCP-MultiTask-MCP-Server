# AI Optimizer MCP 🧠🔧 - Multi-Task MCP Server

Développer par Barack Ndenga ♥️

[![PyPI version](https://badge.fury.io/py/ai-optimizer-mcp.svg)](https://badge.fury.io/py/ai-optimizer-mcp)
[![Tests](https://github.com/yourusername/ai-optimizer-mcp/actions/workflows/ci.yml/badge.svg)](https://github.com/yourusername/ai-optimizer-mcp/actions)
[![Coverage](https://img.shields.io/badge/coverage-90%25-brightgreen)](https://github.com/yourusername/ai-optimizer-mcp)

## Détails

**Multi-tâche MCP Server** pour VSCode/Cursor, CLI, agents autonomes. Optimisation code IA + tests + extensible.

- **Transports:** Stdio (VSCode), subprocess, HTTP (futur)
- **Use Cases:** VSCode chat, agent loops, CI/CD, remote servers
- **Sécurité:** Env vars, sandbox exec

## Manifeste (Multi-Task Capabilities)

- 🛠️ **3+ Tools:** Code test/optimize/objective (+extensibles)
- 🔌 **VSCode/Cursor:** mcp.json natif
- 🖥️ **CLI Standalone:** `ai-optimizer-mcp run`
- 🤖 **Agents:** examples/agent.py loop
- ⚙️ **Multi-Env:** Local/dev/prod via .env
- 📊 **Memory/History:** JSON persistent
- 🔄 **Boucles Itératives:** Auto-improve

## Configuration Multi-Plateforme

### 1. VSCode/Cursor (Recommandé)

Fichier `.vscode/mcp.json` (multi-servers):

```json
{
  "servers": {
    "ai-optimizer": {
      "command": "python",
      "args": ["-m", "ai_optimizer_mcp.server"]
    },
    "ai-optimizer-dev": {
      "command": "python",
      "args": ["-m", "ai_optimizer_mcp.cli", "run", "--dev"]
    }
  }
}
```

*Multi-task: Switch servers en chat!*

### 2. CLI / Scripts / Agents

```bash
ai-optimizer-mcp run  # Stdio server (pipes)
ai-optimizer-mcp run --dev  # Debug
ai-optimizer-mcp --install-mcp  # Print mcp.json
```

### 3. Agents Autonomes / Subprocess

```python
# examples/agent.py
import asyncio
from mcp.client.stdio import stdio_client

async def agent_loop():
    async with stdio_client(command=["python", "-m", "ai_optimizer_mcp.server"]) as client:
        # Multi-task calls
        score = await client.call_tool("run_tests", {"code_snippet": code})
        improved = await client.call_tool("generate_improvement", {"code": code, "test_result": score})
```

### Prérequis (.env)

```bash
cp .env.example .env
# OPENAI_API_KEY=sk-...
# OBJECTIVE="Your custom goal"
```

## Usage Multi-Tâche

1. **VSCode Chat:** `use_mcp_tool("ai-optimizer", "run_tests", ...)`
2. **CLI Pipe:** `echo code | ai-optimizer-mcp run`
3. **Agent Loop:** `python examples/agent.py`
4. **CI/CD:** Subprocess dans GitHub Actions/Jenkins

**Exemple Réponse Tool:**
```
run_tests → "Tests passed: score=4/4 (f(2)=4)"
generate_improvement → "def f(x): return 2 * x"
```

## Troubleshooting Multi-Env

- **VSCode:** Reload window après mcp.json
- **No API Key:** ValueError → Check .env
- **Timeout:** `TEST_TIMEOUT=10` in .env
- **Memory:** `rm memory.json`
- **Logs:** `--dev` ou `LOG_LEVEL=DEBUG`

## Développement

```bash
pip install -e .[dev]
pre-commit install
pytest
```

## Tools MCP (Extensibles)

| Tool                     | Args                      | Use Case                  |
|--------------------------|---------------------------|---------------------------|
| `run_tests`              | `code_snippet: str`       | VSCode/CLI test code      |
| `generate_improvement`   | `code, test_result`       | Auto-optimize             |
| `get_objective`          | -                         | Read goal any context     |

**Apache 2.0** - Multi-task ready! VSCode, CLI, Agents, CI. Contribute!

[CHANGELOG](CHANGELOG.md)
