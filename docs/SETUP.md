# Machine Setup — recreating the CCA-F prep environment

This guide reproduces the exact working environment on a **new machine** from a fresh
clone. The repo tracks the *code* and *config*, but two things are intentionally **not**
in git and must be recreated locally:

| Not in git (gitignored) | Why | How to recreate |
| --- | --- | --- |
| `venv/` | Virtual environments aren't portable across machines/OSes | Rebuild from `requirements.txt` (steps below) |
| `.env` | Contains your secret API key | Copy `.env.example` → `.env` and paste your key |

**Prerequisite:** Python **3.12.x** (original machine used 3.12.4) and Git.
Check with `python --version` and `git --version`.

---

## Quick start

### Windows (PowerShell)

```powershell
# 1. Clone
git clone git@github.com:jisujit/cca-f-prep.git
cd cca-f-prep

# 2. Create the virtual environment
python -m venv venv

# 3. Activate it  (note: you may need to allow scripts once — see Troubleshooting)
.\venv\Scripts\Activate.ps1

# 4. Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

# 5. Set up your API key
copy .env.example .env
notepad .env            # replace the placeholder with your real key

# 6. Verify
python src/test_env.py
```

### macOS / Linux (bash/zsh)

```bash
git clone git@github.com:jisujit/cca-f-prep.git
cd cca-f-prep

python3 -m venv venv
source venv/bin/activate

python -m pip install --upgrade pip
pip install -r requirements.txt

cp .env.example .env
$EDITOR .env            # replace the placeholder with your real key

python src/test_env.py
```

A successful run prints the venv's Python path and `Environment is working cleanly`.

---

## Running things

```powershell
# Activate first (every new terminal session)
.\venv\Scripts\Activate.ps1        # Windows
# source venv/bin/activate         # macOS/Linux

# Run a script
python src/<script>.py

# Launch Jupyter for the notebooks (e.g. 01_making_a_request.ipynb)
jupyter lab                        # opens in your browser
```

When choosing a kernel inside Jupyter, pick the one pointing at this project's `venv`.

---

## Verify the API key works end-to-end

```powershell
python -c "import os; from dotenv import load_dotenv; load_dotenv(); print('Key loaded:', bool(os.getenv('ANTHROPIC_API_KEY')))"
```

Prints `Key loaded: True` when `.env` is set up correctly.

---

## Troubleshooting

**PowerShell: "running scripts is disabled on this system"** (blocks `Activate.ps1`)
Run once, per user (safe, non-admin):
```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

**Wrong Python version** — `python -m venv` uses whatever `python` resolves to. If you have
multiple versions, target 3.12 explicitly, e.g. on Windows with the launcher:
```powershell
py -3.12 -m venv venv
```

**`ModuleNotFoundError`** — the venv isn't activated, or deps aren't installed. Re-activate
and re-run `pip install -r requirements.txt`.

**Git asks for a password / SSH fails** — this repo's remote is SSH
(`git@github.com:jisujit/cca-f-prep.git`). Make sure the new machine has an SSH key added to
your GitHub account (`ssh -T git@github.com` should greet you by username). If you'd rather
use HTTPS on that machine:
```powershell
git remote set-url origin https://github.com/jisujit/cca-f-prep.git
```

---

## Keeping `requirements.txt` current

`requirements.txt` lists the **direct** packages, pinned. When you `pip install` something
new that you want on other machines, add it there.

To capture a **complete, exact** snapshot of everything installed (including transitive
dependencies) as a lock file:

```powershell
pip freeze > requirements.lock.txt
```

Then on another machine, `pip install -r requirements.lock.txt` reproduces the environment
byte-for-byte. (`requirements.txt` stays the human-friendly source of truth; the lock file is
the exact reproduction.)
