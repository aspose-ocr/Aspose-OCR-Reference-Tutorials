---
category: general
date: 2026-06-28
description: 學習如何使用 Python OCR 辨識文字圖像、提取文字 PNG 檔案，並以穩健的錯誤處理列印辨識出的文字。
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: zh-hant
og_description: 逐步教學：在 Python 中辨識文字圖像、提取文字 PNG，並安全列印辨識文字。
og_title: 使用 Python OCR 識別文字圖像 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 使用 Python OCR 識別文字圖像 – 完整指南
url: /zh-hant/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 識別文字圖像 – 完整指南

有沒有想過如何在 Python 程式中 **recognize text image** 而不需要引入龐大的框架？你並不孤單。許多開發者需要一個快速的方式來 *load image OCR* 截圖、掃描收據或簡單的 PNG，並取得文字內容。  

在本教學中，我們將建立一個最小的 OCR 引擎，掛接自訂 logger，**load image OCR**，執行 **process image OCR**，最後 **print recognized text**。完成後，你將擁有一個獨立的腳本，亦可按需 **extract text png** 檔案。

## 你將學到的內容

- 一段完整可運作的 Python 程式碼，能建立 OCR 引擎、記錄每一步，並優雅地處理失敗。  
- 清晰說明每行程式碼的 *why*（原因），讓你能將程式碼套用到 Tesseract、EasyOCR 或其他後端。  
- 常見陷阱的提示（缺少字型、損壞的 PNG）以及除錯方法。  

### 前置條件

- 已安裝 Python 3.8 以上版本  
- 具備提供 `OcrEngine` 類別的 OCR 函式庫（範例使用虛構但常見的 API；請改為 `pytesseract`、`easyocr` 等）。  
- 一張欲分析的 PNG 圖片，存於你可控制的資料夾中，檔名為 `input.png`。  

> **Pro tip:** 若使用 `pytesseract`，請先安裝系統的 Tesseract 二進位檔（在 Linux 上執行 `sudo apt install tesseract-ocr`），再執行 `pip install pytesseract pillow`。

---

## ## 識別文字圖像：設定 Logger

良好的 logger 是任何 OCR 流程中不被讚揚的英雄。它會告訴你 *when*（何時）引擎啟動、*what*（哪個）檔案被開啟，以及 *why*（為何）可能失敗。

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*為何重要：*  
logger 將診斷輸出與 OCR 核心解耦，使得日後輕鬆將日誌重新導向至檔案、監控服務，甚至 UI。

---

## ## 載入圖像 OCR：向引擎提供 PNG

在引擎能 **process image OCR** 之前，需要一個適當的圖像物件。大多數函式庫接受 Pillow 的 `Image` 實例。

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*重點：*  

- **load image ocr** – `Image.from_file` 抽象化 PNG 解碼細節。  
- 保持路徑可配置；硬編碼會使腳本脆弱。  
- logger 呼叫可確認圖像已成功讀取，對於檔案缺失或損壞時很有幫助。  

---

## ## 處理圖像 OCR：文字辨識

現在開始繁重的工作。引擎掃描位圖，套用神經網路或啟發式演算法，並輸出 Unicode 字串。

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*為何將其包在 `try/except` 中：*  
OCR 在低解析度 PNG、未支援的色彩空間或缺少語言資料時可能失敗。捕捉 `OcrException` 可讓你僅在實際有結果時 **print recognized text**，避免為最終使用者呈現難以理解的堆疊追蹤。

---

## ## 列印辨識文字與抽取文字 PNG

若辨識成功，我們會顯示結果，並可選擇寫入與原始 PNG 同名的 `.txt` 檔案。

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*你會得到：*  

- **print recognized text** – 在終端機即時顯示文字回饋。  
- 一個相對應的 `.txt` 檔案，可有效 **extract text png** 用於後續處理（搜尋索引、資料輸入等）。

---

## ## 常見邊緣案例與處理方式

| 情況 | 症狀 | 解決方案 |
|-----------|---------|-----|
| PNG 為灰階 | OCR 回傳空字串 | 在送入引擎前轉換為 RGB (`Image.convert("RGB")`)。 |
| 語言不支援 | `OcrException`，代碼為 `LANG_NOT_FOUND` | 安裝語言套件（例如法語的 `tesseract‑lang‑fra`），並設定 `ocr_engine.language = "fra"`。 |
| 圖像過大（> 5 MB） | 辨識緩慢或記憶體錯誤 | 在 `set_image` 前使用 `image.thumbnail((2000, 2000))` 縮小尺寸。 |
| 出現意外字元 | 輸出亂碼 | 確保圖像真的是 PNG；有些檔案偽裝成 PNG 其實是 JPEG。使用 `Image.verify()` 進行驗證。 |

---

## ## 完整可執行範例（直接複製貼上）

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**預期的主控台輸出（正常情況）：**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

若發生錯誤，會看到清晰的 `[ERROR]` 行與原因，這全賴自訂 logger。

---

## ## 後續步驟與相關主題

- **extract text png** 從批次處理：將腳本包在遍歷目錄樹的 `for` 迴圈中。  
- **process image ocr** 前使用 OpenCV 進行前處理（去傾斜、提升對比度）再送入引擎。  
- 透過替換 `OcrEngine` 實作，切換至雲端 OCR 服務（Google Vision、Azure Read），其餘程式碼保持不變。  
- 學習使用 `reportlab` 將 **print recognized text** 輸出為 PDF，以自動化報告產生。  

---

## 結論

我們剛剛示範了一個精簡且可投入生產的 **recognize text image** 方法，從載入 PNG、**print recognized text** 到儲存結果。透過注入小型 logger、處理例外，並可選擇性保存輸出，這個腳本即可用於快速實驗，也能整合至更大型的流程中。  

試著使用自己的螢幕截圖執行，調整圖像前處理，你很快就能從任何 PNG 抽取文字。有問題嗎？留下評論——祝 OCR 順利！  

![識別文字圖像範例](placeholder.png)


## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從圖像抽取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何使用 Aspose OCR 從串流執行圖像文字抽取](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [將圖像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}