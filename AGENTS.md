# AGENTS.md — Federation Society (super-repo)

This repository is the **submodule super-repo** for the Federation ecosystem. It
does not contain application code directly; it composes independent, standalone
component repositories as Git submodules.

## Repository boundary

Work only inside `/home/drdeek/projects/Federation-Society` for super-repo-level
operations (root docs, `.gitmodules`, sync workflow, gitlink commits).

- A submodule is its own repository. To change a component, edit it inside its
  own subtree (`watchtower/`, `plugins/watchtower-sdk/`,
  `plugins/watchtower-adapter/`, `federation/`, `agent-character-kit/`) — do not
  treat it as a folder of this repo.
- Do not inspect, edit, commit, push, deploy, or configure a sibling project
  unless explicitly authorized for that separate operation.
- Never push or commit the super-repo (or any submodule) unless explicitly
  requested. Push order: **children first** (`watchtower`, `plugins/*`,
  `federation`, `agent-character-kit`), then **Federation Society last**.

## Layout

- `watchtower/` — agent observability / coordination platform
  (`drdeeks/federation-watchtower`)
- `plugins/watchtower-sdk/` — `@federation-watchtower/sdk`
  (`drdeeks/watchtower-sdk`)
- `plugins/watchtower-adapter/` — `@the-federation/watchtower-adapter`
  (`drdeeks/watchtower-adapter`)
- `federation/` — The Federation parent platform (`drdeeks/the-federation`)
- `agent-character-kit/` — `@drdeeks/character-kit`
  (`drdeeks/agent-character-kit`)

`plugins/` holds re-pluggable components. The SDK is its own standalone
component under `plugins/`, not nested inside the adapter.

## Recovery directive

Never delete. Removed or legacy material goes to `.trash/` with its original
context preserved. `.trash/` is the canonical recovery location for this
ecosystem (versioned local doctrine wins over the universal `.archive/`
reference). Do not use `.trash/` as an active source of truth.

## FOREVER doctrine

- `federation/docs/FOREVER_DOCTRINE.yaml` — local versioned truth (v2.0.0).
- `FOREVER-SYSTEM/FOREVER_DOCTRINE_UNIVERSAL.yaml` — universal reference (v1.0.0).

## Auto-sync

`.github/workflows/sync-submodules.yml` updates submodule pointers hourly and
pushes via `SUBMODULE_SYNC_TOKEN`. Local manual `git submodule update --remote`
mirrors this; do not hand-edit gitlinks except through that flow.
