# 🚀 Phase 0 — Python + uv + Git Cheat Sheet

A quick reference guide for setting up and managing Python projects with **uv** and **Git**.

---

## 📑 Table of Contents

1. [Standard Project Structure](#1-️-standard-project-structure)
2. [Starting a New Python Project](#2--starting-a-new-python-project)
3. [Dependencies](#3--dependencies)
4. [Running Python](#4-️-running-python)
5. [Virtual Environment](#5--virtual-environment)
6. [Important Files](#6--important-files)
7. [.gitignore](#7--gitignore)
8. [.env vs .env.example](#8--env-vs-envexample)
9. [Git Basics](#9--git-basics)
10. [GitHub](#10--github)
11. [Cloning an Existing uv Project](#11--cloning-an-existing-uv-project)
12. [uv Commands Reference](#12--uv-commands-reference)
13. [Git Commands Reference](#13--git-commands-reference)
14. [Everyday Workflow](#14--everyday-workflow)
15. [Mental Model](#15--mental-model)
16. [7 Things to Memorize](#-7-things-to-memorize)
17. [30-Second Revision](#-30-second-revision)

---

## 1. 🏗️ Standard Project Structure

```text
my-ai-project/
│
├── src/
│   └── my_ai_project/
│       ├── __init__.py
│       └── main.py
│
├── tests/
│
├── .env.example
├── .gitignore
├── .python-version
├── README.md
├── pyproject.toml
└── uv.lock
```

**Local-only files** — never commit these:

| File / Folder | Reason |
|---------------|--------|
| `.venv/` | Local isolated environment |
| `.env` | Contains real secrets |
| `.git/` | Managed by Git itself |

---

## 2. 🐍 Start a New Python Project

```bash
mkdir my-project
cd my-project

uv init
uv sync
```

---

## 3. 📦 Dependencies

| Task | Command |
|------|---------|
| Add package | `uv add requests` |
| Remove package | `uv remove requests` |
| Sync environment | `uv sync` |
| View dependencies | `cat pyproject.toml` |

---

## 4. ▶️ Run Python

```bash
# Recommended
uv run python src/main.py

# Run a module
uv run python -m my_ai_project.main

# Run tests
uv run pytest
```

---

## 5. 🧪 Virtual Environment

**Created by:**

```bash
uv sync
```

**Creates:** `.venv/`

**Activate manually:**

```bash
source .venv/bin/activate
which python
python --version
deactivate
```

**Or skip activation entirely:**

```bash
uv run python src/main.py
```

> 💡 `.venv` is the project's isolated Python environment.

---

## 6. 📄 Important Files

### `pyproject.toml`

- Project configuration
- Dependencies
- Python requirement
- Project metadata
- Tool configuration

> **Think:** *What does my project need?*

### `uv.lock`

- Exact resolved dependency versions
- Dependency graph
- Reproducible environment

> **Think:** *What exactly should be installed?*

✅ **Commit it.**

❌ **Don't manually edit it.**

### `.python-version`

Example:

```text
3.13
```

> **Think:** *Which Python version does this project use?*

### `README.md`

Should explain:

- What is the project?
- How to install?
- How to run?
- How to configure?
- How is it structured?

---

## 7. 🚫 .gitignore

Your project `.gitignore` should commonly contain:

```gitignore
.venv/
.env
__pycache__/
*.pyc
.DS_Store
```

> **Remember:**
>
> - `project/.gitignore` ← **you manage**
> - `.venv/.gitignore` ← leave alone
> - global Git ignore ← leave alone for project rules

---

## 8. 🔐 .env vs .env.example

### `.env` — Real secrets

❌ **NEVER commit.**

```env
OPENAI_API_KEY=real-secret
DATABASE_URL=real-url
```

### `.env.example` — Template

✅ **Commit.**

```env
OPENAI_API_KEY=
DATABASE_URL=
```

> `.env` → real secrets
>
> `.env.example` → required variables / template

---

## 9. 🌿 Git Basics

```bash
git status                # Check changes
git add .                 # Stage
git commit -m "feat: ..." # Commit
git push                  # Push
git pull                  # Pull
git log --oneline         # View commits
```

---

## 10. 🌐 GitHub

```bash
# Clone a repo
git clone <repo-url>
cd <project>

# Connect an existing local repo
git remote add origin <repo-url>
git remote -v

# Push
git push -u origin main
```

After the first push:

```bash
git push
```

---

## 11. 🔄 Clone an Existing uv Project

```bash
git clone <repo-url>
cd <project>
uv sync

uv run python src/main.py
```

**Mental model:**

```text
GitHub
   ↓
git clone
   ↓
pyproject.toml + uv.lock + .python-version
   ↓
uv sync
   ↓
NEW .venv
   ↓
uv run
```

> You don't need the original developer's `.venv`.

---

## 12. 🆚 uv Commands

| Command | Meaning |
|---------|---------|
| `uv init` | Create Python project |
| `uv add package` | Add dependency |
| `uv remove package` | Remove dependency |
| `uv sync` | Sync / create environment |
| `uv run ...` | Run inside project environment |
| `uv lock` | Update / resolve lockfile |
| `uv --version` | Check uv version |
| `uv python list` | List available Python versions |

---

## 13. 🆚 Git Commands

| Command | Meaning |
|---------|---------|
| `git status` | See changes |
| `git add .` | Stage changes |
| `git commit` | Create snapshot |
| `git push` | Upload commits |
| `git pull` | Get latest changes |
| `git clone` | Download repository |
| `git log` | View history |
| `git remote -v` | View remote repository |

---

## 14. 🔥 Everyday Workflow

### Start work

```bash
cd my-project
git pull
uv sync
```

### During development

```bash
uv run python src/main.py
```

Add a package when needed:

```bash
uv add <package>
```

### Finish work

```bash
git status
git add .
git commit -m "feat: ..."
git push
```

---

## 15. 🧠 Mental Model

```text
                PROJECT
                   │
          ┌────────┴────────┐
          ↓                 ↓
 pyproject.toml          .python-version
          │
          ↓
       uv add
          │
          ↓
       uv.lock
          │
          ↓
       uv sync
          │
          ↓
        .venv
          │
          ↓
       uv run
          │
          ↓
       YOUR CODE
          │
          ↓
         Git
          │
    ┌─────┴─────┐
    ↓           ↓
  commit       push
                  ↓
               GitHub
```

---

## ⭐ 7 Things to Memorize

| # | File | Purpose |
|---|------|---------|
| 1 | `pyproject.toml` | Project configuration + dependencies |
| 2 | `uv.lock` | Locked dependency resolution |
| 3 | `.python-version` | Python version |
| 4 | `.venv` | Local isolated environment |
| 5 | `.gitignore` | What Git should ignore |
| 6 | `.env` | Real secrets — **NEVER commit** |
| 7 | `.env.example` | Secret / config template — safe to commit |

---

## 🚀 30-Second Revision

```bash
# New project
uv init
uv add <package>
uv sync
uv run python ...

# Existing project
git clone <repo>
cd <project>
uv sync
uv run python ...

# Daily Git
git pull
# work
git status
git add .
git commit -m "..."
git push
```

---

## 🏆 Golden Rule

> **`pyproject.toml`** says what the project needs →
>
> **`uv.lock`** locks the resolution →
>
> **`.venv`** contains the local environment →
>
> **`uv run`** executes using it →
>
> **Git** tracks the project →
>
> **`.gitignore`** keeps local / generated / secrets out.

---

# 🧠 Python/AI Project Structure — Quick Revision

When you open a Python project, think in **5 categories**:

```text
PROJECT
│
├── 💻 CODE
│   └── src/
│
├── 🧪 TESTS
│   └── tests/
│
├── ⚙️ CONFIG
│   ├── pyproject.toml
│   ├── uv.lock
│   └── .python-version
│
├── 📚 DOCUMENTATION / GIT / SECRETS
│   ├── README.md
│   ├── .gitignore
│   └── .env.example
│
└── 🔒 LOCAL ONLY
    ├── .env
    ├── .venv/
    └── .git/
```

## 🔥 What each one means

| File / Folder | Remember it as | Commit? |
|---------------|----------------|---------|
| `src/` | 💻 My code | ✅ |
| `tests/` | 🧪 Test my code | ✅ |
| `pyproject.toml` | ⚙️ Project configuration + dependencies | ✅ |
| `uv.lock` | 🔒 Exact dependency resolution | ✅ |
| `.python-version` | 🐍 Python version | ✅ |
| `README.md` | 📚 How/what is this project? | ✅ |
| `.gitignore` | 🚫 Don't track these files | ✅ |
| `.env.example` | 🔑 What environment variables are needed? | ✅ |
| `.env` | 🔐 Actual secrets | ❌ |
| `.venv/` | 🐍 Local Python environment | ❌ |
| `.git/` | 🌳 Git's internal history | ❌ |

## 📁 The structure to remember

```text
my-ai-project/
│
├── src/
│   └── my_ai_project/
│       ├── __init__.py
│       └── main.py
│
├── tests/
│
├── .env.example
├── .gitignore
├── .python-version
├── README.md
├── pyproject.toml
└── uv.lock
```

**Locally:**

```text
.venv/   ← generated, don't commit
.env     ← real secrets, don't commit
.git/    ← Git internals, don't commit
```

## 🧠 10-Second Memory Trick

```text
src/              → CODE
tests/            → TEST
pyproject.toml    → PROJECT
uv.lock           → LOCK
.python-version   → PYTHON
README.md         → DOCS
.gitignore        → IGNORE
.env.example      → TEMPLATE
.env              → SECRET ❌
.venv/            → ENVIRONMENT ❌
.git/             → GIT ❌
```

## The golden rule

> Start with the small structure. Add `agents/`, `tools/`, `services/`, `models/`, `docs/`, `scripts/`, `Dockerfile`, etc. **only when your project actually needs them.**

That's the clean-project mindset you want to carry into your AI engineering journey.