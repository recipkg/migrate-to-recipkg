# Shared project skill repositories / 项目技能仓库

Every skill has one canonical repository. Migrated projects reference these same repositories as fixed-commit Git submodules, rather than copying Markdown or creating project-specific skill repositories. Reuse existing correct checkouts when an agent uses a different skill directory.

| Skill | Canonical GitHub repository | Default project path |
| --- | --- | --- |
| `add-dependency` | [recipkg/add-dependency](https://github.com/recipkg/add-dependency) | `.agents/skills/add-dependency/` |
| `build-software-package` | [recipkg/build-software-package](https://github.com/recipkg/build-software-package) | `.agents/skills/build-software-package/` |
| `discover-dependencies` | [recipkg/discover-dependencies](https://github.com/recipkg/discover-dependencies) | `.agents/skills/discover-dependencies/` |
| `manage-git-repository` | [recipkg/manage-git-repository](https://github.com/recipkg/manage-git-repository) | `.agents/skills/manage-git-repository/` |
| `migrate-to-recipkg` | [recipkg/migrate-to-recipkg](https://github.com/recipkg/migrate-to-recipkg) | `.agents/skills/migrate-to-recipkg/` |
| `prompt-to-software` | [recipkg/prompt-to-software](https://github.com/recipkg/prompt-to-software) | `.agents/skills/prompt-to-software/` |
| `rewrite-software` | [recipkg/rewrite-software](https://github.com/recipkg/rewrite-software) | `.agents/skills/rewrite-software/` |
| `rewrite-to-recipkg` | [recipkg/rewrite-to-recipkg](https://github.com/recipkg/rewrite-to-recipkg) | `.agents/skills/rewrite-to-recipkg/` |
| `software-to-prompt` | [recipkg/software-to-prompt](https://github.com/recipkg/software-to-prompt) | `.agents/skills/software-to-prompt/` |
| `test-feedback` | [recipkg/test-feedback](https://github.com/recipkg/test-feedback) | `.agents/skills/test-feedback/` |
| `update-recipkg-in-project` | [recipkg/update-recipkg-in-project](https://github.com/recipkg/update-recipkg-in-project) | `.agents/skills/update-recipkg-in-project/` |

## Add and update

```sh
git submodule add https://github.com/recipkg/test-feedback.git .agents/skills/test-feedback
git submodule update --init --recursive
git -C .agents/skills/test-feedback fetch origin
# Inspect changes and local work, then select a reviewed full commit.
git -C .agents/skills/test-feedback checkout <reviewed-commit>
git add .gitmodules .agents/skills/test-feedback
```

Repeat the add operation for missing skills using each row's exact repository URL. Preserve existing topics, user edits, and unrelated files. A dirty submodule requires reviewing its local work before updating; never reset or force an overwrite. Commit the consumer's pointer deliberately. A source-only download or a directory with copied files is not a submodule: the parent Git tree must show mode `160000`.

Skills are scoped working instructions, not implicit permission to publish or contact others. Their Git workspaces and `.git` metadata never enter a Markdown-only recipe archive. CLI skill synchronization remains a managed-copy option for non-Git environments; it does not create these project submodules.

每个技能只维护一个独立仓库。迁移项目应添加上述相同仓库为子模块，默认全部放到 `.agents/skills/`，已有正确路径则沿用。不要逐项目复制技能内容或创建带项目后缀的副本。更新时先保留本地修改、审查并选择提交，再显式提交父仓库指针；不要 reset 或强制覆盖。
