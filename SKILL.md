---
name: migrate-to-recipkg
description: Initialize Recipkg for an existing project or migrate software into a Markdown-only Recipkg recipe with recursive dependencies and observable acceptance criteria. Use when asked to initialize or set up Recipkg in a project, or migrate an existing software project to Recipkg.
---

# Migrate software to Recipkg

[简体中文](SKILL.zh-CN.md)

## Inputs and boundaries

Treat requests such as "initialize Recipkg for this project" or "在项目中初始化 Recipkg" as requests to apply this migration workflow to the current project. Respect a narrower explicit request to create only an empty recipe scaffold with `recipkg init`.

Use the software directory, Git repository, or observable product; behavior to preserve; target environments; and a recipe output location. A recipe preserves requirements, interfaces, dependencies, and acceptance conditions for a future rebuild. Keep implementation source, binaries, generated output, and installation scripts out of its payload. Writing a recipe is not rebuilding software.

## Resolve choices before changing the layout

Read the conversation and project materials first. Ask only for consequential missing information, grouping questions together. While waiting for required answers, inspect material without creating repositories or changing their layout.

1. **Language preferences:** retain the source language or select languages suitable for the target platforms. Record the preference and whether the rebuilding agent may choose another language.
2. **Product intent:** identify problems to solve, behavior to preserve, requested changes, non-goals, and constraints.
3. **Design and interaction:** for visual products, establish references, identity, hierarchy, density, color, typography, and motion where known. Avoid generic AI dashboards. CLI/API products still need readable output, errors, and documentation.
4. **Internationalization:** preserve current languages or specify additional locales, right-to-left support, formatting, time zones, and translation maintenance. Mark unknowns explicitly.
5. **Target platforms:** identify applicable desktop, mobile, browser, server, or embedded environments, including known minimum versions and architectures.
6. **Performance:** identify important workloads, devices, latency, throughput, memory, network, or distribution-size constraints. Do not invent targets; record unknown budgets and real baselines when measurement is in scope.
7. **Repository layout:** use a separate migration workspace with the original repository pinned as a `source/` submodule by default, or retain an established same-repository layout with `recipes/<package-name>/`. Existing conventions or user choices take precedence. The source checkout is observation material, never a recipe dependency or archive payload.

Before adding a source submodule, verify its remote and reviewed commit. Preserve local work; resolve the observation scope when uncommitted source affects it. Do not overwrite an existing output directory.

## Procedure

1. Read applicable project instructions, README, licensing, build metadata, interfaces, and acceptance evidence. Record the observation version and scope; distinguish observations, assertions from tests/docs, inferences, and unknowns.
2. Generate an observation checklist with `recipkg extract <target> --lang en` or `--lang zh-CN`. The CLI only prints a task; actually inspect authorized source or products.
3. Reuse a valid recipe, or create a scaffold with `recipkg init <output> --name <package-name>`. Complete `RECIPE.md`, `BUILD_PROMPT.md`, and `ACCEPTANCE.md` with behavior, interfaces, environment, language/platform choices, design direction, quality constraints, and measurable acceptance conditions.
4. Describe necessary components as recursively complete recipes. Distinguish dependencies from operating systems, compilers, accounts, datasets, remote services, and references. Source-only repositories are not recipe dependencies. Use `recipkg search [keywords]` for candidates, then inspect the recipe and pin a reviewed source.
5. Define success, failure, boundary, and integration checks. For UI products include important states, narrow layouts, and accessibility. Record performance workloads, environments, commands, and methods only when measured; keep unperformed checks unverified.
6. GitHub repositories publishing Recipkg recipes must carry the `recipkg` topic. When publication is authorized, use `gh repo edit <owner/repo> --add-topic recipkg` or available tooling, preserve existing topics, and read back the result. For local-only repositories record this publishing requirement. Topics enable discovery, not validation or trust.
7. Ensure every payload file is UTF-8 `.md` without implementation source, binaries, filesystem links, or execution hooks. Run `recipkg check <output>`. If dependencies are complete, pack into a temporary directory, check the archive, and render its full build prompt; delete the temporary archive after validation. Keep or deliver a persistent archive only when the user explicitly requests one.

