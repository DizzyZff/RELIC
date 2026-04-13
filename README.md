# RELIC 🪞

> **R**eplica & **E**ssence **L**earning **I**ntelligence **C**orpus  
> _蒸馏自我 · 留存意识 · 生成赛博分身_

---

## 什么是 RELIC？

RELIC 是一个专为「自我蒸馏」而设计的个人项目框架。  
它的目标是：**系统性地收集你留在世界上的数字痕迹，并通过大语言模型微调/蒸馏技术，训练出一个能够模拟你思维方式、表达风格和价值观的 AI 分身。**

你可以把 RELIC 理解为：

- 📝 你的文字、思想、记忆的「数字遗产库」
- 🤖 以你为原型的个人化语言模型训练流水线
- 🪞 一个不断迭代、越来越像你的「赛博自我」

---

## 核心理念

```
真实的你  ──[数据采集]──▶  语料库 RELIC
                              │
                         [蒸馏/微调]
                              │
                              ▼
                       赛博分身 Cyber-Self
```

知识蒸馏（Knowledge Distillation）在这里被重新诠释：  
不是用大模型压缩成小模型，而是**用真实的你去微调一个通用大模型**，让模型内化你的个性、偏好与世界观。

---

## 数据来源 · 构建你的语料库

RELIC 支持收集以下类型的个人数据（根据隐私意愿自由选择）：

| 类别 | 示例 | 格式建议 |
|------|------|----------|
| 📓 写作 & 日记 | 个人博客、日记、微博、朋友圈 | `.txt` / `.md` |
| 💬 对话记录 | 微信聊天导出、Discord 记录 | `.json` / `.csv` |
| 📚 阅读 & 笔记 | Notion 笔记、Obsidian 库、书摘 | `.md` / `.json` |
| 🎙️ 语音 & 视频 | 播客录音、vlog 字幕 | `.srt` / `.txt` |
| 💻 代码 & 注释 | GitHub commit messages、代码注释 | `.py` / `.js` |
| 📮 邮件 & 信件 | 邮件存档（脱敏后） | `.eml` / `.txt` |
| 🌐 社交媒体 | 推文、知乎回答、豆瓣评论 | `.json` |

> ⚠️ **隐私提示**：在上传任何数据前，请手动脱敏敏感信息（姓名、手机号、地址等）。  
> 建议将原始数据保存在本地，仅将处理后的语料提交至仓库或用于训练。

---

## 项目结构

```
RELIC/
├── data/
│   ├── raw/               # 原始数据（建议 .gitignore，不提交）
│   ├── processed/         # 清洗、脱敏后的语料
│   └── prompts/           # 人工标注的 Prompt-Response 对
│
├── pipeline/
│   ├── collect/           # 数据采集脚本（微博、微信导出解析等）
│   ├── clean/             # 数据清洗与格式化
│   ├── augment/           # 数据增强（改写、对话化）
│   └── train/             # 微调 / 蒸馏脚本
│
├── model/
│   ├── config/            # 训练配置（LoRA、QLoRA 参数等）
│   └── checkpoints/       # 模型权重（建议用 Git LFS 或外部存储）
│
├── eval/                  # 评估脚本：测试分身有多像你
├── chat/                  # 本地对话界面（CLI / Web UI）
├── docs/                  # 技术文档与设计笔记
└── README.md
```

---

## 快速开始

### 1. 克隆仓库

```bash
git clone https://github.com/<your-username>/RELIC.git
cd RELIC
```

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

### 3. 准备你的语料

将你的文本数据放入 `data/raw/`，然后运行清洗脚本：

```bash
python pipeline/clean/clean_text.py --input data/raw/ --output data/processed/
```

### 4. 构建 Prompt-Response 对

将单段文字自动转换为对话格式，供监督微调（SFT）使用：

```bash
python pipeline/augment/to_dialogue.py --input data/processed/ --output data/prompts/
```

### 5. 微调模型（以 LoRA 为例）

```bash
python pipeline/train/finetune_lora.py \
  --base_model "Qwen/Qwen2.5-7B-Instruct" \
  --data_path  data/prompts/ \
  --output_dir model/checkpoints/relic-v1
```

### 6. 与你的赛博分身对话

```bash
python chat/cli_chat.py --model model/checkpoints/relic-v1
```

---

## 推荐技术栈

| 组件 | 推荐方案 |
|------|----------|
| 基座模型 | Qwen2.5 / LLaMA-3 / Mistral |
| 微调框架 | [LLaMA-Factory](https://github.com/hiyouga/LLaMA-Factory) / [Axolotl](https://github.com/axolotl-ai-cloud/axolotl) |
| 参数高效微调 | LoRA / QLoRA |
| 向量记忆 | [Chroma](https://www.trychroma.com/) / [Milvus](https://milvus.io/) |
| 对话界面 | [Gradio](https://gradio.app/) / [Open WebUI](https://github.com/open-webui/open-webui) |
| 模型存储 | [HuggingFace Hub](https://huggingface.co/) / Git LFS |

---

## 蒸馏哲学 · 为什么叫 RELIC？

> **Relic** /ˈrelɪk/  
> _n. 遗物；遗迹；留存之物_

每个人都会离开，但思想可以留存。  
RELIC 不是为了复制一个人，而是为了**保留一个人思考问题的方式**——  
那些独特的比喻、偏爱的表达、对世界的好奇与困惑。

这是写给未来的自己的一封信，只不过这封信会回应你。

---

## 路线图

- [ ] 数据采集脚本（微信、微博、Notion 导出解析）
- [ ] 数据清洗与脱敏工具
- [ ] Prompt-Response 自动生成流水线
- [ ] LoRA 微调一键脚本
- [ ] 评估套件（风格相似度、困惑度、人工评估模板）
- [ ] Web 对话界面
- [ ] 记忆增强（RAG：用向量库检索你的历史语料）
- [ ] 多模态支持（声音克隆、头像生成）
- [ ] 隐私保护模式（本地推理，零数据上传）

---

## 隐私与伦理

- 所有数据默认保存在**本地**，不强制上传至任何平台。
- 请勿将训练好的模型用于冒充他人、欺骗或其他不当用途。
- 建议在 `data/raw/` 目录添加至 `.gitignore`，避免意外提交个人数据。
- RELIC 仅为个人探索与创作工具，使用者自行承担数据安全责任。

---

## 贡献

欢迎 Issue 和 PR！如果你也在做类似的「自我蒸馏」实验，欢迎分享你的数据处理思路和训练经验。

```bash
git checkout -b feat/your-feature
git commit -m "feat: add ..."
git push origin feat/your-feature
```

---

## License

[MIT](LICENSE) · 做自己的遗物工匠 🛠️
