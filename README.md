# 音樂類型分類：結合歌詞與音訊特徵

## 專案簡介

本專案旨在透過分析歌曲的**歌詞**和**音訊特徵**來實現音樂類型分類。我們認為音樂類型分類是一個多模態任務，整合歌詞的語義資訊和音訊的聲學特性，有助於建立更準確、更全面的分類模型。

## 資料與預處理

我們使用了來自 Kaggle 的資料集 ，包含歌曲歌詞和從 Spotify 獲取的音訊特徵。資料集涵蓋六種音樂類型：Rap、EDM、Pop、Rock、Latin、R&B 。

資料經過一系列預處理步驟，包括清理、編碼、特徵選擇、分割和標準化，以確保資料品質並適合模型訓練 。

## 模型介紹

我們實作並評估了多種模型，以探索不同模態和架構在音樂類型分類上的表現：

* **MLP (Multi-Layer Perceptron) Based on Audio Features**: 這是我們的音訊基準模型，使用結構化的音訊特徵來捕捉歌曲的音訊風格訊號，以預測其類型 。
* **CNN (Convolutional Neural Network) Based on Lyrics**: 這是我們的歌詞基準模型，利用多尺度 1D CNN 從歌詞中提取語言模式，捕捉局部語義模式 。
* **CNN+MLP Fusion Model**: 這個模型結合了歌詞 (CNN) 和音訊 (MLP) 的表示。它透過特徵串聯和聯合學習來利用兩種模態的互補資訊，以提升分類性能 。
* **Attention BiLSTM (Bidirectional Long Short-Term Memory) Model**: 這個模型利用雙向 LSTM 和注意力機制來處理歌詞，更好地捕捉歌詞中的序列和上下文依賴性，並將其與音訊特徵結合進行預測 。
* **GRU (Gated Recurrent Unit) + Cross Attention Model**: 該模型使用 GRU 高效編碼歌詞，並透過跨注意力機制使音訊特徵引導對歌詞的關注，實現模態間的動態互動。此外，它還結合了藝術家嵌入以提供額外的風格資訊 。
* **BERT (Bidirectional Encoder Representations from Transformers) - Chunked Lyrics**: 我們探索了 BERT 作為獨立分類器及混合分類器。由於 BERT 的輸入長度限制，歌詞被分割成重疊的塊進行處理，BERT 旨在捕捉歌詞的深層語義意義。其輸出可進一步結合音訊特徵，透過 MLP 或 Random Forest 進行分類 。
* **Transformer + MLP Model**: 這個模型結合了 Transformer 處理歌詞的長距離依賴性，以及 MLP 處理數值和虛擬變數（如音訊特徵）。兩種架構的輸出會被串聯起來進行最終分類 。
* **Ensemble (Majority Vote) Model**: 這是我們最終的模型，透過多數投票的方式結合了前面所有模型的預測結果。這種策略旨在降低單一模型的偏差，提高整體分類的可靠性和準確性 。
