# Migration Report

## Moved And Renamed

| Original path | New path | Notes |
| --- | --- | --- |
| `GeometricDeepLearning/` | `01_projects/geometric_deep_learning/` | Project folder moved and normalized to `snake_case` |
| `QCFluid/` | `01_projects/qcfluid/` | Project folder moved and normalized to lowercase |
| `quantum_computing/` | `01_projects/quantum_computing/` | Project folder moved |
| `quantum_computing/conforence.md` | `01_projects/quantum_computing/conference.md` | Obvious spelling fix |
| `quantum_computing/hamitonian_simulation/` | `01_projects/quantum_computing/hamiltonian_simulation/` | Obvious spelling fix |
| `gpt/` | `02_reference/gpt/` | Classified as reusable reference material |
| `gpt/useful links.md` | `02_reference/gpt/useful_links.md` | Normalized spacing to `snake_case` |
| `cmake_windows.md` | `02_reference/cmake_windows.md` | Reusable technical reference |
| `memory_manager.md` | `02_reference/memory_manager.md` | Reusable technical reference |
| `useful_links.md` | `02_reference/useful_links.md` | Reusable technical reference |
| `wsl_revelant/` | `02_reference/wsl_related/` | Classified as reference and spelling fixed conservatively |
| `note_about_life.md` | `03_life/note_about_life.md` | Personal note moved under life |

## New Files Created

- `README.md`
- `01_projects/geometric_deep_learning/README.md`
- `01_projects/qcfluid/README.md`
- `01_projects/quantum_computing/README.md`
- `00_inbox/migration_report.md`
- `90_archive/.gitkeep`
- `assets/.gitkeep`

## Updated Files

- `.gitignore`

## Files And Folders Left Untouched

- `.git/`
- `.codex/`
- `01_projects/qcfluid/不同初态和哈密顿量.md`
- `01_projects/qcfluid/7af40ad162d9f2d3763ce60ca7ec8a136327cc20.webp`
- `01_projects/qcfluid/image.png`
- `01_projects/quantum_computing/ibm/`
- `01_projects/quantum_computing/paper_reading/`
- `01_projects/quantum_computing/report/`

## Ambiguous Cases

- `gpt/` could have been treated as a project, but it currently contains a single links note, so it was placed under `02_reference/`.
- `useful_links.md` is broad and may later be worth splitting by topic, but it currently fits better as general reference material than as a project note.
- Nothing was moved into `90_archive/` because no existing material was clearly inactive or redundant enough to archive without guessing.

## Chose Not To Rename

- `01_projects/qcfluid/不同初态和哈密顿量.md` was left unchanged to preserve the original note title.
- `01_projects/quantum_computing/ibm/ibm_api.md` was left unchanged.
- `01_projects/quantum_computing/ibm/ibmtutorials.md` was left unchanged.
- `01_projects/quantum_computing/nqi_with_code.md` was left unchanged.
- `02_reference/wsl_related/virtualenvwrapper.md` was left unchanged.

## Link Check

- No Markdown content links needed updating.
- The only relative Markdown links found were the two image links in `01_projects/qcfluid/不同初态和哈密顿量.md`, and they remain valid because the images moved with the folder.
