---
category: general
date: 2026-06-25
description: 使用 Python 進行 OCR 圖像前處理，並從掃描文件中辨識文字。逐步教學，附完整程式碼。
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: zh-hant
og_description: 預處理圖像以進行 OCR，並使用 Python 從掃描文件中辨識文字。請跟隨此詳細且可執行的教學。
og_title: Python 圖像 OCR 前處理完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python 圖像 OCR 前處理完整指南
url: /zh-hant/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中預處理影像以供 OCR – 完整指南

有沒有想過如何 **preprocess image for OCR**，讓文字變得乾淨且可靠？你並不孤單——大多數開發者在掃描頁面歪斜或對比度不佳時都會遇到同樣的問題。好消息是，只要幾行 Python 代碼就能把這些混亂整理好，將圖片二值化，並回傳清晰、可搜尋的文字。

在本教學中，我們將逐步說明如何 **preprocess image for OCR** *以及* **recognize text from scanned document** 檔案，使用一個流行的 OCR 函式庫。完成後，你將擁有一個可直接執行的腳本，了解每個設定的原因，並知道如何針對棘手的邊緣情況進行調整。

## 需要的條件

- Python 3.8 或更新版本（程式碼在 3.10+ 也可執行）
- 具備 `OcrEngine`、`ImagePreProcessingOptions` 與 `Image` 類別的 OCR 套件（例如本範例使用的虛構 `ocr` 模組）
- 一份略為傾斜或低對比度的掃描或拍攝文件
- 你喜愛的 IDE 或簡易終端機——不需要繁重的 GUI

就這樣。無需額外二進位檔，亦不需要 Docker 操作。讓我們開始吧。

## Preprocess Image for OCR – 步驟說明

以下是核心工作流程，分為五個清晰階段。每個階段都包含 **為何** 這麼做、精確的 **code**，以及簡短的 **explanation**，說明背後的運作原理。

### 步驟 1：建立 OCR Engine 實例

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:*  
`OcrEngine` 物件是整個操作的核心。它保存了語言套件、信心門檻等設定，且最重要的是影像前處理旗標。先建立它即可提供一個乾淨的起點，讓我們能啟用後續的技巧。

### 步驟 2：啟用自動去斜與二值化

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Why this matters:*  
- **Deskewing** 會將影像旋轉，使文字行變為水平。當基線傾斜超過幾度時，OCR 引擎會表現不佳。  
- **Binarization** 將圖片轉為純黑白，去除可能干擾字元分類器的背景雜訊。  
這兩個選項在許多現代函式庫中都是 *automatic*，但仍需手動開啟——因此需要明確指派。

> **Pro tip:** 若來源影像已經完全對齊，你可以將 `auto_deskew=False`，以節省一毫秒的處理時間。

### 步驟 3：載入要處理的傾斜影像

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Why this matters:*  
`Image.load` 方法會將檔案讀入記憶體，並包裝成 OCR 引擎能理解的物件。它同時會擷取 DPI 等中繼資料，這可能會影響去斜的預設縮放係數。

> **Edge case:** 若影像是多頁 TIFF，需遍歷每一頁或使用如 `ocr.MultiPageImage.load` 的輔助函式。相同的前處理設定會套用到每一頁。

### 步驟 4：對前處理過的影像執行 OCR

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Why this matters:*  
此時引擎會套用先前啟用的去斜與二值化步驟，接著在清理過的點陣圖上執行其神經網路（或傳統的 Tesseract 風格流程）。回傳的 `result` 物件通常包含純文字、信心分數，有時還會有每個詞的位置信息。

> **What if the text is still garbled?**  
檢查影像解析度：OCR 在 300 dpi 或更高時表現最佳。若來源解析度較低，請考慮在載入前先升級，或向文件來源索取原始掃描檔。

### 步驟 5：輸出辨識出的文字

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Why this matters:*  
`result.text` 是引擎能讀取的所有內容的純字串表示。將其印出對快速除錯很方便；在實際應用中，你可能會將它寫入 `.txt` 檔、資料庫，或輸入到後續的 NLP 流程中。

---

## Recognize Text from Scanned Document – 超越基礎應用

既然基本流程已可運作，接下來讓我們探索在實際使用 **recognize text from scanned document** 圖片時可能遇到的幾種常見變化。

### 1. 處理多語言

若文件同時包含英文與法文，請在步驟 1 前設定引擎：

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

大多數 OCR 引擎接受 ISO‑639‑2 代碼；載入額外語言套件會稍增負擔，但能顯著提升多語言頁面的辨識準確度。

### 2. 微調二值化門檻

自動二值化適用於大多數情況，但某些舊版影印件需要自訂門檻：

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

在 120 到 220 之間嘗試不同數值，直至背景消失且不抹除淡弱字元。

### 3. 抽取版面資訊

有時候你需要的不只是純文字——你想知道每段落在頁面上的位置。許多引擎會提供 `result.blocks` 集合：

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

這對於重建表格或保留欄位順序非常寶貴。

### 4. 批次處理檔案

若你有一個資料夾內放滿已轉為 JPEG 的掃描 PDF，請將整個流程包在迴圈中：

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

此迴圈會重複使用同一個 `engine` 實例，比每個檔案重新建立更有效率。

### 5. 處理低解析度掃描

低解析度影像（< 150 dpi）常會產生模糊字元。快速的解決方法是先使用高品質演算法升級影像，再送入 OCR 引擎：

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

升級不會奇蹟般產生細節，但二值化步驟能在較銳利的邊緣上運作，提供適度的提升。

## 預期輸出

在中度傾斜、300 dpi 的掃描上執行原始的五步腳本，應會印出類似以下內容：

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

若看到亂碼，請再次確認前處理旗標、影像解析度與語言設定。

## 結論

我們已完整說明如何使用 Python **preprocess image for OCR** 與 **recognize text from scanned document** 檔案。從全新的 engine 實例開始，我們啟用了自動去斜與二值化，載入傾斜的圖片，執行辨識，並印出乾淨的文字。過程中我們也探討了多語言支援、手動門檻調整、版面抽取、批次處理與低解析度的應對方式。

將腳本套用在自己的掃描檔上試試看——可能是一疊收據、手寫表單，或舊報紙剪報。熟悉之後，可嘗試加入 PDF 產生或將輸出送入搜尋索引。無限可能等你發揮。

**Ready for the next challenge?** 前往我們的教學 *「使用 Python 從掃描 PDF 中抽取表格」* 與 *「使用 TensorFlow 訓練自訂 OCR 模型」*，持續擴充你的文件自動化工具箱。

祝程式開發愉快，願你的 OCR 永遠清晰！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通額外的 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}