# Financial Intelligence Report Generator (FIRG)

基于财经新闻的AI自动研报生成系统。

## 功能

- 从主流财经网站（路透社、彭博社、东方财富等）爬取实时财经新闻
- 利用AI（OpenAI GPT）生成专业财经研报
- 保存新闻数据和生成的研报

## 安装

1. 克隆仓库：
   ```bash
   git clone https://github.com/yourusername/financial-intelligence-report-generator.git
   cd financial-intelligence-report-generator
   ```

2. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```

3. 配置环境变量：
   - 复制 `.env.example` 为 `.env`
   - 在 `.env` 中设置你的OpenAI API密钥
   - 配置代理（如果需要）

## 使用

运行主程序：
```bash
python src/main.py
```

程序将：
1. 爬取配置中启用的新闻源
2. 保存新闻数据到 `data/raw_news/`
3. 生成财经研报并保存到 `data/reports/`

## 配置说明

在 `.env` 文件中可配置：

- `OPENAI_API_KEY`: OpenAI API密钥（必须）
- `OPENAI_MODEL`: 使用的AI模型（默认gpt-3.5-turbo）
- `PROXY_ENABLED`: 是否启用代理
- `HTTP_PROXY`/`HTTPS_PROXY`: 代理设置

在 `config/settings.py` 中可调整：
- 爬虫启用状态和参数
- 数据存储路径
- 财经关键词列表

## 项目结构

```
financial-intelligence-report-generator/
├── config/                   # 配置文件
├── data/                     # 数据存储
├── src/                      # 源代码
├── tests/                    # 测试
├── requirements.txt          # 依赖
├── .env                      # 环境变量
└── README.md                 # 项目文档
```

## 自定义研报格式

要修改研报格式，编辑 `src/ai/prompt_templates.py` 中的模板：

```python
PROMPT_TEMPLATES = {
    "standard": (
        "你是一位资深财经分析师，请基于以下财经新闻生成一份专业、全面的财经研报。"
        "研报结构包括：\n"
        "1. 宏观经济形势概览（300字）\n"
        "2. 重点行业动态分析（400字）\n"
        "3. 金融市场表现与趋势预测（300字）\n"
        "4. 投资策略建议（300字）\n"
        "5. 风险提示（200字）\n\n"
        "要求：\n"
        "- 使用专业财经术语\n"
        "- 数据准确，分析深入\n"
        "- 逻辑清晰，结构严谨\n"
        "- 给出具体投资建议\n\n"
        "新闻摘要如下：\n"
        "{news_summary}"
    ),
    # 可添加其他模板...
}
```

## 注意事项

- 遵守目标网站的爬虫协议（robots.txt）
- 控制爬取频率，避免对目标网站造成压力
- 仅用于个人研究和学习目的

## 许可

MIT License
