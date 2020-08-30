# commitlint-cli

## 前言

最近在公司内部需要引入commit规范以及相关配置，但是项目工程过多，一个个单独引用太过于麻烦，后续修改配置、升级想想就头大，于是花了几个小时找了以下资料，再结合自身的思考，写了一个简单的cli工具来完成自动引入commit配置，并把相关规范也写入工具中，以后只需要升级规范，重新运行命令即可更新配置😄。

## commitlint-cli介绍

用于在项目中快速引入 commit message 规范和 commitlint 相关配置规范

实现了自动引入 `git-cz` `commitizen` `commitlint` `conventional-changelog-cli` `husky` 依赖以及封装好的commit规范和commitlint相关配置，开箱即用，只需要安装`commitlint-cli`后，运行`commitlint-cli`命令后就能生成相关配套设置，简单粗暴。

附上Github地址：[commitlint-cli](https://github.com/ht1131589588/commitlint-cli)

commit规范和相关配置可以去另外一篇文章看一下: [commit规范及自动生成changelog](https://juejin.im/post/6863342912320339982)

再说明一下，让我自己一行一行去写规范的代码，太花时间了，直接借用了别人写好的代码，稍微简单修改了一下，附上连接：[开箱即用的代码提交规范](https://juejin.im/post/6844904004749623309)

## 功能列表

1. 自动检测 commit 是否规范，不规范不允许提交
2. 自动提示 commit 填写格式。不怕忘记规范怎么写
3. 集成 git add . && git commit 不需要在执行两个命令
4. 自动生成 changelog
5. 自动生成以上配置

## 使用

安装 `commitlint-cli`

```bash
npm i commitlint-cli -D
```

执行`npx commitlint-cli`

```bash
npx commitlint-cli
```

会自动在 package.json 中添加相关配置和命令

```json
{
  "scripts": {
    "log": "conventional-changelog --config ./node_modules/commitlint-cli/lib/log -i CHANGELOG.md -s -r 0",
    "commit": "npm log && git add . && git-cz"
  },
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
  "config": {
    "commitizen": {
      "path": "./node_modules/commitlint-cli/lib/cz"
    }
  }
}
```

会自动增加 `commitlint.config.js` 文件

```js
module.exports = {
  extends: ['./node_modules/commitlint-cli/lib/lint']
};
```

## 命令介绍

```bash
npm run commit  # npm run log && git add . && git-cz
npm run log # 生成 CHANGELOG
```

## commit type 规则简单说明

* **feat**: 一个新特性
* **fix**: 修了一个 Bug
* **docs**: 更新了文档（比如改了 Readme）
* **style**: 代码的样式美化，不涉及到功能修改（比如改了缩进）
* **refactor**: 一些代码结构上优化，既不是新特性也不是修 Bug（比如函数改个名字）
* **perf**: 优化了性能的代码改动
* **test**: 新增或者修改已有的测试代码
* **chore**: 跟仓库主要业务无关的构建/工程依赖/工具等功能改动（比如新增一个文档生成工具）

## 参考资源

- [开箱即用的代码提交规范](https://juejin.im/post/6844904004749623309)

有问题欢迎指出，有用欢迎点个赞😊