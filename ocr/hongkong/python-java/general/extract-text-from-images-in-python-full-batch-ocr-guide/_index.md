---
category: general
date: 2026-06-19
description: 使用簡易 OCR 引擎在 Python 中從圖像提取文字。了解如何將掃描圖像轉換為文字、從圖片辨識文字，以及高效地使用 Python 列出圖像檔案。
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: zh-hant
og_description: 使用輕量級 OCR 引擎於 Python 中提取圖像文字。本指南將示範如何將掃描圖像轉換為文字、從圖片辨識文字，並在簡單步驟中列出
  Python 圖像檔案。
og_title: 使用 Python 從圖像提取文字 – 完整批次 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: 使用 Python 從圖片提取文字 – 完整批次 OCR 指南
url: /zh-hant/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（Python） – 完整批次 OCR 指南

是否曾經需要 **從圖像中提取文字**，卻不知從何開始？你並不孤單——開發者常常面臨將掃描的 PDF、拍攝的收據或螢幕截圖轉換為可搜尋文字的挑戰。在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **將掃描圖像轉換為文字**、從圖片中辨識文字，甚至以 **list image files python** 風格列出圖像檔案。完成後，你將擁有一個可重複使用的腳本，一次處理整個資料夾。

我們會涵蓋所有必備內容：所需函式庫、每一步的重要性、邊緣案例處理，以及一些除錯技巧。無需追尋外部文件；以下程式碼是完整自足的，說明同時回答「如何」*以及*「為什麼」。打開你最喜愛的 IDE，讓我們馬上開始吧。

---

## 你將建立的內容

- 初始化 OCR 引擎（本教學示範使用 `ocr` 套件）。
- 掃描目錄並以 **list image files python** 風格列出圖像檔案，過濾 PNG、JPG 與 TIFF。
- 對所有找到的圖片執行 **batch OCR** 作業。
- 列印每個檔案的提取文字，並清楚標示。

> **專業提示：** 若尚未安裝 `ocr` 套件，你可以改用 `pytesseract`，只需做少量修改——核心邏輯保持不變。

---

## 前置條件

- Python 3.8+（腳本使用 f‑strings 與型別提示）。
- 具備提供 `OcrEngine` 並支援 `recognize_batch` 的 OCR 套件。本教學假設使用虛構的 `ocr` 套件，但此模式同樣適用於真實套件。
- 一個包含欲處理圖像檔案的資料夾（`.png`、`.jpg`、`.tif`）。

---

## 第一步 – 安裝與匯入必要模組

首先，確保 OCR 套件已安裝。若使用真實的套件如 `pytesseract`，請相應替換匯入語句。

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **為什麼這很重要：** 匯入 `os` 可提供跨平台的路徑處理，而 `typing.List` 有助於 IDE 自動完成與未來相容性。

---

## 第二步 – **Extract Text from Images**：初始化 OCR 引擎

建立引擎是任何 OCR 工作的第一步。我們同時將語言設定為自動偵測，讓引擎能處理混合語言的文件。

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **說明：** 透過將引擎建立封裝於函式中，使程式碼保持模組化。若日後需要調整 DPI 或 OCR 模式，只需修改此處即可。

---

## 第三步 – **List Image Files Python**：從目錄收集檔案

現在我們需要找出所有要處理的圖片。以下的列表推導式映射了常見的 “list image files python” 範式。

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **邊緣案例處理：** 此函式會忽略子資料夾（日後可加入遞迴），並自動過濾隱藏檔，因為它們通常不會以支援的副檔名結尾。

---

## 第四步 – **Convert Scanned Images to Text**：執行批次 OCR

大多數 OCR 套件提供批次方法，速度遠快於一次處理單張圖像。以下示範如何呼叫它。

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **為什麼使用批次？** 一次傳送所有圖像可減少開銷（例如重複載入 OCR 模型），且通常能更有效利用 CPU/GPU。

---

## 第五步 – **Recognize Text from Pictures**：顯示結果

最後，我們遍歷檔名與 OCR 結果的配對，為每張圖像印出整潔的標題。

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **提示：** `strip()` 會移除 OCR 常加入的前後空白字元。

---

## 完整腳本 – 整合所有步驟

以下為完整、可執行的程式。將其儲存為 `batch_ocr.py`，然後執行 `python batch_ocr.py <your_folder>`。

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### 預期輸出

假設資料夾內有 `invoice1.png` 與 `receipt.jpg`，可能會看到以下輸出：

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

每個區塊都有清楚的標籤，使後續處理（例如儲存至資料庫）變得簡單。

---

## 處理常見問題

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **沒有文字顯示** | OCR 語言未偵測到或影像對比度過低。 | 強制指定語言 (`engine.language = ocr.Language.English`) 或預先處理影像（提升對比度）。 |
| **大批次記憶體錯誤** | 引擎嘗試一次載入所有影像。 | 將 `image_files` 分割成多個區塊（`batch_size = 20`），並重複呼叫 `recognize_batch`。 |
| **不支援的檔案格式** | 你加入了 `.gif` 或 `.bmp`。 | 擴充 `supported_exts` 元組或事先將影像轉為 PNG/JPG。 |
| **Unicode 亂碼** | OCR 回傳位元組而非字串。 | 確保 OCR 套件輸出 Unicode（如有需要使用 `result.text.decode('utf‑8')`）。 |

---

## 擴充工作流程

既然你已能 **extract text from images**，可以考慮以下後續步驟：

- **Export to CSV** – 將每個檔名與其提取文字寫入試算表，以供分析。
- **Parallel processing** – 使用 `concurrent.futures.ThreadPoolExecutor` 同時處理多個批次。
- **Integrate with cloud OCR** – 將本地引擎替換為 Google Vision 或 Azure OCR，以在複雜版面上獲得更高準確度。
- **Add image preprocessing** – 如 Pillow 或 OpenCV 等函式庫可在 OCR 前進行去斜、去噪或二值化，提升結果。

所有這些想法皆使用我們已建立的核心函式，無需從頭開始。

---

## 結論

我們剛剛完整示範了在 Python 中 **extract text from images** 的解決方案，涵蓋從 **list image files python**、**recognize text from pictures** 到最終的 **convert scanned images to text**，全部以整潔的批次方式完成。此腳本刻意保持簡潔，同時具備彈性，可作為更大型專案的基礎——無論是數位化收據、建構可搜尋的檔案庫，或是驅動資料抽取管線。

試著執行它，調整前處理步驟，觀察 OCR 準確度提升。若遇到問題，請回顧「處理常見問題」表格；大多數問題只需微調設定即可解決。

準備好接受下一個挑戰了嗎？試著加入使用 `pdf2image` 的 PDF 轉圖像步驟，然後將這些圖像直接輸入同樣的管線。結合 OCR 與 Python 豐富的生態系統，無所不能。

祝編程愉快，願你的文字永遠清晰可讀！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [提取文字圖像 – Aspose.OCR for Java 基礎](/ocr/english/java/ocr-basics/)
- [如何使用 Aspose.OCR for Java 從 URL 提取圖像文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}