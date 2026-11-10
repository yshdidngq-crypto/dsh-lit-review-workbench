# 文献综述工作台 · DSH 插件

把一批**已经下好的论文**整理成一份**单文件离线 HTML 工作台**：能点、能筛、能对比、能判断先读哪篇。
不是下载器，不是阅读器，不是摘要生成器，也不写成品综述。

装好之后，`lit-review-workbench` 这个 skill 出现在 DSH 的技能列表里，模型会自己用，你也可以用 `/skill` 点名。

## 它做什么

- **研究现状八问**：主题构成、技术环节、逐年变化、方法分布、数据集、发表分布、集中单位、质量标记，每条结论都带口径与 caveat。
- **方向树**：把研究空白做成可点开的树，节点标机会分与风险。
- **文献数据库**：搜索、筛选、排序、对比、阅读状态、笔记。
- **查新**：给一句话方向，去 Crossref / arXiv 找最像的 10–40 篇，标「可能撞车 / 部分重合 / 关系不大」，并标检索时间与命中最新年份。
- **外部文献**：候选池、相关性打分、BibTeX/RIS 导出。

## 三道可执行门禁

产出必须过 `scripts/build.py` → `scripts/validate.js` → `scripts/smoke.js`：样式锁在 `assets/` 里，数据写进 `config.json` + `data/*.json`，所以换人换机器产出一致。

```bash
python scripts/build.py <项目目录>
node scripts/validate.js <产物.html>
node scripts/smoke.js <产物.html>
```

## 依赖

- Python ≥ 3.10（只有 `scripts/pdf2md.py` 需要 PyMuPDF，其余全用标准库）
- Node ≥ 22（`validate.js`、`smoke.js`、`check_docs.js`、`test_click.js`）
- `test_click.js` 额外需要本机 Edge 或 Chrome；没有浏览器时它会以退出码 2 退出，表示「没测」而不是「通过」。

## 它不做什么

- 不替你下载论文，不抓知网/万方（中文库不在查新范围里）。
- 不判断你有没有创新 —— 查新只回答「这两个库里有没有像的」。
- 不保证你录入的数据是对的：`band`、`relevance` 与阈值不一致时门禁会提醒，但改不改是你的事。

## 安装

在 DSH 的「插件管理 → 添加插件」里填本仓库，或在插件市场里搜「文献综述工作台」。

## License

MIT
