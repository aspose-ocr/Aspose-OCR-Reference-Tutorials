---
category: general
date: 2026-07-05
description: 學習如何在 Python 中載入圖像進行 OCR，並以 Python 方式從圖像中提取文字。本一步步教學示範如何有效使用 OCR 函式庫。
draft: false
keywords:
- load image for OCR
- extract text from image python
- how to use OCR library
- Python OCR tutorial
- OCR performance metrics
language: zh-hant
og_description: 載入圖片以在 Python 中進行 OCR，並以 Python 風格從圖片提取文字。跟隨本指南了解如何使用 OCR 函式庫及其效能指標。
og_title: 在 Python 中載入圖像以進行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to load image for OCR in Python and extract text from image
    python style. This step‑by‑step tutorial shows how to use OCR library efficiently.
  headline: Load Image for OCR in Python – Complete Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: 在 Python 中載入影像以進行 OCR – 完整指南
url: /zh-hant/python-java/general/load-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中載入影像以進行 OCR – 完整指南

是否曾經需要在 Python 中 **載入影像以進行 OCR**，卻不知從何開始？你並非唯一遇到這個問題的人；許多開發者在首次處理圖片文字提取時都會卡關。在本教學中，我們將一步步示範完整、可執行的範例，說明 **如何使用 OCR 函式庫**，從安裝套件到擷取每個字元，甚至測量效能。

想像一下，你正在打造收據掃描應用程式或自動表單處理系統。只要能可靠地 **載入影像以進行 OCR** 並抽取文字，整個流程就會順暢運作。讓我們立即深入，今天就把它搞定吧。

## 你將學會的內容

- 一個乾淨的 Python 腳本，能 **載入影像以進行 OCR**、執行辨識，並印出擷取的文字與效能統計。  
- 了解每個步驟為何重要，而不僅僅是「做什麼」。  
- 處理常見陷阱的技巧（語言設定錯誤、大檔案、記憶體激增）。  
- 快速路線圖，讓你能擴充範例——加入前處理、批次處理，或切換至其他 OCR 引擎。

### 前置條件

- 已安裝 Python 3.8 以上（程式碼使用 f‑strings）。  
- 熟悉 pip 與虛擬環境的基本操作。  
- 一個想要處理的影像檔案（支援 PNG、JPEG、TIFF）。

除了 OCR 函式庫本身外，沒有其他大型相依套件，讓你能在數分鐘內快速上手。

---

## 第一步：安裝與匯入 OCR 函式庫

首先，我們需要一個 Python OCR 套件。你提供的程式碼片段使用了通用的 `ocr` 模組，所以我們假設你使用的是透過 `pip install ocr` 取得的流行 **ocr** 包裝器。如果你偏好 `pytesseract`，概念相同，只需更換匯入的程式行。

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # on Windows use `venv\Scripts\activate`

# Install the OCR library
pip install ocr
```

Now import the pieces you’ll need:

```python
import ocr               # The main OCR package
import os                # For path handling and optional file checks
```

> **專業提示：** 保持 `requirements.txt` 整潔——只要加入 `ocr==<latest>`，未來的建置就能重現。

---

## 第二步：初始化 OCR 引擎並設定語言

為何要使用明確的引擎物件？大多數 OCR 後端（如 Tesseract、EasyOCR 等）都需要先配置階段，告訴引擎要載入哪種語言模型。跳過此步驟可能導致輸出亂碼或處理速度大幅變慢。

```python
# Step 2: Initialize the OCR engine and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # Switch to 'ocr.Language.SPANISH' for Spanish text
```

如果需要處理多語言文件，只要更改 `language` 屬性或傳入列表——大多數函式庫接受以逗號分隔的字串。

---

## 第三步：載入影像以進行 OCR

這就是本教學的核心：**載入影像以進行 OCR**。`ocr.Image.load` 方法會將檔案讀入引擎可理解的內部格式，同時執行少量驗證（例如確認檔案是否存在）。

```python
# Step 3: Load the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "performance_test.png")

# Guard against missing files – a small but often‑overlooked edge case
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Cannot find image at {image_path}")

