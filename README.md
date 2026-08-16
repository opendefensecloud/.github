# `.github`

Organization-level defaults for [**opendefensecloud**](https://github.com/opendefensecloud).

This is GitHub's special [`.github` repository](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file). It holds two kinds of things:

1. **Reusable workflows** that other repositories across the org call.
2. **Workflows and configuration that run for _this_ repository.**

> [!NOTE]
> GitHub automatically shares *community health files* (e.g. `CONTRIBUTING.md`, issue templates, `CODE_OF_CONDUCT.md`) from this repo with every other repo in the org. **Workflows are _not_ shared automatically** — a reusable workflow only runs in another repo when that repo explicitly calls it (see below).

## Workflows

All workflows live in [`.github/workflows/`](.github/workflows). Two kinds coexist there, distinguished by their trigger rather than their location:

| File pattern | Trigger | Purpose |
|---|---|---|
| `reusable-*.yml` | `on: workflow_call` | Called by other workflows / other repos |
| everything else | `on: push`, `pull_request`, `issues`, … | Runs for this repo |

Each concern is split into a **reusable workflow** (the logic) and a thin **caller** (the trigger) that runs it here:

| Concern | Reusable | Caller (runs here) |
|---|---|---|
| Enforce SHA-pinned actions | `reusable-update-action-pins.yml` | `update-action-pins.yml` |
| Conventional-commit PR titles & messages | `reusable-conventional-commits.yml` | `conventional-commits.yml` |
| Label new issues (`needs-triage`) | `reusable-issues-add-labels.yml` | `issues-add-labels.yml` |
| Add issues/PRs to the org project board | `reusable-issues-add-to-project.yml` | `issues-add-to-project.yml` |

### Calling a reusable workflow from another repo

Reference it by its full path, **pinned to a full-length commit SHA** — not a mutable ref like `@main` or a tag. Add the human-readable ref as a trailing comment:

```yaml
# .github/workflows/pr.yml in some-other-repo
name: PR checks
on:
  pull_request:
    types: [opened, edited, synchronize, reopened]

permissions:
  pull-requests: read          # the caller must grant the permissions the workflow needs

jobs:
  conventional-commits:
    uses: opendefensecloud/.github/.github/workflows/reusable-conventional-commits.yml@c81a854fd0c66cab2f30c5429f5dcbda68634ef4 # main
```

Two things the caller is responsible for:

- **Permissions** — the `GITHUB_TOKEN` is scoped by the *caller*. Grant whatever the reusable workflow needs (e.g. `issues: write` for labelling).
- **Secrets** — custom secrets aren't passed automatically. For `reusable-issues-add-to-project.yml`, pass the project PAT:

  ```yaml
  jobs:
    add-to-project:
      uses: opendefensecloud/.github/.github/workflows/reusable-issues-add-to-project.yml@c81a854fd0c66cab2f30c5429f5dcbda68634ef4 # main
      secrets:
        ADD_TO_PROJECT_PAT: ${{ secrets.ADD_TO_PROJECT_PAT }}
  ```
