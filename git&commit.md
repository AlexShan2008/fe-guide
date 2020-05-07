# Git Commit Guidelines

> 使用 Angular 团队提交规范

1 主要有以下组成

```jsx
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

- 标题行: 必填, 描述主要修改类型和内容
- 主题内容: 描述为什么修改, 做了什么样的修改, 以及开发的思路等等
- 页脚注释: 放 Breaking Changes 或 Closed Issues

2 具体说明

- scope: commit 影响的范围, 比如: route, component, utils, build...
- subject: commit 的概述
- body: commit 具体修改内容, 可以分为多行
- footer: 一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接.

> 常用的修改项

## DEMO

> 例如本次开发实现了用户登录的功能；则`commit`提交样式如下：

```sh
feat(login): add login feature

1.mobile login
2.email login
3.find password
```

## type: commit 的类型

- build: 影响build system 或者相关依赖（如: gulp, broccoli, npm, yarn）
- ci: 更改 CI 配置文件或者脚本（如：Circle, BrowserStack, SauceLabs）
- docs: 文档修改
- feat: 新特性
- fix: 修改问题
- perf: 性能优化
- refactor: 代码重构
- style: 代码格式修改, 注意不是 css 修改
- test: 测试用例修改
- chore: 其他修改, 比如构建流程, 依赖管理.

**可以使用`Commitizen`代替 git commit**
可以使用[cz-cli](https://github.com/commitizen/cz-cli)工具代替 git commit

全局安装，并在项目根目录初始化安装

```bash
yarn add -g commitizen cz-conventional-changelog

commitizen init cz-conventional-changelog --yarn --dev --exact
```

then some change in your `package.json`

```JSON
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
  }
```

全局安装后使用`git cz`代替 `git commit`就可以了。

## Commit 格式校验

### 1 安装`commitlint`

1.安装工具

```sh
npm install -g @commitlint/cli @commitlint/
```

2.生成配置文件`commitlint.config.js`

#### 方法 1 命令行工具生成

```sh
config-conventional
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

#### 方法 2 手动生成

项目根目录下创建`commitlint.config.js`这个文件，并配置

```js
module.exports = { extends: ["@commitlint/config-conventional"] };
```

### 2 安装`husky`工具

```sh
yarn add -D husky
```

2 配置`husky`校验规则
//package.json

```json
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  }
```

## Semantic Versioning 版本号命名规则

> 避免出现依赖地狱

- 版本信息
  先行版本号（1 2 3）

1. alpha 内部测试
2. beta 外部测试
3. rc 公测（Release Candidate）
   X.Y.Z-alpha.0
   X.Y.Z-beta.0
4. X 主版本号：当你做了不兼容的 API 修改
5. Y 次版本号：当你做了向下兼容的功能新增
6. Z 当你做了向下兼容的问题修正

> v1.0.2-alpha

## 自动生成 Changelog

1 首次生成`change log`日志

```sh
conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

2 非首次生成`change log`日志

```sh
npm install -g conventional-changelog-cli
cd my-project
conventional-changelog -p angular -i CHANGELOG.md -s
```

3 可以配置脚本
//package.json

```json
  "scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0",
    "version": "conventional-changelog -p angular -i CHANGELOG.md -s && git add CHANGELOG.md"
  },
```

4 通过脚本创建`change log`日志

```sh
yarn version
```

## 监控`webpack`编译性能

// package.json

```json
{
  "build:stats": "webpack --env production -json > stats.json"
}
```
