# BahaMyth-DEV

Controller repo for the BahaMyth multi-repository project. It holds no
application code — only the VS Code workspace, the setup script, and the
gitignore rules that keep the 7 real repos out of this one's history.

## Layout

```
BahaMyth-DEV/
├── BahaMyth.code-workspace   # multi-root workspace (relative paths, safe to move)
├── scripts/setup.ps1       # clone whichever child repos are missing + npm install
├── BahaMyth-APP/
├── BahaMyth-SDB/
├── BahaMyth-TRX/
├── BahaMyth-EXE/
├── BahaMyth-PWA/
├── BahaMyth-PKG/
├── BahaMyth-WEB/
```

Each `BahaMyth-*` folder is its own git repository (own `.git`, own GitHub
remote under `ZYDRAXYL/`). `.gitignore` excludes them entirely from this repo.

## Chained repositories

From [`BahaMyth-APP/chain/chain.json`](https://github.com/ZYDRAXYL/BahaMyth-APP/blob/main/chain/chain.json):

| Repo | Role | Owns | Releases | Visibility |
|---|---|---|---|---|
| [BahaMyth-APP](https://github.com/ZYDRAXYL/BahaMyth-APP) | hub | `.claude/`, `chain/`, `docs/`, `process/`, `tools/` | — | private |
| [BahaMyth-SDB](https://github.com/ZYDRAXYL/BahaMyth-SDB) | schema | `schema/`, `supabase/`, `assets/`, `generated/` | `sdb-v*` | public |
| [BahaMyth-TRX](https://github.com/ZYDRAXYL/BahaMyth-TRX) | service | `netlify/`, `public/`, `netlify.toml` | — | public |
| [BahaMyth-EXE](https://github.com/ZYDRAXYL/BahaMyth-EXE) | app | `electron/` | `v*` | private |
| [BahaMyth-PWA](https://github.com/ZYDRAXYL/BahaMyth-PWA) | build | `tools/`, `shim/`, `dist/` | — | public |
| [BahaMyth-PKG](https://github.com/ZYDRAXYL/BahaMyth-PKG) | content | `packages/`, `index.json` | `pkg-v*` | public |
| [BahaMyth-WEB](https://github.com/ZYDRAXYL/BahaMyth-WEB) | site | `*.html`, `assets/` | `mirror` | public |

Changes flow one way along the chain:

```
EXE    APP > SDB, TRX > EXE > PKG, WEB, PWA
PWA    APP > SDB, TRX > EXE > PWA > WEB
```

## First-time setup on a new device

Prerequisites: [Git](https://git-scm.com/) with access to the `ZYDRAXYL` org (APP, EXE are private), and [Node.js LTS](https://nodejs.org/).

```powershell
git clone https://github.com/ZYDRAXYL/BahaMyth-DEV.git
cd BahaMyth-DEV
./scripts/setup.ps1
```

Then open `BahaMyth.code-workspace` in VS Code.

> If PowerShell refuses to run the script, run it once as:
> `powershell -ExecutionPolicy Bypass -File .scriptssetup.ps1`

## License

MIT — see [LICENSE](LICENSE). Created by LDKTC.
