First fix: your list has the same skill twice.

## Bottom line

For **local multi-repo workspace management**, the current `git-workflow-manager` skill is too narrow. Its README/SKILL are focused on **conventional commits, semantic versioning, changelog updates, and release notes**. That is useful, but it is a **release-policy skill**, not a **multi-repo workspace controller**. ([GitHub][1])

GitHub Projects is worth keeping, but as the **tracking/control plane**, not as the workspace engine. Projects can aggregate **issues and PRs from any organization**, support **custom fields, views, charts, and automation**, and can be managed through the **GraphQL API** and `gh project` commands. ([GitHub Docs][2])

## Reality check on the graph requirement

A **true unified commit DAG across unrelated repos** is not a native Git concept. `git worktree` only manages multiple working trees for the **same repository**, and submodules explicitly keep the histories of the embedded repo and superproject **separate**. The closest native linkage is a superproject tracking a submodule commit via a `gitlink`. So for polyrepo work, “cross-repo commit graph” should usually be treated as a **synthetic overlay graph**, not a literal merged Git history, unless you intentionally move to a superproject/submodule or monorepo model. ([Git][3])

## Recommended tool list

| Role                         | Recommendation                                     |           Keep? | Why                                                                  |
| ---------------------------- | -------------------------------------------------- | --------------: | -------------------------------------------------------------------- |
| Commit/release policy        | `git-workflow-manager`                             | Yes, but demote | Good for commit/release hygiene only. ([GitHub][1])                  |
| Multi-repo execution         | `gitopolis` **or** `mr` **or** `git for-each-repo` |             Add | This is the missing layer.                                           |
| Per-repo commit graph UX     | `git-branchless`                                   |             Add | Best fit for stacked work and graph repair. ([GitHub][4])            |
| Cross-repo work tracking     | GitHub Projects + `gh project`                     |            Keep | Strong cross-repo planning/tracking layer. ([GitHub Docs][2])        |
| Cross-repo code/entity graph | SCIP-based indexing                                |        Optional | For symbol/reference relationships, not work tracking. ([GitHub][5]) |

## Best choices by function

### 1. Multi-repo workspace runner

**Best “pure Git” option:** `git for-each-repo`
It is built into Git and runs Git commands over a configured repo list, but the docs explicitly mark it as **experimental**. ([Git][6])

**Best minimal mature option:** `mr` / myrepos
`mr` is specifically designed to manage many repos “as if they were one combined repository,” with commands like `mr update`, `mr commit`, and `mr status`. ([GitHub][7])

**Best structured polyrepo option:** `gitopolis`
`gitopolis` is the strongest fit for your stated needs because it adds a **shared TOML state file**, **repo tags**, **multiple remotes**, and fan-out execution like `gitopolis exec -- git status`. That gives you a real local workspace inventory layer instead of just a command runner. It also has Arch/AUR packaging. ([GitHub][8])

### 2. Commit graph visualization

Use `git-branchless` for **per-repo** history UX. It gives you **smartlog**, **restack**, **sync**, and tools to repair broken commit graphs. It is optimized for large repos/monorepos, but it still works well as the per-repo graph tool inside a polyrepo workspace. ([GitHub][4])

### 3. Cross-repo tracking

GitHub Projects is strong here:

* Projects can include issues/PRs from **any organization**. ([GitHub Docs][9])
* Projects support **custom fields**, saved views, grouping, charts, and automation. ([GitHub Docs][2])
* GitHub now supports **sub-issues**, **issue dependencies**, and **cross-repo PR→issue linking** using syntax like `Fixes owner/repo#123`. ([GitHub Docs][10])

That is enough to build a strong **cross-repo work graph**, even though it is not a code/entity graph.

### 4. Cross-repo entity relationships

If by “entity relationships” you mean **code symbols, definitions, references, implementations**, then GitHub Projects is the wrong tool. A better fit is a code-index layer such as **SCIP**, which is a language-agnostic protocol for indexing source code to power **go to definition**, **find references**, and **find implementations**. ([GitHub][5])

## My optimized list

### Minimal stack

