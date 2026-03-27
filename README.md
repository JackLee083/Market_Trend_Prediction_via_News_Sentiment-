# Market Trend Prediction via News Sentiment & AutoGluon
**基於新聞情緒分析與 AutoGluon 的股市漲跌預測系統**

## 📝 專案簡介
本專案旨在透過自動化收集市場新聞與指數資料，利用大型語言模型（GPT-4o）進行每日財經新聞的情緒評分（Sentiment Analysis），最後將情緒分數與市場特徵輸入至自動化機器學習框架（AutoGluon 與 LazyPredict）中，以預測股市的未來漲跌趨勢。

## 🏗️ 系統架構與工作流程
本專案的資料管線（Data Pipeline）分為四個主要階段：

1. **資料爬取 (Data Crawling)**：自動從財經網站（如 MoneyDJ）抓取即時新聞，並同步抓取對應的歷史指數資料。
2. **情緒分析 (Sentiment Scoring)**：將每日新聞文本交由 GPT-4o 模型進行情緒解讀，轉換為量化的情緒分數（如看多、看空、中立分數）。
3. **基準測試 (Baseline Evaluation)**：使用 LazyPredict 快速訓練並評估數十種傳統機器學習模型，確認資料集的預測潛力與基準表現。
4. **模型訓練與預測 (Model Training & Prediction)**：利用 AutoGluon 進行自動化特徵工程、模型整合（Ensemble）與超參數調優，產出最終的高精度漲跌預測模型。

## 📂 檔案結構說明
專案包含以下核心 Jupyter Notebook 檔案：

* `爬蟲 新聞.ipynb`：負責抓取財經新聞文本，並將資料匯出為 `news_data.csv`。
* `爬蟲 指數.ipynb`：負責抓取市場指數與歷史價格資料，匯出為 `index_data.csv`。
* `LP GPT4o.ipynb`：使用 `lazypredict` 套件，將結合了 GPT-4o 情緒分數的特徵資料進行快速的模型海選與基準測試。
* `AG GPT4o.ipynb`：專案核心預測模組。使用 `autogluon.tabular` 載入處理好的特徵集，進行深度的模型訓練、驗證，並輸出最終的漲跌預測結果與準確率（Accuracy / Recall 等指標）。

## 🛠️ 環境需求與安裝
建議使用 Python 3.8 或以上版本。請在終端機或 Jupyter Notebook 中安裝以下依賴套件：

```bash
# 基礎資料處理與網頁請求
pip install pandas numpy requests openpyxl

# 機器學習與預測框架
pip install lazypredict
pip install autogluon
