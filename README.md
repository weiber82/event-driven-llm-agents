📘 Project Overview：An Event-Driven Multi-Layer Agent Framework for Intraday Trading with LLMs

本專案旨在建立一套 事件驅動（Event-Driven） 的盤中市場決策架構，
透過三層式代理人流程 —— L0 市場事件偵測、L1 事件語義化、L2 LLM 決策代理人 ——
探索大型語言模型在盤中市場情境中的推理能力、決策一致性與可行性。

此 Repository 作為論文研究的版本控管工具，內容包含：

文獻整理

方法設計

架構實作

實驗流程與結果

研究紀錄與補充說明

🎯 Objectives（研究目標）

建立 事件驅動式盤中市場分析流程

使用 XGBoost 構建 L0 市場事件偵測模型

設計 事件語義化與 Prompt 生成流程（L1）

建立 LLM 決策代理人（L2）

分析 LLM 在事件情境下的：

決策行為

推理品質

一致性

限制

提供一套 可重現、可驗證的研究架構

🏗️ System Architecture（系統架構）
L0 — Event Detection Layer（XGBoost）

使用盤中資料建立 監督式事件偵測模型

根據未來短期報酬 / 波動度定義事件標註

處理資料不平衡問題

使用 SHAP 分析模型解釋性

作為整個系統的 事件觸發器

L1 — Event Semantic Layer（事件語義化）

將 L0 偵測結果轉換為 LLM 可解讀的語義描述

整合市場上下文（如最近 1–5 分鐘 K 線）

自動生成標準化 Prompt

作為 L2 決策代理人 的輸入

L2 — LLM Decision Agent（決策代理人）

LLM 基於事件語義與上下文輸出：

多 / 空 / 不進場

推理理由

信心度數值（0.00–1.00）

研究重點在：

推理品質

行為一致性

對事件敏感度

決策模式
而非最終報酬率本身。

📁 Repository Structure
docs/
   literature/    文獻導讀
   design/        架構與方法設計
notes/            研究紀錄
src/
   L0/            事件偵測模型（XGBoost）
   L1/            事件語義化與 Prompt 模組
   L2/            LLM 決策代理人
data/
   examples/      資料格式示例（無實際金融資料）
README.md

📚 Literature Overview

所有文獻導讀位於 docs/literature/。
每篇包含：

研究背景

動機

目的

方法

實驗

結果

限制

與本研究之關聯

（不含主觀推論，僅整理原文內容）

目前已完成：

Park (2024) – LLM-based Multi-Agent Reasoning Framework（核心文獻）

🚀 Current Progress（目前進度）

Repository 初始化完成

第一篇文獻導讀（Park 2024）已加入

L0/L1/L2 整體架構已確立

README 已調整為事件驅動版本

開始規劃 L0 資料處理與標註策略

🗺️ Roadmap
L0 — Event Detection

盤中資料前處理

事件標註與定義

XGBoost 訓練與優化

SHAP 特徵分析

L1 — Event Semantic Layer

Prompt 模板設計

事件語義化格式

生成 L2 輸入資料

L2 — LLM Decision Agent

初版推理流程測試

決策格式化

行為一致性分析

📊 Evaluation（實驗）

事件偵測分布

事件命中率（recall）

LLM 決策一致性

決策模式分析

事件前後市場反應

初步回測（非最終策略）
