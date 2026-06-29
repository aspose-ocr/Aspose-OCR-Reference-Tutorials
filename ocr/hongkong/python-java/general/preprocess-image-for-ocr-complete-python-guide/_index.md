---
category: general
date: 2026-06-28
description: 使用 Python 進行圖像預處理以提升 OCR 準確度。學習完整的圖像預處理流程，改善 OCR 結果，並從西里爾字母圖像中提取文字。
draft: false
keywords:
- preprocess image for OCR
- how to improve OCR accuracy
- python OCR with preprocessing
- image preprocessing pipeline python
- extract text from Cyrillic image
language: zh-hant
og_description: 在 Python 中對圖像進行 OCR 前置處理，並學習如何提升 OCR 準確度。本指南將帶領你完成完整的前置處理流程，並從西里爾字母圖像中提取文字。
og_title: OCR 圖像預處理 – 完整 Python 教學
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the code works on 3.10+ as well). - Basic familiarity
      with Python packages and virtual environments. - An OCR library that provides
      `OcrEngine`, `Language`, and `ImagePreprocessor` classes (e.g., a wrapper around
      Tesseract or a commercial SDK). - A sample Cyrillic image (`cyri'
  - name: Why These Three Steps?
    text: 1. **Deskew** – OCR engines assume left‑to‑right (or top‑to‑bottom) alignment.
      A few degrees of rotation can drop accuracy by 30 % or more. 2. **Binarize**
      – Converting to a binary image reduces the data the OCR engine must analyze,
      sharpening character edges. 3. **Denoise** – Small specks or compre
  - name: How This Improves OCR Accuracy
    text: '- By feeding a **clean, deskewed, binarized** image, the engine can focus
      on character shapes rather than fighting noise. - Specifying `Language.Cyrillic`
      activates the correct character set and language model, which is a key factor
      in **how to improve OCR accuracy** for non‑Latin scripts.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR 圖像前處理 – 完整 Python 指南
url: /zh-hant/python-java/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 圖像前處理 – 完整 Python 指南

有沒有想過如何 **preprocess image for OCR**，讓文字呈現晶瑩剔透？你並不孤單——許多開發者在 OCR 引擎輸出亂碼時卡住，尤其是面對傾斜或雜訊較多的西里爾字掃描。好消息是？精心設計的圖像前處理流水線可以大幅提升辨識率。

在本教學中，我們將直接深入 **Python OCR with preprocessing** 解決方案，處理去傾斜、二值化與去雜訊，並示範如何 **extract text from Cyrillic image** 檔案。完成後，你將擁有可重複使用的腳本，了解 **how to improve OCR accuracy**，並能將此流水線套用於任何語言或圖像來源。

## 你將學到什麼

- 每個前處理步驟背後的原理以及為何對 OCR 重要。
- 如何組裝一個可在多個專案中重複使用的 **image preprocessing pipeline python**。
- 完整且可執行的範例，建立 OCR 引擎、前處理西里爾圖像，並印出辨識文字。
- 處理極端傾斜、低對比或多語言文件等邊緣情況的技巧。
- 後續想法，例如批次處理、自訂語言套件，以及整合雲端 OCR 服務。

### 前置條件

- Python 3.8 或更新版本（程式碼在 3.10+ 亦可運作）。
- 具備 Python 套件與虛擬環境的基本認識。
- 具備提供 `OcrEngine`、`Language` 與 `ImagePreprocessor` 類別的 OCR 函式庫（例如 Tesseract 包裝或商業 SDK）。
- 一張範例西里爾圖像（`cyrillic_skewed.jpg`）放置於你可控制的資料夾中。

> **Pro tip:** 如果你沒有現成的 OCR 包裝器，可參考開源的 `pytesseract` 套件，並搭配 `opencv-python`。本指南中的概念可直接套用。

---

## 第一步：安裝與匯入必要套件

首先，先把相依套件處理好。我們將使用一個假想的 `ocr_lib`，它整合了引擎與前處理工具。如果你使用 `pytesseract` + OpenCV，請相應地替換匯入語句。

```python
# Install the (fictional) OCR library – replace with your actual package manager command
# pip install ocr-lib

from ocr_lib import OcrEngine, Language, ImagePreprocessor
import os
```

> **Why this matters:** 匯入正確的類別可確保 OCR 引擎（辨識）與圖像前處理器（增強）之間保持清晰分離。混合使用可能導致程式碼糾結，難以除錯。

---

## 第二步：建立 **Preprocess Image for OCR** 流水線

現在我們要建立本教學的核心：一條對輸入圖像進行去傾斜、二值化與去雜訊的流水線。每個轉換都針對 OCR 引擎的特定弱點。

```python
# Step 2: Initialise the pre‑processing chain
preprocessor = ImagePreprocessor()

# Deskew – correct rotation so text lines are horizontal
preprocessor = preprocessor.deskew()

# Binarize – convert to pure black‑and‑white using a threshold (180 works well for most scans)
preprocessor = preprocessor.binarize(threshold=180)

# Remove noise – apply a mild median filter (strength=2) to smooth speckles
preprocessor = preprocessor.removeNoise(strength=2)
```

### 為何選擇這三個步驟？

1. **Deskew** – OCR 引擎假設文字左至右（或上至下）對齊。僅幾度的旋轉就可能使準確率下降 30 % 以上。  
2. **Binarize** – 將圖像轉為二值可減少 OCR 引擎需分析的資料量，並使字元邊緣更銳利。  
3. **Denoise** – 細小的斑點或壓縮雜訊可能被誤認為標點或變音符號，尤其在西里爾字母中許多字形相似。

> **Edge case note:** 若來源圖像已相當乾淨，可省略 `removeNoise` 或降低 `strength` 參數。過度去雜訊可能抹除變音點等細節。

---

## 第三步：載入圖像並套用流水線

流水線準備好後，我們將檔案路徑傳入。`apply` 方法會回傳一個處理過的圖像物件，OCR 引擎可直接使用。

```python
# Path to the original Cyrillic image (adjust as needed)
image_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")

# Run the preprocessing pipeline
processed_image = preprocessor.apply(image_path)
```

如果需要預覽結果，可將其寫入磁碟：

```python
# Optional: save the preprocessed image for visual verification
processed_image.save("preprocessed_cyrillic.jpg")
print("Preprocessed image saved – check the file to confirm deskewing and binarization.")
```

> **Why preview?** 觀察轉換後的圖像有助於微調閾值。有時 180 的閾值過於嚴苛，降低至 150 可能保留較淡的筆劃。

---

## 第四步：設定 OCR 引擎並辨識文字

現在切換到實際的 OCR 部分。我們會設定引擎使用西里爾語言套件，這對 **extract text from Cyrillic image** 檔案至關重要。

```python
# Initialise the OCR engine
engine = OcrEngine()

# Tell the engine we’re working with Cyrillic text
engine.setLanguage(Language.Cyrillic)

# Perform recognition on the preprocessed image
ocr_result = engine.recognizeImage(processed_image)

# Extract plain text from the OCR result object
recognized_text = ocr_result.getText()
print("=== Recognized Text ===")
print(recognized_text)
```

### 這如何提升 OCR 準確率

- 將 **clean, deskewed, binarized** 圖像輸入，引擎即可專注於字形，而非與雜訊抗爭。  
- 指定 `Language.Cyrillic` 會啟用正確的字元集與語言模型，這是提升非拉丁文字 **how to improve OCR accuracy** 的關鍵因素。

---

## 第五步：將所有步驟封裝成可重複使用的函式（可選）

如果你打算處理大量檔案，將邏輯封裝成函式可讓程式碼更簡潔、易於維護。

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Preprocess an image and extract Cyrillic text using the OCR engine.

    Parameters
    ----------
    image_path : str
        Full path to the source image.

    Returns
    -------
    str
        Recognized Cyrillic text.
    """
    # Build the preprocessing pipeline (could be cached for performance)
    preprocessor = (ImagePreprocessor()
                    .deskew()
                    .binarize(threshold=180)
                    .removeNoise(strength=2))

    processed = preprocessor.apply(image_path)

    engine = OcrEngine()
    engine.setLanguage(Language.Cyrillic)

    result = engine.recognizeImage(processed)
    return result.getText()


# Example usage
if __name__ == "__main__":
    sample_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")
    text = extract_cyrillic_text(sample_path)
    print("Extracted Cyrillic text:")
    print(text)
```

> **Why a function?** 它將前處理邏輯獨立，使得更換語言或調整參數變得簡單，無需重寫整個腳本。

---

## 常見陷阱與解決方法

| Issue | Symptom | Fix |
|-------|----------|-----|
| **極端傾斜 (>15°)** | 文字顯示為亂碼或缺失 | 提升 `deskew()` 的魯棒性，或使用 OpenCV 的 `getRotationMatrix2D` 手動預先旋轉。 |
| **低對比度** | 二值化後全部變白 | 降低 `threshold` 值，或在 `binarize()` 前執行對比度拉伸。 |
| **字體過小** | 二值化後字元合併 | 使用更高解析度的來源圖像，或在閾值化前套用輕度高斯模糊。 |
| **多語言** | 西里爾字母變得無法辨識 | 若函式庫支援多語言模式，請設定 `engine.setLanguage([Language.Cyrillic, Language.English])`。 |
| **不支援的圖像格式** | `apply()` 拋出錯誤 | 先使用 Pillow（`Image.open().convert('RGB')`）將圖像轉為 PNG 或 JPEG。 |

---

## 擴充 **Image Preprocessing Pipeline Python** 方法

- **Batch Processing** – 迭代圖像目錄，將每個結果存入 CSV 檔案。  
- **Parallel Execution** – 使用 `concurrent.futures.ThreadPoolExecutor` 加速大型工作負載。  
- **Custom Filters** – 為印刷表單加入形態學操作（`erode`、`dilate`）。  
- **Cloud OCR Integration** – 將 `OcrEngine` 換成 API 客戶端（Google Vision、Azure Computer Vision），同時保留相同的前處理步驟。

```python
# Example of batch processing with ThreadPoolExecutor
from concurrent.futures import ThreadPoolExecutor, as_completed

def batch_extract(folder: str):
    files = [os.path.join(folder, f) for f in os.listdir(folder) if f.lower().endswith('.jpg')]
    results = {}

    with ThreadPoolExecutor(max_workers=4) as executor:
        future_to_file = {executor.submit(extract_cyrillic_text, f): f for f in files}
        for future in as_completed(future_to_file):
            file_path = future_to_file[future]
            try:
                results[file_path] = future.result()
            except Exception as exc:
                results[file_path] = f"Error: {exc}"
    return results
```

---

## 視覺摘要

![OCR 圖像前處理範例](/images/ocr_preprocess_example.png "示意圖顯示 OCR 圖像前處理流水線：去傾斜 → 二值化 → 去雜訊 → OCR 引擎")

*此圖示說明 **preprocess image for OCR** 工作流程的每個階段，從原始掃描到最終文字輸出。*

---

## 結論

我們已完整示範了在 Python 中的 **preprocess image for OCR** 解決方案，涵蓋從安裝正確套件、構建穩健的 **image preprocessing pipeline python**，到最終 **extract text from Cyrillic image** 檔案的全過程。透過在將圖像送入 OCR 引擎前先執行去傾斜、二值化與去雜訊，你將明顯提升 **how to improve OCR accuracy**，尤其針對挑戰性的西里爾文字。

準備好迎接下一個挑戰了嗎？試著將語言模型換成阿拉伯語、實驗自適應閾值，或將流水線接入 Flask API 以實現即時文件處理。只要有此基礎，你就能將雜亂的掃描檔轉換為乾淨、可搜尋的文字，前景無限。

祝程式開發愉快，願你的 OCR 結果永遠晶瑩剔透！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [計算 OCR 圖像前處理的傾斜角度](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [如何設定 OCR 圖像辨識的閾值](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}