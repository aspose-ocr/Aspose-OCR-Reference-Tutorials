---
category: general
date: 2026-06-22
description: 使用 Aspose OCR 於 Python 中對圖像進行預處理，以提取圖像文字並提升 OCR 準確度。附上完整可執行範例。
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: zh-hant
og_description: 預處理圖像以進行 OCR，從圖像中提取文字，並使用 Aspose OCR 提升 OCR 準確度。學習 Python 完整工作流程。
og_title: 圖像前處理（OCR）– 完整 Python 教學
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR 圖像前處理 – 逐步 Python 指南
url: /zh-hant/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 圖像前處理以進行 OCR – 完整 Python 教程

如果你需要 **前處理圖像以進行 OCR**，大概已經遇過噪點掃描、頁面傾斜或低對比度照片無法配合的情況。曾經嘗試從圖像中擷取文字，卻只得到一團亂碼嗎？這時一條完整的前處理流程就能決定是只有少量可讀文字，還是整個轉錄噩夢。

在本指南中，我們將一步步示範一個 **從圖像擷取文字** 的完整端到端範例，並說明如何使用 Aspose OCR for Python **提升 OCR 準確度**。沒有模糊的參考——只有可以直接 copy‑paste 的程式碼、每一行背後的原理，以及實務上常見邊緣案例的技巧。

## 你將學會什麼

- 一個可直接執行的 Python 腳本，能載入雜訊文件、清理圖像，並印出辨識出的文字。  
- 為何每個前處理濾鏡都很重要，以及如何調整其參數。  
- 處理常見陷阱的策略，例如大量斑點噪聲、極端旋轉或低對比度掃描。  

### 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Aspose OCR 的 wheel 針對現代直譯器。 |
| `aspose-ocr` 套件 (`pip install aspose-ocr`) | 提供 `OcrEngine`、`ImagePreprocessor` 與濾鏡類別。 |
| 範例圖像（例如 `noisy-document.jpg`） | 我們會使用一張刻意雜亂的圖片來展示前處理的效益。 |
| 基本的 Python 函式概念 | 幫助你將腳本套用到自己的流程中。 |

> **Pro tip:** 若你使用 Windows，請在虛擬環境中執行腳本，以避免版本衝突。

---

## 使用 Aspose OCR（Python）前處理圖像以進行 OCR

以下是本教學的核心——一步步拆解你需要的程式碼。每個段落同時說明 **我們在做什麼** 以及 **為什麼要這麼做**，讓你日後調整流程時不會摸不著頭緒。

![前處理圖像以進行 OCR 範例](ocr-preprocess.png){alt="前處理圖像以進行 OCR"}

### 步驟 1 – 初始化 OCR 引擎並載入來源圖像

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **為何** 需要 `OcrEngine`？它封裝了辨識器、語言設定，且（稍後）會掛載前處理器。  
- **為何** 使用 `ImageStream.from_file`？它抽象化檔案類型處理，讓你可以在不改程式碼的情況下把 JPEG 換成 PNG。

### 步驟 2 – 建立前處理鏈以清理圖像

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**這些濾鏡如何提升 OCR 準確度：**  
- **Deskew** 消除常見的「頁面傾斜」問題，避免字元分割錯誤。  
- **Despeckle** 針對低品質掃描產生的斑點；強度越高噪聲移除越多，但可能侵蝕細節。  
- **ContrastBoost** 讓深色文字在淺色背景上更突出，對大多數 OCR 引擎都是顯著提升。

> **Edge case:** 若文件已經完全筆直，可省略 `Deskew()` 以節省幾毫秒的處理時間。

### 步驟 3 – 將前處理器附加至引擎

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

現在每次呼叫 `ocr_engine.recognize()` 時，都會先依照我們定義的順序執行三個濾鏡。順序很重要：必須 **先去除傾斜再去除斑點**，否則斑點濾鏡可能把旋轉的邊緣誤判為噪聲。

### 步驟 4 – 執行 OCR 並從圖像擷取文字

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- `recognize()` 會回傳一個 `RecognitionResult` 物件，除了原始文字外，還包含信心分數、邊框與語言資訊。  
- 這裡我們只取純文字，但你也可以查閱 `recognition_result.get_confidence()` 進行 **提升 OCR 準確度** 的快速檢查。

### 步驟 5 – 驗證輸出並微調以獲得更佳準確度

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

如果輸出仍有亂碼，請考慮以下調整：

| Issue | Suggested Fix |
|-------|----------------|
| 文字仍然模糊 | 將 `ContrastBoost(level)` 提升至 2.0，或在去斑點前加入 `ocr.Filters.GaussianBlur(radius=1)`。 |
| 雜散字符過多 | 將 `Despeckle(strength)` 提升至 3，或插入 `ocr.Filters.RemoveLines()` 以去除水平線。 |
| 傾斜仍未校正 | 呼叫 `ocr.Filters.Deskew(max_angle=5)`，限制校正範圍於輕微旋轉。 |

---

## 完整、可執行的腳本

將下方程式碼複製到名為 `ocr_preprocess.py` 的檔案中。將 `YOUR_DIRECTORY/noisy-document.jpg` 替換為實際圖像路徑，然後執行 `python ocr_preprocess.py`。

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

在一張噪點且稍微旋轉的 JPEG 上執行此腳本，應可得到乾淨、可讀的文字——充分展示精心設計的前處理鏈 **大幅提升 OCR 準確度** 的效果。

---

## 常見問題與解答

**Q: 這能處理多頁 PDF 嗎？**  
A: 能。先將每頁轉成圖像（例如使用 `pdf2image`），再在迴圈中套用相同的管線。每頁都會執行相同的 `preprocess image for OCR` 步驟。

**Q: 若文件使用非英文語言該怎麼辦？**  
A: 在辨識前設定語言：`engine.set_language(ocr.Language.FRENCH)`。前處理濾鏡保持不變，只有語言模型會改變。

**Q: 可以再加入更多濾鏡嗎？**  
A: 當然可以。`ImagePreprocessor` 可擴充——只要再呼叫一次 `add_filter`。對於重點點狀背景，`ocr.Filters.MedianFilter(kernel=3)` 會很有幫助。

---

## 小結

我們已完成 **圖像前處理以進行 OCR**、執行 Aspose 的引擎，並 **從圖像擷取文字**，同時示範了多項 **提升 OCR 準確度** 的技巧。完整範例可直接套用於任何專案，且模組化的濾鏡設計讓你可以依需求自由增減步驟。

接下來，你可以探索：

- 使用 `concurrent.futures` 進行 **批次處理** 多筆掃描。  
- 結合拼寫檢查函式庫（如 `pyspellchecker`）進行 **後處理**，清理 OCR 帶來的錯字。  
- 以 Flask 或 FastAPI **整合** 此腳本，打造即時 OCR 微服務。

試著跑跑看，調整濾鏡強度，觀察辨識率的提升。如果遇到問題，歡迎留言——祝開發愉快！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}