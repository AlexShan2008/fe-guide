
# 《热云前端开发规范之分支管理规范V1.0.0》

1. **分支名不能为汉字，必须以英文开头**
2. **分支命名应该遵循`Type + Name`的规范， `Type`为分支类型，`Name`为功能名称**

- `Type`可选类型如下：
  - feat: 新特性
  - fix: 修改问题
  - test: 测试分支
  - docs: 文档修改
  - style: 代码格式修改, 注意不是 css 修改
  - perf: 性能优化
  - build: 影响build system 或者相关依赖（如: gulp, broccoli, npm, yarn）
  - ci: 更改 CI 配置文件或者脚本（如：Circle, BrowserStack, SauceLabs）
  - refactor: 代码重构
  - chore: 其他修改, 比如构建流程, 依赖管理.

## 分支简介

- master（生产分支）
- pre（预发布分支，代码永远具备可发布生产环境的条件）
- dev（开发分支，时刻保持代码具备发发布测试环境的条件）
- feat-feature-name (新功能开发，应尽可能将功能点拆分）
- fix-feature-name (bug修复)
- test-feature-name (测试分支)

## 示例

- `feature-login` (新功能分支，功能为`login`）
- `fix-login` (`login bug`修复)