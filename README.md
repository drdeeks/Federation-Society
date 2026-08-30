# Federation Society

> The durable foundation for a growing society of independently built systems,
> districts, institutions, services, and experiences — composed, not consolidated.

## The Society

Federation Society is not a single application. It is the structural and
organizational foundation for an expanding **civilization** of components built
under the Federation.

The first components are infrastructural — an agent observability and
coordination platform (`watchtower`), its integration SDK, a translator bridge
to behavioral enforcement (`agent-character-kit`), and the Federation parent
platform itself. But that is only the seed. Everything built from here on —
gaming centers shared by agents and humans, an online marketplace, art
festivals, commerce districts, and whatever else gets made — becomes another
attribute and component of the same society.

Each new thing is a `Federation-<name>` and joins as a **district, institution,
service, or experience** in the same civilization. The society grows by
absorption: a new hackathon project, a new facility, a new offering is not a
separate venture — it is integrated into the whole.

## What this repository is

This repository is the **submodule super-repo** for that society. It does not
contain application code directly. It is the connective layer that lets many
independent repositories coexist as one federated whole — each component keeping
its own Git history, identity, language, release cycle, and (where applicable)
npm package, while being cloned and tracked together here.

A submodule super-repo pins other repositories by commit. Each component
remains a standalone repo; this one records where each currently points and
keeps the pointers in sync.

## How a component joins

A new part of the society is added as a Git submodule under a scoped path
(`plugins/` for re-pluggable components, or a top-level `Federation-<name>/`
district). It keeps its own repository and development process. The super-repo
only tracks its commit pointer — it never absorbs the component's code or
couples its release cycle to the others.

This is deliberate: the Federation favors **composition over consolidation**. A
gaming center, a marketplace, and an observability platform should be able to
evolve, be replaced, or fail independently without forcing the rest of the
society to be rebuilt around them.

## Current components (the seed)

| Path                         | Repository                          | Package                       | Role                                  |
| ---------------------------- | ----------------------------------- | ----------------------------- | ------------------------------------- |
| `watchtower/`                | `drdeeks/federation-watchtower`     | —                             | Agent observability / coordination platform |
| `plugins/watchtower-sdk/`    | `drdeeks/watchtower-sdk`            | `@federation-watchtower/sdk`  | Canonical SDK/MCP for Watchtower integration |
| `plugins/watchtower-adapter/`| `drdeeks/watchtower-adapter`        | `@the-federation/watchtower-adapter` | Translator bridge (CharacterKit ⇄ Watchtower) |
| `federation/`                | `drdeeks/the-federation`           | —                             | The Federation parent platform        |
| `agent-character-kit/`       | `drdeeks/agent-character-kit`       | `@drdeeks/character-kit`      | Behavioral config + fail-closed enforcement |

These are the foundation layer. Gaming centers, marketplaces, art festivals, and
other `Federation-<name>` components are added here as they are built.

## Auto-sync

`.github/workflows/sync-submodules.yml` runs hourly (and on manual
`workflow_dispatch`): it initializes submodules, forces them to follow each
remote's default branch (HEAD), runs `git submodule update --remote`, then —
if any gitlink moved — commits and pushes the updated pointers using the
workflow's built-in `GITHUB_TOKEN` (`permissions: contents: write`). Children
are expected to push to their own remotes first; this super-repo is pushed last.

## Independence

Federation components are not required to share a single implementation,
language, framework, deployment model, or development workflow. Independence is
intentional — it is what lets the society keep expanding without ever becoming a
monolith. A component evolves by its own requirements while remaining part of
something larger than itself.
