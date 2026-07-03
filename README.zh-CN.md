# Agent Secret Guard Action

语言： [English](README.md) | 简体中文

通过 GitHub Actions 运行 `agent-secret-guard`，扫描 AI agent、MCP 和本地自动化仓库中的高风险 secret 与权限配置。

[![GitHub Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-Agent%20Secret%20Guard-blue?logo=github)](https://github.com/marketplace/actions/agent-secret-guard)
[![Main repo](https://img.shields.io/badge/Main%20repo-agent--secret--guard-0f172a?logo=github)](https://github.com/aolingge/agent-secret-guard)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

这个包装 Action 保持很小。扫描器源码、规则、文档和示例都放在主仓库：

- Marketplace：<https://github.com/marketplace/actions/agent-secret-guard>
- 主仓库：<https://github.com/aolingge/agent-secret-guard>
- npm 包：<https://www.npmjs.com/package/agent-secret-guard>
- 修复指南：<https://github.com/aolingge/agent-secret-guard/blob/main/docs/remediation.md>
- 更新记录：[CHANGELOG.md](CHANGELOG.md)

## 快速开始

```yaml
name: Agent Secret Guard

on:
  pull_request:
  push:
    branches: [main]

permissions:
  contents: read

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
        with:
          persist-credentials: false
      - uses: aolingge/agent-secret-guard-action@v0.1.5
        with:
          path: .
          fail-on: high
```

## 输入参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| `path` | `.` | 要扫描的目录或文件。 |
| `fail-on` | `high` | 触发失败的最低严重级别：`low`、`medium`、`high` 或 `critical`。 |
| `format` | `text` | 输出格式：`text`、`json` 或 `sarif`。 |
| `output` | 空 | 可选输出文件路径。 |

## SARIF 示例

```yaml
- uses: aolingge/agent-secret-guard-action@v0.1.5
  with:
    path: .
    fail-on: high
    format: sarif
    output: agent-secret-guard.sarif

- uses: github/codeql-action/upload-sarif@v4
  if: always()
  with:
    sarif_file: agent-secret-guard.sarif
```

## 版本策略

每个 Action tag 都会在 `action.yml` 里固定一个 `agent-secret-guard` npm 包版本，保证 workflow 可复现。

想获得新的扫描规则时，请先查看这个包装器的 [更新记录](CHANGELOG.md) 和主扫描器的 [release notes](https://github.com/aolingge/agent-secret-guard/releases)，再升级 Action tag。

## 它会检查什么

- MCP token 是否通过命令参数泄露。
- API / package token 是否硬编码。
- agent 或自动化配置里的广泛文件系统访问。
- 浏览器 profile 和凭据存储暴露。
- agent 指令中的危险 shell 命令。
- 过度开放的 GitHub Actions workflow。

## 发布前指南

准备发布 AI agent、MCP server 或自动化仓库时，先看主项目的 [launch kit](https://github.com/aolingge/agent-secret-guard/blob/main/docs/launch-kit.md) 和 [remediation guide](https://github.com/aolingge/agent-secret-guard/blob/main/docs/remediation.md)。

## 隐私

这个 Action 会在 workflow 里直接运行 npm CLI 包，不会把结果上传到远程服务。文本、JSON 和 SARIF 报告都可能包含私有路径或上下文证据，仍应视为敏感产物。

## 贡献

包装器相关修改见 [CONTRIBUTING.md](CONTRIBUTING.md)。扫描规则的修改应提交到主仓库 [`agent-secret-guard`](https://github.com/aolingge/agent-secret-guard)。

## License

MIT

## Support

包装器运行问题请通过 [bug report form](https://github.com/aolingge/agent-secret-guard-action/issues/new?template=bug_report.yml) 提交。扫描规则建议和误报反馈请到主仓库 [`agent-secret-guard`](https://github.com/aolingge/agent-secret-guard)。

如果这个项目帮你节省了时间，可以在这里支持后续维护：[Buy Me a Coffee](https://www.buymeacoffee.com/aolingge)。
