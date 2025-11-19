Hybrid Event-Driven Trading System using XGBoost and Large Language Models
基於 XGBoost 事件偵測與大型語言模型語義推理之混合式盤中交易決策系統
📌 專案總覽（Overview）

本專案致力於建立一套盤中事件驅動（Event-Driven）的交易決策系統，透過傳統機器學習與大型語言模型（LLM）結合，提升訊號偵測能力、解釋性與決策一致性。

系統包含三大核心模組：

L0 — XGBoost 事件偵測（Signal Detection）

L1 — SHAP 語義轉譯（Semantic Translation）

L2 — LLM 決策代理人（Decision Agent）

此架構將 ML 的量化精確度與 LLM 的語義推理能力整合，打造出能「理解市場背景、過濾假訊號、產生可解釋決策」的 AI 交易系統。

📂 專案資料夾結構
├── data/
│   ├── raw/                 # 原始 Tick / K 線資料
│   ├── processed/           # 前處理與特徵工程後的資料
│   └── labels/              # Triple-Barrier 標註結果
│
├── docs/
│   ├── literature/          # 文獻整理、筆記
│   ├── methodology/         # 架構圖、公式推導、方法說明
│   ├── experiments/         # 測試與實驗紀錄
│   └── thesis/              # 論文內容（LaTeX / Markdown）
│
├── src/
│   ├── L0_detect/           # XGBoost 訓練 + Triple-Barrier 標註
│   ├── L1_semantic/         # SHAP-to-text 語義生成邏輯
│   ├── L2_agent/            # LLM 推理與決策模組
│   ├── features/            # 技術指標 & 微結構特徵
│   └── backtest/            # 回測引擎與績效計算
│
├── experiments/             # 可重現的實驗組合（資料、模型、參數）
│
├── requirements.txt
└── README.md

🧠 系統架構（System Architecture）
整體流程（Mermaid 示意圖）
flowchart LR
    A[市場資料 Tick/K線] --> B[L0: XGBoost 事件偵測]
    B --> C[L1: SHAP 語義轉譯]
    C --> D[L2: LLM 決策代理人]
    D --> E[最終決策<br>BUY / SELL / NO_ACTION]

🔍 L0 — 事件偵測層（XGBoost + Triple Barrier）
主要功能

使用 XGBoost 建立多分類事件偵測模型

透過 Triple-Barrier Method 製作標籤

輸入特徵包含：

RSI、MACD、Bollinger Bands

量能不平衡（Volume Imbalance）

波動率分類（Volatility Regime）

滾動視窗統計（Rolling Windows）

輸出

類別（0 = 中性，1 = 做多機會，2 = 做空機會）

機率分佈

SHAP 特徵重要度

🗣️ L1 — 語義轉譯層（SHAP → 自然語言描述）

此模組將 L0 的內部特徵貢獻值轉換為「結構化語義摘要」。

範例輸出
訊號類型：LONG
重要因素：
- 量能不平衡 +0.47（買盤壓力強）
- RSI 從 35 上升至 48（短期動能回升）
- 價格突破 Bollinger 中線

市場狀態：高波動、多方偏強


這份摘要將作為 L2 的提示（Prompt）。

🤖 L2 — LLM 決策代理人（Decision Agent）

LLM 負責對 L0/L1 的訊號進行「二階推理」，包含：

確認訊號是否符合市場趨勢

過濾假訊號

加入風險控管判斷

產生可解釋的最終進出場建議

結果格式範例
動作（Action）：BUY
信心度（Confidence）：0.82
理由（Reason）：
- XGBoost 訊號符合中期上升趨勢
- 買盤力量提高且未出現背離
- 市場波動率雖高，但方向性明確

🎯 研究目標（Research Objectives）
1. 混合式架構的可行性

Hybrid（XGBoost + LLM）是否優於純 ML / 純 LLM？

2. 模型解釋性

SHAP-to-Text 是否真實描述市場微結構？

3. 決策一致性

LLM 在相似情境是否給出一致的決策？

📄 文獻搜尋建議（後續會放入 docs/literature）

推薦關鍵字：

triple barrier method

event-driven trading

SHAP explainability finance

LLM trading agent

hybrid intelligence in finance

market microstructure features

🚀 使用說明（Getting Started）
1. 安裝套件
pip install -r requirements.txt

2. 訓練 L0 模型
python src/L0_detect/train_xgb.py

3. 執行 L1 語義生成
python src/L1_semantic/generate_summary.py

4. 執行 L2 決策代理人
python src/L2_agent/run_agent.py

📈 回測（Backtesting）

回測模組位於：

src/backtest/


支援的績效指標：

命中率（Hit-rate）

Sharpe Ratio

最大回撤（Max Drawdown）

事件驅動的 Precision / Recall