image = ocr.Image.load(image_path)
```

> **為何重要：** 早期載入影像可讓你檢查其尺寸、DPI 或色彩模式——這些資訊在之後的前處理（例如轉為灰階）時可能需要。

---

## 第四步：執行 OCR 辨識

現在我們終於以 **extract text from image python** 方式抽取文字。`engine.recognize` 呼叫負責繁重的運算：執行神經網路或傳統模式匹配，然後回傳包含原始文字、信心分數與時間指標的結果物件。

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

`result` 物件通常具有以下屬性：

- `text` – 認識到的純文字字串。  
- `confidence` – 介於 0 到 1 之間的浮點數，表示整體確信度。  
- `processing_time` – 引擎處理此影像所花費的毫秒數。  
- `memory_used` – 執行期間分配的千位元組記憶體。

---

## 第五步：輸出擷取的文字與效能指標

讓我們以整齊的格式印出所有資訊。這不僅滿足「如何使用 OCR 函式庫」的好奇心，也能在之後的效能分析中提供快速回饋。

```python
# Step 5: Output the recognized text and performance metrics
print("=== OCR RESULT ===")
print(result.text)                         # The extracted text
print(f"Confidence: {result.confidence:.2%}")  # Convert to percentage
print(f"Time taken: {result.processing_time} ms")
print(f"Memory used: {result.memory_used} KB")
```

**預期輸出**（實際文字會依影像而異）：

```
=== OCR RESULT ===
Performance Test
Confidence: 98.73%
Time taken: 124 ms
Memory used: 58 KB
```

如果信心分數偏低，請考慮二值化或去斜等前處理步驟——這些在「下一步」章節中有說明。

---

## 第六步：處理邊緣案例與常見陷阱

即使是完美的腳本，在真實資料上也可能遇到問題。以下列出幾種可能的情況以及對策。

| 情況 | 檢查項目 | 快速解決方案 |
|-----------|---------------|-----------|
| **語言錯誤** | `engine.language` 與文字不匹配 | Set `engine.language = ocr.Language.FRENCH` or use `engine.languages = ["ENGLISH", "SPANISH"]`. |
| **影像過大（> 5 MB）** | 記憶體激增，`processing_time` 增長 | Downscale with `PIL.Image.thumbnail` before loading. |
| **未偵測到文字** | `result.text` 為空，信心分數為 0 | Verify image contrast; try adaptive thresholding. |
| **找不到函式庫** | `ocr` 出現 ImportError | Ensure you installed the correct package (`pip install ocr`) and activated your virtual env. |

```python
# Example: simple preprocessing with Pillow
from PIL import Image as PilImage

def preprocess(path):
    img = PilImage.open(path)
    # Convert to grayscale and resize to a max of 1024px width
    img = img.convert("L")
    img.thumbnail((1024, 1024))
    # Save to a temporary file that OCR can read
    tmp_path = "temp_preprocessed.png"
    img.save(tmp_path)
    return ocr.Image.load(tmp_path)

# Use the helper
image = preprocess(image_path)
result = engine.recognize(image)
```

---

## 第七步：整合完整腳本 – 完整範例

以下是完整、可直接執行的程式，能 **載入影像以進行 OCR**、抽取文字，並印出效能數據。將其複製貼上至 `ocr_demo.py`，然後執行 `python ocr_demo.py`。

```python
#!/usr/bin/env python3
"""
Load Image for OCR in Python – Full Example
Demonstrates how to use OCR library, extract text from image python, and measure performance.
"""

import os
import ocr
from PIL import Image as PilImage   # Optional, for preprocessing

def preprocess(image_path: str) -> ocr.Image:
    """Resize and grayscale the image to improve OCR accuracy."""
    img = PilImage.open(image_path)
    img = img.convert("L")
    img.thumbnail((1024, 1024))
    tmp_path = "temp_preprocessed.png"
    img.save(tmp_path)
    return ocr.Image.load(tmp_path)

def main():
    # 1️⃣ Initialize engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Locate image
    image_path = os.path.join("YOUR_DIRECTORY", "performance_test.png")
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # 3️⃣ Load image for OCR (with optional preprocessing)
    image = preprocess(image_path)          # Swap with ocr.Image.load(image_path) if you skip preprocessing

    # 4️⃣ Recognize text
    result = engine.recognize(image)

    # 5️⃣ Show results
    print("=== OCR RESULT ===")
    print(result.text)
    print(f"Confidence: {result.confidence:.2%}")
    print(f"Time taken: {result.processing_time} ms")
    print(f"Memory used: {result.memory_used} KB")

if __name__ == "__main__":
    main()
```

**執行它**：

```bash
python ocr_demo.py
```

你應該會看到 `performance_test.png` 的文字內容，以及處理時間與記憶體使用量。若數據異常，請重新檢查前處理函式或再次確認語言設定。

---

## 結論

我們剛剛說明了如何在 Python 中 **載入影像以進行 OCR**、以 **extract text from image python** 方式抽取文字，並測量操作速度——這是任何在實際專案中詢問 *how to use OCR library* 的人必備的技能。此腳本簡潔易懂，同時具備彈性，可擴充為批次作業、雲端函式，甚至行動端後端。

接下來可以嘗試將 `ocr` 換成 `pytesseract`，觀察 API 有何差異，實驗不同的語言套件，或將輸出整合至資料庫以產生可搜尋的 PDF。基礎已經穩固，您可以在此基礎上持續開發，而不必重新發明輪子。

對特定影像類型有疑問，或想了解如何直接處理 PDF？留下

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}