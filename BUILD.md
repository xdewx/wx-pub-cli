# wx-pub-cli 本地构建与使用

本仓库基于 Wenyan CLI 源码，保留 Apache-2.0 许可和原 `wenyan` 命令，并提供 `wx-pub-cli` 命令。`publish` 会将文章写入微信公众号草稿箱，不会直接公开发表或群发。

本地从源码构建（已用 Node.js 24、pnpm 10.7.1 验证）：

```bash
pnpm install --frozen-lockfile
pnpm build
pnpm pack
```

在本机安装构建出的 `.tgz` 包：

```bash
npm install -g ./xdewx-wx-pub-cli-2.0.12.tgz
wx-pub-cli --help
```

将 `WECHAT_APP_ID` 和 `WECHAT_APP_SECRET` 仅配置在本机私密环境中，并将本机出口 IP 加入公众号白名单。准备包含标题和封面的 Markdown 后运行 `wx-pub-cli publish -f article.md`。先以测试文章验证账号的草稿接口权限；未提供凭证时可以运行 `wx-pub-cli render -f article.md` 做离线排版验证。

安装 `.tgz` 时，npm 会按包声明解析依赖；若需要严格复现本次构建，应使用仓库锁文件执行 `pnpm install --frozen-lockfile` 并从源码运行 `node dist/cli.js`。
