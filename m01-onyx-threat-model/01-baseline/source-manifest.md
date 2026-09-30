# M01-00 Environment and source identity manifest

## Record

| Field | Observation | Class | Evidence |
|---|---|---|---|
| Intended repository | `https://github.com/onyx-dot-app/onyx` | PLAN (engagement scope) | User-supplied scope; not locally verified |
| Local repository root | `/workspace/M01` | RUN | `EVID-M01-001` |
| Current branch | `work` | RUN | `EVID-M01-001` |
| Current HEAD | `c593972edc2c4ddcc0890d7bfc5e6b7b670bccfa` (`Initialize repository`) | RUN | `EVID-M01-001` |
| Requested research revision | `e7240a64ed06fff6f665fdde2bd90c4a3052d004` | PLAN (engagement scope) | User-supplied scope |
| Requested revision locally available | No; `git cat-file -e` failed | RUN | `EVID-M01-001` |
| Configured Git remote | None | RUN | `EVID-M01-001` |
| Working tree before evidence creation | Clean; `git status --short` produced no output | RUN | `EVID-M01-001` |
| Inspection date | 2026-09-30 UTC environment date | RUN/metadata | Environment context and `EVID-M01-001` |
| Source retrieval method | Local read-only Git object inspection only | RUN | `EVID-M01-001` |
| Onyx source verification | **I cannot confirm this.** | — | Pin absent; remote absent |
| Runtime verification | **NOT RUN** | PLAN | Outside M01-00 authorization |

## Expected versus actual

- **Prediction:** `/workspace/M01` might be an Onyx checkout containing the pinned commit.
- **Expected:** Git identifies the repository root, clean/dirty state, current HEAD, remote, and pinned commit metadata without changing repository state.
- **Actual:** `/workspace/M01` is a Git repository on branch `work` at an initialization commit, with a clean pre-investigation working tree and no configured remote. The requested Onyx commit is absent, so its metadata and source cannot be inspected locally.
- **Explanation:** The local repository has no object or provenance evidence connecting it to the intended Onyx repository.
- **Evidence:** `../07-evidence/commands/EVID-M01-001-environment-source-identity.txt`.
- **Confidence:** High for local Git state; no confidence claim about the pinned Onyx source.
- **Unknowns:** Whether an Onyx checkout exists elsewhere; whether the pinned source URL is accessible; authoritative commit metadata; all requested source architecture and runtime configuration.
- **Next action:** Obtain explicit authorization to retrieve the exact pin from the supplied repository URL, or receive an immutable local archive/worktree containing that object. Verify its hash before M01-01 source analysis.

## Gate

**INCOMPLETE — the authoritative research object is unavailable locally and no remote is configured.** Source analysis must not proceed from the unrelated initialization commit.
