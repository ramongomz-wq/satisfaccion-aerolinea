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

*(We'll add notes here as we go — virtual environments, Jupyter notebooks, pandas, etc.)*