1. `git-workflow-manager` → keep, but rename mentally to **release-policy**
2. `gitopolis` → add for local repo inventory + fan-out ops
3. `git-branchless` → add for per-repo commit graph work
4. GitHub Projects + `gh project` → keep for cross-repo tracking

### Heavier but stronger stack

1. `git-workflow-manager`
2. `gitopolis`
3. `git-branchless`
4. GitHub Projects + GraphQL / `gh project`
5. SCIP index pipeline for cross-repo code-entity graph

## Concrete modification to the skill setup

I would split the current skill into **three** skills:

### A. `git-workflow-manager`

Leave it focused on:

* conventional commits
* semver
* changelog
* release notes

### B. `multi-repo-workspace-manager`

New skill. This should own:

* repo registry/manifest
* fan-out commands
* repo tags
* remote sync
* workspace status
* synthetic cross-repo graph export

### C. `gh-project-sync`

New skill. This should own:

* creating/updating project items
* syncing repo/issue/PR metadata into project fields
* dependency/sub-issue creation
* cross-repo linkage via issue/PR references

## Suggested local architecture

Use a local SSOT manifest, not GitHub as the SSOT:

```yaml
workspace:
  name: dev-workspace

repos:
  - id: api
    path: ~/ws/api
    remote: git@github.com:org/api.git
    tags: [backend, core]
  - id: web
    path: ~/ws/web
    remote: git@github.com:org/web.git
    tags: [frontend]
  - id: docs
    path: ~/ws/docs
    remote: git@github.com:org/docs.git
    tags: [docs]

edges:
  - type: depends_on
    from: web
    to: api
  - type: tracked_by
    from: api
    to: org/platform#123
  - type: relates_to_commit
    from: api@abc1234
    to: web@def5678
    via: org/platform#123
```

That gives you:

* **repo graph**
* **tracking graph**
* **synthetic commit relation graph**

## One strong Arch/systemd-specific add

Because you run Linux/systemd, add `git maintenance` to the design. Git can register repos into `maintenance.repo`, use `git for-each-repo` for fan-out maintenance, and on Linux it can create **user systemd timers** automatically. The incremental strategy runs **commit-graph** hourly. ([Git][11])

## Final recommendation

Use this:

* **Keep:** GitHub Projects
* **Keep, but narrow:** `git-workflow-manager`
* **Add:** `gitopolis`
* **Add:** `git-branchless`
* **Optional:** SCIP indexing

And treat **cross-repo commit graphs as an overlay artifact**, not a native Git structure.

If you want, I can turn this into a **concrete workspace spec** with:

* directory layout
* manifest schema
* command set
* `just`/shell wrappers
* graph export format
* GitHub Project field model

[1]: https://github.com/serejaris/ris-claude-code/tree/main/skills/git-workflow-manager "ris-claude-code/skills/git-workflow-manager at main · serejaris/ris-claude-code · GitHub"
[2]: https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects "About Projects - GitHub Docs"
[3]: https://git-scm.com/docs/git-worktree "Git - git-worktree Documentation"
[4]: https://github.com/arxanas/git-branchless "GitHub - arxanas/git-branchless: High-velocity, monorepo-scale workflow for Git · GitHub"
[5]: https://github.com/sourcegraph/scip "GitHub - sourcegraph/scip: SCIP Code Intelligence Protocol · GitHub"
[6]: https://git-scm.com/docs/git-for-each-repo "Git - git-for-each-repo Documentation"
[7]: https://github.com/RichiH/myrepos "GitHub - RichiH/myrepos · GitHub"
[8]: https://github.com/timabell/gitopolis "GitHub - timabell/gitopolis: Manage multiple git repositories - CLI tool - run commands, clone, and organize repos with tags · GitHub"
[9]: https://docs.github.com/en/issues/planning-and-tracking-with-projects/managing-items-in-your-project/adding-items-to-your-project "Adding items to your project - GitHub Docs"
[10]: https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/adding-sub-issues "Adding sub-issues - GitHub Docs"
[11]: https://git-scm.com/docs/git-maintenance "Git - git-maintenance Documentation"
