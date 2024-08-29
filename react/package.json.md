# package.json

> **package.json** 是 Node.js 项目的配置文件，你可以把它想象成项目的身份证。它详细描述了项目所需要的各种模块、项目的配置信息（比如名称、版本、许可证等元数据），以及一些自定义的脚本命令。

### package.json 的主要作用：

- 依赖管理：
  - **列出依赖项：** 清晰地列出项目所依赖的所有第三方模块，以及它们的版本号。
  - **自动安装：** 通过 `npm install` 命令，根据 package.json 中的配置自动安装所有依赖。
  - **版本控制：** 使用语义化版本控制，确保项目在不同环境下保持一致性。
- 项目配置：
  - **项目信息：** 包括项目名称、版本号、描述、作者等基本信息。
  - **脚本配置：** 定义自定义的脚本命令，例如启动开发服务器、构建项目、运行测试等。
- 项目发布：
  - **发布到 npm：** 将项目发布到 npm 上，方便其他人使用。
  - **提供元数据：** 为 npm 上的项目提供详细的元数据信息。





**package.json** 是 Node.js 项目的配置文件，它包含了项目所需的各种信息，如项目名称、版本、依赖、脚本等。下面我们来详细介绍一下 package.json 中各个字段的作用：

### 必需字段

- **name:** 项目的名称，必须是唯一的，通常是小写字母和连字符的组合。
- **version:** 项目的版本号，遵循语义化版本规范（Semantic Versioning，SemVer）。

### 描述性字段

- **description:** 项目的简短描述，用于说明项目的功能。
- **keywords:** 项目的关键词，用于搜索和分类。
- **author:** 项目作者的信息，可以是姓名或邮箱地址。
- **license:** 项目使用的许可证，例如 MIT、GPL 等。
- **homepage:** 项目的主页地址。
- **bugs:** 报告 bug 的地址，通常是一个 issue tracker 的链接。
- **repository:** 项目的代码仓库地址。

### 依赖管理字段

- **dependencies:** 项目在生产环境中所依赖的模块，以及它们的版本号。
- **devDependencies:** 项目在开发环境中所依赖的模块，如测试框架、构建工具等。
- **peerDependencies:** 项目的运行依赖于其他特定的模块，但这些模块不会被自动安装。
- **optionalDependencies:** 项目的可选依赖，即使安装失败也不会影响项目的运行。

### 配置字段

- **main:** 指定模块的入口文件。
- **bin:** 指定可执行文件的路径。
- **scripts:** 自定义的脚本命令，例如 `start`、`test`、`build` 等。
- **config:** 配置项目的一些选项，例如环境变量。
- **files:** 指定打包时需要包含的文件。
- **man:** 指定项目的文档。
- **directories:** 指定项目目录的结构。

### 其他字段

- **engines:** 指定项目支持的 Node.js 版本。
- **os:** 指定项目支持的操作系统。
- **cpu:** 指定项目支持的 CPU 架构。
- **private:** 设置为 true 时，表示该项目不会发布到 npm。
- **publishConfig:** 发布到 npm 时的一些配置选项。



**package.json** 文件中的 `scripts` 字段是用来定义自定义脚本命令的。这些脚本命令可以通过 `npm run` 命令来执行。

### 为什么使用 scripts？

- **自动化任务：** 可以将常用的开发任务（如启动开发服务器、运行测试、构建项目等）定义为脚本，简化操作。
- **提高效率：** 通过自定义脚本，可以避免手动执行繁琐的命令。
- **统一团队规范：** 团队成员可以通过运行相同的脚本命令来执行相同的任务，保证开发环境的一致性。

### 常用的 scripts 命令

- **start:** 启动开发服务器
- **dev:** 运行开发环境
- **build:** 构建生产环境代码
- **test:** 运行测试用例
- **lint:** 代码风格检查
- **format:** 代码格式化
- **clean:** 清除构建产物
- **prepublishOnly:** 在发布到 npm 之前执行的脚本

### scripts 的高级用法

- **环境变量：** 可以使用 `process.env` 获取环境变量。
- **npm scripts 生命周期脚本：** preinstall、postinstall、prepublishOnly、postpublish 等。
- **并行执行：** 使用 `&&` 或 `||` 连接多个命令。
- **跨平台脚本：** 使用 cross-env 或 npm-run-all 等工具。

### 示例：

```json
{
  "scripts": {
    "start": "cross-env NODE_ENV=development nodemon index.js",
    "build:prod": "cross-env NODE_ENV=production webpack --mode production",
    "test:unit": "jest",
    "test:e2e": "cypress run"
  }
}
```