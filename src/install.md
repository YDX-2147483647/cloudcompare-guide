# 安装 CloudCompare

前往 [CloudCompare - Downloads](https://cloudcompare.org/release/) → Latest stable release，下载合适平台发行版并安装。

如果能正常启动，可直接前往[下一节](./data.md)。

## 已知的兼容问题

CloudCompare一直在升级维护，新环境都能正常用，主要是不兼容旧的。

### 老旧显卡驱动

**问题**：如果是 Radeon 等老旧显卡驱动，CloudCompare 会报如下错误而无法启动，完全不可使用。

> This application needs OpenGL 2.1 at least to run!

**解决办法**：在 [CloudCompare - Downloads](https://cloudcompare.org/release/) 继续向下滚动，改用 Older stuff → Last version compatible with old intel / ATI graphic cards (2.6.3 beta)。

v2.6发布于2016年，不支持自动设置旋转中心，不支持 [SBF 数据格式](https://www.cloudcompare.org/doc/wiki/index.php/SBF)，但也基本可用。

<details>
<summary>详细原因</summary>

CloudCompare [使用 Qt 管理 OpenGL 等图形渲染库](https://www.cloudcompare.org/forum/viewtopic.php?t=6598)，并[于 v2.7.0 从 Qt 4 升级到 Qt 5](https://github.com/CloudCompare/CloudCompare/releases/tag/v2.6.3.1)，而 Qt 5 不兼容这些老旧显卡驱动。

</details>

### Ubuntu 20

**问题**：如果是 Ubuntu 20，CloudCompare 的“打开”菜单无法识别数据格式，打开时会乱；但拖动数据文件到 CloudCompare 内则能正常打开，勉强能用。

可运行以下命令查看 Ubuntu 版本。

```shell
$ lsb_release --description
Description:    Ubuntu 20.04.3 LTS
```

**解决办法**：

- 忽略问题，不用“打开”菜单，只**拖动**数据文件到 CloudCompare 内。
- 或者升级到 Ubuntu 22.04+。

<details>
<summary>详细情况</summary>

原因不明。Ubuntu 20 将于2025年四月停止维护，而开发者精力有限，计划放弃修复这一问题。

相关讨论：

- [Linux Flatpak applications failed to load .las file via 'Open' dialog on Kubuntu · Issue #2072 · CloudCompare/CloudCompare](https://github.com/CloudCompare/CloudCompare/issues/2072#issuecomment-2417884742)
- [Wrong number of points when opening a point cloud, however OK in CLI/ccViewer · Issue #2099 · CloudCompare/CloudCompare](https://github.com/CloudCompare/CloudCompare/issues/2099#issuecomment-2550846517)

</details>
