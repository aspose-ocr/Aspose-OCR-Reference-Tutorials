---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 在 Python 中從 TIFF 檔案提取文字。了解如何快速且可靠地將 TIFF 轉換為文字。
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: zh-hant
og_description: 使用 Aspose OCR 於 Python 從 TIFF 檔案提取文字。本指南逐步說明如何將 TIFF 轉換為文字。
og_title: 從 TIFF 中提取文字 – 完整 Python 指南
tags:
- OCR
- Python
- Aspose
title: 從 TIFF 中提取文字 – 完整 Python 指南
url: /zh-hant/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 TIFF 提取文字 – 完整 Python 指南

需要在你的 Python 專案中 **從 TIFF 提取文字** 嗎？本指南將向你展示如何使用 Aspose OCR 函式庫 **將 TIFF 轉換為文字**，而且步驟簡單，即使是初學者也能跟上。  

如果你曾經盯著多頁的 TIFF，想知道如何在不手動輸入的情況下取得文字內容，那麼你來對地方了。我們將走過整個流程——從安裝套件到處理加密檔案等邊緣情況——讓你可以專注於構建真正重要的功能。

## 你將學會

* 如何在 Python 中設定 Aspose OCR。
* 讀取多頁 TIFF 所需的完整程式碼。
* 處理常見問題的方法，例如缺少字型或頁面損毀。
* 在大規模 **從 TIFF 提取文字** 時提升準確度與效能的技巧。

完成後，你將擁有一個可直接執行的腳本，能將任何 TIFF 轉換為純文字，方便索引、搜尋或輸入後續的 NLP 流程。

### 前置條件

* Python 3.8 或更新版本（函式庫支援 3.7 以上）。
* 有效的 Aspose OCR 授權—或可先使用免費試用版（程式碼在評估模式下仍可運作，只是輸出會有浮水印）。
* 對 Python 虛擬環境有基本了解（非必須，但建議使用）。

---

## 第一步 – 安裝 Aspose OCR 套件

首先，你需要 `aspose-ocr` 套件。它託管於 PyPI，只要執行簡單的 `pip` 安裝即可。

```bash
pip install aspose-ocr
```

> **專業提示：** 使用虛擬環境 (`python -m venv venv`) 以保持相依套件相互隔離。這可避免與其他專案的版本衝突。

> **為何重要：** 安裝套件會同時下載原生 OCR 引擎二進位檔，這些才是真正執行繁重運算的核心。若缺少它們，`recognize_from_tiff` 方法將不存在，會拋出 `ImportError`。

---

## 第二步 – 匯入函式庫並建立 OCR 引擎

現在函式庫已安裝在你的機器上，匯入它並建立一個 `OcrEngine`。此物件是負責處理影像資料的核心引擎。

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*`OcrEngine` 類別封裝了所有 OCR 設定，如語言、解析度與前處理選項。我們稍後會微調其中幾項，以提升準確度。*

---

## 第三步 – 指定你的多頁 TIFF 檔案

你需要提供欲讀取的 TIFF 檔案路徑。函式庫支援絕對或相對路徑，但使用絕對路徑可避免腳本在不同工作目錄執行時產生意外。

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **常見錯誤：** 在 Windows 上忘記跳脫反斜線 (`C:\\Images\\file.tif`)。使用原始字串 (`r"C:\Images\file.tif"`) 或正斜線可避免此問題。

---

## 第四步 – 從所有頁面辨識文字

以下是本教學的核心：呼叫 `recognize_from_tiff`。此方法會回傳 `OcrResult` 物件的列表——每一頁對應一個物件，讓你能逐一處理。

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**為什麼這樣有效：** Aspose OCR 會在內部將 TIFF 拆分為各個影格，對每個影格執行 OCR，然後彙整結果。這比使用 Pillow 或 ImageMagick 手動分頁更可靠。

---

## 第五步 – 迭代結果並輸出文字

最後，遍歷 `OcrResult` 列表，將擷取的文字印出（或儲存）。如果你的工作流程需要，也可以將每頁寫入各自的 `.txt` 檔案。

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**預期輸出**（為簡潔起見已截斷）：

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **邊緣案例處理：** 若某頁未偵測到可辨識文字，`page_result.text` 會是空字串。你可能需要將這些頁面記錄下來，以便日後手動檢查。

---

## 加分 – 調整 OCR 設定以提升準確度

有時預設設定不足以應付低解析度掃描或特殊字型。以下提供幾個可調整的設定：

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*這些選項為可選項目，但常能決定輸出是雜亂還是乾淨、可搜尋的文字稿。*

---

## 常見陷阱與避免方法

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 所有頁面輸出為空 | 檔案路徑錯誤或 TIFF 壓縮格式不支援 | 確認路徑正確，且 TIFF 使用受支援的壓縮方式（例如 LZW、PackBits）。 |
| 文字亂碼（例如 �） | 語言設定不正確或缺少字型檔案 | 將 `ocr_engine.language` 設為正確的語系；在作業系統上安裝所需字型。 |
| 大型 TIFF 處理緩慢 | 預設為單執行緒模式 | 若函式庫版本支援，可使用 `ocr_engine.recognize_from_tiff(..., parallel=True)` 以平行處理。 |
| 授權警告 | 使用試用版卻未提供授權檔案 | 透過 `aocr.License().set_license("Aspose.OCR.lic")` 提供授權金鑰。 |

---

## 完整腳本 – 可直接執行

以下為完整、獨立的腳本，已整合上述所有步驟與可選的調整設定。將其複製貼上為 `extract_tiff_text.py`，然後執行 `python extract_tiff_text.py`。

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**執行腳本**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

你會在終端看到每頁的預覽，且會在 `output` 資料夾中產生 `page_1.txt`、`page_2.txt` 等檔案。

---

## 結論

我們已完整說明如何使用 Python 與 Aspose OCR **從 TIFF 提取文字**。從安裝套件、處理多頁文件、調整設定以提升準確度，到儲存結果，整個工作流程現在已在你手中。  

若你打算在生產環境中 **將 TIFF 轉換為文字**，可考慮批次處理檔案、平行呼叫 OCR，並將輸出存入可搜尋的索引（如 Elasticsearch）。想挑戰更高階的，可嘗試其他語言 (`aocr.Language.Spanish`) 或將原始 OCR 結果送入拼寫檢查函式庫，以清理 OCR 噪聲。  

有關擴充、授權或與雲端儲存整合的問題嗎？歡迎在下方留言，祝開發順利！ 

---

![從 TIFF 提取文字的 OCR 流程圖](https://example.com/placeholder-image.png "使用 Python 從 TIFF 提取文字")

*Image alt text: 從 TIFF 提取文字的 OCR 流程圖*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}