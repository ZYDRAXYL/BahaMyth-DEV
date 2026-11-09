# AGENTS.md

Guidance for Codex working in **BahaMyth-DEV**.

## What this is

BahaMyth-DEV is the **controller/workspace repo**, not an application repo. It tracks
only `BahaMyth.code-workspace`, `scripts/`, `README.md`, `LICENSE` and the git
dotfiles.

The 7 `BahaMyth-*/` folders beside it are **separate git repositories**, each
with its own GitHub remote under `ZYDRAXYL/`. `.gitignore` excludes them here.

If you are here to change app behaviour or design docs, **you are in the wrong
folder.** Pick the owning repo, `cd` into it, and work there.

| Repo | Role | Owns |
|---|---|---|
| **APP** | hub | `.claude/`, `chain/`, `docs/`, `process/`, `tools/` |
| **SDB** | schema | `schema/`, `supabase/`, `assets/`, `generated/` |
| **TRX** | service | `netlify/`, `public/`, `netlify.toml` |
| **EXE** | app | `electron/` |
| **PWA** | build | `tools/`, `shim/`, `dist/` |
| **PKG** | content | `packages/`, `index.json` |
| **WEB** | site | `*.html`, `assets/` |
| **DEV** (here) | workspace | the workspace file, the setup script |

`BahaMyth-APP/chain/chain.json` is the machine-readable contract. Read it rather
than trusting this table where the two disagree.

## Hard rules

1. **Never `git add`/`git commit` from this root for a change inside a child
   repo** — those paths are ignored here, so the commit captures nothing:
   ```bash
   git -C BahaMyth-APP status
   git -C BahaMyth-APP commit -am "..."
   ```
   Commit from this root *only* for the workspace file, scripts, or docs.
2. **Keep `scripts/setup.ps1`, `.gitignore` and `BahaMyth.code-workspace` in step
   with `chain.json`** when a repo is added or removed.
