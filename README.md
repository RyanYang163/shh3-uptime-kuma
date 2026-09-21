# Uptime Kuma

| 项 | 值 |
|---|---|
| 应用 ID | `shh3-uptime-kuma` |
| 形态 | Docker 应用（Compose） · WebUI 外开（浏览器新标签） |
| 版本 | 1.0.006 |
| 上游项目 | https://github.com/louislam/uptime-kuma |
| 上游许可证 | MIT |
| 宿主端口 | 18803 |

## 简介

自托管服务监控：HTTP/TCP/Ping/证书到期监测，带公开状态页。

## 打包

```bash
./build.sh
```

产物在 `build/output/shh3-uptime-kuma.tar.gz`，同级生成 `.sha256`。
归档根层恰好 4 个文件（`config.ini` / `shh3-uptime-kuma.lang` / `shh3-uptime-kuma.svg` /
`docker-compose.yml`），架构由 `config.ini` 的 `platform` 决定，与压缩包无关。

## 提交前必办事项

- ⚠️ 官方默认禁止跨域 iframe 嵌入（`UPTIME_KUMA_DISABLE_FRAME_SAMEORIGIN` 默认 false），因此本应用采用「浏览器外开」形态，不用内嵌。
- ⚠️ 必须使用 v2 镜像（v1 已被官方标记 deprecated，且存在多个未修复 advisory）。本封装锁定 `2.5.5-slim`（`-slim` 变体不捆绑 Chromium，可消除绝大部分漏洞）。
- 若启用 Docker 容器监控需挂载 `/var/run/docker.sock`，这等于把 Docker daemon 的完全控制权交给本应用，权限模型需单独评估，**本封装默认不挂载**。
- [ ] 真机安装、启动、停止、卸载残留四项实测
- [ ] 首屏加载 ≤ 5 秒（指引 H10）
- [ ] x86_64 与 aarch64 分别提交（指引 H7）
- [ ] 提交前跑一遍指引 13.9 上架前自查清单

## 隐私政策

见 [PRIVACY.md](./PRIVACY.md)（对应审核项 C3–C8）。

## 许可证与出处

本仓库**仅包含 TOS 平台集成所需的配置文件与打包脚本**，应用本体的源码与二进制来自上游项目：
https://github.com/louislam/uptime-kuma

上游许可证：**MIT**。本封装保留上游许可证声明，未修改上游代码。

应用名称与图标为上游项目的标识；本仓库图标为自行绘制的简易图形，不含上游商标元素（对应审核项 H19）。

## 已知镜像漏洞基线（审核项 T1 / S10）

上游镜像 `louislam/uptime-kuma:2.5.5-slim` 内捆绑了若干第三方组件，带有已知 HIGH/CRITICAL 通告：

| 来源 | 说明 |
|------|------|
| `usr/bin/cloudflared` | 上游捆绑的 Go 二进制（Go stdlib 1.26.3 + `golang.org/x/crypto` + `grpc`） |
| `app/extra/healthcheck` | 上游捆绑的 Go 二进制（Go stdlib 1.20.5） |
| Debian 12 基础层 | `libgnutls30`、`libpcre2-8-0`、`python3.11`（apprise 依赖）、`curl`、`libssh2-1` 等 |
| Node 依赖 | `tar`、`protobufjs`、`brace-expansion`、`minimatch`、`liquidjs`、`nodemailer` 等 |

**这些漏洞全部位于上游发布的镜像内部。** 本仓库不含任何镜像层，只有
`config.ini` / `.lang` / `.svg` / `docker-compose.yml` 四个文件，换 tag 或改封装都无法消除。

`trivy 0.74.0`（DB 2026-09-21）实测：**HIGH/CRITICAL 共 225 个，其中存在官方修复的 118 个**。
本封装已选用 `-slim` 变体，把不捆绑 Chromium 的那部分漏洞（原为 1786 个）先行消除。

发版工作流采用**回归门禁**（可修复数不得超过已声明基线）而非零容忍门禁，并把完整报告随
Release 附上。该情况已按**平台 T1 豁免通道**申报 —— 依《开发者审核表 V2.3》，T1「无已知高危 CVE」
属**挂起 + 豁免**项，驳回项仅 V4（恶意代码）与 V12（违法内容）两条。

上游修复进展：<https://github.com/louislam/uptime-kuma>

## 更新记录

### v1.0.2（2026-09-21）
- 镜像由浮动 tag `2-slim` 改为锁定 `2.5.5-slim`（符合「锁定具体版本」要求）
- 补 container healthcheck（此前完全缺失，违反指引 6.3）
- 补 `docker-compose.yml` 内的上游许可与版权声明头（审核项 C2：Docker 包根层限 4 文件，
  许可证只能声明在包内）
- 重写 `PRIVACY.md`：原先描述的是 systemd 加固措施，对本 Docker 应用并不存在；改为按容器实际机制描述
- 发版工作流：trivy 门禁由零容忍改为「已声明基线的回归门禁」

### v1.0.1（2026-09-20）
- 补齐合规材料（LICENSE / NOTICE / PRIVACY.md），分类改为官方白名单值

### v1.0.0
- 首次发布
