# MSSP Speech Paper Skim 使用说明

这个仓库从 arXiv 自动收集 speaker-centric speech research，并按四个主题生成论文速览：

- Speech Separation
- Speech Enhancement
- Speaker Diarization
- Multi-Talker ASR (Speaker-Attributed ASR)

## 本地运行

```bash
python3 -m pip install -r requirements.txt
python3 daily_arxiv.py
```

论文数据累积在 `docs/mssp-arxiv-daily*.json`，随后生成 `README.md`、`docs/index.md` 和 `docs/wechat.md`。

每周补查论文代码链接：

```bash
python3 daily_arxiv.py --update_paper_links
```

## 如何调整主题

在 [config.yaml](../config.yaml) 的 `keywords` 下修改主题：

- `filters`：标题关键词，多个关键词用 `OR` 连接。
- `field`：`ti` 只查标题，相关性更高；`all` 同时查标题和摘要，召回率更高。
- `categories`：arXiv 分类过滤。语音任务通常使用 `eess.AS`、`eess.SP`、`cs.SD`、`cs.MM` 和 `cs.CL`。
- `max_results`：每个主题每次抓取的数量。

如果新增主题，只需在 `keywords` 下添加同样结构的配置，不需要修改 Python 代码。若想完全重建历史，先备份并删除 `docs/mssp-arxiv-daily*.json`，再重新运行脚本。
