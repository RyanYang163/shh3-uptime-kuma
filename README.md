# Uptime Kuma

| 项 | 值 |
|---|---|
| 应用 ID | `shh3-uptime-kuma` |
| 形态 | Docker 应用（Compose） · WebUI 外开（浏览器新标签） |
| 版本 | 1.0.0 |
| 上游项目 | https://github.com/louislam/uptime-kuma |
| 上游许可证 | MIT |
| 宿主端口 | 18803 |

## 简介

自托管服务监控：HTTP/TCP/Ping/证书到期监测，带公开状态页。

## 打包

```bash
./build.sh                # 默认 x86_64
./build.sh aarch64        # ARM（Deb 应用）
```

产物在 `build/output/`，同级生成 `<包名>.sha256`。

## 提交前必办事项

- ⚠️ 官方默认禁止跨域 iframe 嵌入（UPTIME_KUMA_DISABLE_FRAME_SAMEORIGIN 默认 false），因此本应用采用「浏览器外开」形态，不用内嵌。
- ⚠️ 必须使用 v2 镜像（v1 已被官方标记 deprecated，且存在多个未修复 advisory）。
- 若启用 Docker 容器监控需挂载 /var/run/docker.sock，这等于把 Docker daemon 的完全控制权交给本应用，权限模型需单独评估，本封装默认不挂载。
- [ ] 真机安装、启动、停止、卸载残留四项实测
- [ ] 首屏加载 ≤ 5 秒（指引 H10）
- [ ] x86_64 与 aarch64 分别构建并测试（指引 H7）
- [ ] 提交前跑一遍指引 13.9 上架前自查清单

## 隐私政策

见 [PRIVACY.md](./PRIVACY.md)（对应审核项 C3–C8）。

## 许可证与出处

本仓库**仅包含 TOS 平台集成所需的配置文件与打包脚本**，应用本体的源码与二进制来自上游项目：https://github.com/louislam/uptime-kuma

上游许可证：**%s**。本封装保留上游许可证声明，未修改上游代码（Deb 形态下按上游许可证要求随包提供 LICENSE）。

应用名称与图标为上游项目的标识；本仓库图标为自行绘制的简易图形，不含上游商标元素（对应审核项 H19）。
