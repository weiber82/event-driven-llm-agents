anomaly-triggered-llm-agents
Project Overview

本專案研究以「異常事件觸發」為核心的盤中市場決策架構，
透過三層式流程：L0 異常偵測、L1 事件語義化、L2 LLM 決策代理人，
探索大型語言模型在盤中事件中的推理能力與決策一致性。

此 Repository 用於論文研究的版本控管，包含文獻整理、方法設計、實作與實驗結果。

Objectives

建立事件觸發式盤中市場分析流程

使用 XGBoost 進行異常偵測（L0）

設計事件語義化與提示生成（L1）

建立 LLM 決策代理人（L2）

分析模型行為、決策一致性與限制

建立可重現、可驗證的研究架構

System Architecture
L0 Anomaly Detection (XGBoost)

使用盤中資料建立監督式異常偵測模型

以未來短期報酬與波動度為標註基準

支援不平衡資料與 SHAP 模型解釋

L1 Event Semantic Layer

將 L0 偵測事件轉換成 LLM 可理解的語義描述

整合必要的市場上下文（如最近 1–5 分鐘 K 線）

自動生成 L2 的輸入格式

L2 LLM Decision Agent

LLM 針對事件輸出：多、空、不進場

附理由與信心度

重點在推理能力與行為模式，而非最終報酬率

Repository Structure
docs/
    literature/   文獻整理
    design/       架構與方法設計
    notes/        研究紀錄
src/
    L0 L1 L2 模組程式碼
data/
    資料格式與示例（不含實際金融資料）
README.md

Literature

所有文獻導讀放置於 docs/literature
每篇包含：背景、動機、目的、方法、實驗、結果、限制、總結（不含研究者主觀推論）

Current Progress

Repository 初始化

新增第一篇文獻導讀（Park 2024）

確立 L0 L1 L2 研究方向

README 更新為 XGBoost 版本

Roadmap
L0

盤中資料前處理

標註策略

XGBoost 訓練

SHAP 分析

L1

Prompt 模板設計

事件語義化格式

L2

LLM 初版推理測試

決策格式化

行為分析

Evaluation

異常事件分布

命中率

決策一致性

回測
