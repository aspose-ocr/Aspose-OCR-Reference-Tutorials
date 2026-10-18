---
category: general
date: 2026-06-06
description: 如何使用 Python 進行 OCR 圖像前處理。學習使用 Otsu 方法二值化圖像、如何校正掃描文件的傾斜，以及提升德文文本的 OCR
  準確度。
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: zh-hant
og_description: 如何在 Python 中對圖像進行 OCR 前處理。本教程展示如何使用 Otsu 方法二值化圖像、如何校正掃描文件的傾斜，以及如何提升德文圖像的
  OCR 準確度。
og_title: 如何為 OCR 預處理圖像 – 完整 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: 如何為 OCR 預處理圖像 – 完整 Python 指南
url: /zh-hant/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何為 OCR 前處理圖像 – 完整 Python 指南

有沒有想過 **如何為 OCR 前處理圖像**，讓文字呈現得晶瑩剔透？你並不是唯一有此困擾的人。掃描文件——尤其是雜訊較多的德文頁面——對任何 OCR 引擎來說都是噩夢。好消息是，只要採取幾個聰明的前處理步驟，就能把模糊、斑點密布的掃描件變成乾淨、機器可讀的圖像。

在本教學中，我們將示範一個實用範例，說明 **如何為 OCR 前處理圖像**，使用 Python 完成。你將學會 **使用 Otsu 進行二值化**、**如何校正掃描文件的傾斜**，以及在 **從德文圖像檔案中提取文字** 時 **如何提升 OCR 準確度**。沒有冗長說明，只有可直接複製貼上的完整腳本。

## 需要的環境

- **Python 3.9+**（任何較新的版本皆可）
- 提供 `OcrEngine` 類別的 OCR 套件——此示範假設有一個通用的 `ocr` 套件，請使用 `pip install ocr-lib` 安裝。
- 一個雜訊較多的德文掃描檔（`noisy_german_scan.tif`）作為測試對象。
- 基本的 Python 函式概念（只要寫過 `def` 就足夠）。

> **小技巧：** 若你使用的是其他 OCR SDK（例如透過 `pytesseract` 的 Tesseract），概念仍然相同，只需對應調整方法名稱即可。

## 解決方案概覽

1. **建立 OCR 引擎實例。**  
2. **設定辨識語言為德文。**  
3. **建構自訂前處理管線**，包含校正傾斜、去雜訊、二值化（Otsu）與對比度拉伸。  
4. **將管線掛載至引擎**，讓每張圖像自動通過前處理。  
5. **對雜訊德文掃描執行 OCR**。  
6. **列印擷取出的文字**，以驗證結果。

以下逐步說明每個步驟的意義，並提供完整程式碼。

![如何為 OCR 前處理圖像範例](image.png "如何為 OCR 前處理圖像範例")

## 步驟 1：建立 OCR 引擎實例

首先，沒有引擎就什麼都不會發生。`OcrEngine` 物件是後續所有處理的入口。

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*為什麼重要：* 初始化引擎會配置內部資源（例如語言模型），同時為之後掛載自訂管線提供乾淨的起點。

## 步驟 2：設定辨識語言為德文

OCR 的準確度高度依賴語言。告訴引擎使用德文，即可啟用正確的字元集與語言模型。

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

若省略此步驟，引擎可能預設為英文，導致無法正確辨識變音符（ä、ö、ü）與 ß，這是處理德文掃描時常見的陷阱。

## 步驟 3：建構自訂前處理管線

這是 **如何為 OCR 前處理圖像** 的核心。我們將串接四個轉換：

| 轉換 | 功能說明 | 為什麼有幫助 |
|------|----------|--------------|
| **校正傾斜** | 將圖像旋轉回水平（最大 5°） | 掃描件很少能完美對齊；校正傾斜可去除會干擾字元分割的斜度。 |
| **去雜訊** | 降低隨機斑點（強度 0.7） | 雜訊會產生偽邊緣，OCR 可能把它當成字元。 |
| **二值化（Otsu）** | 使用 Otsu 方法轉為黑白圖 | 乾淨的二值圖提供文字與背景之間的高對比度。 |
| **對比度拉伸** | 擴展動態範圍 | 提升舊文件中淡弱筆劃的可讀性。 |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### 如何校正掃描文件的傾斜

