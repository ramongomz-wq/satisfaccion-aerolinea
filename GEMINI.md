# Project & Learning Context

## About Me
- I am a **learner** building this project step by step.
- Please explain concepts clearly, use plain language, and walk through commands and actions step by step rather than assuming I already know the jargon.
- Match the language I write to you in (English or Spanish).

## My 2-Laptop Setup (Simulated 2-Person Team)
- I work on this project across **2 computers**: one at **home** and one at **school** (including **Windows + WSL2**).
- Although I have full access to both, I want to **simulate two teammates / two workspaces** collaborating on the same repository:
  - Both computers clone the same GitHub repo (`origin`) and stay in sync via branches, pushes, pulls, and **Pull Requests (PRs)**.
  - Commit author on this computer: **`Ray`** (nickname: **Xiquilin** — the main/lead engineer setting up `main` and the base project)
  - Commit author on the other computer: **`Ramon_G@Katana`** (second engineer / teammate)
  - Prefer working on feature branches and merging into `main` via Pull Requests (rather than pushing everything directly to `main`), so I can practice real team workflows (branching, PR reviews, merging, and resolving conflicts).
- Each machine / WSL environment creates its own virtual environment (`.venv/`) from `requirements.txt` (`.venv/` stays ignored in `.gitignore`).
- Keep editor extensions needed for this project listed in `.vscode/extensions.json` so it's easy to set up on both laptops and in WSL.
- Remind me to `git pull` when switching computers and to work cleanly with branches/PRs when finishing a session if relevant.

## Learning Log (`docs/learning_log.md`)
- We maintain a personal cheat sheet of everything I learn in `docs/learning_log.md`.
- Whenever I learn a new useful trick, shortcut, command, or workflow (or ask you to save one), add a concise, easy-to-scan entry to `docs/learning_log.md` under the appropriate section.
- Keep entries practical: include the exact shortcut or command and a 1–2 line explanation of *why* or *when* to use it.
