# migrate-to-recipkg

Initialize Recipkg for an existing project or migrate software into a Markdown-only recipe with reviewed standard-library dependencies and observable acceptance criteria. An explicit request for only an empty `recipkg init` scaffold remains limited to that scaffold.

Read [SKILL.md](SKILL.md) for the workflow and linked resources. This is the canonical standalone skill repository used by [Recipkg](https://github.com/recipkg/recipkg).

## Use as a project submodule

```sh
git submodule add https://github.com/recipkg/migrate-to-recipkg.git .agents/skills/migrate-to-recipkg
git submodule update --init --recursive
```

Keep the same repository across projects. Review upstream changes and local work before checking out a new commit, then explicitly commit the consumer gitlink. Do not copy and hand-maintain a second skill or overwrite custom modifications.

This repository is also a Markdown-only Recipkg skill recipe: validate with `recipkg check .`, then pack it outside this directory. [License](LICENSE.md).

## 中文

本技能用于在现有项目中初始化、接入 Recipkg，或将软件迁移为配方；明确只要求创建空配方骨架时按该范围执行。编写配方时先查阅标准库，复用适用且已审阅的真实配方依赖，并记录来源与验收缺口。本仓库只维护 `migrate-to-recipkg` 技能。不同项目应把此同一仓库作为固定提交的 Git 子模块引用，不复制技能正文。修改先回本仓库，再更新项目指针；注意保护本地改动。技能入口与说明见 [SKILL.md](SKILL.md)。
