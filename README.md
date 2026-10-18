# dsh-journal-panel

「思维年轮」的 DSH 浮动面板插件。在 DSH 右上角放一个「年」按钮，点开后读取本机 `http://127.0.0.1:8765/api/summary`，显示：

- 会话数 / 已确认洞察 / 待确认洞察
- 本周一句话 + 周报链接
- 五维状态（证据不足时显示“观察中”）
- 最新画像摘要、L4 档案链接
- 打开完整网页

完整网页仍然是主界面；这个面板只做“大概”。

主项目（引擎 + 网页 + 报告）：**[Hagen121212/dsh-journal](https://github.com/Hagen121212/dsh-journal)**。装这个插件之前，主项目要已经能跑起来，本地 Web 服务在 `127.0.0.1:8765` 上。

> 非官方插件。它依赖 DSH 的内部注入点（`webserver/index-inject`、`webServer.register`、`tapIndex`），只在 2026-10 的 DeepSeek Harness 桌面版上验证过；升级 DSH 后若按钮消失，先按下面的回滚。

## 安装

从本地目录（克隆后）：

```powershell
git clone https://github.com/Hagen121212/dsh-journal-panel.git
dsh plugin --profile desktop add .\dsh-journal-panel
```

从 npm（发布后）：

```powershell
dsh plugin --profile desktop add dsh-journal-panel
```

安装后**完整重启** DeepSeek Harness。桌面端的注入表在启动时收集，热加载只会注册 API，不会补上按钮。

## 配置

面板默认连 `http://127.0.0.1:8765`。如果本地 Web 换了端口，改 `lib/client.js` 顶部的默认值，或在页面里提前注入：

```html
<script>window.__DSH_JOURNAL_API__ = "http://127.0.0.1:9000";</script>
```

这个变量必须在插件脚本执行前设置。

## 回滚

```powershell
dsh plugin --profile desktop remove dsh-journal-panel
```

## 边界

- 只读本机的 `127.0.0.1`，不向外发任何请求。
- 面板不写数据库；接受/驳回洞察仍在完整网页里完成。
- 主项目升级后，这个仓库的 `lib/client.js` 可能与网页的 `/api/summary` 字段不同步；升级主项目时一起看。

## 许可证

MIT，见 [LICENSE](LICENSE)。与 DeepSeek 官方无关。
