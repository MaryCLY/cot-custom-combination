# cot-custom-combination

## 更新上游汉化版

脚本使用 Python 标准库，无需安装依赖。它会查询
`BlackTeaPie/Course-of-Temptation-Chinese-Localization` 的最新 release，并完成以下操作：

- 从普通版与兼容版加载器压缩包中提取 HTML，保存为固定文件名
  `vanilla/index.html` 和 `vanilla/polyfill.html`。
- 将图片包和汉化包去掉版本号后保存为
  `mods/CoTGameOriginalImagePack.mod.zip` 和 `mods/ModI18N.mod.zip`。
- 更新首页版本号、加载器元数据，并启用兼容模式入口。

仅更新本地文件：

```powershell
python .\update_upstream.py
```

仅检查是否存在新版本：

```powershell
python .\update_upstream.py --check
```

更新后自动提交并推送到 `origin`：

```powershell
python .\update_upstream.py --publish
```

`--publish` 要求运行前工作区干净。脚本默认根据首页中的
`cot-loader-version` 元数据判断是否需要更新；使用 `--force` 可强制重新下载。
设置 `GITHUB_TOKEN` 或 `GH_TOKEN` 可以避免 GitHub API 的匿名请求限流；
未设置或 API 限流时，脚本会自动改用 GitHub release 页面查询。

## 自动更新

GitHub Actions 工作流每天北京时间凌晨 3:17 自动运行更新脚本。也可以在仓库的
Actions 页面手动运行 `Update upstream release` 工作流，或发送类型为
`upstream_release` 的 `repository_dispatch` 事件触发更新。

工作流使用仓库自带的 `GITHUB_TOKEN` 提交并推送更新，需要仓库允许 GitHub
Actions 对内容进行写入。