## Conflicting evidence and reproducible comparison

For behavior the user needs preserved, compare version-pinned documentation with relevant source or tests and, where feasible, run the original using isolated data. Record inputs, configuration, version, output, and exit status; label observations based only on documentation or source. If sources and runtime disagree, check versions, build options, and conditions, then retain the conflict and its limits. When resolved, update both the recipe and its acceptance cases with the confirmed behavior and counterexample. Do not generalize a single case across platforms; leave unresolved behavior unknown.

## Consult the standard library and reuse dependencies

When writing or updating a recipe, consult the [Recipkg standard library catalog](https://github.com/recipkg/standard-library) and evaluate candidates against the product's capabilities, category, and design needs. Read each candidate's actual recipe, source, license, coverage status, and recursive dependencies; a name, topic, or catalog entry is not proof of completeness. Reuse applicable design foundations, design directions, and software capabilities by declaring real recipe dependencies in `RECIPE.md`, pinning Git sources to reviewed full commit hashes, and specifying their purpose, integration contract, and acceptance checks in the build materials. Do not duplicate an already recursive dependency unnecessarily. Mark gaps in drafts and never claim unverified completeness or reconstruction. If no candidate fits, record the search and missing capabilities instead of adding unrelated dependencies. If the catalog is unavailable, report the limitation, use verified local material, and leave the search pending. This is an agent authoring step; CLI prompt rendering and checks remain offline.

## Deliverable

Provide the recipe directory, source version, languages/platforms/layout, preserved behavior, recursive dependencies, external prerequisites, inference, and unperformed checks. Provide a persistent archive only when explicitly requested. Preserve attribution and licensing. Successful packaging proves structural delivery, not successful independent reconstruction.

## Generated source layout

Treat recipes as the primary input. In a same-repository layout, `generated/` is a container beside `recipes/`. Put actual implementation source in a separate Git repository and add it as a pinned child submodule such as `generated/cli-source/`; do not commit ordinary implementation files directly under `generated/`. Do not put source code in the recipe payload. If consolidating an existing implementation, preserve its work, publish the separate source repository within the task authorization, add the child gitlink, and update build paths and evidence references. When the user identifies obsolete source directories for removal, inspect their contents and Git/submodule state, remove the requested directories, and update submodule metadata and references so the old source tree does not remain alongside the new layout. Do not delete other directories merely because their names look familiar. Do not overwrite unrelated or unrequested data. `generated/` contains named source submodules, never a flat source tree; use the same lowercase, hyphenated name for the source repository and its child directory. Keep observation checkouts separate. Create remotes and push only within existing publication authorization; otherwise complete local work and record its unpublished state.

Do not ignore `generated/` or its source-repository entries in Git; the parent must be able to track each gitlink. Check ignore rules even for tracked paths with `git check-ignore --no-index`. Preserve existing source and uncommitted changes; do not turn an existing nested repository into a submodule by discarding work. Ignore individual build outputs inside their own source repository as appropriate.

Keep the original project and primary repository name; do not append `-recipkg`. Independently managed source repositories use lowercase, hyphenated names.

## Shared project skill submodules

Read [PROJECT_SKILLS.md](PROJECT_SKILLS.md). Reuse the listed canonical upstream skill repositories as pinned Git submodules, normally under `.agents/skills/<skill-name>/`. Reuse a correct existing checkout even when the project uses another supported agent directory. Add each missing upstream skill from its own repository, not the entire Recipkg repository. Do not create or publish project-specific skills, skill repositories, or forks to satisfy this requirement. Preserve the target project's existing custom skill files; do not replace or delete them. If the user separately requests a new project-owned skill, handle that as a distinct request.

Verify `.gitmodules`, gitlink mode `160000`, the remote URL, commit, clean/dirty state, and readable skill resources. Update a skill in its own repository first, then review and explicitly update each consumer pin. Preserve local modifications and inspect conflicts before replacing existing ordinary skill directories. Git submodules provide the editable upstream checkout; never include their Git metadata in a Markdown-only recipe archive. If a recipe must distribute a skill, package only its UTF-8 Markdown payload and record the pinned source.
