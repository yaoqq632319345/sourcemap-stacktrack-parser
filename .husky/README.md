# 添加 git hooks

### 项目内安装

`npm i husky -D`

### 创建.husky/目录并指定该目录为 git hooks 所在的目录

在 package.json 中添加 prepare 脚本

```
"scripts": {
  "prepare": "husky install"
}
```

- prepare 脚本会在执行 npm install 之后自动执行。
- 也就是说当我们执行 npm install 安装完项目依赖后会执行 husky install 命令。

### 添加 git hooks

创建一条 pre-commit hook

`npx husky add .husky/pre-commit "npm run lint"`
执行该命令后，会看到.husky/目录下新增了一个名为 pre-commit 的 shell 脚本。

这样，在之后执行 git commit 命令时会先触发 pre-commit 这个脚本。

pre-commit 脚本内容如下：
`#!/bin/sh . "$(dirname "$0")/\_/husky.sh" npm run lint`

### 规范 commit message 信息

`npx husky add .husky/commit-msg 'npx --no-install commitlint --edit $1'`

### 安装 commitlint

`npm i @commitlint/cli @commitlint/config-conventional -D`

### 配置 commitlint.config.js

`echo "module.exports = {extends: ['@commitlint/config-conventional']};" > commitlint.config.js`
