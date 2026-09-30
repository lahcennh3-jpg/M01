# M01-01 Public source retrieval

## Current objective

Create `/workspace/onyx-source` as a separate, minimally retrieved public Onyx Git repository and prove that revision `e7240a64ed06fff6f665fdde2bd90c4a3052d004` and the required source paths resolve without changing `/workspace/M01` provenance or importing Onyx source into its history.

## Authorization boundary

The user authorized public HTTPS source and Git metadata retrieval from `https://github.com/onyx-dot-app/onyx` for the exact research revision. Runtime execution, application requests, scanning, Docker, SaaS, credentials, model-provider access, upstream modification, and publication remain prohibited.

## Expected versus actual

- **Prediction:** The target would not exist, and a partial no-checkout clone would create a separate Git object database from which the pin could be inspected.
- **Expected:** `origin` would identify the authorized URL; `cat-file` and `rev-parse` would resolve the exact full commit; commit/tree metadata, all ten required paths, and their blob IDs would be recordable without a checkout.
- **Actual (RUN):** `/workspace/onyx-source` was absent. The authorized `git clone --filter=blob:none --no-checkout` was rejected by the environment's CONNECT path with HTTP 403. A prior diagnostic `git ls-remote` and codeload archive HEAD request were also rejected with HTTP 403. `ls-remote` only enumerates advertised references and was **not** treated as an authoritative arbitrary-commit existence check. The failed clone left `/workspace/onyx-source` absent.
- **Explanation (INF):** The consistent proxy response indicates an outbound network restriction in this execution environment. It does not establish upstream repository or revision availability.
- **Evidence:** `EVID-M01-002-public-source-retrieval.txt`.
- **Confidence:** High for commands executed, local filesystem state, and observed HTTP response; none for upstream commit contents.
- **Unknowns:** Upstream commit metadata/tree, provenance verification, required path existence, blob IDs, file hashes, and all source behavior.
- **Next action (PLAN):** Re-run the same bounded clone in an environment whose HTTPS policy permits the authorized GitHub URL, or provide an immutable Git bundle/archive for the exact revision. Then perform M01-01C through M01-01E before interpreting source.

## Retrieval and verification status

| Step | Intended proof | Result | Class |
|---|---|---|---|
| M01-01A | Evidence repository state and target absence | Passed | RUN |
| M01-01B | Separate Onyx object database | Blocked by HTTP 403; target remains absent | RUN |
| M01-01C | Remote, Git directory, exact commit, tree and author/committer metadata | Not run because no repository exists | PLAN / NOT RUN |
| M01-01D | Ten required paths exist in pinned tree | Not run because pin is unavailable | PLAN / NOT RUN |
| M01-01E | Immutable blob IDs for required paths | Not run because pin is unavailable | PLAN / NOT RUN |

## Resumption attempt — EVID-M01-003

On 2026-09-30, the evidence repository was rechecked as clean at `3b0acf669fc166ebc0ef1c3caea49522467f78ba`, with no configured remote and no `/workspace/onyx-source` target. A second authorized minimal clone was attempted and again failed at the environment's CONNECT boundary with HTTP 403. The failed clone left no target directory.

The authoritative future commit-existence check remains local possession and successful resolution of `e7240a64ed06fff6f665fdde2bd90c4a3052d004^{commit}` with `git cat-file` and `git rev-parse`; a URL-based `ls-remote <URL> <SHA>` query will not be used for that conclusion.

## Safety and repository separation

`/workspace/M01` was clean before retrieval and remains the evidence repository. No remote was added to it, it was not reset or replaced, and no Onyx source was copied into its Git history. The separate source target was not partially retained after the failed clone.

## Gate

**INCOMPLETE — authorized public source retrieval was attempted but blocked by the environment's HTTP 403 response.**

M01 source interpretation must remain stopped. **I cannot confirm this** revision's provenance, metadata, paths, blobs, or security behavior until the immutable object is locally available and verified.
