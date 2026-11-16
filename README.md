# 欲蓝财务 · 插件索引仓库

这是 [插件市场](https://yulancloud.us.ci/market/) 的数据源。**插件本体存在 GitHub 上**（开发者自己的仓库 / Release，或本仓库 `packages/`），市场页只读取本仓库的 `plugins.json` 来渲染，纯静态、无后端。

配套仓库：[yulancloud/plugin-template](https://github.com/yulancloud/plugin-template)（模板仓库，点 `Use this template` 一键创建插件仓库）。

## 目录

```
plugins/
├── plugins.json                        ← 索引清单（市场页读这个）
├── packages/                           ← 官方示例插件包（可选，也可用各自仓库 Release）
│   └── hello-world-v1.0.0.zip
├── assets/                             ← 图标等静态资源
│   └── hello-world.svg
└── .github/ISSUE_TEMPLATE/
    ├── plugin-submit.yml               ← 「上传插件」提交表单（Issue Form）
    └── config.yml                      ← 入口分流
```

## 用户怎么上传插件

市场页的「上传插件」按钮会打开本仓库的 **Issue Form 表单**（`plugin-submit.yml`）。用户填写插件信息与 zip 直链后提交为一个 Issue，维护者审核，通过后把条目合并进 `plugins.json`，市场页下次加载就会自动出现。

> 这就是 GitHub 专门提供的两种仓库能力：**Template repository**（开发者一键建仓）和 **Issue Forms**（结构化收集提交），不需要自己搭服务器或数据库。

## plugins.json 字段

| 字段 | 必填 | 说明 |
| --- | --- | --- |
| `id` | ✅ | 小写英文 + 连字符，全市场唯一 |
| `name` | ✅ | 显示名称 |
| `version` | ✅ | 语义化版本，如 `1.0.0` |
| `author` | ✅ | 作者名 / GitHub ID |
| `description` | ✅ | 一句话说明加了什么功能，建议 40–80 字 |
| `category` | ✅ | 必须是 `categories` 里的值 |
| `tags` | | 数组，展示成小标签 |
| `icon` | | svg/png 公开直链，留空则市场页用首字占位 |
| `download` | ✅ | **zip 公开直链**（Release 资产或 raw 链接），点「下载」直接取这个文件 |
| `homepage` | | 插件仓库 / 介绍页 |
| `docs` | | 安装说明页，默认指向文档站安装教程 |
| `requires` | ✅ | 兼容的系统版本，如 `>=1.1.0` |
| `build` | | 适配的 build 号，如 `20261115a` |
| `updated` | ✅ | `YYYY-MM-DD`，市场页按它排序 |
| `size` | | 包大小，纯展示 |
| `verified` | | 官方审核过标 `true`，卡片显示「已验证」 |
| `featured` | | 推荐位标 `true` |

`schema` / `name` / `updated` / `market` / `template` / `submit` / `docs` / `submitDocs` / `categories` 是顶层配置，`plugins` 是插件数组。

## 维护者审核清单

- [ ] zip 直链能公开下载，解压后含 `plugin.json` + `INSTALL.md` + `files/`
- [ ] `plugin.json` 合法 JSON，`id` 不重复，版本号与文件名一致
- [ ] `INSTALL.md` 写清备份、复制、迁移、bump、验证、卸载
- [ ] 包内无 `data/shop.sqlite`、`config/config.php`、密钥、`.git/`
- [ ] 代码无远程上报 / 外链脚本 / 混淆，与描述的功能一致
- [ ] 在干净的 v1.1.0 上按 `INSTALL.md` 实测安装与卸载
- [ ] 合并后 `plugins.json` 仍是合法 JSON，本地跑 `python3 -m json.tool plugins.json` 确认

审核通过后把条目加进 `plugins` 数组，更新顶层 `updated`，回复并关闭 Issue。

## 相关链接

- [插件市场](https://yulancloud.us.ci/market/)
- [如何安装插件（小白教程）](https://doc.yulancloud.us.ci/plugins/install)
- [如何上传插件](https://doc.yulancloud.us.ci/plugins/submit)
- [插件开发模板仓库](https://github.com/yulancloud/plugin-template)
- [功能自定义教程（怎么加新功能）](https://doc.yulancloud.us.ci/developer/custom)
