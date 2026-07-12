# CCA-F Prep Workspace

## Purpose
Hands-on practice and notes for Anthropic CCA-F certification.

## Structure
- docs/ → notes and summaries
- src/ → reusable Python scripts
- exercises/ → course exercises
- outputs/ → generated outputs

## Setup

Requires **Python 3.12.x** and Git. Full instructions (macOS/Linux, troubleshooting,
running Jupyter) are in [`docs/SETUP.md`](docs/SETUP.md).

Quick start (Windows PowerShell):

```powershell
git clone git@github.com:jisujit/cca-f-prep.git
cd cca-f-prep

python -m venv venv
.\venv\Scripts\Activate.ps1        # macOS/Linux: source venv/bin/activate

pip install -r requirements.txt    # or requirements.lock.txt for exact versions

copy .env.example .env             # then paste your ANTHROPIC_API_KEY
python src/test_env.py             # verify
```

`venv/` and `.env` are gitignored, so they're rebuilt locally from
`requirements.txt` and `.env.example`.

### Using an IDE

Activating the venv (above) is only needed for the CLI. In an IDE you instead
point it at the same interpreter (`venv/Scripts/python.exe` on Windows,
`venv/bin/python` on macOS/Linux) once:

- **VS Code / Cursor / Antigravity** (and other VS Code forks): the committed
  [`.vscode/settings.json`](.vscode/settings.json) makes the Python extension
  auto-detect `venv/` on any OS and auto-activate it in the integrated terminal —
  no manual step. If it isn't picked up, run Command Palette → **Python: Select
  Interpreter** and choose the `./venv` entry.
- **PyCharm**: `Settings → Project → Python Interpreter → Add → Existing` and
  point at the venv interpreter (PyCharm uses its own config, not `.vscode/`).

See [`docs/SETUP.md`](docs/SETUP.md) for the full explanation.

## Environment
Python venv used for isolation. Dependencies are pinned in `requirements.txt`
(direct deps) and `requirements.lock.txt` (full snapshot for exact reproduction).