上面的 `deskew` 呼叫即是 **如何校正掃描文件的傾斜** 的具體答案。它會透過 Hough 變換估算主要文字行的角度，然後將圖像旋轉回正。若文件傾斜超過 5°，可將 `max_angle` 提高，但需注意過度旋轉可能產生 artefacts。

### 使用 Otsu 進行二值化

`binarize(method="otsu")` 這行直接回應 **二值化圖像使用 Otsu** 的需求。Otsu 演算法會計算一個使類內變異最小的阈值，特別適合文字（暗）與背景（亮）呈雙峰分佈的文件。

## 步驟 4：將管線掛載至引擎

現在告訴 OCR 引擎，所有進入的圖像都要經過剛才建立的管線。

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*為什麼重要：* 若未註冊管線，引擎會直接處理原始掃描，忽略我們剛配置的清理步驟。此步驟確保 **如何提升 OCR 準確度**，讓前處理始終如一地套用。

## 步驟 5：辨識雜訊德文掃描的文字

把所有東西組合起來，將雜訊德文圖像交給引擎處理。

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

如果想了解效能，可以測量呼叫時間：

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## 步驟 6：輸出辨識結果

最後，列印擷取出的字串。這正是 **從德文圖像中提取文字** 的直接答案。

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### 預期輸出

假設範例掃描包含句子 “Die schnelle braune Füchsin springt über den faulen Hund.”，則應看到類似以下結果：

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

若輸出仍出現亂碼，請考慮調整 `denoise` 強度或提升 `max_angle` 以改善校正。

## 常見問題與解決方式

- **缺少語言模型：** 忘記呼叫 `set_recognition_language(Language.GERMAN)` 常會導致變音符遺失，請務必檢查此行程式。  
- **過度去雜訊：** 強度超過 0.9 可能會抹除細小筆劃，特別是舊字體。大多數情況建議使用 0.5‑0.7。  
- **檔案格式不正確：** 某些 OCR 引擎無法處理多頁 TIFF。若有多頁文件，請先拆分為單頁檔。  
- **管線順序錯誤：** 本範例的順序（校正傾斜 → 去雜訊 → 二值化 → 對比度拉伸）是特意安排的。若先二值化再去雜訊，噪點會被鎖定，效果會變差，務必先去雜訊。

## 延伸管線（下一步是什麼？）

有了穩固的基礎後，你可以考慮：

- **加入形態學開運算** 以清除微小斑點（`.morph_open(kernel=3)`）。  
- **整合語言模型** 進行後處理校正（`ocr_engine.apply_spellcheck()`）。  
- **平行化批次處理**，使用 `concurrent.futures` 針對大型資料集加速。

以上皆是自然的延伸，仍保留 **如何為 OCR 前處理圖像** 的核心概念，同時進一步提升 **如何提升 OCR 準確度**。

## 結論

我們已完整說明 **如何為 OCR 前處理圖像**：建立引擎、設定德文、建構包含 **使用 Otsu 進行二值化**、**校正掃描文件的傾斜** 的管線，最後 **從德文圖像中提取文字**，並大幅提升辨識品質。依照上述六個步驟操作，你會明顯感受到辨識品質的提升——不再需要無止盡的手動校正。

快把腳本套用到自己的掃描件上，調整參數，讓結果說話吧。對特定前處理技巧有疑問嗎？留下評論，我們一起深入探討。

祝編程愉快，願你的 OCR 永遠精準！

## 接下來該學什麼？

以下教學與本指南緊密相關，能在此基礎上延伸技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在專案中探索其他實作方式。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}