# Learning Log & Personal Cheat Sheet

A growing reference of tips, shortcuts, and workflows learned while building this project.

---

## Editor & WSL

### How to reopen a project quickly
- **Shortcut inside the editor:** Press `Ctrl+R` (**Open Recent**) and pick `satisfaccion-aerolinea [WSL: ...]` from the list.
- **From the menu:** `File` → `Open Recent`.
- **From a WSL terminal:**
  ```bash
  cd ~/proyectos/satisfaccion-aerolinea
  code .
  ```
- **Tip:** When reopening a WSL project, pick the entry that shows **`[WSL: ...]`** so it opens inside Linux instead of through the slow Windows path.

### Windows vs. WSL extensions
- Opening a folder in **WSL** does **not** delete your Windows extensions — they stay installed on Windows (`LOCAL - INSTALLED`).
- **UI extensions** (themes, icons) keep working automatically.
- **Workspace extensions** (Python, Jupyter, Git tools, linters) need to be installed inside **WSL** once per WSL distro:
  1. Open Extensions (`Ctrl+Shift+X`).
  2. Click **"Install in WSL"** on the ones you want under `LOCAL - INSTALLED`, or press `Ctrl+Shift+P` → **`Install Local Extensions`** to install several at once.

### Opening your Ubuntu terminal inside WSL
- Once your project is open in WSL, **`bash` IS your Ubuntu Linux terminal** (you won't see a separate "Ubuntu (WSL)" entry because you are already *inside* Ubuntu).
- Click **`+`** / **`bash`**, or press `Ctrl+Shift+ñ` (Spanish keyboard) to open a new Ubuntu terminal directly in your project folder.

### Bash gotcha: `event not found` with `!`
- Inside **double quotes (`"..."`)**, interactive `bash` treats `!` as a special history shortcut (causing `bash: !: event not found`).
- Inside **single quotes (`'...'`)**, `bash` treats everything literally — no special characters expanded. Swap quotes (`'...'` outside, `"..."` inside) whenever your command contains `!`.

---

## Working Across 2 Laptops (Git & Sync)

### Basic routine when switching laptops
1. **Before you start working:** Pull the latest changes from GitHub:
   ```bash
   git pull
   ```
2. **When you finish working:** Stage, commit, and push your changes:
   ```bash
   git status
   git add .
   git commit -m "Describe what you changed"
   git push
   ```

### `origin` vs `main` (don't mix them up!)
- **`origin`** = the **remote repository on GitHub** (the *where* — your repo URL).
- **`main`** (and `xiquilin/setup-env`) = **branches** (different versions/timelines of your code).
- So `git push -u origin xiquilin/setup-env` means: *"upload my `xiquilin/setup-env` branch to GitHub (`origin`)"* — it does **not** touch `main`.

### Keeping environments consistent
- **Virtual environments (`.venv/`):** Never committed to Git (listed in `.gitignore`). Each laptop builds its own from `requirements.txt`.
- **Extensions:** Add project extensions to `.vscode/extensions.json` so the second laptop offers a one-click install, and/or turn on **Settings Sync** (gear icon in bottom-left).

### Simulating 2 teammates (Author names + Branches + Pull Requests)
- **Set a different commit author name on the second computer** (run once inside the repo):
  ```bash
  git config user.name "Ramon_G@Katana"
  ```
  *(Check the active author anytime with `git config user.name`.)*
- **Feature branch + Pull Request (PR) cycle:**
  1. Start from an up-to-date `main`:
     ```bash
     git switch main
     git pull
     ```
  2. Create a new branch for your task (e.g., prefixed with your persona + task):
     ```bash
     git switch -c ray/task-name
     ```
  3. Work, commit, and push the branch to GitHub:
     ```bash
     git add .
     git commit -m "Describe the change"
     git push -u origin ray/task-name
     ```
  4. On **GitHub**, open a **Pull Request** (`ray/task-name` → `main`), review your own diff, and **Merge** it (then delete the merged branch).
  5. Next time you switch computers, run `git switch main && git pull` to grab the merged changes before starting a new branch.

---

## Python & Data Science

### Creating and using a virtual environment (`.venv`)
A virtual environment gives this project its own isolated Python + libraries so packages don't clash with other projects.

- **One-time Ubuntu/WSL prerequisite** (if `venv` complains about `ensurepip`):
  ```bash
  sudo apt update && sudo apt install -y python3.12-venv
  ```
- **Create `.venv`** (inside the project folder):
  ```bash
  python3 -m venv .venv
  ```
- **Activate `.venv` in Linux / WSL (`bash`):**
  ```bash
  source .venv/bin/activate
  ```
  *(You'll see `(.venv)` at the start of your prompt. To exit it, run `deactivate`.)*
- **Select it in VS Code:** Press `Ctrl+Shift+P` → **`Python: Select Interpreter`** → pick `./.venv/bin/python` *(so autocomplete, Run, and Jupyter notebooks use `.venv` instead of Ubuntu's global Python)*.
- **One `.venv` per project:** Don't reuse the same `.venv` across different projects — separate environments prevent package version conflicts ("dependency hell"). You can safely delete an old project's `.venv` anytime to save space and rebuild it later from `requirements.txt` (`pip` caches downloads locally so reinstalling is fast).

### Installing project packages (`requirements.txt`)
- **Install everything listed in `requirements.txt`** (with `(.venv)` active):
  ```bash
  pip install -r requirements.txt
  ```
  - `-r` comes from **`--requirement`** — it tells `pip` to read and install all packages listed in the file that follows (`requirements.txt`).
- **Python packages vs. system tools:** Libraries like `pandas` and `streamlit` go in `requirements.txt` (installed with `pip`). System tools like **Docker** are installed at the OS level, not via `pip`.
