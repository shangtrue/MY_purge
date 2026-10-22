# MY_purge

`dsh-purge` 的独立维护分支。

## 为什么有这个仓库

上游仓库 `YuJunZhiXue/dsh-purge` 已被作者删除（GitHub API 返回 404）。
本仓库是删除前最后一版源码的快照（v1.1.71，profile lockfile 里钉的 commit
`6c1d638d1bdcc45ede50fc30249c753d58122a51`），用于继续使用与维护。

## 相对上游的改动

1. **崩溃修复** `lib/desktop.js:1768`：`repairOfficialCliAfterUnpack()` 备份 `dsh.cmd` 时把
   async 的 `atomicCopyFile` 当同步调用，rejection 逃出 `try/catch` 成为
   `unhandledRejection`，Node 24 直接判死 → `dsh: fatal load failure` → host exit 1。
   改为同步 `fs.copyFileSync`。

2. **仓库地址**：`package.json` 的 repository / homepage / bugs / `dsh.install` 四处，
   以及 `lib/update.js:12` 的 `REPO` 常量、`client.js` 的欢迎页链接、
   `lib/redteam/ui.js` 的仓库名，全部指向本仓库，使插件内置的「检查更新」
   能查到这里而不是一个已删除的地址。

## 安装

```sh
dsh plugin --profile desktop add github:shangtrue/MY_purge
```

## 许可

原项目 MIT，版权归原作者「小杨」，见 [LICENSE](./LICENSE)。本仓库保留原 LICENSE 不变。
